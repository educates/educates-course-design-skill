# Project: educates-course-design skill

This project is a **Claude Code skill package**, not a regular application. The files here define the `educates-course-design` skill, which guides users through designing multi-workshop courses for the [Educates](https://educates.dev/) interactive training platform.

When working on this project, you are editing skill definition files. Follow skill-authoring best practices.

## Key files

| File / Directory | Role |
|---|---|
| `SKILL.md` | Main skill definition — loaded when the skill is invoked |
| `resources/` | Structured reference guides linked from SKILL.md |
| `VERSION.txt` | Skill version |
| `README.md` | User-facing install and usage documentation |
| `.github/workflows/release.yaml` | Packages and releases the `.skill` archive |

## Companion skill

This skill handles course **design** (planning documents). The companion skill `educates-workshop-authoring` handles **implementation** (creating actual workshop files). The two are used sequentially: design first, then implement.

## Conventions

- SKILL.md links to resources via markdown references (e.g., `[Course Brief Reference](resources/course-brief-reference.md)`) — the skill framework bundles these automatically.
- Resources are structured reference guides with specific headings and formats. Maintain their structure when editing.
- The 6-step workflow in SKILL.md is the core user experience. Changes must preserve its sequential logic.
- Test changes by invoking the skill locally via `/educates-course-design`.
