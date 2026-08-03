# Design Evaluation Frameworks — Full Reference

Load this when you need precise wording, edge cases, or a deeper explanation to share with the user. The summaries in `SKILL.md` are enough for most evaluations.

## Table of Contents
1. [Nielsen's 10 Usability Heuristics](#nielsens-10-usability-heuristics)
2. [Shneiderman's 8 Golden Rules](#shneidermans-8-golden-rules)
3. [Gerhardt-Powals' Cognitive Engineering Principles](#gerhardt-powals-cognitive-engineering-principles)
4. [Fogg Behavior Model](#fogg-behavior-model)
5. [Laws of UX](#laws-of-ux)

---

## Nielsen's 10 Usability Heuristics
*Source: Nielsen Norman Group — nngroup.com/articles/ten-usability-heuristics/*

Originally developed by Jakob Nielsen and Rolf Molich (1990), refined in 1994
through factor analysis of 249 usability problems. These are "rules of thumb,"
not rigid checklists — apply judgment.

### H1 — Visibility of System Status
The design should always keep users informed about what is going on, through
appropriate feedback within a reasonable amount of time.
- Communicate system state clearly; no consequential action should be taken without informing users.
- Present feedback as quickly as possible (ideally immediately).
- Build trust through open and continuous communication.
- *Example:* Progress bars, loading spinners, confirmation toasts, "You Are Here" indicators on maps.

### H2 — Match Between System and the Real World
The design should speak the users' language — familiar words, phrases, and
concepts rather than internal jargon. Follow real-world conventions so
information appears in a natural, logical order.
- Avoid assuming your mental model matches the user's.
- User research surfaces familiar terminology and mental models.
- *Example:* A stovetop whose control layout mirrors its burner layout.

### H3 — User Control and Freedom
Users often perform actions by mistake and need a clearly marked "emergency
exit" — a way to leave an unwanted state without going through an extended
process.
- Support Undo and Redo.
- Show a clear Cancel option.
- *Example:* Gmail's "Undo Send" toast.

### H4 — Consistency and Standards
Users should not have to wonder whether different words, situations, or actions
mean the same thing. Follow platform and industry conventions.
- Maintain internal consistency (within the product) and external consistency
  (with industry conventions). Failing either forces users to learn something new.
- *Example:* The hamburger icon for mobile navigation; checkout flows that
  match e-commerce norms.

### H5 — Error Prevention
Good error messages matter, but the best designs prevent problems from
occurring in the first place.
- Two error types: **slips** (unconscious, from inattention) and **mistakes**
  (conscious, from mental-model mismatch).
- Eliminate error-prone conditions or present confirmation dialogs before
  committing to irreversible actions.
- *Example:* Graying out inapplicable menu items; inline form validation.

### H6 — Recognition Rather than Recall
Minimize memory load by making elements, actions, and options visible. Users
should not have to remember information from one part of the interface to apply
it elsewhere.
- Offer just-in-time help rather than asking users to memorize a tutorial.
- *Example:* Autocomplete, persistent filter chips showing active state, breadcrumbs.

### H7 — Flexibility and Efficiency of Use
Shortcuts (accelerators), hidden from novices, can speed up expert workflows —
letting the design serve both audiences.
- Provide keyboard shortcuts, gestures, and customization.
- Allow personalization of frequent actions.
- *Example:* Ctrl+K command palettes, swipe-to-archive on mobile email.

### H8 — Aesthetic and Minimalist Design
Every extra unit of information competes with relevant information and
diminishes its relative visibility. Interfaces should not contain irrelevant
or rarely needed information.
- This is not a mandate for flat/minimal visual style — it's about informational
  focus. Ensure visual elements support primary user goals.
- *Example:* Google's homepage; removing decorative elements that create noise.

### H9 — Help Users Recognize, Diagnose, and Recover from Errors
Error messages should: (a) be in plain language with no error codes, (b)
precisely indicate the problem, (c) constructively suggest a solution.
- Use visual treatments (color, icon) that make errors noticeable.
- Offer actionable next steps, not dead ends.
- *Example:* "Your password must be at least 8 characters — you entered 5."

### H10 — Help and Documentation
It's best if the system needs no documentation, but when necessary, help
should be: easy to search, focused on the user's task, concrete, and concise.
- Present help in context at the moment it's needed.
- *Example:* Tooltip on hover, inline FAQ, contextual onboarding tooltips.

---

## Shneiderman's 8 Golden Rules
*Source: Ben Shneiderman, "Designing the User Interface," 6th Ed. (2016)*
*cs.umd.edu/~ben/goldenrules.html*

Developed in 1985, refined over three decades. Originally applicable to
"most interactive systems"; now widely used across desktop, web, and mobile.

### R1 — Strive for Consistency
Consistent sequences of actions, terminology, color, layout, and fonts
throughout. Exceptions (e.g., confirming a delete) should be comprehensible
and limited.

### R2 — Seek Universal Usability
Design for plasticity across novice/expert differences, age ranges,
disabilities, cultural variations, and device diversity. Add explanations for
novices and shortcuts for experts.

### R3 — Offer Informative Feedback
Every user action should receive interface feedback. Frequent/minor actions
warrant modest responses; infrequent/major actions warrant more substantial
ones.

### R4 — Design Dialogs to Yield Closure
Group sequences into beginning, middle, and end. Completion feedback gives
users a sense of accomplishment and signals they can move on.
- *Example:* E-commerce confirmation page that completes a transaction.

### R5 — Prevent Errors
Design so users cannot make serious errors (e.g., gray out non-applicable
items, block non-numeric input in numeric fields). After an error, offer
simple, constructive, specific recovery — and don't make users redo
everything.

### R6 — Permit Easy Reversal of Actions
Actions should be reversible. This reduces anxiety, encourages exploration of
unfamiliar options. Reversibility can be single-action, task-level, or
group-level.

### R7 — Keep Users in Control
Experienced users want to feel in charge. Avoid surprises, changes in familiar
behavior, tedious data-entry sequences, and inability to get needed information.
Users should be initiators, not responders.

### R8 — Reduce Short-Term Memory Load
People can hold ~7±2 items in working memory. Avoid forcing users to remember
information from one screen to apply on another. Keep forms compact; avoid
requiring re-entry of data the system already has.

---

## Gerhardt-Powals' Cognitive Engineering Principles
*Source: Gerhardt-Powals (1996), via Wikipedia Heuristic Evaluation article*

A more cognitive/systems-oriented complement to Nielsen's heuristics.
Ten principles for reducing cognitive overhead in complex interfaces.

1. **Automate unwanted workload** — Eliminate mental calculations, comparisons,
   and unnecessary thinking to free resources for high-level tasks.
2. **Reduce uncertainty** — Display data clearly and obviously to reduce
   decision time and error.
3. **Fuse data** — Aggregate lower-level data into meaningful summations to
   reduce cognitive load.
4. **Present new information with meaningful aids to interpretation** — Use
   familiar frameworks, schemas, metaphors, and everyday terms.
5. **Use names that are conceptually related to function** — Context-dependent
   labels improve recall and recognition.
6. **Group data in consistently meaningful ways** — Logical grouping on a
   screen; consistent grouping across screens. Reduces search time.
7. **Limit data-driven tasks** — Use color and graphics to reduce the effort of
   assimilating raw data.
8. **Include only information needed at a given time** — Exclude extraneous
   information so users can focus on critical data.
9. **Provide multiple codings of data when appropriate** — Offer data in
   varying formats/levels of detail to promote cognitive flexibility and meet
   user preferences.
10. **Practice judicious redundancy** — Sometimes consistency requires showing
    more information than strictly needed at the moment; balance principles 6
    and 8.

---

## Fogg Behavior Model
*Source: BJ Fogg, Stanford Behavior Design Lab — behaviormodel.org*

**B = MAP**: Behavior occurs when **Motivation**, **Ability**, and a **Prompt**
converge at the same moment. When a desired behavior isn't happening, at least
one element is missing or insufficient.

### Motivation
The user's desire to perform the behavior. Fogg identifies three core
motivators (each with a positive and negative pole):
- Pleasure / Pain
- Hope / Fear
- Social Acceptance / Rejection

Design note: Motivation is hard and expensive to change. Don't rely on
motivation when you can increase ability instead.

### Ability (= Simplicity)
Ability is how easy the behavior is relative to the user's available resources.
Fogg often substitutes "Simplicity" because **simplicity is a function of the
user's scarcest resource at that moment**.

Ability factors (the weakest link determines difficulty):
1. **Time** — Does the user have enough time to do this?
2. **Money** — Is there a cost barrier?
3. **Physical effort** — How much physical work is required?
4. **Cognitive effort** — How hard is it to think through?
5. **Social deviance** — Does the action go against social norms?
6. **Non-routine** — Is this outside the user's habitual behavior?

Design insight: **Increase ability before increasing motivation.** Scaling back
the behavior (making it smaller, simpler) is usually more effective than
training users or motivating them harder.

### Prompt (Trigger / Cue)
A signal that prompts the behavior at the right moment. Prompts fail when
motivation or ability is too low. Three types:
- **Spark** — Motivates action when ability is high but motivation is low
  (e.g., a compelling headline).
- **Facilitator** — Makes action easier when motivation is high but ability is
  low (e.g., "Sign in with Google").
- **Signal** — A simple reminder when both motivation and ability are already
  sufficient (e.g., a notification).

### Design Application
Use the B=MAP lens to diagnose why key actions aren't being taken:
1. Is the user motivated? If not, what's blocking desire?
2. Is the action simple enough? Which resource is scarce?
3. Is there a clear, well-timed prompt?
4. Are all three aligned at the same moment?

---

## Laws of UX
*Source: lawsofux.com — Jon Yablonski*

### Hick's Law
**The time to make a decision increases with the number and complexity of choices.**

Key takeaways:
- Minimize choices when response time is critical.
- Break complex tasks into smaller steps to reduce cognitive load.
- Highlight recommended options to guide decisions.
- Use progressive disclosure for onboarding.
- Don't simplify to the point of removing necessary functionality.

Design test: Count the decisions a user must make on a single screen. Each
choice adds decision time. Consider which can be deferred, defaulted, or removed.

### Fitts's Law
**Time to acquire a target is a function of the distance to it and its size.**
Fast movements + small targets = higher error rates (speed-accuracy tradeoff).

Key takeaways:
- Touch targets must be large enough for accurate selection (minimum 44×44px
  on mobile per Apple HIG / 48×48dp per Material Design).
- Adequate spacing between targets prevents mis-taps.
- Place targets close to where the user's attention and finger/cursor already are.
- Primary actions should be larger and more central than secondary/destructive ones.

Design test: On mobile especially, measure tap target sizes and distances
between adjacent interactive elements.

### Miller's Law
**The average person can hold 7 (±2) items in working memory.**

Key takeaways:
- Chunk information into meaningful groups to aid processing, understanding,
  and memory.
- Don't misuse "the magic number 7" to justify navigation with 7 items —
  chunking quality matters more than raw count.
- Working memory capacity varies by individual, prior knowledge, and context.

Design test: Count ungrouped items in a list, menu, or form. Consider chunking
related items under meaningful headers.

### Jakob's Law
**Users spend most of their time on other products. They expect your product to
work like the ones they already know.**

Key takeaways:
- Users transfer mental models from familiar products to yours.
- Leverage existing mental models so users focus on their tasks, not on learning.
- When redesigning, allow users to continue with a familiar version temporarily
  to ease the transition (as YouTube did in 2017).

Design test: Is there a strong reason to deviate from the established pattern?
If not, follow convention. Novel patterns require clear user benefit to justify
the learning cost.

### Peak-End Rule
**People judge an experience based largely on how they felt at its peak and at
its end — not the average of every moment.**

Key takeaways:
- Identify and design the most intense (peak) moment of the user journey to be
  positive and memorable.
- The ending of the experience is disproportionately important to overall
  perception.
- Negative experiences are remembered more vividly than positive ones.
- A painful wait can become a negative peak; a delightful confirmation screen
  can rescue a rough flow.

Design test: Map the emotional journey of the core user flow. Where is the
peak? How does it end? Are both moments given intentional design attention?
