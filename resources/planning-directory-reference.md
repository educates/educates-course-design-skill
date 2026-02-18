# Planning Directory Reference

This document describes the directory structure and file naming conventions for course planning documents.

## Directory Layout

All planning documents live in the `planning/` directory at the project root:

```
project-root/
├── planning/                       # Course design and planning documents
│   ├── course-brief.md                 # Course vision, scope, and requirements
│   ├── course-topics.md                # Master list of topics organized by part
│   ├── part-1-workshops.md             # Part 1 workshops breakdown
│   ├── part-2-workshops.md             # Part 2 workshops breakdown (when planned)
│   └── workshop-plans/                 # Per-workshop detailed plans
│       ├── lab-first-workshop.md
│       ├── lab-second-workshop.md
│       └── ...
└── workshops/                      # Actual Educates workshop implementations
    ├── lab-first-workshop/
    ├── lab-second-workshop/
    └── ...
```

The `planning/` and `workshops/` directories serve distinct purposes:

- **`planning/`** holds the design artefacts produced during course planning. These are consumed by the AI and the course author, not by the Educates platform.
- **`workshops/`** holds the actual Educates workshop implementations (YAML, instruction pages, exercise files). These are what gets published to the Educates platform.

## File Naming Conventions

All planning document filenames use **lowercase letters and dashes only**. No uppercase, no underscores, no spaces.

### Top-Level Planning Files

| File | Purpose |
|---|---|
| `course-brief.md` | Course vision, scope, audience, navigation model, design principles |
| `course-topics.md` | Master list of topics organized by part, with selection notes |
| `part-N-workshops.md` | Workshop breakdown for part N (one file per part) |

Part-level files use a numeric identifier: `part-1-workshops.md`, `part-2-workshops.md`, etc. The number matches the part number used throughout the course.

### Per-Workshop Plan Files

Per-workshop plans live in the `workshop-plans/` subdirectory. Each file is named to match the workshop directory name with a `.md` extension:

- Workshop directory: `workshops/lab-first-decorator/`
- Plan file: `planning/workshop-plans/lab-first-decorator.md`

The `lab-` prefix on workshop names follows the Educates naming convention (see the educates-workshop-authoring skill for details).

## Cross-Reference Conventions

Planning documents reference each other frequently. Use these patterns consistently.

### Part-level file referencing topics

In `part-N-workshops.md`, reference topics by number and name as they appear in `course-topics.md`:

```markdown
**Covers ideas** — Topics 1–2 from course-topics.md (Functions as First-Class
Objects, Closures and Nested Functions)
```

### Part-level file linking to workshop plans

Each workshop entry in `part-N-workshops.md` includes a "Detailed plan" link using a relative path to the `workshop-plans/` subdirectory:

```markdown
### Workshop N: Workshop Title

**Detailed plan:** [workshop-plans/lab-workshop-name.md](workshop-plans/lab-workshop-name.md)

**Directory name:** `lab-workshop-name`
```

The link text and URL both use the `workshop-plans/` prefix since the link is relative to the `planning/` directory where the part-level file lives.

### Workshop plans referencing parent files

Per-workshop plan files may reference their parent files by filename (without path, since the reader understands the context):

```markdown
This workshop covers Topic 3 from course-topics.md.
```

```markdown
The learning objectives are aligned with part-1-workshops.md.
```

## Document Hierarchy

The planning documents form a hierarchy where each level feeds the next:

1. **Course brief** (`course-brief.md`) — Establishes the "why" and "what" of the course. Created first, referenced by everything else.
2. **Topics** (`course-topics.md`) — Brainstormed content inventory, organized by part. Derived from the course brief.
3. **Part workshops** (`part-N-workshops.md`) — Topics mapped into concrete workshops with objectives and structure. Derived from the topics list.
4. **Workshop plans** (`workshop-plans/lab-*.md`) — Detailed implementation blueprints for each workshop. Derived from the part-level file.

Each level adds specificity. The course brief is high-level and stable; workshop plans are detailed and may evolve as implementation reveals refinements.
