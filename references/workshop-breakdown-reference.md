# Workshop Breakdown Reference

The workshop breakdown files bridge the gap between the brainstormed topic list (or the user's workshop ideas) and per-workshop implementation plans. They map topics into concrete workshops with objectives, prerequisites, and structural details.

## Purpose

A workshop breakdown file answers: "How do we turn these topics into actual workshops?" It defines:

- Which topics combine into which workshops (the mapping is not necessarily 1:1)
- The prerequisite chain between workshops
- What each workshop teaches and what hands-on activities it includes
- For courses using the core/elective model: which workshops are core (mandatory) and which are elective (optional)

## File Naming

Create one file per module, named `planning/course-module-X.md` where X is a lowercase letter (a, b, c, etc.):

```
planning/course-module-a.md        # Module A workshop breakdown
planning/course-module-b.md        # Module B (when applicable)
```

For focused and standard courses with a single module, create `planning/course-module-a.md`. Each module has its own workshop breakdown file.

## Document Structure

### Introduction

Open with a brief paragraph explaining how the topics were mapped into workshops. For focused courses where Step 2 was skipped, briefly describe what each workshop covers and why. Mention any notable decisions (e.g., "Topics 1 and 2 are combined into a single workshop because...").

### Workshop Structure Conventions

Define what each workshop entry in this document includes. This section sets expectations for the reader. Adapt the fields to the course scope:

**For courses using the core/elective model:**

```markdown
## Workshop Structure Conventions

Each workshop described below includes:

- **Covers ideas** — which topics from course-topics.md are addressed.
- **Type** — whether this is a core (mandatory prerequisite) or elective workshop.
- **Status** — current workshop status and link to tasks (added once `tasks.md` exists).
- **Prerequisites** — which workshops must be completed first.
- **Learning objectives** — what the learner will be able to do after completing it.
- **Narrative arc** — the progression of the workshop from start to finish.
- **Code exercises** — the specific hands-on coding activities, described in
  enough detail to evaluate whether the workshop has sufficient interactive
  substance.
- **Key code examples** — the types of example code that will be needed (not
  the full code itself, but enough to assess feasibility and interest level).
```

**For linear or focused courses** (no core/elective classification):

```markdown
## Workshop Structure Conventions

Each workshop described below includes:

- **Covers ideas** — which topics are addressed (or a description if no
  topics document exists).
- **Status** — current workshop status and link to tasks (added once `tasks.md` exists).
- **Prerequisites** — which workshops must be completed first.
- **Learning objectives** — what the learner will be able to do after completing it.
- **Narrative arc** — the progression of the workshop from start to finish.
- **Code exercises** — the specific hands-on coding activities, described in
  enough detail to evaluate whether the workshop has sufficient interactive
  substance.
- **Key code examples** — the types of example code that will be needed (not
  the full code itself, but enough to assess feasibility and interest level).
```

### Organizing Workshops

**For courses using the core/elective model**, organize workshops into two sections:

```markdown
## Core Workshops

These workshops form the mandatory core sequence. Each one builds directly on
the previous and cannot be skipped.

## Elective Workshops

These workshops branch off the core and can be taken in any order once their
prerequisites are met.
```

**For linear or focused courses**, list all workshops in sequence without splitting into core and elective sections. A simple numbered list under a single heading is sufficient.

### Individual Workshop Entries

Each workshop gets a level-3 heading with its workshop code. The code consists of the module letter and a two-digit zero-padded sequence number (e.g., A01, A02, B01):

**Full template** (for courses using core/elective classification):

```markdown
### Workshop A01: Workshop Title

**Detailed plan:** [workshop-plans/lab-a01-workshop-name.md](workshop-plans/lab-a01-workshop-name.md)

**Status:** Needs moderate fixup — [tasks](tasks.md#workshop-a01-workshop-title)

**Directory name:** `lab-a01-workshop-name`

**Covers ideas** — Topics 1–2 from Module A in course-topics.md (Topic Title, Topic Title)

**Type** — Core

**Prerequisites** — None (first workshop) / Workshop A01: Title

**Learning objectives:**
After completing this workshop, the learner will be able to:
- Objective 1
- Objective 2
- Objective 3

**Narrative arc:**
Description of how the workshop progresses...

**Code exercises:**
Description of the hands-on activities...

**Key code examples:**
Description of the code that will be needed...
```

**Simplified template** (for linear or focused courses without core/elective):

```markdown
### Workshop A01: Workshop Title

**Detailed plan:** [workshop-plans/lab-a01-workshop-name.md](workshop-plans/lab-a01-workshop-name.md)

**Status:** Needs moderate fixup — [tasks](tasks.md#workshop-a01-workshop-title)

**Directory name:** `lab-a01-workshop-name`

**Covers ideas** — Description of what this workshop covers

**Prerequisites** — None / Workshop A01: Title

**Learning objectives:**
After completing this workshop, the learner will be able to:
- Objective 1
- Objective 2
- Objective 3

**Narrative arc:**
Description of how the workshop progresses...

**Code exercises:**
Description of the hands-on activities...

**Key code examples:**
Description of the code that will be needed...
```

The **Detailed plan** link is added once the per-workshop plan is created (Step 4). Until then, omit it.

The **Status** line is added once `tasks.md` is created and tasks exist for the workshop. Until then, omit it. If a workshop has no outstanding tasks, the Status line can read "Complete" with no link, or be omitted.

## Classifying Workshops as Core or Elective

*This section applies to courses using the core/elective navigation model. For linear or focused courses, skip this section.*

### Core Workshops

A workshop is **core** if:
- It introduces concepts that subsequent workshops depend on
- Skipping it would leave a gap in the learner's understanding
- It is part of a strict progression (A → B → C)

Core workshops should be ordered so each one builds naturally on the previous. The narrative arc of each core workshop should bridge to the next.

### Elective Workshops

A workshop is **elective** if:
- It applies previously-learned concepts to a specific use case
- It sits alongside other workshops that cover similar patterns with different applications
- Skipping it does not prevent the learner from understanding later material

Elective workshops should list only core workshops as prerequisites (not other electives), unless there is a genuine dependency between specific electives.

## Prerequisites

Prerequisites must be **explicit** — list the specific workshop(s) by name, not "all previous workshops" or "the core." This allows learners navigating non-linearly to know exactly what they need.

For core workshops, the prerequisite is typically the immediately preceding core workshop. For electives, it is typically the last core workshop before the elective branching point. For simple linear courses, the prerequisite is simply the previous workshop (or "None" for the first).

## Learning Objectives

Learning objectives describe what the learner will be able to **do** (not what they will "understand" or "learn about"). Use action verbs:

- "Write a decorator that accepts arguments using the factory pattern"
- "Apply `functools.wraps` to preserve function metadata"
- "Identify when a class-based decorator is more appropriate than a function-based one"

Learning objectives in the workshop breakdown file are the **source of truth**. Per-workshop plans copy them (and may refine wording) but should stay aligned.

## Mapping Topics to Workshops

Topics do not map to workshops 1:1. Common patterns:

- **Combining topics**: Two related but individually thin topics may form a single rich workshop. This is common when one topic provides context and the other provides the hands-on component.
- **Splitting topics**: A large topic with many subtopics may be split across two workshops if it would otherwise be too long.
- **Folding conceptual topics**: Topics flagged as "primarily conceptual" in the topic notes are folded into neighbouring practical workshops as introductory context, not given their own workshop.

When combining or splitting, update the "Covers ideas" field to reflect the mapping accurately.

## Future Expansion Ideas

*Include this section for focused and standard courses. Optional for comprehensive courses.*

At the end of the module file, include a section suggesting directions for growth:

```markdown
## Future Expansion Ideas

If this course grows, consider:
- Adding a workshop on [topic] to cover [gap]
- Splitting Workshop A01 into two workshops if [topic] proves too large for a
  single session
- Creating a second module focused on [advanced area]
```

This supports incremental course development — users can plan a few workshops now and return later to add more, guided by these suggestions.
