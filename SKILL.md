---
name: educates-course-design
description: >
  Guide for designing workshops and courses for the Educates interactive
  training platform. Handles everything from planning a single workshop
  through to designing structured multi-part courses. Use this skill when
  planning new workshops, designing a course, extending an existing course,
  or creating detailed workshop plans.
---

# Educates Course Design Skill

This skill guides the design of Educates workshops and courses, from a single workshop idea through to a structured multi-part course. The output is a set of planning documents that serve as blueprints for workshop creation using the educates-workshop-authoring skill.

The workflow progresses through six steps, from establishing requirements down to per-workshop implementation plans. Each step produces a planning document in the `planning/` directory. Steps are typically done in order for a new course, but you can enter at any step when extending an existing course (e.g., jump to Step 3 to plan new workshops, or Step 4 to create a plan for a single workshop). For smaller courses, some steps are simplified or skipped entirely — the workflow adapts based on the course scope established in Step 1.

## Step 1: Establish Course Requirements

### Determine Course Scope

Before gathering detailed requirements, understand the scale and structure the user has in mind. Listen to how they describe what they want — they might say "I want to build a comprehensive course on X" or "I have an idea for a workshop or two on Y" or anything in between.

Gauge the scope from the conversation and propose one of these classifications:

- **Focused** (1–3 workshops): A small set of workshops, possibly just an idea the user wants to flesh out. No parts, no spine/elective model. The user may not have the full picture yet — help them plan what they have now and suggest what they could add later.
- **Standard** (4–10 workshops): A coherent course with several workshops. Parts are optional (a single grouping is fine). A simple linear sequence is the default; spine/elective is available if the user wants flexible ordering.
- **Comprehensive** (10+ workshops across multiple parts): A large structured course. Parts and a navigation model (spine/elective recommended) help learners navigate the material.

Confirm the scope with the user before proceeding. The scope is not rigid — it can be revised later — but it shapes how much structure the workflow introduces. Record the scope in the course brief.

### Gather Requirements

Gather the following information from the user or infer from context:

- **Subject and scope**: What the course covers and how broad/deep it goes
- **Target audience**: Who the course is for and what difficulty range it spans (beginner, intermediate, advanced, or a progression)
- **Navigation model** *(standard and comprehensive only)*: Whether the course uses a spine/elective model (recommended for comprehensive courses where learners pick and choose) or a linear sequence. For focused courses, workshops are standalone or follow a simple linear order — no navigation model section is needed.

If the user provides a broad topic but not explicit details, propose reasonable defaults and confirm before proceeding. The course brief captures the "why" and "what" of the course before any topics are brainstormed.

### Create the Course Brief

Create `planning/course-brief.md`. The sections below adapt to the course scope — include only what is relevant:

- **Course Vision** — What the course covers and why it exists. For courses with multiple parts, describe the progression and any organising theme or narrative arc across parts. For focused courses, a few paragraphs establishing the subject matter and learning goals is sufficient.
- **Target Audience** — Who the course is for, what prior knowledge is assumed, and how the course accommodates different experience levels.
- **Delivery Platform** — That the course is delivered on the Educates training platform as interactive browser-based workshops.
- **Course Structure** *(standard with parts and comprehensive only)* — A high-level overview of how the course is divided into parts, with a brief description of each part's theme and focus. Omit for focused courses and standard courses without parts.
- **Navigation Model** *(standard and comprehensive only)* — How workshops relate to each other. For spine/elective courses: what spine and elective mean, how prerequisites work, and how learners navigate non-linearly. For linear courses: the expected sequence. Omit for focused courses.
- **Design Principles** — The recommended approach to learner interaction (guided experience using clickable actions is the default; the course author may choose a more hands-on approach where learners type code and commands themselves) and any course-specific design decisions (e.g., how conceptual material should be handled).
- **Scope and Growth Path** *(focused and standard)* — Record the current scope and suggest directions for future expansion. For example: "This focused course covers X with N workshops. Natural next steps could include Y and Z." This supports users who want to build incrementally, coming back later to add workshops.

Refer to [Course Brief Reference](resources/course-brief-reference.md) for detailed guidance on each section.

### Create the AI Assistant Instructions File

Create an AI assistant instructions file in the project root so that future AI interactions automatically know the project context and which skills to use. For Claude Code, this file is `CLAUDE.md`; other AI coding agents use different conventions (e.g., `AGENTS.md`).

The instructions file should contain:

- A pointer to `README.md` for the project overview, directory structure, and navigation model
- A pointer to `planning/course-brief.md` for the full course vision and design principles
- **Project-specific workshop conventions** established during this step — for example, the workshop naming prefix, which session applications workshops need (terminal, editor, Kubernetes, etc.), the programming language and runtime version, and any other defaults that apply across all workshops in this course
- **Skill references** — when to invoke each skill:
  - The **educates-course-design** skill for course planning (topics, workshop breakdowns, per-workshop plans)
  - The **educates-workshop-authoring** skill for workshop-authoring knowledge (used both when writing per-workshop plans and when creating actual workshop files)
- **Design principles** — a brief assertion of the approach chosen in the course brief (e.g., fully guided clickable actions, or a more hands-on approach), with a reference to `planning/course-brief.md` for details

Keep this file focused on AI-specific instructions and project-specific overrides. Do not duplicate content that already exists in `README.md` or `planning/course-brief.md` — reference those files instead.

## Step 2: Brainstorm and Organize Topics

This step adapts to the course scope:

- **Focused**: This step is optional. If the user already knows what their 1–3 workshops will cover, skip directly to Step 3 (or Step 4 for a single workshop). If the user wants to brainstorm what topics to include or explore expansion ideas, create a lightweight topics list without aiming for exhaustive coverage.
- **Standard**: Work with the user to identify the topics the course will cover and note ideas for future expansion. The goal is to cover the planned scope and capture growth ideas, not to enumerate everything the subject could possibly include.
- **Comprehensive**: Generate a thorough inventory of topics the course could cover and organize them into the parts defined in the course brief. The goal is completeness — it is better to list more topics and prune later.

This step is collaborative and iterative — the AI proposes topics based on the course vision and the user refines, adds, removes, and reorders them. The topic list is an inventory, not a 1:1 mapping to workshops. That mapping happens in Step 3.

### Create the Topics Document

Create `planning/course-topics.md` with:

- **Topics organized by part** *(for courses with parts)* or **as a flat numbered list** *(for courses without parts)* — Each topic has a heading (numbered for reference) and bullet points describing what it covers.
- **Notes on Topic Selection** — Annotations identifying:
  - Topics that are primarily conceptual and may need folding into practical neighbours
  - Clusters of topics with similar code structure that work well as electives *(for courses using the spine/elective model)*
  - **Future expansion ideas** — topics the user is not planning to cover now but might want to add later *(especially valuable for focused and standard courses)*
  - Any other observations that should guide the mapping from topics to workshops

Multiple topics may be combined into a single workshop, or a large topic may be split across workshops. That mapping happens in Step 3.

Refer to [Course Topics Reference](resources/course-topics-reference.md) for detailed guidance.

## Step 3: Plan Workshop Breakdown

Map the topics from Step 2 (or the user's workshop ideas, if Step 2 was skipped) into concrete workshops.

### Create the Workshops Document

The file structure depends on the course scope:

- **Focused and standard without parts**: Create a single `planning/workshops.md`.
- **Standard with parts and comprehensive**: Create one file per part, named `planning/part-N-workshops.md` (e.g., `part-1-workshops.md`, `part-2-workshops.md`).

Each file opens with:
- A brief introduction explaining how topics were mapped to workshops (or, for focused courses, what each workshop covers)
- A **Workshop Structure Conventions** section defining what each workshop entry includes

Then each workshop is described with:

- **Covers ideas** — Which topics from `course-topics.md` are addressed (omit if Step 2 was skipped)
- **Type** *(only for courses using the spine/elective model)* — Spine (mandatory, sequential) or elective (optional, can be taken in any order once prerequisites are met)
- **Prerequisites** — Which workshops must be completed first (explicit, not implied). For focused courses with a simple sequence, "Previous workshop" or "None" is sufficient.
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

For **focused and standard courses**, include a **Future Expansion Ideas** section at the end of the workshops file suggesting directions for growth — topics or workshops the user might add later. This supports incremental course development.

Refer to [Workshop Breakdown Reference](resources/workshop-breakdown-reference.md) for detailed guidance.

## Step 4: Create Per-Workshop Detailed Plans

For each workshop defined in Step 3, create a detailed implementation plan that serves as the blueprint for workshop creation.

### Before Writing a Plan

**Load workshop-authoring knowledge**: Before writing the first plan in a session, invoke the **educates-workshop-authoring** skill to load its knowledge of Educates workshop structure. This does not mean creating workshop files — it means having the authoring skill's knowledge available so plans use correct clickable action types, realistic YAML configuration options, proper page structure conventions, and accurate exercise file layouts. The authoring skill's knowledge ensures plans are implementation-ready rather than aspirational.

For **workshops with a predecessor in a sequential chain** (spine workshops, or any workshop in a linear sequence that follows another): always read the plan for the immediately preceding workshop (and the workshop breakdown descriptions for both workshops) before writing the new plan. This ensures continuity and prevents unnecessary overlap.

For **elective workshops**: read the spine prerequisites listed in the workshops file but do not assume any other elective has been completed.

For **standalone workshops or the first workshop in a course**: no prior plan reading is needed.

### Create a Workshop Plan

Create the plan file in `planning/workshop-plans/`, named to match the workshop directory (e.g., `planning/workshop-plans/lab-first-decorator.md` for the workshop that will live in `workshops/lab-first-decorator/`).

Each plan follows a standard 8-section structure:

1. **Workshop Metadata** — Name, title, description, duration, difficulty, type, prerequisites
2. **Workshop Configuration** — Session applications needed and any special setup
3. **Learning Objectives** — Aligned with the workshops file (the source of truth)
4. **Connection to Previous Workshop** — What the learner already knows and what should NOT be re-taught. Substantive for workshops with a predecessor; omit for standalone or first workshops.
5. **Exercise Files to Create** — Every file under `exercises/`, with filename, purpose, and initial contents
6. **Workshop Instruction Pages** — Page-by-page breakdown with content outlines and clickable action types
7. **Terminal Working Directory Tracking** — Starting directory and any changes through the workshop
8. **Design Notes** — Design decisions, rationale, and deliberate setups for future workshops. For focused courses, note expansion ideas — what future workshops could build on the patterns established here.

After creating the plan, add the **Detailed plan** link to the workshop's entry in the workshops file (see Step 3).

Refer to [Workshop Plan Reference](resources/workshop-plan-reference.md) for the full structure, and [Plan Authoring Guidelines](resources/plan-authoring-guidelines.md) for conventions on sequential workshop flow, deliberate gaps, elective independence, and other guidelines.

## Step 5: Implement Workshops

Once a per-workshop plan exists, hand off to the **educates-workshop-authoring** skill to create the actual workshop files.

For each workshop to be implemented:
1. Read the per-workshop plan from `planning/workshop-plans/`
2. Invoke the educates-workshop-authoring skill
3. The plan serves as the blueprint — it specifies the exercise files, page structure, clickable action types, and terminal patterns
4. The authoring skill handles the Educates-specific implementation details (YAML configuration, clickable action syntax, page structure, verification checklists)

The workshop files are created in the `workshops/` directory, separate from the `planning/` directory.

## Step 6: Verify Consistency

Periodically check for consistency across planning documents and generated workshops. This is especially useful after creating multiple workshops or when returning to a project after a break. The checks below adapt to the course scope — skip checks that do not apply.

### What to Check

**Planning document consistency:**
- All workshops listed in the workshops file(s) (`workshops.md` or `part-N-workshops.md`) have corresponding plan files in `workshop-plans/`
- Topics referenced in workshop entries exist in `course-topics.md` *(skip if no topics document)*
- Prerequisites referenced in plans and workshop files actually exist as defined workshops
- For courses with sequential workshops: the narrative chain is continuous — each workshop's summary bridges to the next *(skip for standalone workshops)*

**Implementation consistency** (for workshops that have been created):
- All plan files with completed workshops have corresponding directories under `workshops/`
- Workshop directory names match the names in plan files
- Exercise files listed in the plan exist in the workshop's `exercises/` directory

**Cross-reference integrity:**
- "Detailed plan" links in workshop files point to existing files with correct paths
- File references between planning documents use current names (no stale references from renames)

**Growth path** *(focused and standard courses)*:
- Future expansion suggestions in the workshops file and course brief are still relevant and have not been superseded by workshops that were actually created

Report findings directly in conversation rather than generating report files. Suggest corrections for any issues found.

## Planning Directory Structure

All planning documents live in the `planning/` directory at the project root. The layout depends on the course scope:

**Courses without parts** (focused, or standard without parts):
```
planning/
├── course-brief.md             # Step 1: Course vision, scope, and requirements
├── course-topics.md            # Step 2: Topics list (optional for focused)
├── workshops.md                # Step 3: Workshop breakdown
└── workshop-plans/             # Step 4: Per-workshop detailed plans
    ├── lab-first-workshop.md
    └── ...
```

**Courses with parts** (standard with parts, or comprehensive):
```
planning/
├── course-brief.md             # Step 1: Course vision, scope, and requirements
├── course-topics.md            # Step 2: Topics organized by part
├── part-1-workshops.md         # Step 3: Part 1 topics mapped to workshops
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
- [Workshop Breakdown Reference](resources/workshop-breakdown-reference.md) — How to map topics into workshops with objectives, prerequisites, and classification
- [Workshop Plan Reference](resources/workshop-plan-reference.md) — The standard 8-section structure for per-workshop implementation plans
- [Plan Authoring Guidelines](resources/plan-authoring-guidelines.md) — Conventions for sequential workshop flow, deliberate gaps, elective independence, and other plan-writing guidelines

## Skill Version

When asked about the skill version, read the `VERSION.txt` file and report its contents to the user.

## Getting Help

For more information about Educates, visit the Educates documentation: https://docs.educates.dev/
