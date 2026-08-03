---
name: design-eval
description: >
  Comprehensive UX/UI design evaluation grounded in Nielsen's 10 Usability
  Heuristics, Shneiderman's 8 Golden Rules, Gerhardt-Powals' Cognitive
  Engineering Principles, the Fogg Behavior Model (B=MAP), and Laws of UX
  (Hick's, Fitts's, Miller's, Jakob's, Peak-End). Use when the user wants to
  evaluate, critique, audit, or review a design — screenshots, mockups,
  wireframes, prototypes, described flows, or any UI — or asks for UX feedback,
  a heuristic evaluation, design review, accessibility considerations, or ways
  to improve a product. Also trigger on "what do you think of this design?" or
  "how could this be better?"
---

# Design Eval

Produce structured, actionable design evaluations grounded in established
usability and behavioral science frameworks. Identify specific problems,
explain *why* they matter, and recommend how to fix them.

## Before you start

Clarify only what's missing (don't over-ask — start with what you have and note
assumptions):

- What is the product / screen / flow?
- Who is the target user? (novice/expert, accessibility needs)
- What is the user's primary goal in this view?
- What platform/device? (desktop, mobile, touch)
- Any specific concerns the requester wants addressed?

If a screenshot or image was shared, examine it carefully. If a flow was
described in text, work from that description.

## Frameworks (quick reference)

Summaries below are enough for most evaluations. See [reference.md](reference.md)
for precise wording, edge cases, or deeper explanation to share with the user.

### Nielsen's 10 Usability Heuristics
1. **Visibility of system status** — Timely feedback on what's going on.
2. **Match between system and real world** — Familiar language and conventions.
3. **User control and freedom** — Clear undo/redo and exit paths.
4. **Consistency and standards** — Platform and industry conventions.
5. **Error prevention** — Design out error-prone conditions.
6. **Recognition over recall** — Make options visible; minimize memory load.
7. **Flexibility and efficiency** — Shortcuts for experts; usable for novices.
8. **Aesthetic and minimalist design** — Remove irrelevant content/visuals.
9. **Help users recognize, diagnose, and recover from errors** — Plain-language errors with solutions.
10. **Help and documentation** — Task-focused, searchable, in-context help.

### Shneiderman's 8 Golden Rules
1. Strive for consistency
2. Seek universal usability (novices → experts, accessibility)
3. Offer informative feedback
4. Design dialogs to yield closure (beginning → middle → end)
5. Prevent errors
6. Permit easy reversal of actions
7. Keep users in control
8. Reduce short-term memory load

### Gerhardt-Powals' Cognitive Engineering Principles
Automate unwanted cognitive workload; reduce uncertainty; fuse/chunk data
meaningfully; use conceptually related names; limit data-driven tasks (use
color/graphics); show only what's needed now; provide multiple codings when
appropriate.

### Laws of UX
- **Hick's Law** — Decision time grows with number + complexity of choices. Minimize options; progressive disclosure.
- **Fitts's Law** — Time to reach a target ∝ distance / size. Large, nearby targets.
- **Miller's Law** — Working memory ~7 ±2 items. Chunk; don't justify clutter with "the magic number."
- **Jakob's Law** — Users expect your product to work like others they use.
- **Peak-End Rule** — Memory is dominated by the emotional peak and the ending.

### Fogg Behavior Model (B = MAP)
Behavior occurs when **Motivation**, **Ability**, and a **Prompt** converge.
- **Motivation** — Does the user want to? (pleasure/pain, hope/fear, social acceptance/rejection)
- **Ability / Simplicity** — Is it easy enough? Fix ability before boosting motivation.
- **Prompt** — Is there a clear, well-timed cue? Prompts fail when motivation or ability is too low.

## Working method

1. Understand context (above).
2. Systematically check the design against each framework. Only report genuine
   issues and strengths — no padding.
3. For each finding, capture: **framework + principle**, **what you observe**,
   **why it matters**, **recommendation**.
4. Calibrate depth to the request:
   - Quick gut-check → 3–5 issues max
   - Full audit → complete structured report

## How to report

### Design Evaluation: [Product / Screen / Flow Name]

**Context:** [One sentence: what this is, platform, user goal]

#### Critical Issues
Issues that likely cause task failure, significant frustration, or data loss.
Each: **Finding** | Framework | User impact | Recommendation.

#### Moderate Issues
Degrade experience or create friction but don't prevent task completion.

#### Strengths
What the design does well, with the principle it upholds. Keep brief (2–4 items
unless asked for more).

#### Opportunities
Improvements beyond fixing problems — enhancements that could elevate the experience.

#### Summary
2–3 sentence overall assessment. Call out the single most impactful change.

### Severity guide

| Severity | Criteria |
|----------|----------|
| Critical | Violates a core heuristic AND causes user failure or strong negative emotion |
| Moderate | Increases cognitive load, causes confusion, or slows users down noticeably |
| Minor / Strength | Polish issue, or something done well worth calling out |

## Tips

- Be specific. "The back button is missing" beats "navigation is unclear."
- Connect principle to impact — always explain the user consequence.
- Lead with the highest-impact finding.
- For conversion/engagement problems, use Fogg: diagnose Motivation, Ability, or Prompt — fix Ability first.
- Peak-End applies to flows, not just screens: design the emotional high point *and* the ending.
- Fitts's Law is especially critical on mobile — small or distant tap targets are common and easy to fix.
- Hick's Law compounds: count the decisions on a single screen.
- Jakob's Law cuts both ways: novel patterns need clear user benefit to justify the learning cost.

## Additional resources

- Full framework detail: [reference.md](reference.md)
