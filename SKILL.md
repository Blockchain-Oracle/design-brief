---
name: design-brief
description: Standing brief for any UI work. Don't invent the design, source it. Take the look and the screen patterns from Refero (real shipped products) and the components from 21st.dev (finished, community-rated components), then adapt them to one set of tokens. Use whenever you build, redesign or polish a page, screen, section or component (landing pages, dashboards, onboarding, forms, empty and loading states), when planning the UI of a new product, and whenever the user says the UI looks generic, AI-generated, "vibe-coded" or mediocre, even if they never mention Refero or 21st.dev.
---

# Design brief

Left alone, a coding agent designs from memory, and memory gives the average of everything: the centred hero, the purple gradient, three cards with an icon each. Real products have already solved every screen you are about to build, and finished components already exist that are better than anything improvised in one sitting. So treat your own design instincts as average and stop inventing. The job is to **find, compare, pick and adapt**.

Two sources do the work, and they do different jobs:

| Source | What it gives you | Use it for |
|---|---|---|
| **Refero** | Screens, flows and styles from real shipped products | Deciding what a screen should do and look like |
| **21st.dev** | Finished components made by people and rated by the community | The actual component that goes into the code |

Refero tells you what to build; 21st.dev hands you the part. Use both. A component picked without a reference is often pretty but wrong for the screen, and a reference without a component gets rebuilt by hand, badly.

## Setup

```bash
# Refero (an MCP server). Then run /mcp and sign in.
claude mcp add --transport http refero https://api.refero.design/mcp

# 21st.dev CLI
npx @21st-dev/cli login     # opens the browser; afterwards the command is `21st`
21st whoami                 # check you are signed in
```

Searching and previews are free on 21st.dev. Pulling a component's code uses a daily quota (`21st usage` shows what's left), so compare first and pull only what you've chosen.

If a tool is missing or signed out, tell the user once, with the command that fixes it, and carry on with the one that works. Don't quietly fall back to hand-built UI.

## Order of work

1. Settle the direction: colours and type.
2. Find the pattern for each screen and flow in Refero.
3. Pick the component for each section from 21st.dev.
4. Adapt everything to one set of tokens.
5. Check the result against the quality bar, in the running app.

For anything bigger than one component, write the UI plan down before coding (template at the end). It is a small table, and it is what stops a screen being improvised halfway through the build.

## 1. Direction

- Colours and type come from what the user already has: their `DESIGN.md`, their existing design system, or a reference they name. Don't override it.
- If they've given nothing, ground the direction in Refero styles from best-in-class products: `refero_search_styles`, then `refero_get_style` on the strongest two or three. Don't default to the framework's stock theme, or to the brand palette of the platform you're building on. That is how every project on that platform ends up looking alike.
- Pick one dominant style and keep its sharp traits. Borrow one or two details from the others. Averaging several references gives the safe middle you were trying to avoid.
- Support light and dark.
- Deliver one design. Don't hand the user three option sets to choose from unless they ask for options; choosing is the work they gave you.
- Write the result down as tokens (colour roles, type scale, spacing, radius, shadows) before installing any component, so every later choice resolves to a token.

## 2. Patterns from Refero

| Tool | Answers | Example query |
|---|---|---|
| `refero_search_styles`, then `refero_get_style` | What should it look and feel like? | `premium fintech website with restrained typography` |
| `refero_search_screens`, then `refero_get_screen` | What goes on this screen, and in which states? | `dashboard empty state`, `data table filters` |
| `refero_search_flows`, then `refero_get_flow` | What are the steps of this journey? | `signup onboarding`, `subscription cancellation` |

Screen and flow searches need a `platform`: `web` or `ios`.

- **Search for what is literally on the screen** ("pricing page annual monthly toggle"), not for adjectives. Adjectives belong in a styles search.
- **Try three to five angles per screen,** including a known product that does it well. The first result is rarely the best one.
- **Look up the states too,** not just the happy screen: empty, loading, error, success.
- When one screen is close, `refero_get_similar_screens` finds its relatives quickly.
- **Keep two or three references per screen** and note what you take from each: structure, hierarchy, states, wording. References inform the screen. They aren't a template to copy.

## 3. Components from 21st.dev

21st.dev is a curated catalog of finished components, not AI generation. For every piece of UI (header, inputs, cards, dropdowns, chat, loading states, animations), search, compare and use the best one.

```bash
21st search "<component>" --type c --limit 10     # components only
21st get <id>                                     # print the code and demo of the one you chose
21st add <author>/<slug>                          # install it (shadcn under the hood)
npx shadcn@latest add "https://21st.dev/r/<author>/<slug>"   # the same install with stock shadcn
21st logo <brand>                                 # real brand logos as SVG, free
```

How to pick:

1. **Search by the slot, not the mood.** "Pricing table", "command menu", "file upload", not "modern clean section". Try two or three wordings.
2. **Compare several, and never take the first hit.** Open the previews. A name and a description don't tell you how a component looks or moves.
3. **Prefer the most downloaded or bookmarked.** The counts are on each component's page on 21st.dev. Popularity is evidence that a component works in real projects. It doesn't prove fit, which is the next check.
4. **Check fit against the Refero reference for that screen.** It should do the same job at the right density, and have the states you need (hover, focus, disabled, loading, empty). Check that it holds up at phone width and with the keyboard, and look at the dependencies it brings.
5. **Adapt one or two things** to your tokens: colour, radius, font. If you find yourself rewriting the component, you picked the wrong one. Go back and pick again.
6. **Keep siblings coherent.** Components from different authors must read as one product once they are reskinned.
7. **Hand-build only the glue** that has no candidate, and say so.

Report each pick so the user can swap it: `section · component · author · one-line why`.

## 4. Quality bar

- Real logos, not generic icons and coloured dots.
- Little text. No walls of copy; let the interface carry it.
- Real UI patterns: tabs, dropdowns, modals, toggles, charts. Not everything is a stack of cards.
- Good loading, empty and error states, with progress for slow actions.
- Motion, and sound and haptics where they fit.
- Everything discoverable: every page reachable from where people already are, and anything clickable looks clickable.
- Low-friction onboarding.
- Flows stay inside the app instead of sending people to third-party sites.
- Responsive, and mobile feels native rather than a shrunk desktop.
- One complaint is a pattern. When the user flags one thing, find and fix its siblings across the app.

Mediocre is never an option.

## 5. Check it in the running app

Open the app in the browser or simulator and use it: light and dark, desktop and phone width, the empty and loading states. Compare each screen with its references and fix the drift. The research is not the finish line; the rendered screen is.

## UI plan template

```markdown
**Direction:** <the user's DESIGN.md, or Refero styles: name, name> · light and dark
**Tokens:** <colour roles, fonts, radius, spacing>

| Screen or flow | Refero references | What we take | 21st.dev component |
|---|---|---|---|
| Onboarding | <app: screen>, <app: flow> | Three steps, progress bar, skip | <author>/<slug> |

**Hand-built (no candidate):** <what, and why>
```
