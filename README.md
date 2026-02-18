# Educates Course Design Skill

A Claude Code skill for designing workshops and courses for the [Educates](https://educates.dev/) interactive training platform.

## Features

- Flexible course scope — from a single workshop idea through to structured multi-part courses
- Scope-adaptive workflow that simplifies steps for smaller courses and supports incremental development
- Organize topics into workshops with optional parts and spine/elective classification
- Create detailed workshop plans that serve as blueprints for the educates-workshop-authoring skill
- Built-in growth path guidance for expanding courses over time
- Maintain consistency across planning documents with built-in verification guidance

## Relationship to educates-workshop-authoring

This skill handles **course planning** — designing the overall structure, organizing topics, and creating detailed per-workshop plans. The [educates-workshop-authoring](https://github.com/educates/educates-workshop-authoring-skill) skill handles **workshop implementation** — creating the actual Educates workshop files (YAML configuration, instruction pages, exercise files) from those plans.

The typical workflow is:

1. Use **educates-course-design** to plan the course and create workshop blueprints
2. Use **educates-workshop-authoring** to implement each workshop from its blueprint

## Installation

### Installation using npx skills

You can install this skill directly from the GitHub repository using the `npx skills` command:

```bash
npx skills add https://github.com/educates/educates-course-design-skill
```

### Installation from .skill file

#### From GitHub Release

Pre-packaged `.skill` files are available from the [GitHub releases](https://github.com/educates/educates-course-design-skill/releases) page. This approach is useful when you want to tie your installation to a specific version tag, ensuring reproducibility and consistent behavior across implementations.

To download the latest release:

```bash
curl -fLO https://github.com/educates/educates-course-design-skill/releases/latest/download/educates-course-design.skill
```

To download a specific version (replace `1.0` with the desired version tag):

```bash
curl -fLO https://github.com/educates/educates-course-design-skill/releases/download/1.0/educates-course-design.skill
```

#### From GitHub Source

1. Clone this repository:

   ```bash
   git clone https://github.com/educates/educates-course-design-skill.git
   cd educates-course-design-skill
   ```

2. Create an archive of the skill:

   ```bash
   zip -r educates-course-design.skill . -x ".git/*" -x ".github/*"
   ```

#### Importing into Claude

Once you have the `.skill` file, either downloaded from a GitHub release or built from source, install it using the Claude Code CLI:

```bash
claude skill install educates-course-design.skill
```

Or in the Claude Code desktop app, go to **Settings > Skills** and use "Install from file" to select the `.skill` file.

### Usage

Once installed, if using Claude invoke the skill with:

```
/educates-course-design
```

Or simply ask Claude to help design an Educates course and it will use the skill automatically based on context.

If you are using this skill with other AI agents that support the skills format, the method for invoking the skill will depend on the specific tool. Please check the documentation or help resources for the AI agent you are using to determine how to invoke skills.

## Other AI Agents

Although this skill is being developed and tested with Claude, the skills format is standardised to a degree, so it may also work with other AI agents that support the same format. However, since Claude's built-in knowledge can vary compared to other agents, your success with other agents may differ.

## Feedback

This skill is continually being improved, and your feedback helps make it better. If you notice areas where the course design guidance could be improved, please open an issue on the [GitHub issue tracker](https://github.com/educates/educates-course-design-skill/issues).

Examples of useful feedback include:

- Workflow steps that are unclear or missing
- Planning document structures that could be improved
- Guidelines that don't work well in practice
- Suggestions for additional capabilities the skill should support

There's no need to submit a pull request — just describe the issue and we'll use AI itself to determine the best approach for incorporating any corrections or additional knowledge into the skill. Your feedback helps improve the skill for everyone.

## Documentation

For more information about Educates, visit the official documentation at https://docs.educates.dev/
