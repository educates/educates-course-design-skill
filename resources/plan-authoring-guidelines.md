# Plan Authoring Guidelines

These guidelines apply when writing per-workshop plan files (`planning/workshop-plans/lab-*.md`). They ensure consistency across plans and maintain the narrative flow that makes the course cohesive.

## Spine Workshop Flow

### Read Before Writing

Always read the plan for the **immediately preceding spine workshop** before writing a new spine workshop plan. Also read the part-level descriptions for both workshops in `part-N-workshops.md`. This ensures the new workshop flows logically from the previous one.

### Continuous Narrative

Spine workshops must flow into each other as a continuous narrative:

- The **summary page** of workshop N should bridge to workshop N+1 by noting limitations, unanswered questions, or capabilities that the next workshop will introduce.
- The **overview page** of workshop N+1 should pick up exactly where N left off, referencing what was learned but not re-teaching it.

This creates a sense of progression — each workshop ends with a reason to continue, and the next workshop begins by fulfilling that promise.

### Identify What NOT to Teach

For each spine workshop, explicitly list concepts the learner already knows from prerequisites. These should be:

- **Referenced briefly** — "as you saw in the previous workshop" or "recall that we used X to achieve Y"
- **Not re-explained** — do not re-teach the concept, re-derive it, or re-run the same demonstrations

The "Connection to Previous Workshop" section of the plan (Section 4) is where this is documented.

### Deliberately Leave Gaps

If a concept will be covered in a later workshop, note the limitation briefly in the current workshop but do not resolve it. For example:

- "Notice that `__name__` now shows `wrapper` instead of the original function name" — but do not introduce `functools.wraps` yet if that is the subject of the next workshop.
- "This decorator works for functions but behaves unexpectedly with methods" — but do not solve the method binding issue yet if that comes later.

Record these deliberate gaps in the Design Notes section of the plan, so the future workshop plan knows to pick them up.

## Elective Workshop Independence

Elective workshops share a common set of spine prerequisites but are **independent of each other**:

- Do not assume any other elective has been completed
- Do not reference code, patterns, or concepts introduced in another elective
- Only reference spine prerequisites listed in `part-N-workshops.md`

This ensures learners can take electives in any order without encountering unexplained concepts.

## Exercise File Guidelines

### Self-Contained Per Workshop

Each workshop's `exercises/` directory must contain everything the learner needs for that workshop. Do not reference or import files from other workshops.

If a workshop builds on concepts from a previous workshop, provide fresh exercise files that incorporate the necessary code rather than pointing the learner to files from the previous workshop.

### Pre-Populated Workspace

The `exercises/` directory serves as a pre-populated workspace, not a blank slate. Provide all the code the learner needs as starter files so the workshop can focus on guided incremental changes rather than writing code from scratch.

### Placeholder File

Always include `exercises/README.md` as a placeholder. The exercises directory must contain at least one file to be preserved when workshop files are published.

## Clickable Actions in Plans

By default, Educates workshops use clickable actions for all code interaction — viewing, running, and modifying code — so learners can follow along without needing to type commands or code manually. This is the recommended approach unless the course brief specifies otherwise.

If the course uses the guided approach, plans should specify which clickable action types will be used on each page:

- **Viewing code:** `editor:open-file`, `editor:select-matching-text`
- **Running code:** `terminal:execute`
- **Modifying code:** `editor:replace-matching-text`, `editor:append-lines-to-file`, `editor:append-lines-after-match`, `editor:create-file`, etc.

Note the action types inline in the content outline of each page so the workshop implementation uses the right actions. The list above covers the most common actions, but the educates-workshop-authoring skill defines the full set of available actions, their exact syntax, and their behavioral nuances. Consult the authoring skill's knowledge when choosing actions for a plan to ensure the planned actions are realistic and correctly specified.

If the course uses a less guided approach (where learners type commands or write code themselves), the plan should still document what actions the learner will perform on each page, but may use prose instructions or `workshop:copy` actions instead of direct clickable actions.

## Terminal Command Patterns

Document terminal command patterns in the plan so the actual workshop implementation uses them consistently. Common patterns:

- `python filename.py` — for running complete scripts
- `python -c "..."` — for quick inline demonstrations
- `python -c "import module; ..."` — for testing imports or brief checks

Consistency in command patterns across workshops helps learners develop familiarity with the terminal workflow.

## Quality Checks

Before considering a plan complete, verify:

- [ ] All 8 sections are present and substantive
- [ ] Learning objectives match the part-level file
- [ ] Connection to Previous Workshop explicitly lists what is and is not new (spine workshops)
- [ ] Every exercise file is described with filename, purpose, and initial contents
- [ ] Every instruction page has a content outline with specific clickable action types
- [ ] Terminal working directory is tracked from start to finish
- [ ] Design notes document deliberate limitations and setups for future workshops
- [ ] The overview page connects to prior workshops without re-teaching
- [ ] The summary page bridges to the next workshop(s) with specific hooks
