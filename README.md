# Portfolio Mockups for Codex

Reusable Codex skill for turning finished app screenshots into polished portfolio mockups. It prefers Figma MCP when connected and falls back to local SVG/HTML/image composition when Figma is unavailable.

## Install from GitHub

Clone the repository into the Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/A7medMajed16/portfolio-mockups.git ~/.codex/skills/portfolio-mockups
```

Restart Codex, or start a new chat if the skill does not appear immediately.

To update an existing installation:

```bash
git -C ~/.codex/skills/portfolio-mockups pull
```

You can also invoke it explicitly with:

```text
$portfolio-mockups
```

## Use it

From an app project, put finished screenshots in:

```text
portfolio/screenshots/
```

Then ask Codex:

```text
Create portfolio mockups for this project.
```

Optional configuration goes in `portfolio/portfolio.config.json`. See [references/config-schema.md](references/config-schema.md).

Generated files are written to:

```text
portfolio/mockups/
```

Typical outputs include `hero.webp`, `overview.webp`, feature mockups, lifestyle compositions, editable source files, and `manifest.json`.

## Figma setup

Connect and authorize the Figma MCP plugin in Codex if you want editable Figma frames and device components. Provide an existing Figma file/template when you have one. The skill can still complete the work locally without Figma.

## Repository contents

```text
SKILL.md                         # Main skill instructions
agents/openai.yaml               # Codex UI metadata
references/config-schema.md      # Optional project configuration
references/local-composition.md  # Fallback composition guidance
```

The skill does not include screenshots, stock mockup assets, external fonts, or product-specific branding.
