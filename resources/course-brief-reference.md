# Course Brief Reference

The course brief (`planning/course-brief.md`) is the highest-level planning artefact for a course. It captures the course vision, scope, audience, and design principles established during the initial planning phase. Everything that follows — topics, workshop breakdowns, per-workshop plans — flows from the decisions made here.

## When to Create

The course brief is the first document created when starting a new course. It should be written before brainstorming specific topics, as it provides the framing that guides topic selection. For focused courses (1–3 workshops), the course brief can be lighter — a few paragraphs establishing vision, audience, scope, and design principles. The full section structure described below is recommended for standard and comprehensive courses.

## Standard Sections

### Course Vision

Describe what the course covers and the overall learning goals. This should answer:

- What is the subject matter?
- How does the course progress (e.g., from fundamentals to advanced)?
- For courses with multiple parts: is there an organising theme or narrative thread that connects the parts?
- What makes this course distinctive or valuable?

Keep this concise — a few paragraphs, not pages. For focused courses, the vision can simply describe what the workshop(s) will teach and why, without needing to describe inter-part connections. The vision guides topic selection but does not enumerate topics (that happens in `course-topics.md`).

### Target Audience

Describe who the course is for:

- What experience levels does the course accommodate? (beginner, intermediate, advanced, or a progression)
- What prior knowledge is assumed at entry points?
- How does the course support different entry points for different experience levels?

If the course uses a spine/elective model, explain how different audiences navigate it (e.g., beginners start at the beginning, experienced learners skip early spine workshops). For focused courses, a simple statement of who the workshop(s) are for and what prior knowledge is assumed is sufficient.

### Delivery Platform

State that the course is delivered on the Educates training platform. Include:

- Each workshop is a self-contained Educates workshop providing an interactive browser-based environment
- The environment includes an embedded terminal, VS Code editor, and step-by-step instructions

This section is brief and largely the same across courses, but it establishes the platform context for readers who may not be familiar with Educates.

### Course Structure

*Include this section for courses that are divided into parts. For focused courses without parts, omit this section. For standard courses with a single grouping of workshops, a brief note on the workshop sequence is sufficient.*

Provide a high-level overview of how the course is divided into parts. For each part:

- A title or theme
- A brief description (1-3 sentences) of what the part covers
- How it relates to other parts (builds on, extends, applies, etc.)

This is an overview, not a detailed breakdown — the detailed breakdown happens in the workshop breakdown files.

### Navigation Model

*Include this section for standard and comprehensive courses. For focused courses (1–3 workshops), a navigation model section is not needed — workshops are standalone or follow a simple linear order.*

Describe how workshops relate to each other and how learners navigate the course.

For courses using the **spine/elective model** (recommended for comprehensive courses where learners pick and choose):

- **Spine workshops** form the mandatory core learning path within each part. They build directly on each other and cannot be skipped.
- **Elective workshops** branch off the spine at defined points. They share spine prerequisites but are independent of each other. Learners can take them in any order, skip them, or return later.
- Each workshop states its prerequisites explicitly.

For **linear courses** (where all workshops are taken in sequence):

- Describe the expected sequence and any flexibility points.

Include indicative prerequisite chains if the course structure is complex enough to benefit from them — which topics form strict chains, which are peers.

### Design Principles

State the design principles that apply to all workshops in the course:

**Hands-on guided experience** (recommended default for Educates courses): Every workshop should have a meaningful hands-on code component. The recommended approach is to drive all code interaction — viewing, running, and modifying — through Educates clickable actions, so learners can focus on concepts rather than mechanics. However, the course author may choose a less guided approach where learners type commands or code themselves, depending on the audience and learning goals. The course brief should state which approach the course will use and why.

**Conceptual material handling**: Conceptual or scene-setting material should be folded into neighbouring practical workshops as introductory context, not left as standalone text-only workshops. Topics that are primarily conceptual can be restructured as "observe and diagnose" exercises.

Add any course-specific design principles relevant to the particular subject matter.

### Scope and Growth Path

*Include this section for focused and standard courses. Optional for comprehensive courses.*

Record the course scope (focused, standard, or comprehensive) and, for non-comprehensive courses, suggest directions for future expansion. This supports users who build courses incrementally — starting with a few workshops and adding more over time.

Example: "This focused course covers X with 2 workshops. If expanded, natural next steps could include Y (which could become a third workshop building on Workshop 2) and Z (which could form the basis of a second part covering advanced topics)."

The growth path is not a commitment — it captures ideas that the user can act on later when they return to extend the course.

## What Not to Include

The course brief focuses on course content and structure. The following are out of scope:

- **Deployment infrastructure** — Index sites, learning management systems, authentication services, and hosting are separate concerns.
- **Specific topics or workshops** — The brief describes the shape of the course, not its detailed contents. Topics are enumerated in `course-topics.md`.
- **Implementation details** — Workshop YAML configuration, clickable action syntax, and Educates platform specifics are handled by the educates-workshop-authoring skill.
