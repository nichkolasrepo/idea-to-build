# Build Funnel Skills

A suite of three AI agent skills that walk a non-technical builder from a raw idea to a concrete build plan, in plain language, one honest step at a time. Each skill runs as a guided conversation and produces one living document that feeds the next.

They are written in the portable [Agent Skills](https://docs.claude.com) format — a `SKILL.md` plus a `references/` folder — but nothing in them is tied to one vendor. The content is a methodology, not a product: any AI assistant or build tool that can read a prompt can run these, and the documents they produce target whatever you build with (Cursor, Lovable, Bolt, Replit, Codex, v0, Claude Code, or a human developer).

## The three skills

1. **ideation** — Turns a raw idea, or no idea at all, into a sharp, pressure-tested product concept. It both shapes the idea and challenges it (real problem, differentiation, adoption, riskiest assumption), scans the real market on the web, and tells the builder honestly when an idea does not hold up. Output: a lean `idea.md`.
2. **architecture-design** — Turns the concept into a full technical plan: stack, hosting, data, auth, integrations, security, cost, and how the pieces fit. Opinionated, names real products, and gives the why and a named alternative for every choice. Output: a living `architecture.md`.
3. **implementation-plan** — Turns the architecture into an ordered, checkable build plan a builder can execute with an AI build tool (UI first, then feature by feature), ending at a first working version. Output: a living `implementation.md`.

## How they chain

```
raw idea  ->  ideation  ->  idea.md
                              |
              architecture-design  ->  architecture.md
                                            |
                          implementation-plan  ->  implementation.md  ->  build
```

Each document is the input to the next skill. The handoff runs both ways: if the architecture step finds the concept rests on a false premise, it sends the builder back to ideation rather than building on sand. Honesty about how proven an idea is travels the whole length of the funnel.

## Repository structure

```
ideation/
  SKILL.md
  references/idea-template.md
architecture-design/
  SKILL.md
  references/architecture-template.md
implementation-plan/
  SKILL.md
  references/implementation-template.md
```

Each top-level folder is a self-contained skill: a `SKILL.md` (the instructions the agent follows, including when to trigger) plus a `references/` folder holding the template that skill fills in.

## Using these

Each folder is a self-contained skill in the Agent Skills format, so there are two ways to use it:

- **As an installed skill.** If your AI tool reads the Agent Skills format (for example Claude — via the apps, the API, or Claude Code), drop the skill's folder wherever that tool loads skills from. Follow your tool's current skills documentation for the exact route.
- **As a prompt, anywhere.** Nothing requires a skill loader. Paste a `SKILL.md` (and its template) into any capable AI assistant as instructions, and it will run the same guided conversation. The output documents are plain Markdown that any build tool or developer can act on.

## Notes

- All three are designed for non-technical builders, with an adaptive register that tightens up if the builder is technical.
- They are living documents: the builder reopens each output and grows it across sessions.
- Built and refined through repeated real-world test runs.
