# Capability: original visual and generative art

## Ground rules

- Make original work. Do not reproduce a specific artwork, logo, poster, album
  cover, or a known character or mascot, even in a different style.
- Generic subjects and invented characters are fine. Public-domain works are fine.
- If a request clearly points at a protected work, say so once and offer an
  original alternative that shares none of its signature features.

## Generative art (code)

Make the piece reproducible and explorable.

- Seed all randomness (`randomSeed(seed)` / `noiseSeed(seed)` in p5.js,
  `random.seed(seed)` in Python) and display the seed.
- Expose a few parameters (density, scale, palette, noise frequency).
- Good starting systems: flow fields (Perlin noise to angle), particle trails,
  recursive subdivision, circle packing, L-systems, reaction-diffusion.
- Limited palette of 3-5 colours; vary value (light/dark) for depth.
- Render a still and look at it; iterate on composition, not just effects.

## Posters and static designs

1. State the concept and mood in two lines.
2. Choose one dominant element and a clear reading order.
3. Type: one headline face, one text face; generous margins.
4. Build in HTML/CSS or SVG, export to PNG or PDF at print resolution
   (300 dpi at final size).
5. Check bleed and margins if it will be printed.

## Animation and GIFs

- Keep loops short (1-3 s), few colours, small canvas for chat tools.
- Ease motion; avoid linear movement.
- Respect size limits of the destination (for example under 2 MB for Slack emoji-style GIFs).

## Brand-style work

Apply a brand's colours and type only when the person supplies the guidelines
or says it is their brand. Do not imitate another company's identity.
