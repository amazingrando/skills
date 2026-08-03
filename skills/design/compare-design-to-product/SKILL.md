---
name: compare-design-to-product
description: Compare a Figma design against a screenshot of the live product to find meaningful differences — content, added/removed elements, layout, and visual/style drift. Use when the user asks to compare design to build, design vs product, design QA, or find where the shipped UI drifted from Figma.
---

# Compare Design to Product

Compare a **design** (a Figma frame created by the design team) against a **screenshot of the live product** (an image pasted onto the canvas showing what developers shipped). Find the **meaningful differences** and report where the build has drifted from the design.

Catch real changes — content developers altered, elements they added or dropped, sections they rearranged, and visual/style choices that diverge. Do **not** act as a pixel-alignment checker.

## Before you start

Identify the two things on the canvas:

1. **The design** — the native Figma frame(s) built by the design team.
2. **The screenshot** — a pasted/imported image of the current live product.

If you can't confidently tell which is which, ask the user to confirm before continuing. If either is missing, stop and say what you need.

Treat the **design as the reference** ("what was intended") and the **screenshot as the actual** ("what shipped"). Describe every difference in terms of how the shipped screenshot differs from the design.

## What counts as a difference worth flagging

Flag differences in these four categories:

- **Content / text** — different copy, labels, headings, button text, numbers, dates, placeholder text, or text that was added or removed.
- **Added / removed elements** — whole components, sections, buttons, fields, icons, or UI blocks present in one but missing from the other.
- **Major layout changes** — reordered sections, restructured arrangement, elements moved to a clearly different position, changed columns/rows, or a different overall composition.
- **Visual / style changes** — meaningfully different color, typography (family, weight, size), component sizing, imagery, or states, where the change is clearly intentional rather than a rounding difference.

## What to ignore

Do **not** report:

- Sub-pixel or few-pixel misalignments and nudges.
- Tiny spacing or padding differences that don't change the layout's meaning.
- Anti-aliasing, compression artifacts, or rendering differences from the screenshot being a raster image.
- Cursor position, scroll position, hover states, or transient UI (tooltips, loading spinners) unless they represent a real structural change.
- Differences caused only by the screenshot being cropped or a different viewport size — note the crop, but don't list clipped content as "removed."

When in doubt about whether something is major, ask: *would a designer or PM care about this in a review?* If yes, flag it. If it's the kind of thing only a pixel-diff tool would catch, skip it.

## How to report — two outputs

### 1. Categorized list with severity

Produce a written summary grouped by the four categories above. For each finding, include:

- **Severity** — one of:
  - `High` — changes meaning, breaks intended UX, or removes/adds significant functionality or content.
  - `Medium` — noticeable divergence a reviewer would want to know about, but not breaking.
  - `Low` — minor but still worth noting (above the "ignore" threshold).
- **Location** — where on the screen it is (e.g. "primary CTA in hero," "third card in the pricing row").
- **Design says** — what the Figma design shows.
- **Shipped shows** — what the screenshot shows.

Order findings within each category by severity, highest first. Start the report with a one-line summary: total number of differences and how many are High.

Use this shape:

```
## Summary
7 differences found — 2 High, 3 Medium, 2 Low.

## Content / text
- [High] Hero headline — Design says "Start free today", shipped shows "Get started".
- ...

## Added / removed elements
- [High] "Trusted by" logo strip present in design, missing from shipped build.
- ...

## Major layout changes
- ...

## Visual / style changes
- ...
```

If a category has no findings, write "None found" under it rather than omitting it.

### 2. Annotations on the canvas

For each **High** and **Medium** finding, place an annotation on the **design frame** pointing at the location of the difference. Each annotation should be short: the category, the severity, and a one-line description (e.g. `[High · Content] Headline changed to "Get started"`). Keep annotations near the affected element so a reviewer can see at a glance where each issue is. Skip `Low` findings on the canvas to avoid clutter — they stay in the written list only.

Place annotations without altering the original design elements themselves. If you can't annotate directly on the canvas, fall back to listing each finding with a clear location description and tell the user annotations weren't possible.

## Working method

1. Read the full design and the full screenshot top to bottom before judging anything — get the whole picture first.
2. Compare region by region (header, hero, body sections, footer) so nothing is skipped.
3. For each region, check all four categories.
4. Collect findings, assign severity, then write the report and place annotations.
5. Be specific and quote actual text. Vague findings ("the button looks different") are not useful — say what differs and how.

## Tone

Be direct and factual. You're helping a designer spot where the build drifted from intent, not writing a critique. Don't speculate about *why* developers made a change unless it's obvious — just report what differs.
