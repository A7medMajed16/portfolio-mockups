# Portfolio mockup configuration

Use `portfolio/portfolio.config.json` only for choices that should be repeatable across runs. All fields are optional.

```json
{
  "project_name": "Example App",
  "subtitle": "A short portfolio subtitle",
  "platform": "iOS",
  "template": "phone-editorial",
  "device": "phone",
  "background": "#F3F0EA",
  "accent": "#6C5CE7",
  "text_color": "#171717",
  "export_format": "webp",
  "scale": 2,
  "screens": {
    "hero": ["01-home.png", "02-detail.png", "03-search.png"],
    "feature": ["02-detail.png"]
  }
}
```

Rules:

- Paths in `screens` are relative to the screenshot directory.
- `template` is a style hint, not a command to fetch an external template. Use a matching local/Figma template only if it is available.
- Supported device hints are `phone`, `tablet`, `laptop`, and `browser`; infer one when omitted.
- Use `export_format` only when the renderer supports it; otherwise use PNG and record the actual format in `manifest.json`.
- Do not fabricate a logo, brand font, app-store badge, or marketing copy because a field is absent.
