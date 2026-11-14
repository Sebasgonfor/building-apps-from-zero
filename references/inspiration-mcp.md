# Agent-readable inspiration sources (verified 2026-11-13)

Recommended setup: `design-index` and `playwright` at user scope; `mobbin` at user scope if your account allows it (OAuth sign-in once via `/mcp`); shadcn MCP per project when the project uses shadcn.

Check that a server is connected (`claude mcp list`) before relying on it. If it is not, say so and fall back to the `design-taste-frontend` library plus cited links from the free sources table in `ui-design-system.md`. Re-verify pricing before recommending a paid one; these change often.

| Source | Status | Free? | Returns | Setup |
|--------|--------|-------|---------|-------|
| `design-taste-frontend` skill | Installed locally | Yes, offline | Researched directions, type, palettes, compositions from 247 real sites | Already in `~/.claude/skills` |
| Index (index.chele.bi) | Exists, about 1,650 design resources, updated 2026-10 | Yes, no key | Catalog of galleries, design systems, type, motion and component resources (links, not screenshots) | `claude mcp add --transport http --scope user design-index https://index-mcp.chele.bi/mcp` |
| shadcn/ui MCP | Official, MIT, runs locally | Yes | Registry components as code, browse and install | Per project: `npx shadcn@latest mcp init --client claude` |
| Mobbin MCP | Official, OAuth, `https://api.mobbin.com/mcp` | Plan requirement unverified | Real app screenshots (image URLs expire after 30 days), no code | Try with a free account before depending on it |
| Figma MCP (official) | Exists | Starter plan: 20 read calls/month, View/Collab seats only | Design files, components, variables, layout | Only for implementing a chosen Figma design |
| 21st.dev Magic | Exists | Credit-limited free tier | Component code and AI generation | Optional |
| Refero | MCP only on paid plans | No | Real web app screens | Use the website manually |
| Built-in browser (Claude desktop app) | Available in desktop sessions | Yes | Navigation, screenshots, page text | Nothing to install: `mcp__Claude_Browser__*` tools |
| Playwright MCP (Microsoft) | Open source | Yes | Navigation, screenshots, accessibility tree | Terminal sessions: `claude mcp add --scope user playwright -- npx @playwright/mcp@latest` |

Not found: a "Frontend Inspo MCP" open-source repo as described by some AI answers. Do not cite it.
