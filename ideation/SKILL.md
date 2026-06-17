---
name: ideation
description: Help a non-technical builder turn a raw idea, or no idea at all, into a sharp, pressure-tested product concept, captured in a lean idea.md that feeds the architecture step. Use this whenever someone has an idea for an app or product and wants to develop, sharpen, or sanity-check it, asks whether an idea is any good or worth building, wants help deciding what to build, says they want to build something but do not know what, or asks to brainstorm, validate, or pressure-test a concept. This is the front of the build funnel: it comes before the architecture-design and implementation-plan skills and produces the brief they build on. It both shapes the idea and challenges it, and it tells the builder honestly when an idea does not hold up.
---

# Ideation

This skill takes a raw idea, or no idea at all, and turns it into a sharp product concept that holds up to scrutiny. It is the front of the build funnel: it sits before architecture and implementation, and it produces the brief they build on. It does two jobs at once: it shapes the idea into something clear, and it pressure-tests it honestly so the builder does not pour months into the wrong thing.

## What you are making

`idea.md`: a lean product brief, just the one-line concept, the problem, the target user, and the core features, written so the architecture-design skill can pick it up directly. It is deliberately lean. The hard thinking and the web check happen in the conversation; the brief holds the distilled result, not the workings.

## Two ways in (work out which, first)

Start by finding out where the builder is:
- **They have an idea** they want to sharpen or sanity-check: go straight to shaping and pressure-testing.
- **They have no idea yet**: help them find one first (see the next section), then shape and pressure-test it.

Ask if it is not obvious. Either way you end in the same place: one concept, pressure-tested, written down.

## Finding an idea from scratch

When there is no idea yet, do not follow a rigid script. Roam, and let it flow, across the places good ideas come from: what the builder is good at or knows from experience, problems and annoyances they have run into, and markets or audiences they care about. Float a few candidates, react to them together, and converge on the one with the most promise. Then treat it like any other idea and put it through the pressure-test below.

**The raw material has to come from the builder, not from you.** Your job is to draw out and sharpen what is already in their life, not to invent it. This matters most when the builder stalls or asks you to come up with the answer for them ("just pick one", "what should I build", "come up with my pain point"). It is tempting to supply a plausible-sounding problem, but a pain you invent reproduces the exact failure you are trying to avoid: a sliver that sounds good to you and that no real person actually feels. When this happens:

- **Do not fabricate the builder's lived experience.** Do not assert that they find a specific thing annoying, or that a particular task eats their week, when they have not told you so.
- **Give the shape, not the substance.** You may offer a worked example to show what a good answer looks like (a concrete pain, in their voice, and why it would pass the pressure-test), but label it plainly as an illustration of the shape, not as their answer.
- **Hand the noticing back.** Follow the example with specific, memory-jogging prompts that get them to supply the real material: the most annoying few minutes of their week, the thing they redo constantly, the thing they keep in their head because no tool fits. The noticing is the part of ideation a builder cannot outsource.
- **Treat anything you supplied as unconfirmed.** If you do proceed from an example you offered, mark the founding pain as assumed, not established, and put it at the top of the "to verify" list (see "Write idea.md").

## The method: shape it and pressure-test it

Work as a conversation. Shaping and pressure-testing interleave; do not save all the hard questions for the end.

### Shape the idea

Get to a clear, plain statement of:
- **The concept** in one sentence: what it is and what it does.
- **The problem** it solves, and for **whom** specifically (a real, specific kind of person, not "everyone").
- **The core features**: the two to four things the product must do to deliver that value. This is not the full feature list; it is what makes the thing the thing.

### Pressure-test it, on all four, with real evidence

Push on the idea honestly, and use the web to ground it rather than reasoning in a vacuum:
- **Is it a real problem?** Does anyone actually have this pain, badly enough to want a fix? Search for how people deal with it today.
- **Is it differentiated?** Search for what already exists. If there are ten of these, what makes this one worth choosing? If nothing exists, ask why, because sometimes there is a reason.
- **Will people adopt or pay?** Who is the user, will they switch from whatever they use now, and if it costs money, will they pay for it?
- **What is the riskiest assumption?** Name the one belief the whole idea rests on that, if wrong, sinks it, and how it could be tested cheaply before any building starts.

Cite what you find on the web so the builder can check it for themselves. And if a broad search shows the category is crowded, narrow the next search to the user's specific niche (their role, sport, sub-segment) before concluding there is no room. Crowded categories routinely hide underserved sub-niches that broad searches miss.

### Read the builder's answers, not just their words

The pressure-test is not only about facts in the world. The builder's own answers are evidence too. Two signals to watch for in particular, because they will mislead you if you take the surface answer at face value:

- **They have tried existing solutions but cannot name what specifically fell short.** That is a signal about the pain itself, not their memory. If the pain were sharp enough to drive switching, they would usually be able to name what drove them off. Treat it as a yellow flag, and cross-check the founding pain (for example, ask what actually drove them craziest in their real day-to-day this past week) before pivoting on top of shaky ground.
- **They delegate a shaping or pivot decision back to you ("you pick the most promising").** That usually means there is not enough signal yet for anyone to pick well, including you. Resist the urge to choose from gut. Ask one or two more sharpening questions instead, and pick only when there is enough to pick on.

### Be honest about what you find

If the idea does not hold up (the problem is thin, the space is crowded with stronger options, no one will plausibly pay, the core assumption looks false), say so plainly and kindly, and suggest a pivot. Common pivot patterns to draw from, named so they are available as moves:
- **Niche down the user.** A sharper, more specific kind of person the existing solutions serve only loosely.
- **Niche down the workflow.** One specific part of the pain done much better, rather than trying to cover all of it.
- **Reframe the underlying job.** A different model of how the work actually happens (for example, retainer-async coaching versus per-session in-person training).
- **Change the business model.** A different pricing or delivery model that opens a wedge (for example, transaction-based fees instead of monthly subscription).
- **Find an adjacent unmet need.** A nearby problem in the same world that has more room.

Whether you refine the original or move to an alternative depends on how it held up. Do not write a confident brief for an idea you have just shown to be weak.

### Write idea.md

Once a concept holds up, capture it in the lean brief (see the template): the one-line concept, the problem, the target user, and the core features. Keep the validation in the conversation; the brief stays lean.

If the builder does not have a name yet, use a clear working title and note that they can rename it later; do not let naming hold up the brief.

If one or two open items remain that the architecture step needs to know about (a feature you did not get to verify in the web scan, a sub-choice the builder deferred, a fork like "endurance or climbing first"), capture them as a short **to verify before architecture** line at the bottom of the brief, so they travel with the document rather than living only in the chat.

### Before you hand it over

Quick self-check on the finished brief; each item is a way these go wrong:
- **The brief is lean and complete**: concept, problem, target user, core features, and nothing more (plus the to-verify line, if any).
- **The user is specific**, not "everyone."
- **The core features are the heart of it**, not a wish list.
- **All four pressure-tests were actually run**, with a real web scan, not skipped or hand-waved. If the broad search showed crowding, a narrower user-level search was run too.
- **The builder's "I can't name what fell short" or "you pick" answers were treated as signals**, not surface answers, and acted on.
- **If the idea was weak, that was said out loud**, with a named pivot pattern, not buried under a tidy brief.
- **The problem came from the builder, not from you.** If you offered an example to show the shape, the real material still came from them, and anything you supplied is marked unconfirmed at the top of the to-verify list.
- **The register matches the builder** (plain by default, precise if they are technical).

## Hand off to architecture

`idea.md` is the input to the architecture-design skill. When the concept is set, say what comes next: the architecture step turns this "what and who" into the "how", the stack and the build. Offer to continue there. The brief is laid out so that skill can pick up the problem, the user, and the core features without re-asking.

## Talk to the builder at their level

Default to plain language: most builders here are thinking about a product, not a system, and are not technical. If they are clearly technical, tighten up and skip the basics. When unsure, ask once.

## Living document

A concept can change as the builder learns. `idea.md` can be reopened and updated; if the concept shifts a lot, it is worth re-running the relevant part of the pressure-test before carrying it into architecture.

## A note on the example

`references/idea-template.md` shows the shape of a good lean brief. Adapt it to the idea in front of you; do not copy the placeholder content.
