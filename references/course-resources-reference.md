# Course Resources Reference

The resources file (`planning/resources.md`) is a curated registry of external documentation, references, and learning materials related to the **course subject matter** discovered during course design. It ensures that useful resources found during research are recorded and available across sessions, preventing redundant web searches and allowing the course author to review and curate the list.

**Scope:** This file tracks resources about the subject the course teaches — language documentation, framework guides, API references, tutorials, specifications, and similar materials. It does **not** track Educates platform documentation. Knowledge about Educates workshop structure, configuration, clickable actions, and authoring conventions is provided by the educates-course-design and educates-workshop-authoring skills and does not need to be recorded here.

## Purpose

During course design, the AI agent researches the course subject extensively — finding official documentation, tutorials, API references, and other materials. Without a persistent record, these resources are lost when conversation context is cleared, forcing the agent to re-search for the same information in later sessions.

The resources file solves this by:

- **Persisting across sessions** — resources found during early design (Steps 1–3) remain available during detailed planning (Step 4) and implementation (Step 5)
- **Enabling user curation** — the course author can review the list, correct versions, flag outdated material, and add preferred alternatives
- **Reducing redundant research** — the agent consults the file before searching the web, saving time and producing more consistent results
- **Informing workshop content** — resources may be referenced in workshop instruction pages or used as background for exercise design

## When to Create

Create `planning/resources.md` during Step 1, alongside the course brief. Even focused courses benefit from tracking resources — a single workshop on a specific framework still involves documentation and references worth recording.

Start the file with whatever resources are found during requirements gathering. It grows throughout the workflow as more resources are discovered during topic brainstorming, workshop breakdown, and detailed planning.

## Structure

The file uses category-based sections. Include only the categories that have entries — do not create empty sections. The categories below are suggestions; add others if the course subject warrants them.

```markdown
# Course Resources

External documentation, references, and learning materials for the course.
These resources were gathered during course design and are maintained as a
shared reference for both AI assistants and course authors.

## Official Documentation

- **[Title]** — [URL]
  [Brief description of what it covers and why it is relevant to the course.]
  Version: [version or date, if applicable]

## Tutorials and Guides

- **[Title]** — [URL]
  [Brief description.]

## API and Library References

- **[Title]** — [URL]
  [Brief description.]
  Relevant to: [topic numbers or workshop names, if known]

## Tools and Utilities

- **[Title]** — [URL]
  [Brief description.]

## Specifications and Standards

- **[Title]** — [URL]
  [Brief description.]

## Curation Notes

Notes on resource quality, version preferences, and corrections.

- [Note about a resource, e.g., "Prefer the Flask 3.x migration guide over
  the 2.x docs listed above — the API changed significantly."]
```

### Entry Format

Each entry includes:

- **Title** (bold) — A descriptive name for the resource
- **URL** — The full URL, placed after an em dash on the same line as the title
- **Description** — A brief note (one to two sentences) on what the resource covers and why it is useful for this course
- **Version or date** *(optional)* — The version of the documentation or the date it was last verified, to help identify when resources may have become outdated
- **Relevance** *(optional)* — Which topics (by number from `course-topics.md`) or workshops the resource relates to, if the connection is specific rather than general

### Categories

Use these categories as a starting point. Adapt them to the course subject:

| Category | What belongs here |
|---|---|
| **Official Documentation** | Language docs, framework docs, platform docs — the authoritative sources |
| **Tutorials and Guides** | Third-party tutorials, blog posts, how-to guides, learning resources |
| **API and Library References** | Documentation for specific APIs or libraries used in course exercises |
| **Tools and Utilities** | Tools the learner will use or that inform exercise design (e.g., linters, testing frameworks, CLI tools) |
| **Specifications and Standards** | RFCs, language specifications, standards documents |

For courses that don't fit neatly into these categories, use whatever groupings make sense. The goal is findability, not rigid adherence to a template.

### Curation Notes

The curation notes section at the end of the file captures corrections, preferences, and quality observations:

- Version corrections (e.g., "The linked Python docs are for 3.11; update to 3.12 when available")
- Preferred alternatives (e.g., "The Real Python tutorial is more practical than the official tutorial for this audience")
- Deprecated or unreliable resources to avoid
- Notes from the course author about which resources to prioritise

The course author can edit this section at any time. The AI agent should check the curation notes before using a resource, as they may indicate that a listed resource is outdated or that a preferred alternative exists.

## Maintaining the Resources File

### When to Add Resources

Add a resource to the file whenever a web search or web fetch yields useful material during any step of the workflow. Do not wait until the end of a step — add resources as they are discovered so they are captured even if the session ends unexpectedly.

Specifically:

- **Step 1** (requirements gathering) — Documentation and references found while understanding the course subject
- **Step 2** (topic brainstorming) — Resources found while researching what topics exist and how they work; annotate entries with the topic numbers they relate to
- **Step 3** (workshop breakdown) — Resources found while assessing the feasibility of specific exercises
- **Step 4** (detailed planning) — Resources found while designing exercises and instruction content; annotate entries with the workshop names they relate to
- **Step 5** (implementation) — Resources found while writing actual workshop content

### When to Consult Resources

Before searching the web for information about the course subject, check `planning/resources.md` first. If a relevant resource is already listed, use it directly. This applies especially when:

- Starting a new session after context has been cleared
- Writing a per-workshop plan (Step 4) — the resources file may already contain the documentation needed
- Implementing a workshop (Step 5) — resources curated during design are likely more vetted than fresh search results

### Keeping Resources Current

- Remove resources that turn out to be unhelpful after closer inspection
- Update version annotations when newer versions of documentation are discovered
- Move corrections and preferences into the curation notes section rather than silently replacing entries — this creates a record that helps the course author understand what changed and why
