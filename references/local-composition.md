# Local composition guidance

Use this reference only when the Figma route is unavailable or not requested.

## Composition recipe

1. Load the selected screenshots and fit them inside a shared screen ratio without stretching. Crop only when the device frame requires it, and keep the primary content visible.
2. Build the device once as an editable vector/SVG or HTML/CSS component: outer shell, screen mask, optional speaker/camera detail, and shadow. Reuse that component for every screen.
3. Compose `hero` with one dominant device and one or two smaller devices. Compose `overview` as a balanced grid. Use `feature-01` for the strongest screen with enough negative space for the device to read clearly.
4. Keep a safe margin around every device. Avoid shadows touching the canvas edge and avoid placing text over important UI.
5. Render the editable source to PNG/WebP with an available local renderer. If using a browser-based renderer, capture at the intended scale; if using an image library, preserve alpha and use high-quality resampling.

## Quality checks

- no screenshot is stretched or mirrored;
- no device screen leaks outside its mask;
- all exports use the same device proportions and visual treatment;
- text added outside the app is legible at thumbnail size;
- the exported canvas has enough breathing room for a portfolio card;
- filenames are stable and lowercase so later runs can replace assets predictably.

Do not download stock mockup images or fonts unless the user explicitly asks and the environment provides an authorized source. A clean local device frame is preferable to an unverified external asset.
