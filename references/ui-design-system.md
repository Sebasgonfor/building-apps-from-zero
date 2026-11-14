# Stage 4 — UI Design and Design System

Goal: turn validated flows and wireframes into an interface that is distinctive, consistent, accessible, responsive and ready to build. Quality comes from clear hierarchy, consistent spacing, careful type, coherent components and predictable behavior. Effects, gradients and shadows complement those bases; they never replace them.

## 4.1 Visual research and art direction (before any token)

The model's default look is the average of every interface it has seen. Replace defaults with decisions taken from real references.

1. **Research 5-10 real products** that solve a similar problem. Note navigation, hierarchy, forms, data density, states.
2. **Derive three clearly different directions** from what the research showed. Combine sources: Index MCP to discover references, the browser to open and screenshot them, product galleries (Mobbin, Refero, Page Flows) for shipped patterns, art-direction galleries (Awwwards, Land-book) for composition and type. `design-taste-frontend` is one optional source among these (a library distilled from 247 curated sites that can deal directions), not a required step.
3. **Build an intentional moodboard.** For each reference, write which decision you take from it (type, composition, color, icons, motion) and why it fits this product.
4. **Present the three directions with trade-offs and wait for the user to pick one.** The user approves the art direction; Claude never picks it alone.
5. **Design one pilot screen** with real content, navigation, a form or input, components and its states.
6. **Score it** with the rubric below, refine, then extend to the rest.

Research pipeline: find references (Index MCP, the free sources below) → open each in a browser and screenshot it → analyze what the screenshots show → deal three directions → user picks → design system → build with shadcn components.

Browser for looking: in the Claude desktop app use the built-in browser (`mcp__Claude_Browser__*`: navigate, screenshot, read page); in a terminal session use Playwright MCP. `design-taste-frontend` also screenshots your own pages with its inspector. Respect each site's terms: look and screenshot, never bulk-scrape.

Research rules:
- **Never claim to have analyzed a design you have not seen.** Visual claims (composition, hierarchy, type, spacing, color) require a screenshot or rendered page you actually viewed in this session. If you could not open it, say so and limit yourself to what the source text states.
- Cite a link for every external reference; never invent a reference. Say plainly when a source could not be reached.
- Separate proven UX patterns (shipped products) from experimental visuals (galleries, concepts).
- Take decisions, never copy whole screens, and do not mix incompatible styles.

### Free sources

| Need | Source | Use it for |
|------|--------|-----------|
| Discovery of references | Index MCP | Find galleries, design systems, type and motion resources to open |
| Researched directions, offline | `design-taste-frontend` skill library (optional) | Directions, type systems, palettes, compositions distilled from real sites |
| Real app screens and flows | Mobbin (free tier), Page Flows | Onboarding, settings, payments, empty and error states as shipped |
| Real web/SaaS screens | Refero | Concrete screens and patterns for web apps |
| Art direction, composition, type | Awwwards, Land-book | Distinctive layouts; check usability, many prioritize experiment |
| Visual concepts | Dribbble | Graphic treatment and icon ideas only; many shots were never built |
| Products worth studying | Linear (hierarchy, density), Notion (content organization), Stripe Dashboard (tables, forms), Raycast (speed, keyboard, feedback) | Study one decision each, then build a different identity |
| Type | Typewolf | Pairings seen in real sites |
| Color | Coolors | Explore palettes, then verify contrast |
| Icons | Lucide, Phosphor | One family per product |
| Components and systems | Component Gallery, Material Design 3, Apple HIG, shadcn/ui | How real systems name, vary and document components |
| Motion | Motion (motion.dev) | Implementation patterns for transitions |

Agent-readable sources (MCP servers), their verified status, cost and setup: `references/inspiration-mcp.md`. Use the connected ones; never claim a source you could not reach.

### Direction rubric (1-5 each)

| Criterion | Question |
|-----------|----------|
| Distinct identity | Does it look like no generic AI template? |
| Visual hierarchy | Is what matters obvious at first glance? |
| Coherence | Do components, type and spacing follow one logic? |
| Usability | Does it make the real tasks easier? |
| Fit | Does the style match the product, context and audience? |
| Detail | Are states, copy and interactions cared for? |

Below 4 on average: explore and refine before extending.

## 4.2 Design tokens

Name tokens by role, never by value: `color.text.primary`, `color.surface.elevated`, `color.border.subtle`, `color.action.primary`, `color.status.danger`. Components use tokens only, so a theme change touches one file.

| Token | Controls |
|-------|----------|
| Color | Backgrounds, surfaces, text, borders, actions, states (success, warning, danger, info), light and dark |
| Typography | Families, sizes, weights, line heights, letter spacing |
| Spacing | A fixed scale (for example 4, 8, 12, 16, 24, 32) for padding and gaps |
| Radius | Rounding per component size |
| Elevation | Shadows and depth levels |
| Borders | Width, style, color |
| Breakpoints | Where composition changes |
| Motion | Durations and easing curves per interaction type |
| Opacity | Disabled, overlays, dimmed states |
| Z-index | Layers: dropdowns, sticky headers, modals, toasts |

Type scale: define display, heading, subheading, body, caption with size and line height, adapted to platform, audience and accessibility.

## 4.3 Component library

Build only the components the product uses now. For each important one document: variants and sizes; states (default, hover, focus, pressed, disabled, loading, error as they apply); props and behavior; correct and incorrect use; accessibility and keyboard; responsive behavior. Prefer an existing accessible base (shadcn/ui, Radix) over inventing one.

## 4.4 Motion

An animation must communicate, keep continuity or give feedback; if it does none, remove it. Define when transitions happen, what may animate, durations per interaction (many micro-interactions land around 100-300 ms, not a universal rule), easing, and the reduced-motion fallback. Animate `transform` and `opacity`.

## 4.5 Responsive and accessibility

- Composition changes per device, not just shrinking: desktop distributes content and may use side navigation; mobile prioritizes content, compacts navigation, uses touch targets. Also tablets, landscape, browser zoom, enlarged system fonts, safe areas, touch vs pointer.
- WCAG 2.2 AA where it applies: contrast, target size, visible focus, keyboard, screen readers, motion alternatives. Never use color alone to signal an error or state.

## 4.6 Final screens

1. Take one flow validated in UX.
2. Apply the chosen direction and tokens.
3. Build screens from reusable components.
4. Complete states, variants and responsive versions.
5. Review consistency, accessibility and behavior (`ui-polish`, `impeccable`).
6. Validate before development.

Never generate each screen independently with AI: it produces inconsistent spacing, type, icons and components. The AI follows the design system; it does not invent a new one per screen.

### Brief for Claude Design or any design agent

Context: the PRD and UX flows. References: attached screenshots and links; extract design decisions, do not copy screens. Goals: distinctive coherent identity, legibility and hierarchy first, realistic domain content, reusable components, states, accessibility, responsive. Constraints: no decorative gradients without reason, no glassmorphism or heavy shadows, no needless cards, no generic dashboards with filler charts, no invented metrics or features, no animation that communicates nothing, no literal copies. Process: analyze references → propose three distinct directions with trade-offs → wait for the choice → design one representative screen → refine before extending.

## Deliverables

Real product: `docs/design/` with `visual-direction.md`, `design-tokens.md`, `typography.md`, `color-system.md`, `component-library.md`, `motion-guidelines.md`, `responsive-guidelines.md`, `accessibility.md`, `screens/`.

Small project: one `docs/design-system.md` (direction, tokens, type scale, components used, motion rules, responsive and accessibility notes) plus tokens in code (CSS variables or Tailwind theme).

## Done when

- [ ] Visual direction chosen by the user from three researched options, with cited references
- [ ] Palette and semantic colors documented, light and dark if applicable
- [ ] Type scale and spacing consistent
- [ ] Tokens defined and used by components
- [ ] Main components have variants and states
- [ ] Interactions and animations specified
- [ ] Critical screens have final design
- [ ] Target devices have adaptations
- [ ] Accessibility requirements verified
- [ ] Designs ready to implement with no improvisation left
