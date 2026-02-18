# Workshop Plan Reference

A per-workshop plan (`planning/workshop-plans/lab-*.md`) is a detailed implementation blueprint for a single Educates workshop. It contains everything needed to create the actual workshop files using the educates-workshop-authoring skill.

## File Naming

Plan files are named to match the workshop directory name with a `.md` extension:

- Workshop directory: `workshops/lab-first-decorator/`
- Plan file: `planning/workshop-plans/lab-first-decorator.md`

## Standard Structure

Every plan file follows the same 8-section structure. All sections are required, though the "Connection to Previous Workshop" section is only substantive for spine workshops.

### 1. Workshop Metadata

Basic identification and classification:

```markdown
## Workshop Metadata

- **Name:** lab-workshop-name
- **Title:** Human-Readable Workshop Title
- **Description:** One to two sentence description of what the workshop covers.
- **Duration:** 15m / 30m / 45m / 1h (estimated completion time)
- **Difficulty:** beginner / intermediate / advanced
- **Type:** spine / elective
- **Prerequisites:** Workshop N: Title (or "None" for the first workshop)
```

The **name** matches the directory name and the `metadata.name` in the workshop's `resources/workshop.yaml`.

### 2. Workshop Configuration

What session applications and setup the workshop needs:

```markdown
## Workshop Configuration

- **Terminal:** Enabled (split layout)
- **Editor:** Enabled
- **Other applications:** None required
```

Most workshops need only the terminal and editor. Note any special requirements (e.g., a web application dashboard, extra tools to install via setup scripts, environment variables to set via a profile).

### 3. Learning Objectives

What the learner will be able to do after completing the workshop:

```markdown
## Learning Objectives

After completing this workshop, the learner will be able to:

- Objective 1 (action verb: write, apply, identify, explain, etc.)
- Objective 2
- Objective 3
```

These are copied from the part-level workshops file (the source of truth). They may be refined in wording but should stay aligned in substance.

### 4. Connection to Previous Workshop

For **spine workshops**, explicitly state what the learner already knows and what is new:

```markdown
## Connection to Previous Workshop

**What the learner already knows** (from Workshop N: Title):
- Concept A — can be referenced briefly but not re-taught
- Concept B — the learner has used this in exercises

**What is new in this workshop:**
- Concept C — introduced for the first time
- Concept D — builds on Concept A but goes further

**What should NOT be re-taught:**
- Do not re-explain Concept A; reference it as established knowledge
- Do not repeat the X exercise pattern from the previous workshop
```

This section prevents unnecessary overlap between sequential spine workshops. It forces the plan author to be explicit about what is assumed knowledge versus new material.

For **elective workshops**, this section is briefer — state which spine prerequisites are assumed and what specific concepts from them are relevant.

### 5. Exercise Files to Create

Every file that should exist under `exercises/` when the workshop session starts:

```markdown
## Exercise Files to Create

### exercises/README.md
Placeholder file to ensure the exercises directory exists. Contains a brief
note such as "Exercise files for the [Workshop Title] workshop."

### exercises/example.py
**Purpose:** Starting point for the main exercise.
**Initial contents:** A Python module containing [description of what the file
contains before any clickable actions modify it].

### exercises/helpers.py
**Purpose:** Supporting functions used across multiple exercises.
**Initial contents:** [Description of initial contents].
```

For each file, describe:
- The filename and path under `exercises/`
- Its purpose (which exercises use it, what role it plays)
- What the file contains when the session starts (before any clickable actions modify it)

The `exercises/README.md` placeholder is always required (the directory must contain at least one file to be preserved in publishing).

### 6. Workshop Instruction Pages

A page-by-page breakdown of the workshop content:

```markdown
## Workshop Instruction Pages

### 00-workshop-overview.md
**Purpose:** Introduce the workshop and set context.

**Content outline:**
- Connect to prior workshop(s): reference what the learner already knows about
  [concept] from [previous workshop].
- Introduce the problem or question this workshop addresses.
- State the learning objectives.
- Open the main exercise file (`editor:open-file`).

### 01-first-topic.md
**Purpose:** [One sentence describing the page's purpose.]

**Content outline:**
- Explain [concept] with a brief introduction.
- Open [file] and highlight [section] (`editor:open-file`, then
  `editor:select-matching-text`).
- Run the code to demonstrate the current behaviour (`terminal:execute`).
- Discuss the output and what it shows about [concept].

### 02-second-topic.md
...

### 99-workshop-summary.md
**Purpose:** Recap and bridge to the next workshop(s).

**Content outline:**
- Summarise the key concepts covered: [list].
- Note what was deliberately left unaddressed (to create motivation for the
  next workshop): [specific limitation or unanswered question].
- For spine workshops: bridge to the next workshop by name and topic.
- For elective workshops: suggest related workshops the learner might try next.
```

For each page, specify:
- The filename with numeric prefix
- A one-sentence purpose
- A content outline describing the narrative flow
- Specific clickable action types to use, noted inline (e.g., `editor:open-file`, `terminal:execute`, `editor:replace-matching-text`)

Pages `00` (overview) and `99` (summary) are always present. Core content pages start at `01` and increment.

### 7. Terminal Working Directory Tracking

Document the terminal state throughout the workshop:

```markdown
## Terminal Working Directory Tracking

**Starting directory:** `~/exercises` (exercises directory exists)

**Directory changes:**
- No `cd` commands in this workshop; all commands run from `~/exercises`.

**Terminal command patterns:**
- `python filename.py` for running complete scripts
- `python -c "..."` for quick inline demonstrations
```

Track:
- The starting directory (`~/exercises` when the exercises directory exists)
- Any `cd` commands that change the working directory
- Typical command patterns used in the workshop

This ensures that when the actual workshop instructions are written, all file paths are correct relative to the current working directory at each point.

### 8. Design Notes

Design decisions, rationale, and forward-looking notes:

```markdown
## Design Notes

- This workshop covers Topics N and M from course-topics.md. Topic N provides
  the conceptual foundation; Topic M provides the hands-on application.
- [Design decision]: We chose to [approach] because [reason].
- [Deliberate limitation]: The learner will notice that [limitation]. This is
  intentionally left unresolved — Workshop K addresses it.
- [Future setup]: The [pattern/concept] introduced here is used again in
  Workshop L, so it needs to be memorable.
```

Record:
- Which topics from the master list this workshop covers
- Why specific design decisions were made
- Limitations deliberately introduced that future workshops will resolve
- Concepts that future workshops will build on (so they are introduced clearly)
