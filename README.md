# claude-mode

A portable skill that gives an AI coding/agent environment (built for Google
Antigravity, usable in any skill-aware agent) a careful, evidence-first working
style plus practical know-how for common deliverables.

## What is inside

```
claude-mode/
  SKILL.md                     core loop, principles, routing tables
  GEMINI-rules-snippet.md      12 short always-on rules for global rules files
  references/                  process: planning, recon, verification, research,
                               deliverables, communication, context-and-memory,
                               safety-and-honesty
  capabilities/                how-to modules: docx, xlsx, pptx, pdf,
                               frontend-design, data-viz, deep-research,
                               coauthoring-and-comms, skills-and-mcp, teaching,
                               visual-art, browser-and-computer
```

`SKILL.md` is short on purpose. The agent opens a reference or capability file
only when the task needs it.

## Install (Antigravity)

Pick one:

- **This project only:** copy the `claude-mode` folder to
  `<your-project>/.agent/skills/claude-mode/`
- **All projects:** copy it to `~/.gemini/antigravity/skills/claude-mode/`

Paths can differ between Antigravity versions. If the skill is not picked up,
check the Skills section in Antigravity's settings for the current location.

Optional but recommended: paste the contents of `GEMINI-rules-snippet.md` into
your global rules (`~/.gemini/GEMINI.md`) so the core habits apply even when the
skill does not auto-trigger.

## Test it

Run the same 3-5 tasks from your own work with and without the skill. Compare
whether the result works and whether claims were backed by output. Adjust the
`description` in `SKILL.md` if it triggers too often or never.

## Honest limits

- A skill changes how the model works, not how capable it is. Gemini will not
  become another model.
- Antigravity may not provide every tool the guidance mentions (parallel
  helpers, persistent memory, browser control). The guidance degrades gracefully:
  the agent should use what exists and skip the rest.
- The capability modules assume common tools are installed: Python with
  python-docx, openpyxl, python-pptx, pypdf, pdfplumber, reportlab; LibreOffice
  (`soffice`), poppler (`pdftoppm`), pandoc, tesseract. Install what is missing.
- Skills tied to specific products (CRMs, design tools, finance platforms) are
  not included because they depend on connectors Antigravity does not have.
- This is original guidance written for portability. It is not a copy of any
  vendor's bundled skills.
