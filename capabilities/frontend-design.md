# Capability: frontend and visual design

Use when building a web page, UI, landing page, or app screen.

## Decide a direction before writing code

State in two lines: who it is for, and the feel (calm, bold, editorial,
playful, technical). Every choice below serves that direction. Avoid the
generic template look: default fonts, purple gradients on white, identical
rounded cards, stock hero layout.

## Fundamentals

- **Type**: one distinctive display face plus one readable text face. Use a
  scale (for example 14/16/20/28/40/56). Body line length 60-75 characters,
  line height 1.5.
- **Colour**: define tokens once (`--bg`, `--fg`, `--muted`, `--accent`,
  `--border`). One strong accent. Provide a dark theme via
  `prefers-color-scheme`. Contrast at least 4.5:1 for body text.
- **Space**: a spacing scale (4/8/12/16/24/32/48/64). Generous whitespace
  beats decoration. Align things to a grid.
- **Hierarchy**: size, weight, and contrast tell the eye where to go. One
  primary action per view.
- **Motion**: short (150-250 ms), purposeful, respect `prefers-reduced-motion`.

## Build rules

- Mobile first; verify at 375px wide and at desktop. No horizontal scroll.
- Semantic HTML (`header`, `nav`, `main`, `button`, `label`). Real buttons
  and links, not clickable divs.
- Every input has a label; focus states are visible; everything works by keyboard.
- Images have alt text; icons that carry meaning have accessible names.
- One self-contained file for small tools, using CSS variables for theming.
- Use real or clearly placeholder content. Never invent testimonials, stats,
  or logos of real companies.

## Review checklist

- Squint test: is the hierarchy still clear when blurred?
- Does it hold up with long text, empty states, and error states?
- Contrast, tap targets of at least 44px, readable at 200% zoom.
- Does it look like it belongs to its audience, not like a template?

Open the page in a browser or screenshot it and look before delivering.
