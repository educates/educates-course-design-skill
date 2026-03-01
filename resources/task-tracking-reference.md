# Task Tracking Reference

The task tracking file (`planning/tasks.md`) provides a centralized view of outstanding work across all workshops in a course. It tracks known issues, gaps, and to-do items discovered during planning, implementation, and verification.

## When to Create

Create `planning/tasks.md` when the first tasks emerge — typically during Step 4 (after writing workshop plans), when retrofitting an existing course, or during Step 6 verification. The file is not needed until there are tasks to track. For a brand-new course where plans are still being written, it is fine to defer creation until issues are first identified.

## File Structure

The file is organized by workshop, with a global section for course-level tasks. Each workshop section includes a status line and a link to the workshop's plan file. For courses with parts, workshop sections may be grouped under part headings.

### Template

```markdown
# Course Tasks

Outstanding tasks for the course. Organized by workshop, with priorities:

- **P1** — Must fix: broken functionality, missing core content, or incorrect syntax
- **P2** — Should fix: incomplete sections, redundant files, or weak guidance
- **P3** — Nice to have: cosmetic improvements, edge case handling

---

## Course-Level Tasks

Tasks not specific to a single workshop (e.g., updating shared configuration, adding new workshops).

- [ ] **P2** — Update trainingportal.yaml to include new workshop.

---

## workshop-title

**Status:** Needs moderate fixup

**Plan:** [workshop-plans/lab-workshop-name.md](workshop-plans/lab-workshop-name.md)

- [ ] **P1** — Fix broken terminal command on page 03 (references wrong filename). ([source](../workshops/lab-workshop-name/workshop/content/03-page.md))
- [ ] **P2** — Add missing exercise file listed in plan but not created. ([source](../workshops/lab-workshop-name/exercises/))
- [x] **P1** — Correct learning objectives to match workshops.md.
```

For courses with parts, add part headings above the workshop sections:

```markdown
## Part 1: Part Title

### workshop-title

**Status:** Mostly complete
...

### another-workshop

**Status:** Incomplete
...

## Part 2: Part Title

### yet-another-workshop
...
```

## Workshop Status Values

Each workshop section has a **Status** line summarizing the workshop's current state. Use one of these values:

| Status | Meaning |
|---|---|
| **Mostly complete** | Workshop is functional with only minor issues remaining. All core content and exercises work. |
| **Needs moderate fixup** | Workshop has identifiable gaps or errors that need attention but the overall structure is sound. |
| **Incomplete** | Workshop has significant gaps — some pages or exercises are missing or placeholder. |
| **Significantly incomplete** | Workshop is essentially a skeleton or proof-of-concept; substantial content needs to be written. |

Update the status when tasks are completed. When all tasks for a workshop are checked off, either remove the workshop's section from the tasks file or set its status to "Mostly complete."

## Task Format

Each task is a markdown checkbox with a priority label and description:

```markdown
- [ ] **P1** — Description of what needs to be done. ([source](path/to/file))
- [ ] **P2** — Description of what needs to be done.
- [x] **P3** — Description of what was done (completed).
```

Include a source link when the task relates to a specific file. The link uses a relative path from `planning/` to the relevant file.

### Priority Levels

| Priority | Meaning | Examples |
|---|---|---|
| **P1** | Blocks the workshop from being usable | Broken exercises, missing critical pages, incorrect prerequisites, wrong terminal commands |
| **P2** | Should be fixed but workshop is usable without it | Missing optional content, misaligned learning objectives, incomplete design notes, redundant files |
| **P3** | Nice to have, low urgency | Polish, additional examples, expanded explanations, cosmetic improvements |

### Writing Good Task Descriptions

- Start with an action verb: "Fix", "Add", "Update", "Remove", "Rewrite"
- Be specific about the location: reference the page filename, exercise file, or section name
- Include enough context that someone returning to the project after a break can understand the task without reading the full plan
- When a task stems from an external discovery (e.g., an upstream library behaving differently than documented), add indented sub-bullets capturing the investigation context:

  ```
  - [ ] **P2** — Revisit decorator exercise to use `functools.wraps` once upstream fix lands. ([source](../workshops/lab-decorators/workshop/content/04-wraps.md))
    - **Tried:** Calling `functools.wraps` with a class-based decorator per the docs
    - **Failed because:** `update_wrapper` raises `AttributeError` on `__wrapped__` when the decorator is a class (library v2.3.1)
    - **Workaround applied:** Used a function-based decorator instead; updated page 04 narrative to match
    - **Upstream:** https://github.com/example/library/issues/1234
  ```

  The sub-bullets make the task self-contained — someone can understand what happened, reproduce the issue, check whether an upstream fix has landed, and revert the workaround without re-investigating from scratch.

## Cross-Referencing

### From workshop breakdown entries

Each workshop entry in the breakdown file(s) includes a **Status** line that links to the corresponding section in `tasks.md`:

```markdown
### Workshop 1: Workshop Title

**Detailed plan:** [workshop-plans/lab-workshop-name.md](workshop-plans/lab-workshop-name.md)

**Status:** Needs moderate fixup — [tasks](tasks.md#workshop-title)

**Directory name:** `lab-workshop-name`
```

The anchor link uses the markdown heading anchor format (lowercase, hyphens for spaces). Add the Status line once `tasks.md` is created. If a workshop has no tasks, the Status line can read "Complete" with no link, or be omitted.

### From workshop plans

Each workshop plan includes a **Status** line in the Workshop Metadata section:

```markdown
## Workshop Metadata

- **Name:** lab-workshop-name
- **Title:** Human-Readable Workshop Title
- **Status:** Needs moderate fixup — [tasks](../tasks.md#workshop-title)
...
```

The relative path uses `../tasks.md` since plan files are in the `workshop-plans/` subdirectory. Add this line once `tasks.md` is created.

## Task Lifecycle

1. **Tasks are added** during plan creation (Step 4), after implementation (Step 5), during verification (Step 6), when retrofitting an existing course, or whenever the user identifies issues.
2. **Tasks are completed** by checking the box: `- [x] **P1** — ...`
3. **Workshop status is updated** when tasks are resolved — if all P1 and P2 tasks are done, the status typically improves (e.g., from "Incomplete" to "Mostly complete").
4. **Cross-references are updated** — Status lines in the workshop breakdown entry and plan file should match the status in `tasks.md`.
5. **Completed tasks are cleaned up** periodically — when all tasks for a workshop are checked off, they can be removed from the file and the workshop section deleted. This is at the course developer's discretion.

## Adapting to Course Scope

- **Focused courses** (1–3 workshops): The tasks file is lightweight. A single flat list may suffice instead of per-workshop sections if there are only one or two workshops.
- **Standard courses**: Per-workshop sections organized as shown in the template. Part headings are optional.
- **Comprehensive courses**: Per-workshop sections organized under part headings. The Course-Level Tasks section is particularly useful for tracking cross-cutting concerns.

## Recommending Next Work

When the user asks "what should I work on next?", consult `planning/tasks.md` and recommend work based on:

1. **P1 tasks first** — these block workshops from being usable
2. **Workshops with the worst status** — prioritize "Significantly incomplete" over "Needs moderate fixup"
3. **Sequential dependencies** — fix earlier workshops in a chain before later ones, since later workshops may depend on decisions made in earlier ones
4. **P2 tasks** — after all P1s are resolved
5. **P3 tasks** — lowest priority, suggest these when everything else is in good shape
