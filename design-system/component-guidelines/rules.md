# Figma Component Rules

> Agent entry point. Read this file before creating or editing any Figma component.
> Each rule has an ID. Explanations and value tables live in `shape.md`, `layout.md`, `properties.md`.

## Shape (SH)

- SH-01 Height scale in 8px steps: 24, 32, 40, 48, 56, 64. Desktop default 32–40, mobile/public default 44–48.
- SH-02 Buttons, inputs, selects and icon buttons share the same height scale.
- SH-03 Control height is FIXED; vertical padding 0; content centered vertically.
- SH-04 Horizontal padding = height × 0.35, rounded to a multiple of 4 (32→12, 40→16, 48→16, 56→20, 64→24).
- SH-05 Text buttons are horizontal rectangles. Square only for icon-only buttons.
- SH-06 Icon size inside a control: height ≤40 → 16, 48 → 20, ≥56 → 24. Icon–label gap 4–8.
- SH-07 Hit area ≥ 44×44 (48×48 for touch-first products). If the visual is smaller, add a wrapper.
- SH-08 Radius stays the same or grows as size grows. Never shrinks.
- SH-09 Bind padding, gap, radius and fills to variables. No hard-coded values.
- SH-10 Light/dark themes via variable modes. Never duplicate components per theme.

## Layout (LA)

- LA-01 Every container is an auto-layout frame.
- LA-02 Horizontal default: FILL for anything that follows its container width.
- LA-03 Vertical default: HUG. Vertical FILL only for overlays and state layers.
- LA-04 Button root: H=HUG, V=FIXED. Full width → override the instance to H=FILL.
- LA-05 Icons, icon buttons, checkbox/radio/switch controls, shapes: FIXED on both axes.
- LA-06 Tag, chip, badge: H=HUG, V=FIXED. Tooltip: HUG/HUG.
- LA-07 Input, select trigger, list item, menu item: H=FILL, V=HUG. Text inside input: H=FILL.
- LA-08 Card: H=FILL in grids (FIXED when standalone), V=HUG.
- LA-09 Dialog: H=FIXED, V=HUG; body text H=FILL.
- LA-10 App bar, nav bar, tab bar: H=FILL, V=FIXED.
- LA-11 Single-line text: auto width. Multi-line text: auto height + H=FILL.
- LA-12 Separate layers: background/radius → state layer → content.
- LA-13 Absolute position only for state layers, focus rings, badge dots, tooltip arrows.

## Properties (PR)

- PR-01 BOOLEAN controls visibility only. Name it `Show X` (or `hasX` when mirroring a code prop). One convention per library.
- PR-02 An optional icon is a pair: BOOLEAN (`Show icon`) + INSTANCE_SWAP (`Icon`).
- PR-03 Every INSTANCE_SWAP has preferredValues.
- PR-04 Every user-visible string is bound to a TEXT property.
- PR-05 Expose nested instances for sub-components (checkbox in list item, button in dialog).
- PR-06 SLOT only for free-form regions (card body, dialog content, menu list). Not for icons.
- PR-07 Building blocks are private: prefix `.` or `_`.
- PR-08 Before editing an instance, read `componentPropertyDefinitions` from its component set. Never guess property names.
- PR-09 Instance edit order: text → instance swap → slot → override. Never detach by default.
