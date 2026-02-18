# Course Topics Reference

The topics document (`planning/course-topics.md`) is a comprehensive inventory of everything the course could cover, organized by part. It bridges the high-level course vision and the concrete workshop breakdowns.

## Purpose

The topics document serves as a brainstorming artefact and reference list. It is:

- **Comprehensive** — it aims to capture everything that *could* be covered, not just what *will* be covered.
- **Organized by part** — topics are grouped under the parts defined in the course brief.
- **Annotated** — notes identify topics that need special handling (conceptual topics, elective clusters, etc.).
- **Not a 1:1 mapping to workshops** — multiple topics may be combined into a single workshop, or a single large topic may span multiple workshops. That mapping happens in the part-level workshop files.

## Structure

### Title

Use a descriptive title that identifies the course:

```markdown
# Workshop Ideas: [Course Subject]
```

### Topics by Part

Each part gets a level-2 heading, and each topic gets a level-3 heading with a sequential number:

```markdown
## Part 1 — [Part Title]

### 1. [Topic Title]
- Key concept or subtopic
- Another aspect to cover
- Practical application or example

### 2. [Topic Title]
- ...
```

Number topics sequentially across the entire document (not restarting at 1 for each part). This makes it easy to reference specific topics by number from other documents.

Each topic includes bullet points describing what it covers in enough detail to assess:
- Whether the topic has enough substance for a workshop (or part of one)
- What the hands-on component would involve
- How it relates to other topics

### Notes on Topic Selection

After all topics, include a section with annotations that guide the mapping from topics to workshops:

```markdown
## Notes on Topic Selection
```

Common annotations include:

**Topics that are primarily conceptual**: Identify topics that may not have enough hands-on code content to sustain a standalone workshop. Note which neighbouring topics they could be folded into.

**Elective clusters**: Identify groups of topics that follow a similar code pattern (e.g., "build a decorator that does X") where the scaffolding is repetitive but the internal logic differs. These work well as elective workshops that learners pick from based on interest.

**Prerequisite observations**: Note obvious prerequisite chains that should inform the spine/elective classification in Step 3.

## Brainstorming Process

When working with the user to generate topics:

1. **Start from the course brief** — use the vision, scope, and part structure as the framework.
2. **Be comprehensive** — it is better to list more topics and prune later than to miss important ones. Topics can always be marked as "out of scope for now" without being deleted.
3. **Think about progression** — within each part, order topics roughly from foundational to advanced. This ordering is not binding but helps identify natural prerequisite chains.
4. **Consider the hands-on angle** — for each topic, think about what the learner would *do* in a workshop. If a topic is primarily "learn about X" with no clear code activity, flag it in the notes.
5. **Identify patterns** — look for clusters of topics that share a similar structure. These are candidates for elective workshops.
6. **Collaborate iteratively** — propose topics, get feedback, refine. The user knows the subject matter; the AI brings structure and completeness checking.

## Maintaining the Topics Document

The topics document is a living reference during the planning phase. As workshops are planned and implemented:

- Topics may be refined or clarified based on what is learned during detailed planning.
- New topics may be added if gaps are discovered.
- Topics may be annotated as "covered by Workshop N" for traceability, though this is not required.

The document should not be significantly restructured once workshop planning has begun, as other documents reference topics by number.
