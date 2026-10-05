---
name: portfolio-mockups
description: Create polished, reusable portfolio mockups from finished app screenshots. Use when the user asks for app presentation images, device mockups, case-study covers, or says “Create portfolio mockups for this project”; prefer Figma MCP when connected and otherwise compose assets locally.
---

# Portfolio Mockups

Turn finished app screenshots into a small, consistent portfolio asset set. The result is presentation material, not a UI redesign and not a request to modify the product UI.

## Invocation

Treat prompts such as these as sufficient to start:

- “Create portfolio mockups for this project.”
- “Make portfolio images from these app screenshots.”
- “Prepare this app for my portfolio.”

Use reasonable defaults and inspect the project before asking questions. Ask only when a missing choice would materially change the result, such as no usable screenshots, an inaccessible Figma file, or a required brand direction that cannot be inferred.

## Setup

The skill is installed at `~/.codex/skills/portfolio-mockups` and is discoverable automatically. In a project:

1. Put finished app screenshots in `portfolio/screenshots/` (or use one of the supported input folders below).
2. Optionally add `portfolio/portfolio.config.json` for the project name, colors, device, template hint, and screen mapping.
3. Run `Create portfolio mockups for this project` or invoke `$portfolio-mockups` explicitly.

For the Figma route, connect/authorize the Figma MCP plugin in Codex and provide either an existing Figma file/template or permission to create a new one. No Figma setup is required for the local fallback.

## Inputs

Look for screenshots in this order:

1. `portfolio/screenshots/`
2. `assets/portfolio/screenshots/`
3. `screenshots/`
4. A user-provided folder or image paths

Accept PNG, JPG/JPEG, and WebP. Prefer 5–8 clear screenshots, with the most important screen named or ordered first. Preserve source images; never overwrite them.

Optional project configuration is `portfolio/portfolio.config.json`. Its useful fields are documented in [references/config-schema.md](references/config-schema.md). If it is absent, infer the project name from the repository/app metadata and use a restrained visual direction that complements the screenshots.

## Workflow

1. Inventory screenshots, dimensions, orientation, transparency, and likely screen roles (hero, home, feature, detail, settings, empty/loading state).
2. Choose a coherent presentation direction: background, accent, typography, device type, corner radius, shadows, and spacing. Keep the app screenshots unchanged inside the mockups.
3. Produce a minimum useful set when enough screenshots exist:
   - `hero`: 2–3 device mockups, suitable as the project cover.
   - `overview`: a clean multi-screen arrangement.
   - `feature-01` and optionally `feature-02`: a larger device with the strongest feature.
   - `lifestyle` or `detail`: a contextual composition when the source material supports it.
4. Use the Figma route when Figma MCP is connected and a Figma deliverable is useful. Otherwise use the local fallback below.
5. Export the final assets at high resolution, inspect them visually, and fix obvious clipping, unreadable text, bad crops, inconsistent device proportions, or excessive decoration.
6. Write a small `manifest.json` beside the exports listing source files, generated assets, dimensions, and the route used (`figma` or `local`).

## Figma MCP route

Use an existing user-specified Figma file/template when available. Do not overwrite a shared file or its source frames unless the user explicitly authorizes that; create a clearly named page or duplicate/template-derived file instead.

When the Figma tools are available:

- Before any `use_figma` call, load the `figma:figma-use` skill. If creating a new Figma file, also load `figma:figma-create-new-file` before the create-file call.
- Inspect the file/template first. Reuse its device components, variables, styles, masks, and export settings instead of rebuilding equivalent pieces.
- Import each local screenshot as an image fill or image node, then place it into the template’s device screen mask/frame. Keep one source screenshot per named screen frame so replacements remain easy.
- Use Figma components or existing device frames for phones, tablets, laptops, and browser windows. If no device component exists, use a simple restrained frame with a consistent aspect ratio; do not spend the task building a full design system.
- Create named frames for `hero`, `overview`, `feature-01`, `feature-02`, and `lifestyle` only when each is supported by the available screenshots.
- Add project title/subtitle only if requested or configured. Keep copy secondary to the product UI.
- Export each final frame as PNG or WebP at 2x or 3x. If the MCP cannot export locally, leave the frames organized in Figma and report the exact frame names and the remaining manual export action.

If Figma MCP is unavailable, disconnected, or cannot accept local images, continue with the local route. Do not make the user install Figma merely to complete the fallback.

## Local fallback route

Compose assets in the project workspace using an existing local template when one exists. Otherwise create a small reusable composition from SVG/HTML/CSS or the available image-processing tools. Use the same design decisions for every export:

- device silhouette or frame with a consistent screen ratio;
- rounded screen mask, subtle bezel, and soft shadow;
- one background treatment and one accent color;
- predictable margins and export dimensions;
- no invented product features or fake UI inside the screenshots.

Prefer editable local source (for example `portfolio/mockups/source/`) plus rendered PNG/WebP exports. If a local renderer is unavailable, preserve the source composition and report what could not be rendered rather than silently claiming completion. Read [references/local-composition.md](references/local-composition.md) when implementing this route.

## Outputs

Write generated files under `portfolio/mockups/` unless the project already defines a portfolio output directory. Keep editable source separate from final exports:

```text
portfolio/
├── screenshots/                 # user-owned inputs; never overwrite
├── portfolio.config.json        # optional
└── mockups/
    ├── source/                  # Figma notes or local SVG/HTML source
    ├── hero.png or hero.webp
    ├── overview.png or overview.webp
    ├── feature-01.png or feature-01.webp
    ├── feature-02.png or feature-02.webp   # only when useful
    ├── lifestyle.png or lifestyle.webp     # only when useful
    └── manifest.json
```

Use dimensions appropriate for the portfolio surface, normally a wide hero around 2400–3200 px and supporting assets around 1600–2400 px on the long edge. Preserve transparency only when it benefits the intended placement; otherwise use a finished background so the exported asset is immediately usable.

## Completion report

Tell the user which route was used, where the assets were written, which screenshots were used, and any remaining manual Figma export step. Link the generated files when the host supports local file links. Do not claim that a Figma import or export happened unless the tool result confirms it.
