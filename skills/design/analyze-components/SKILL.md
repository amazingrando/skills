---
name: analyze-components
description: Audit every Figma component on the current page for inventory, naming, placement, and external/ghost styles, variables, and remote references, then build a canvas audit document and fix the issues. Use when the user asks to analyze components, audit a Figma page, find ghost components, stray library styles, or clean up design-system dependencies.
source: https://www.figma.com/community/skill/61009/analyze-components?q_id=119b6462-e475-4255-8a80-46598f880ff1
---

# Analyze Components

Audit every component used on the current page or a selected section. Scan for external/ghost styles, variables, and remote component references. Build a structured audit document on the canvas and fix all identified issues.

## Inputs

- **Current page**: The page to audit (traverses ALL nodes on the page, not just selected layers)
- Selected layers are ignored — the audit always covers the full page

## Step 1 — Inventory All Components

Use `evaluate_script` to traverse every node on the current page recursively. For each instance node found, record:

- Component name and component set name (if part of a set)
- Node ID of the main component and component set
- Whether the component is remote (`mainComponent.remote`)
- Which page the main component lives on
- Variant count (number of children if component set)
- Count of instances across the page

Group by component set (use set ID as key; fall back to component ID for standalone components). Sort by instance count descending. Flag:

- **Orphaned components**: Components not on any page (internal read-only nodes, `page === null`)
- **Naming issues**: Typos in variant property names, generic names like "Property 1"
- **Duplicate sets**: Multiple component sets with the same name but different node IDs
- **Misplaced components**: Components on the wrong page

## Step 1b — Scan External Dependencies (Styles, Variables, Ghost Components)

After the component inventory, run a second `evaluate_script` traversal to detect external/ghost references. This catches stray library dependencies that the component scan alone misses.

### Ghost components (remote components from external libraries)

Traverse all INSTANCE nodes. For each, check `instance.mainComponent.remote`. If true, record:

- Component name and component set name
- Library source (infer from naming patterns or component key prefixes)
- Instance count per ghost component
- Node IDs of affected instances

Group by library source. A "ghost component" is any remote component from a library that is NOT the file's primary/intended design system — i.e., leftover references from a different library.

### External styles

Traverse all nodes and check these style properties for bound external styles:

    const styleProps = ["fillStyleId", "strokeStyleId", "textStyleId", "effectStyleId"];

For each non-empty style ID:
1. Look up with `await figma.getStyleByIdAsync(styleId)`
2. Check `style.remote` — if true, it's an external style
3. Record: style name, style type (Fill/Stroke/Text/Effect), library name (from `style.description` or naming patterns), usage count

Group by library source. Separate into:
- **Primary library styles**: Styles from the main design system library (highest usage count library)
- **Ghost styles**: Styles from any other library — these are stray references that should be migrated

### External variables

Traverse all nodes and check `node.boundVariables` for variable bindings:

    const bv = node.boundVariables;
    if (bv) {
      for (const [prop, binding] of Object.entries(bv)) {
        // binding may be a single VariableAlias or an array
        const aliases = Array.isArray(binding) ? binding : [binding];
        for (const alias of aliases) {
          if (alias && alias.id) {
            const variable = await figma.variables.getVariableByIdAsync(alias.id);
            if (variable) {
              const collection = await figma.variables.getVariableCollectionByIdAsync(variable.variableCollectionId);
              // Record: variable name, collection name, resolved type, usage count
              // Flag as "ghost" if collection is from a non-primary library
            }
          }
        }
      }
    }

Group by collection and library source. Flag any variables from non-primary libraries as ghost references.

## Step 2 — Build Audit Document

Create a single 960px-wide frame on the current page using `evaluate_script`. Use **grayscale styling throughout** — color only for severity badges and status tags.

### Document structure (top to bottom):

**Header**
- Title: "Component Audit"
- Subtitle: "Full page audit | X unique components | Y total instances | Z remote components | N component pages | M external styles | V external variables"

**How to Read This Document**
- Light gray card (bg: 0.96 gray, radius 8) explaining each section and the severity legend
- No emojis

**Overview**
- Title: "Overview" (24px Bold)
- Horizontal stat row with 4 cards (bg: 0.96 gray, radius 8, padding 20):
  - "Full Page" / "Screens Audited"
  - component count / "Unique Components"
  - instance count / "Total Instances"
  - page count / "Component Pages"

**Issues & Actions** (single table)
- Purple-header table (rgb 0.42, 0.28, 0.7) with columns: Severity (100px) | Issue (300px) | Action Required (260px) | Status (100px) | Result (200px)
- Severity badges: Critical (red 0.85,0.18,0.18), Warning (orange 0.9,0.55,0.1), Suggestion (blue 0.2,0.45,0.85)
- Status badges: "Done" (green 0.18,0.7,0.35) or "Not Started" (gray 0.6)
- Alternating row backgrounds (white / 0.96 gray)
- Each cell is a vertical auto-layout frame with FIXED width matching column spec

**Component Inventory** (ONE single unified table — do NOT split into category sections)
- Title: "Component Inventory" (24px Bold)
- Subtitle: "All X components on this page. Each row includes an inline preview at default state."
- Purple-header table with these exact columns and FIXED widths:
  - Preview: 160px
  - Component: 220px
  - Category: 120px
  - Variants: 70px
  - Uses: 50px
  - Page: 100px
  - Component ID: 240px
- Every row contains ALL 7 cells at the fixed widths above
- Alternating row backgrounds (white / 0.96 gray)
- ALL 82+ components in a single flat table sorted by usage count descending — no grouping, no category sub-tables
- Assign a short category label to each component (e.g. "Tags", "Icons", "Headers", "Audit", "Utility", "Surfaces", "Data Table", "Color", "Changelog", "Annotations", "Org", "Remote")

**External Dependencies** (section after Component Inventory)
- 1px gray divider
- Section title: "External Dependencies" (20px Bold)
- Summary text listing totals: "X ghost components from N libraries | Y external styles from N libraries | Z external variables from N collections"
- Overview stat row (same card style as Overview section) with 4 cards:
  - ghost component count / "Ghost Components"
  - external style count / "External Styles"
  - ghost style count / "Ghost Styles"
  - external variable count / "External Variables"

**Ghost Components Table** (only if ghost components found)
- Title: "Ghost Components" (16px Semi Bold, red color 0.85,0.18,0.18)
- Explanatory subtitle (12px, gray)
- Red-header table (rgb 0.85,0.18,0.18) with columns: Preview (160px) | Component (200px) | Library Source (150px) | Instances (70px) | Suggested Action (380px)
- Each row includes an inline preview instance (same technique as Component Inventory)
- Alternating row backgrounds

**Ghost Styles Table** (only if ghost styles found)
- Title: "Ghost Styles (Secondary Library)" (16px Semi Bold, orange color 0.9,0.55,0.1)
- Explanatory subtitle (12px, gray): "These styles come from a different library than the primary design system."
- Orange-header table (rgb 0.9,0.55,0.1) with columns: Ghost Style Name (260px) | Type (80px) | Uses (60px) | Suggested Replacement (280px) | Description (280px)
- Type values: Fill, Stroke, Text, Effect
- Suggested Replacement column: blue text (rgb 0.2,0.45,0.85) with the closest primary library equivalent
- Alternating row backgrounds

**Primary Library Styles Table**
- Title: "Primary Library Styles (Library Name)" (16px Semi Bold)
- Subtitle with total count and usage
- Dark-header table (rgb 0.2,0.2,0.2) with columns: Style Name (300px) | Type (80px) | Uses (80px) | Style ID (500px)
- Show top 20 styles by usage count, sorted descending
- If more than 20, add a summary row: "+ N more styles with fewer than X usages each"
- Style ID column: fontSize 9, gray color (0.6)
- Alternating row backgrounds

**External Variables Table** (only if external variables found)
- Title: "External Variables" (16px Semi Bold, orange color 0.9,0.55,0.1)
- Explanatory subtitle (12px, gray)
- Orange-header table with columns: Variable Name (250px) | Collection (200px) | Type (100px) | Uses (70px) | Library Source (340px)
- Group and sort by collection, then by usage count descending
- Alternating row backgrounds

### Inline preview instances (critical):

Every row's first cell (Preview, 160px) must contain a **live component instance** at default state:
1. Look up the component node by ID
2. If COMPONENT_SET: create instance from `defaultVariant` or `children[0]`
3. If COMPONENT: create instance directly
4. Append to the preview cell
5. Set `layoutSizingHorizontal: "FIXED"` and `layoutSizingVertical: "FIXED"` on the instance
6. Scale down if wider than 140px or taller than 48px using `instance.rescale()`
7. Center the instance in the cell using `primaryAxisAlignItems: "CENTER"` and `counterAxisAlignItems: "CENTER"`

### Column cell construction:

Every cell in every row must follow this exact pattern:

    const cell = figma.createFrame();
    cell.layoutMode = "VERTICAL";
    cell.primaryAxisSizingMode = "AUTO";
    cell.counterAxisSizingMode = "FIXED";
    cell.primaryAxisAlignItems = "CENTER";
    cell.fills = [];
    cell.paddingLeft = 12;
    cell.paddingRight = 4;
    cell.resize(COLUMN_WIDTH, 1);  // Use exact width from column spec
    row.appendChild(cell);

Preview cells use HORIZONTAL layout instead of VERTICAL.

### Row construction:

Every data row must follow this pattern:

    const row = figma.createFrame();
    row.layoutMode = "HORIZONTAL";
    row.primaryAxisSizingMode = "FIXED";
    row.counterAxisSizingMode = "AUTO";
    row.fills = solid(rowIndex % 2 === 0 ? WHITE : GRAY_BG);
    row.itemSpacing = 0;
    row.minHeight = 52;
    row.counterAxisAlignItems = "CENTER";
    table.appendChild(row);
    row.layoutSizingHorizontal = "FILL";

### Layout rules:

- Document frame: 960px wide, vertical auto-layout, `primaryAxisSizingMode: AUTO`, padding 48px, itemSpacing 40px
- All direct children of the document use `layoutSizingHorizontal: FILL`
- Table container: vertical auto-layout, cornerRadius 8, clipsContent true, 1px gray stroke
- Table rows: horizontal auto-layout, FILL width, AUTO (hug) height
- Table cells: FIXED width per column spec above, AUTO (hug) height — NEVER let cells hug width
- All text nodes: `textAutoResize: "HEIGHT"`, `layoutSizingHorizontal: "FILL"` within their cell
- Badges: auto-layout frames with `primaryAxisSizingMode: AUTO` (hug text), cornerRadius 4
- Dividers: 1px rectangles with `layoutSizingHorizontal: FILL`
- No emojis anywhere
- Font: Inter (Regular, Semi Bold, Bold) — load all three weights before any text creation
- Component ID column: fontSize 9, gray color (0.6)
- Component name column: Semi Bold
- All other text: Regular, fontSize 11

### Batching:

If there are more than 40 components, split the row creation into multiple `evaluate_script` calls (batch of ~40 rows each). Create the table frame and header row in the first call, then append rows in subsequent calls using the table's node ID.

## Step 3 — Fix Issues

Proceed with fixes immediately after building the audit. Do not ask for confirmation.

### Orphaned components
1. Clone the orphaned node (`node.clone()` — cannot move read-only nodes)
2. Place clone on a suitable component page (Utility or the closest match)
3. Swap all instances across the file: `instance.swapComponent(clone)`
4. Log swap count

### Naming issues (typos in component names or variant properties)
- For component names: rename directly if writable (`node.name = corrected`)
- For variant properties: use `componentSet.editComponentProperty(key, { name: corrected })` and rename variant children
- Count affected instances

### Duplicate component sets
1. Pick one canonical set
2. If orphaned/read-only: clone, fix on clone, place on component page
3. Swap all instances matching by variant property values
4. Log swap count per old set

### After fixes
- Update the Issues & Actions table: change Status badges to "Done" (green) and fill in the Result column with swap counts and details

## Step 4 — Final Sizing Fix Pass

After all sections are built (including external dependencies), run a recursive bottom-up sizing fix on the entire document frame to ensure nothing is clipped:

    function fixSizing(node) {
      if (!("children" in node) || node.type === "INSTANCE") return;
      for (const child of node.children) fixSizing(child);
      if (node.type !== "FRAME" || !node.layoutMode) return;

      // Root doc frame: fixed width, hug height
      if (node.id === docFrame.id) {
        node.primaryAxisSizingMode = "AUTO";
        return;
      }

      // Table rows (horizontal layout inside tables)
      if (node.layoutMode === "HORIZONTAL" && node.parent && node.parent.layoutMode === "VERTICAL") {
        node.counterAxisSizingMode = "AUTO"; // hug height
        for (const cell of node.children) {
          if (cell.type === "FRAME" && cell.layoutMode) {
            cell.primaryAxisSizingMode = "AUTO"; // hug height
            const w = cell.width;
            cell.counterAxisSizingMode = "FIXED";
            cell.layoutSizingHorizontal = "FIXED";
            cell.resize(w, cell.height);
          }
        }
        return;
      }

      // Vertical containers (tables, sections): hug height
      if (node.layoutMode === "VERTICAL") {
        node.primaryAxisSizingMode = "AUTO";
      }
    }

This pass must run bottom-up (children before parents) so that parent frames can correctly measure their children's sizes. It preserves FIXED widths on cells while allowing everything to hug vertically.

Run `fixSizing(docFrame)` as the last operation, then take a screenshot of the document to verify.

## Important Technical Notes

- Use `primaryAxisAlignItems` (NOT `primaryAlignItems`) — the latter crashes
- Cannot move internal read-only nodes — always clone first
- Load fonts with `figma.loadFontAsync()` before any text changes
- When creating instances, always set `layoutSizingHorizontal: "FIXED"` and `layoutSizingVertical: "FIXED"` to prevent them from stretching
- Table cells must have FIXED width (`counterAxisSizingMode: "FIXED"`) — never let them hug, or columns will misalign
- Row frames must have FIXED primary axis (`primaryAxisSizingMode: "FIXED"`) and FILL horizontal sizing, with AUTO counter axis to hug content height
- Use `figma.combineAsVariants(components, parent)` for creating component sets
- After `figma.combineAsVariants()`, set `layoutPositioning: "AUTO"` on each child
- Prefer placing live instances over screenshots — image hashes from `figma.createImage()` may not persist across script calls
- External style detection: check `fillStyleId`, `strokeStyleId`, `textStyleId`, `effectStyleId` on every node, then `await figma.getStyleByIdAsync(id)` and check `style.remote`
- Variable detection: iterate `node.boundVariables` entries — each value may be a single `VariableAlias` or an array; always normalize to array before processing
- `figma.variables.getVariableByIdAsync()` and `figma.variables.getVariableCollectionByIdAsync()` are both async — always await
- Ghost detection heuristic: the library with the highest total style/variable usage count is the "primary" library; all others are ghost/stray references
- When scanning styles/variables, batch results by library source and sort by usage count descending within each library group
- External dependency tables follow the same cell/row/table construction patterns as the Component Inventory — FIXED width cells, FILL width rows, hug height everywhere
- Always add a 1px gray divider rectangle (`layoutSizingHorizontal: FILL`) between major document sections