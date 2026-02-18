---
name: educates-course-design
description: >
  Guide for designing a multi-workshop course for the Educates interactive
  training platform. Covers the full planning workflow from course vision
  through to per-workshop implementation plans. Use this skill when planning
  a new course, adding parts to an existing course, or creating detailed
  workshop plans.
---

# Educates Course Design Skill

This skill guides the design of a course consisting of multiple Educates workshops. The output is a set of planning documents that serve as blueprints for workshop creation using the educates-workshop-authoring skill.

The workflow progresses through six steps, from establishing the course vision down to per-workshop implementation plans. Each step produces a planning document in the `planning/` directory. Steps are typically done in order for a new course, but you can enter at any step when extending an existing course (e.g., jump to Step 3 to plan a new part, or Step 4 to create a plan for a single workshop).

## Step 1: Establish Course Requirements

Gather the following information from the user or infer from context:

- **Subject and scope**: What the course covers and how broad/deep it goes
- **Target audience**: Who the course is for and what difficulty range it spans (beginner, intermediate, advanced, or a progression)
- **Navigation model**: Whether the course uses a spine/elective model (recommended for courses where learners pick and choose) or a strictly linear sequence

If the user provides a broad topic but not explicit details, propose reasonable defaults and confirm before proceeding. The course brief captures the "why" and "what" of the course before any topics are brainstormed.

### Create the Course Brief

Create `planning/course-brief.md` with the following sections:

- **Course Vision** — What the course covers, the progression from beginner to advanced, and any organising theme or narrative arc across the course as a whole.
- **Target Audience** — Who the course is for, what prior knowledge is assumed at each entry point, and how the course accommodates different experience levels.
- **Delivery Platform** — That the course is delivered on the Educates training platform as interactive browser-based workshops.
- **Course Structure** — A high-level overview of how the course is divided into parts, with a brief description of each part's theme and focus.
- **Navigation Model** — How workshops relate to each other. For spine/elective courses: what spine and elective mean, how prerequisites work, and how learners navigate non-linearly. For linear courses: the expected sequence.
- **Design Principles** — The recommended approach to learner interaction (guided experience using clickable actions is the default; the course author may choose a more hands-on approach where learners type code and commands themselves) and any course-specific design decisions (e.g., how conceptual material should be handled).

Refer to [Course Brief Reference](resources/course-brief-reference.md) for detailed guidance on each section.

## Step 2: Brainstorm and Organize Topics

Working with the user, generate a comprehensive list of topics the course could cover and organize them into the parts defined in the course brief.

This step is collaborative and iterative — the AI proposes topics based on the course vision and the user refines, adds, removes, and reorders them. The goal is a complete inventory of what the course *could* cover, not a final commitment to implement every topic as a workshop.

### Create the Topics Document

Create `planning/course-topics.md` with:

- **Topics organized by part** — Each topic has a heading (numbered for reference) and bullet points describing what it covers.
- **Notes on Topic Selection** — Annotations identifying:
  - Topics that are primarily conceptual and may need folding into practical neighbours
  - Clusters of topics with similar code structure that work well as electives
  - Any other observations that should guide the mapping from topics to workshops

The topic list is an inventory, not a 1:1 mapping to workshops. Multiple topics may be combined into a single workshop, or a large topic may be split across workshops. That mapping happens in Step 3.

Refer to [Course Topics Reference](resources/course-topics-reference.md) for detailed guidance.

## Step 3: Plan Part-Level Workshop Breakdown

For each part of the course (or whichever part the user wants to work on next), map the topics from Step 2 into concrete workshops.

### Create a Part Workshops Document

Create one file per part, named `planning/part-N-workshops.md` (e.g., `part-1-workshops.md`, `part-2-workshops.md`).

Each file opens with:
- A brief introduction explaining how topics were mapped to workshops for this part
- A **Workshop Structure Conventions** section defining what each workshop entry includes

Then each workshop is described with:

- **Covers ideas** — Which topics from `course-topics.md` are addressed
- **Type** — Spine (mandatory, sequential) or elective (optional, can be taken in any order once prerequisites are met)
- **Prerequisites** — Which workshops must be completed first (explicit, not implied)
- **Learning objectives** — What the learner will be able to do after completing the workshop
- **Narrative arc** — The progression from start to finish
- **Code exercises** — The specific hands-on activities, described in enough detail to assess whether the workshop has sufficient interactive substance
- **Key code examples** — The types of code needed (not full implementations, but enough to assess feasibility)

As per-workshop plans are created in Step 4, add a **Detailed plan** link to each workshop entry. The link uses a relative path to the `workshop-plans/` subdirectory:

```markdown
### Workshop N: Workshop Title

**Detailed plan:** [workshop-plans/lab-workshop-name.md](workshop-plans/lab-workshop-name.md)

**Directory name:** `lab-workshop-name`
```

Refer to [Part Workshops Reference](resources/part-workshops-reference.md) for detailed guidance.

## Step 4: Create Per-Workshop Detailed Plans

For each workshop defined in Step 3, create a detailed implementation plan that serves as the blueprint for workshop creation.

### Before Writing a Plan

For **spine workshops**: always read the plan for the immediately preceding spine workshop (and the part-level descriptions for both workshops) before writing the new plan. This ensures continuity and prevents unnecessary overlap.

For **elective workshops**: read the spine prerequisites listed in the part-level file but do not assume any other elective has been completed.

### Create a Workshop Plan

Create the plan file in `planning/workshop-plans/`, named to match the workshop directory (e.g., `planning/workshop-plans/lab-first-decorator.md` for the workshop that will live in `workshops/lab-first-decorator/`).

Each plan follows a standard 8-section structure:

1. **Workshop Metadata** — Name, title, description, duration, difficulty, type, prerequisites
2. **Workshop Configuration** — Session applications needed and any special setup
3. **Learning Objectives** — Aligned with the part-level file (the source of truth)
4. **Connection to Previous Workshop** — What the learner already knows and what should NOT be re-taught (spine workshops only)
5. **Exercise Files to Create** — Every file under `exercises/`, with filename, purpose, and initial contents
6. **Workshop Instruction Pages** — Page-by-page breakdown with content outlines and clickable action types
7. **Terminal Working Directory Tracking** — Starting directory and any changes through the workshop
8. **Design Notes** — Design decisions, rationale, and deliberate setups for future workshops

After creating the plan, add the **Detailed plan** link to the workshop's entry in the part-level file (see Step 3).

Refer to [Workshop Plan Reference](resources/workshop-plan-reference.md) for the full structure, and [Plan Authoring Guidelines](resources/plan-authoring-guidelines.md) for conventions on spine flow, deliberate gaps, elective independence, and other guidelines.

## Step 5: Implement Workshops

Once a per-workshop plan exists, hand off to the **educates-workshop-authoring** skill to create the actual workshop files.

For each workshop:
1. Read the per-workshop plan from `planning/workshop-plans/`
2. Invoke the educates-workshop-authoring skill
3. The plan serves as the blueprint — it specifies the exercise files, page structure, clickable action types, and terminal patterns
4. The authoring skill handles the Educates-specific implementation details (YAML configuration, clickable action syntax, page structure, verification checklists)

The workshop files are created in the `workshops/` directory, separate from the `planning/` directory.

## Step 6: Verify Consistency

Periodically check for consistency across planning documents and generated workshops. This is especially useful after creating multiple workshops or when returning to a project after a break.

### What to Check

**Planning document consistency:**
- All workshops listed in `part-N-workshops.md` have corresponding plan files in `workshop-plans/`
- Topics referenced in workshop entries exist in `course-topics.md`
- Prerequisites referenced in plans and part-level files actually exist as defined workshops
- Spine workshop flow is continuous — no gaps in the narrative chain, each workshop's summary bridges to the next

**Implementation consistency** (for workshops that have been created):
- All plan files with completed workshops have corresponding directories under `workshops/`
- Workshop directory names match the names in plan files
- Exercise files listed in the plan exist in the workshop's `exercises/` directory

**Cross-reference integrity:**
- "Detailed plan" links in `part-N-workshops.md` point to existing files with correct paths
- File references between planning documents use current names (no stale references from renames)

Report findings directly in conversation rather than generating report files. Suggest corrections for any issues found.

## Planning Directory Structure

All planning documents live in the `planning/` directory at the project root:

```
planning/
├── course-brief.md             # Step 1: Course vision, scope, and requirements
├── course-topics.md            # Step 2: Master list of topics organized by part
├── part-1-workshops.md         # Step 3: Part 1 topics mapped to concrete workshops
├── part-2-workshops.md         # Step 3: Part 2 (when planned)
└── workshop-plans/             # Step 4: Per-workshop detailed plans
    ├── lab-first-workshop.md
    ├── lab-second-workshop.md
    └── ...
```

The `workshops/` directory (at the project root, alongside `planning/`) holds the actual Educates workshop implementations created in Step 5.

Refer to [Planning Directory Reference](resources/planning-directory-reference.md) for file naming conventions and cross-reference linking patterns.

## Reference Guides

For detailed guidance on specific topics, see:

- [Planning Directory Reference](resources/planning-directory-reference.md) — Directory structure, file naming conventions, and cross-reference linking patterns
- [Course Brief Reference](resources/course-brief-reference.md) — What goes in a course brief and guidance for each section
- [Course Topics Reference](resources/course-topics-reference.md) — How to brainstorm, organize, and annotate topics
- [Part Workshops Reference](resources/part-workshops-reference.md) — How to map topics into workshops with objectives, prerequisites, and classification
- [Workshop Plan Reference](resources/workshop-plan-reference.md) — The standard 8-section structure for per-workshop implementation plans
- [Plan Authoring Guidelines](resources/plan-authoring-guidelines.md) — Conventions for spine flow, deliberate gaps, elective independence, and other plan-writing guidelines

## Skill Version

When asked about the skill version, read the `VERSION.txt` file and report its contents to the user.

## Getting Help

For more information about Educates, visit the Educates documentation: https://docs.educates.dev/
