# Part Workshops Reference

The part-level workshop files (`planning/part-N-workshops.md`) bridge the gap between the brainstormed topic list and per-workshop implementation plans. Each file maps a set of topics into concrete workshops with objectives, prerequisites, and structural details.

## Purpose

A part-level file answers: "How do we turn these topics into actual workshops?" It defines:

- Which topics combine into which workshops (the mapping is not necessarily 1:1)
- Which workshops are spine (mandatory) and which are elective (optional)
- The prerequisite chain between workshops
- What each workshop teaches and what hands-on activities it includes

## File Naming

One file per part, named `part-N-workshops.md`:

- `planning/part-1-workshops.md`
- `planning/part-2-workshops.md`
- etc.

## Document Structure

### Introduction

Open with a brief paragraph explaining how the topics from `course-topics.md` were mapped into workshops for this part. Mention any notable decisions (e.g., "Topics 1 and 2 are combined into a single workshop because...").

### Workshop Structure Conventions

Define what each workshop entry in this document includes. This section is the same across all part files and sets expectations for the reader:

```markdown
## Workshop Structure Conventions

Each workshop described below includes:

- **Covers ideas** — which topics from course-topics.md are addressed.
- **Type** — whether this is a spine (mandatory prerequisite) or elective workshop.
- **Prerequisites** — which workshops must be completed first.
- **Learning objectives** — what the learner will be able to do after completing it.
- **Narrative arc** — the progression of the workshop from start to finish.
- **Code exercises** — the specific hands-on coding activities, described in
  enough detail to evaluate whether the workshop has sufficient interactive
  substance.
- **Key code examples** — the types of example code that will be needed (not
  the full code itself, but enough to assess feasibility and interest level).
```

### Spine and Elective Sections

Organize workshops into two sections:

```markdown
## Spine Workshops

These workshops form the mandatory core sequence. Each one builds directly on
the previous and cannot be skipped.

## Elective Workshops

These workshops branch off the spine and can be taken in any order once their
prerequisites are met.
```

### Individual Workshop Entries

Each workshop gets a level-3 heading with a sequential number within the part:

```markdown
### Workshop 1: Workshop Title

**Detailed plan:** [workshop-plans/lab-workshop-name.md](workshop-plans/lab-workshop-name.md)

**Directory name:** `lab-workshop-name`

**Covers ideas** — Topics N–M from course-topics.md (Topic Title, Topic Title)

**Type** — Spine

**Prerequisites** — None (first workshop) / Workshop N: Title

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

## Classifying Workshops as Spine or Elective

### Spine Workshops

A workshop is **spine** if:
- It introduces concepts that subsequent workshops depend on
- Skipping it would leave a gap in the learner's understanding
- It is part of a strict progression (A → B → C)

Spine workshops should be ordered so each one builds naturally on the previous. The narrative arc of each spine workshop should bridge to the next.

### Elective Workshops

A workshop is **elective** if:
- It applies previously-learned concepts to a specific use case
- It sits alongside other workshops that cover similar patterns with different applications
- Skipping it does not prevent the learner from understanding later material

Elective workshops should list only spine workshops as prerequisites (not other electives), unless there is a genuine dependency between specific electives.

## Prerequisites

Prerequisites must be **explicit** — list the specific workshop(s) by name, not "all previous workshops" or "the spine." This allows learners navigating non-linearly to know exactly what they need.

For spine workshops, the prerequisite is typically the immediately preceding spine workshop. For electives, it is typically the last spine workshop before the elective branching point.

## Learning Objectives

Learning objectives describe what the learner will be able to **do** (not what they will "understand" or "learn about"). Use action verbs:

- "Write a decorator that accepts arguments using the factory pattern"
- "Apply `functools.wraps` to preserve function metadata"
- "Identify when a class-based decorator is more appropriate than a function-based one"

Learning objectives in the part-level file are the **source of truth**. Per-workshop plans copy them (and may refine wording) but should stay aligned.

## Mapping Topics to Workshops

Topics do not map to workshops 1:1. Common patterns:

- **Combining topics**: Two related but individually thin topics may form a single rich workshop. This is common when one topic provides context and the other provides the hands-on component.
- **Splitting topics**: A large topic with many subtopics may be split across two workshops if it would otherwise be too long.
- **Folding conceptual topics**: Topics flagged as "primarily conceptual" in the topic notes are folded into neighbouring practical workshops as introductory context, not given their own workshop.

When combining or splitting, update the "Covers ideas" field to reflect the mapping accurately.
