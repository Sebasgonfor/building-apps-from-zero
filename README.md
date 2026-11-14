# building-apps-from-zero

A [Claude Code](https://claude.com/claude-code) skill that makes the agent build new apps the way a disciplined product team would: discovery before the PRD, UX before visuals, real references before any UI, vertical slices with a Definition of Done, and nothing called "done" without evidence.

## What it enforces

- **Nine stages, each with required outputs:** discovery, PRD, UX, UI and design system, architecture, roadmap and plan, implementation, QA and polish, release.
- **Polish per slice, not at the end:** every slice meets the same Definition of Done (states, motion, keyboard, 375 px, tokens, tests) before the next starts.
- **Deploy on day 1:** slice 1 is a walking skeleton live with CI.
- **No AI slop:** visual research from real, cited references opened in a browser; three directions; the user picks.
- **Quality gates:** feature, integration and release gates; an agent saying "done" is not evidence.
- **Docs sized to the project:** a class project gets one PRD; a real product gets the full `docs/` tree.

## Install

```bash
git clone https://github.com/Sebasgonfor/building-apps-from-zero ~/.claude/skills/building-apps-from-zero
```

Claude Code loads it automatically when you start a new app, write a PRD, plan a product or ask for a polished UI.

## Structure

| File | Stage |
|------|-------|
| `SKILL.md` | Stage map, quality gates, state matrix, Definition of Done, red flags |
| `references/discovery.md` | 1. Product discovery |
| `references/prd.md` | 2. PRD |
| `references/ux.md` | 3. UX design |
| `references/ui-design-system.md` | 4. UI and design system |
| `references/inspiration-mcp.md` | Verified free inspiration sources and MCP servers |
| `references/architecture.md` | 5. Architecture and technical design |
| `references/planning.md` | 6. Roadmap and implementation planning |
| `references/implementation.md` | 7. Implementation workflow |
| `references/qa-polish.md` | 8. QA, UX validation and polish |
| `references/build-and-quality.md` | 9. Release and continuous improvement |

## Works best with

Optional companion skills it calls by name when installed: [superpowers](https://github.com/obra/superpowers) (`brainstorming`, `writing-plans`), `ui-polish`, `impeccable`, `ui-design-system`. Without them the skill still works; those steps fall back to the reference files.

## License

[MIT](LICENSE)
