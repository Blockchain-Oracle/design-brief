# design-brief

A skill for coding agents (Claude Code, Codex and others that read `SKILL.md`). It stops the agent inventing UI from memory and makes it source the design instead:

- **Refero** for what a screen should do and look like, taken from real shipped products.
- **21st.dev** for the finished component that goes into the code.

## What it tells the agent

1. **Direction.** Colours and type come from your `DESIGN.md` or a reference you name. With neither, it grounds them in Refero styles, in light and dark, and delivers one design.
2. **Patterns from Refero.** Which tool answers which question (styles, screens, flows), how to search, and to look up empty, loading and error states too.
3. **Components from 21st.dev.** How to pick one: search by the slot, compare several, prefer the most downloaded or bookmarked, check it fits the reference, adapt one or two things, and hand-build only what has no candidate.
4. **A quality bar.** Real logos, little text, real UI patterns, good loading states, everything discoverable, mobile that feels native.
5. **Check it in the running app,** not just in the plan.

## What you need

| Tool | Setup |
|---|---|
| [Refero](https://refero.design/mcp) MCP | `claude mcp add --transport http refero https://api.refero.design/mcp`, then sign in with `/mcp` |
| [21st.dev](https://21st.dev) CLI | `npx @21st-dev/cli login` |

## Install

```bash
git clone https://github.com/Blockchain-Oracle/design-brief ~/.claude/skills/design-brief
```

For another agent, clone it into that agent's skills folder instead.

Then ask for any UI work ("build the pricing page", "this dashboard looks generic"), or run `/design-brief`.

## Works well with

- [`refero-design`](https://github.com/referodesign/refero_skill): Refero's own skill, with deeper research method and craft references.
- `21st-cli-use`: ships with the 21st CLI (`21st install-skill`); covers sign-in, quota and installs in detail.
- [`premium-ui`](https://github.com/Blockchain-Oracle/premium-ui-skill): section-by-section picks from premium component registries.
