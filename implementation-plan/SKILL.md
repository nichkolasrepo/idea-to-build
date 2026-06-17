---
name: implementation-plan
description: Turn a finished architecture.md into a concrete, step-by-step build plan a non-technical builder can execute with their AI build tool, captured in a living implementation.md. Use this whenever someone has settled their architecture and asks what to build first, how to actually build the thing, to turn the architecture into steps or a checklist, for a "build plan" or "implementation plan" or "build roadmap," or says they have their stack and need to start building, or wants to resume or update a build already underway. This is the continuation of the architecture-design skill: it picks up once the architecture exists and sequences the actual building, UI first, to a first working version. If there is no real architecture yet, send them to do that first.
---

# Implementation Plan

This skill turns a decided architecture into a concrete plan for building it. It does not make architecture decisions; it sequences the building of the ones already made, into an order a non-technical builder can follow with their AI build tool, all the way to a first version that runs.

## What you are making

`implementation.md`: a features chart plus an ordered, checkable sequence of feature chunks that turn the decisions in `architecture.md` into something a non-technical builder can build with their AI build tool, ending at a first working version where every core flow runs end to end. It has two readers: the builder, who follows it and checks chunks off, and the AI build tool, which receives each chunk's "what to implement." Write for both (see the register note below).

## First, require an architecture (do not skip this)

This skill only works on top of real architecture decisions. Before anything else, confirm there is an `architecture.md` (or equivalent) that names: the product and its core flows, the specific tools chosen for each layer (an actual database, host, auth provider, and so on, not categories), and the data the product holds.

If that does not exist, or it is hand-wavy (no named tools, no data model, no clear list of what the product does), STOP. Tell the builder plainly that a build plan is only as reliable as the decisions under it, and that sequencing tools nobody has chosen yet just produces fiction. Offer to do the architecture first (the architecture-design skill), then come back. Do not invent an architecture here to keep moving.

## The method: a guided walkthrough

Work through it as a conversation, confirming as you go.

### 0. Read the architecture

Read `architecture.md` end to end and pull out: the product and its features and core flows, and which screen each feature lives on; the exact stack, tool by tool; integrations and the providers chosen; background work; the security and trust model; and any open items still unresolved. The features and their screens come straight from the architecture and drive everything below, so list them before going on. The build tool named there shapes how you phrase every step, so note it now.

**Carry forward any unconfirmed foundation, and do not let it get quieter as it gets more actionable.** If the architecture (or the idea brief behind it) flags that something load-bearing is still unproven, most often that the core pain or demand has not been validated, that warning must travel into this plan at full volume, not softened into a buried "to confirm" line. A build plan is the most motivating document in the funnel: it is a list of checkboxes a builder will want to start ticking. That is exactly why an unproven foundation is most dangerous here, where it is easiest to skip past. State it at the very top of `implementation.md`, before the build steps, and make the first action a validation step (talk to real users, use a throwaway version yourself) that gates the rest. Never produce a confident-looking build plan that sits silently on an unconfirmed idea.

### 1. Confirm the target and the tool

In plain language, restate the full set of things you are going to build. The scope is everything in the architecture: you are not trimming it to a smaller MVP. (If the architecture looks too large for a sane first version, that is an architecture problem, not a planning one. Say so and point back to it rather than quietly cutting features.) State the finish line: a first working version where each core flow runs from start to end. Confirm which build tool they are using if the architecture did not pin it down.

### 2. Sequence the build: UI first, then feature by feature

Always start with the UI. Using the feature-by-screen map, build the screens for the whole product first, with placeholder or mock content where nothing is wired up yet, so the builder can see and click the entire product from the start. This is the opposite of making them wait through a long backend stretch with nothing to look at, and it is what AI build tools are best at.

Then bring the product to life feature by feature, not layer by layer: take one feature at a time and make it fully real (its data, its logic, the integration it needs, and the rule that protects it) so that feature works end to end before the next. Shared groundwork that several features need (accounts and sign-in, common tables) rides along with the first feature that needs it. Present the order of features as your recommendation with the reasoning attached, not as a fixed template, with a line each on why one feature comes before another (usually the feature the core flow depends on first, the ones that hang off it next, the nice-to-haves last). Mark the point where the first feature runs on real data instead of placeholders, and note any hard "do X before Y" dependencies in passing.

### 3. Write each chunk

After the UI shell, each chunk is one feature brought to life (a whole capability, not a single click), and each one carries:

- **What to do**: the task in one line.
- **What to implement**: the substance. The specific thing to build, named against the architecture's actual tools, and written so the builder can hand it straight to their build tool. Phrase it the way that tool expects (see tailoring), and if the instruction would differ on another common tool, add a one-line general note.
- **How to tell it worked**: one plain check the builder can do by hand. Something they click or look at and a result they should see ("book a walk, and it shows up in your bookings list"), never "write a test."
- **On screen / builds**: which screen the feature lives on, and a pointer to the section of `architecture.md` it implements, so the map and the reasoning stay traceable.

### 4. Assemble implementation.md

Build the document from the template: the **features-by-screen chart** near the top (drawn straight from the architecture), then the build itself, UI shell first and then a checkbox chunk per feature in the recommended order, with the marker for where it starts running on real data, a short "you are here" line at the top, and a changelog at the bottom.

### 5. Close

End with what to confirm or watch as they build (a tool limit you were not sure about, an integration to test early) and a reminder that this is a living plan: they check things off and update it as the build teaches them things.

### 6. Before you hand it over

Quick self-check on the finished plan; each item is a way these go wrong:
- **The features-by-screen chart is there**, and every feature in it comes from the architecture and ends up built.
- **Every chunk names a real tool** from the architecture's stack, not a category.
- **Every chunk has a "how to tell it worked"** the builder can actually perform.
- **The UI comes first**, then features one at a time, with nothing depending on something not yet built.
- **The order of features is given as a recommendation, with a one-line reason for each.**
- **The plan covers every feature in the architecture** and ends at a first working version where every core flow runs on real data.
- **The point where the first feature runs on real data is marked.**
- **If the foundation is unconfirmed, that warning is at the top and gates the build**, as loud here as it was in the idea brief, not softened into a buried line.
- **The register matches the builder** (plain by default, precise if they are technical).

## Tailor to the build tool

The named build tool changes how a chunk should read. Lovable and Bolt generate an app from prompts and bundle their own backend (often Supabase), so "what to implement" is a clear product instruction. v0 is interface-first. Cursor, Claude Code, and Codex edit a real codebase, so they can take more precise, file-level direction. Replit builds and hosts in one place. Write each chunk the way the builder's tool expects, and add a short general note so the chunk still makes sense if they switch tools. If you are unsure whether a tool can do something, check on the web rather than asserting it.

## Talk to the builder at their level

Default to plain language: the builder is driving a tool, not hand-writing code, so say what each chunk does in everyday words. If they are clearly technical, write tighter and more precisely and skip the basics. The architecture they hand you is a strong hint at their level; when unsure, ask once.

## Living document

Builders return to this between sessions. On re-entry, read the current `implementation.md`, see what is already checked off, and continue from the first unchecked chunk. If the architecture changed since the plan was written, update the affected chunks and note it in the changelog so the plan and the architecture never drift apart.

## A note on the example

`references/implementation-template.md` shows the structure and the shape of a good chunk. Adapt it to the product in front of you; do not copy its placeholder content.
