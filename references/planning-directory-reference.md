# Planning Directory Reference

This document describes the directory structure and file naming conventions for course planning documents.

## Directory Layout

All planning documents live in the `planning/` directory at the project root.

```
project-root/
├── CLAUDE.md (or equivalent)          # AI assistant instructions (see Step 1)
├── planning/                       # Course design and planning documents
│   ├── course-brief.md                 # Course vision, scope, and requirements
│   ├── resources.md                    # External references and documentation
│   ├── course-topics.md                # Topics organized by module
│   ├── course-module-a.md             # Module A workshop breakdown
│   ├── course-module-b.md             # Module B workshop breakdown (when applicable)
│   ├── tasks.md                        # Task tracking (created when issues emerge)
│   └── workshop-plans/                 # Per-workshop detailed plans
│       ├── lab-a01-first-workshop.md
│       ├── lab-a02-second-workshop.md
│       └── ...
└── workshops/                      # Actual Educates workshop implementations
    ├── lab-a01-first-workshop/
    ├── lab-a02-second-workshop/
    └── ...
```

For single-module courses, there is just `course-module-a.md`. The layout is the same regardless of how many modules the course has.

The `planning/` and `workshops/` directories serve distinct purposes:

- **`planning/`** holds the design artefacts produced during course planning. These are consumed by the AI and the course author, not by the Educates platform.
- **`workshops/`** holds the actual Educates workshop implementations (YAML, instruction pages, exercise files). These are what gets published to the Educates platform.

The AI assistant instructions file (e.g., `CLAUDE.md` for Claude Code) sits at the project root alongside these directories. It provides project-specific overrides and tells the AI which skills to use. See Step 1 in the main skill document for what this file should contain.

## File Naming Conventions

All planning document filenames use **lowercase letters and dashes only**. No uppercase, no underscores, no spaces.

### Top-Level Planning Files

| File | Purpose |
|---|---|
| `course-brief.md` | Course vision, scope, audience, design principles, and growth path |
| `resources.md` | External documentation, references, and learning materials (created in Step 1, updated throughout) |
| `course-topics.md` | Topics list with selection notes (optional for focused courses) |
| `course-module-X.md` | Workshop breakdown for module X (one file per module, where X is a lowercase letter: a, b, c, etc.) |
| `tasks.md` | Centralized task tracking organized by workshop (created when issues emerge) |

Each module has its own workshop breakdown file: `course-module-a.md`, `course-module-b.md`, etc. The letter matches the module identifier used throughout the course (A, B, C, etc.).

### Per-Workshop Plan Files

Per-workshop plans live in the `workshop-plans/` subdirectory. Each file is named to match the workshop directory name with a `.md` extension:

- Workshop directory: `workshops/lab-a01-first-decorator/`
- Plan file: `planning/workshop-plans/lab-a01-first-decorator.md`

Workshop names use the format `lab-{code}-{descriptive-name}`, where the code is the module letter and a two-digit zero-padded workshop number (e.g., `a01`, `a02`, `b01`). The `lab-` prefix follows the Educates naming convention (see the educates-workshop-authoring skill for details). The workshop code ensures files sort by module and sequence in directory listings.

## Cross-Reference Conventions

Planning documents reference each other frequently. Use these patterns consistently.

### Workshop breakdown file referencing topics

In the workshop breakdown file (`course-module-X.md`), reference topics by number and name as they appear in `course-topics.md`:

```markdown
**Covers ideas** — Topics 1–2 from Module A in course-topics.md (Functions as
First-Class Objects, Closures and Nested Functions)
```

For focused courses where no topics document exists, describe what the workshop covers directly instead.

### Workshop breakdown file linking to workshop plans

Each workshop entry includes a "Detailed plan" link using a relative path to the `workshop-plans/` subdirectory:

```markdown
### Workshop A01: Workshop Title

**Detailed plan:** [workshop-plans/lab-a01-workshop-name.md](workshop-plans/lab-a01-workshop-name.md)

**Directory name:** `lab-a01-workshop-name`
```

The workshop code (e.g., A01) consists of the module letter and a two-digit zero-padded sequence number. The link text and URL both use the `workshop-plans/` prefix since the link is relative to the `planning/` directory where the workshop breakdown file lives.

### Workshop plans referencing parent files

Per-workshop plan files may reference their parent files by filename (without path, since the reader understands the context):

```markdown
This workshop covers Topic 3 from course-topics.md.
```

```markdown
The learning objectives are aligned with the workshop breakdown file.
```

### Workshop breakdown entries linking to task status

Once `tasks.md` exists, each workshop entry in the breakdown file includes a **Status** line linking to the workshop's task section:

```markdown
### Workshop A01: Workshop Title

**Detailed plan:** [workshop-plans/lab-a01-workshop-name.md](workshop-plans/lab-a01-workshop-name.md)

**Status:** Needs moderate fixup — [tasks](tasks.md#workshop-a01-workshop-title)

**Directory name:** `lab-a01-workshop-name`
```

If a workshop has no outstanding tasks, the Status line can read "Complete" with no link, or be omitted.

### Workshop plans linking to task status

Once `tasks.md` exists, each workshop plan includes a **Status** line in the Workshop Metadata section:

```markdown
- **Status:** Needs moderate fixup — [tasks](../tasks.md#workshop-a01-workshop-title)
```

The relative path uses `../tasks.md` since plan files are in the `workshop-plans/` subdirectory.

## Document Hierarchy

The planning documents form a hierarchy where each level feeds the next:

1. **Course brief** (`course-brief.md`) — Establishes the "why" and "what" of the course. Created first, referenced by everything else.
2. **Topics** (`course-topics.md`) — Content inventory, organized by module or as a flat list. Derived from the course brief. *Optional for focused courses — can be skipped if the user proceeds directly to the workshop breakdown.*
3. **Workshop breakdown** (`course-module-X.md`) — Topics mapped into concrete workshops with objectives and structure. Derived from the topics list (or directly from the course brief for focused courses).
4. **Workshop plans** (`workshop-plans/lab-*.md`) — Detailed implementation blueprints for each workshop. Derived from the workshop breakdown file.

Each level adds specificity. The course brief is high-level and stable; workshop plans are detailed and may evolve as implementation reveals refinements. For focused courses, the hierarchy may be shortened: brief → workshop breakdown → plans.

**Cross-cutting: Course resources** (`resources.md`) — A curated registry of external documentation, references, and learning materials discovered during course design. Created in Step 1 and updated throughout the workflow as new resources are found. Unlike the hierarchy above, `resources.md` is not tied to a single step — it accumulates resources across all steps and persists across sessions. See [Course Resources Reference](course-resources-reference.md) for details.

**Cross-cutting: Task tracking** (`tasks.md`) — Tracks outstanding work across all workshops. Unlike the hierarchy above, `tasks.md` is not a step in the sequence — it is populated and updated across Steps 4, 5, and 6 as issues are discovered and resolved. See [Task Tracking Reference](task-tracking-reference.md) for details.
