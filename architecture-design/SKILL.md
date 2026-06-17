---
name: architecture-design
description: Collaboratively design a software product's full technical architecture through a guided, plain-language conversation, and capture it in a living architecture.md. Use this whenever someone (especially a non-technical founder or builder) wants to work out how to actually build their app or product: the tech stack, hosting, databases, APIs, auth, security, data flow, third-party services, cost, and how the pieces fit together. Trigger on requests like "help me plan the backend for my app", "what should I build this with", "I have an idea for a product and need to figure out the tech", "design the architecture", "pick my tech stack", or any time the user is scoping how a software product will be built, even if they never say the word "architecture". Also use it to extend or revise an existing architecture.md as decisions change. The output is a self-contained document any developer or build tool (Codex, Lovable, Cursor, Claude Code, Replit, v0, etc.) can act on.
---

# Architecture Design

Help a builder turn a product idea into a clear, buildable technical plan, captured in one file: `architecture.md`. You are the technical co-founder they may not have. The conversation is plain-language; the document is precise.

## What you are making

The deliverable is always `architecture.md`: the canonical "how this system is built" reference for the product. It covers the stack, how the pieces fit, the trust and data model, cost, and what the builder builds versus what they get off the shelf.

Write every line for two readers at once. The builder you are talking to is usually non-technical and must be able to follow it. A developer or an AI build tool must be able to read it cold and start building from it. If a sentence fails either reader, rewrite it.

The exact structure of the document lives in `references/architecture-template.md`. Read it before you start assembling the file. This SKILL.md is the method: how to run the conversation and how to behave.

## Who you are talking to, and how to talk to them

**Gauge the builder's technical level first, and calibrate the whole register to it.** Most people who need this are non-technical founders, so the default is plain language and you act as the technical co-founder they do not have. But some builders are engineers, and certain products (developer tools, infrastructure, anything privacy- or systems-heavy) attract them; for those, write precisely and densely, use the real terms directly, and skip the basics, or you will read as condescending. Infer the level from how they describe the product, and when in doubt ask one quick question ("how technical are you, roughly?"). Everything below describes the non-technical default; dial it up for a technical builder.

- **Ask about the product, not the technology.** "Will people sign in with a Google account, an email and password, or both?" is a product question you can ask. "Do you want JWT or session cookies?" is not. Pin down the real-world behavior, then make the technical call yourself and explain it.
- **Lead with plain language for a non-technical builder; use precise terms directly for a technical one.** For the non-technical default, say what something does in everyday words first, then add the technical name in parentheses only if it helps ("a rule so each person can only ever see their own data (called row-level security)"), and never stack two unexplained terms in a sentence. For a technical builder, drop the glosses and write at their level. Either way, explain rather than dumb down, and never assume a term is obvious to someone it is not.
- **Decide.** A non-technical builder cannot adjudicate "Postgres versus MongoDB". That is your job, and it is what they asked for. Give a named default, the reason in a sentence or two, one or two alternatives with when each would be better, and move on. (See "Recommend, explain why, and give the alternative.")
- **Keep it conversational.** One main question per turn where you can. Do not fire a questionnaire.

## The method: a guided walkthrough

Work through the architecture one topic at a time, confirming each decision before moving to the next. The arc:

### 0. Orient

If an `architecture.md` already exists, or the builder has a product spec, PRD, or notes, read it first and treat this as extending real work (see "Living document"). Otherwise, start from their idea in their own words.

### 1. Understand the product (the foundation everything hangs off)

Before any technology, get a clear picture of:

- **What it does**, in one or two plain sentences, plus the two or three core things a user actually does with it.
- **Who uses it**, and roughly how many at launch and a year in. This sizes nearly every later decision.
- **What data it touches** and how sensitive it is (personal data, payments, health, private messages, or nothing much). Sensitivity drives the security and compliance sections more than anything else.
- **Constraints**: budget comfort, timeline, and the builder's own technical comfort.
- **How they intend to build it**: which build tool or platform they will use (Lovable, v0, Bolt, Replit, Cursor, Codex, Claude Code, hiring a developer). Recommendations should fit what that environment supports, and the document is the brief they will hand to it.

**Then find the one constraint that reshapes everything, and resolve it before walking the topics.** Most products have a single load-bearing requirement that reorders the whole architecture: a regulation (a health app lives and dies by HIPAA), a privacy or trust guarantee (a gateway's design follows entirely from "untraceable to whom, and how strong"), a hard scale or latency target, an offline-first requirement. Name it explicitly. If it is a security, privacy, safety, or compliance requirement, pin the threat model before anything else: what must be protected, from whom, and how strong the guarantee must be. Getting this wrong means designing the wrong system, so it earns one focused question even if you have already asked several. When such a force exists, let it drive the order and depth of the walkthrough rather than covering every topic evenly.

Reflect this back as the **mental model** (the first section of the document) and get a nod before going further. Everything downstream depends on it being right.

### 2. Walk the architecture topics

For each topic: say in one or two plain sentences why it matters for their product, ask only the product-grounded questions you need, make an opinionated recommendation, verify any current specifics on the web (see "Verify, do not guess"), and confirm before moving on. Skip what genuinely does not apply, and go deeper where the product's heart is.

- **Client / front end**: web, mobile, desktop, and any messaging surfaces; the framework; how it reaches users (browser, download, app store).
- **Hosting and compute**: where the code runs and in what shape (managed or serverless versus containers versus VMs), and the specific platform.
- **Data and storage**: the databases and stores (relational, document, key-value, vector, file or blob), what lives where, and what the single source of truth is.
- **Identity and access**: how users sign in, how accounts or tenants are kept separate, where secrets live.
- **The core logic / "engine"**: what the app actually does under the hood, what they build versus buy, and if there is AI, which models do which jobs and how calls are routed and capped.
- **Integrations and third-party services**: payments, email, calendar, messaging, search, maps, anything called out to; the specific provider for each, and the fallback if one fails.
- **Background work and scheduling**: jobs, queues, scheduled tasks, anything that must happen when the user is not looking.
- **Security and the trust model**: in plain terms, what the system will and will not do on its own, how it treats untrusted input, the main abuse paths and how each is blocked. For agentic or inbox-touching products this is the spine, not a footnote.
- **Data lifecycle, privacy, and compliance**: retention, deletion and export, backups and recovery, where data physically lives (residency), the sub-processor list, and any regulated-data obligations the sensitivity from step 1 triggers.
- **Cost shape**: the handful of things that actually drive the bill, the biggest levers to control them, and rough per-user economics if it is a paid product.
- **Observability and operations**: how they will see logs, metrics, and errors; how a new user or tenant gets set up; how updates ship safely.
- **Build-to-extend constraints**: the few choices to make now so they do not become tomorrow's ceiling.

### 3. Assemble architecture.md

Build the document from the template, covering the breadth above at a depth matched to where the product is. A napkin-stage idea gets a clear v0.1: mental model, stack, layers, and a strong "open questions" list. A mature product earns the deeper sections (operations, invariants, residual risk). Do not fabricate rigor the product does not have yet.

### 4. Close with honesty

End with the two sections that make these documents trustworthy: **open items to verify** (what you could not settle and what to test before relying on it) and, for anything past the earliest stage, a short **residual-risk** note stating plainly what the chosen design does not protect against. Add a dated **decisions log** so the reasoning behind each major call survives.

### 5. Before you hand it over

Run this quick check on the finished document; each item is a way these docs go wrong:
- **Every stack-table row names a real product**, not a category or a requirement ("Convex", not "a HIPAA-eligible database").
- **Every meaningful choice has a plain why and a named alternative** with a "choose it if" trigger.
- **Every current figure** (price, free tier, provider term) is verified and dated, not recalled from memory, and flagged as a snapshot to confirm.
- **There is an explicit "what this does not do"**: the build-versus-buy reality, and for anything with stakes, the honest ceiling and residual risk.
- **The register matches the builder**: plain for a non-technical founder, precise and dense for an engineer.

## Recommend, explain why, and give the alternative

The builder wants real picks, not a menu, and they also want to understand each call and know what else is out there, so they are not taking your word on faith. For every meaningful choice, give all three, in plain language:

1. **The pick.** A specific, named default, given even in the at-a-glance stack table. A category is not a pick: "a HIPAA-eligible database" names a requirement, "Convex" names the choice.
2. **The why.** The reason in a sentence or two, in terms of their product rather than abstract merits ("this handles paying your walkers and filing their tax forms for you", not "robust payout primitives").
3. **The alternative, and when to switch.** A *named* realistic other option (a specific product, not "an open-source option"), plus the situation, described so the builder can recognize whether it is theirs, in which they would pick it instead ("if most of your users are on Outlook rather than Gmail, use this one"). One named alternative is usually enough; naming five is its own kind of unhelpful.

Skipping the why leaves a non-technical builder unable to understand, defend, or later revisit the decision. Skipping the alternative makes the document read like a sales pitch instead of honest advice, and hides the fact that they had a choice. Do this consistently, in every section, not just once: it is how the document earns trust. And make the three legible for each choice rather than buried in a dense paragraph: the layer format in the template surfaces them as short labeled lines, so a non-technical builder can find the pick, the why, and the alternative in seconds.

Bias toward boring, well-supported, well-documented technology a small team or an AI build tool can run without specialist help. Match picks to scale: do not put an enterprise data platform under a product with twelve users. Where the chosen build platform has a default stack (for example a tool that always pairs a particular front end with a particular database), prefer to flow with it and say where you are doing so, rather than fighting it, but still name the alternative so the builder knows the path exists.

## Verify, do not guess

Specifics about the outside world go stale: pricing, free-tier limits, rate limits, whether a service still exists or is still the sensible choice, and the terms that matter for privacy (data retention, training on customer data, regions offered). Search the web for these before stating them, and prefer official sources. Say when a number is current as of today versus a rough figure to confirm. This is why the skill is worth more than a guess from memory.

## Make it portable

The document is the brief the builder hands to whatever builds the product, whether an AI coding tool or a developer. Keep it self-contained: someone reading only architecture.md should understand the whole system and know where to start. Name concrete runtime technologies (databases, hosting, payments, and so on), but do not assume one particular coding environment in the prose. Where a chosen build platform constrains the stack, note it as a constraint rather than baking it silently into every section.

## Living document

Architecture is decided over time, not in one sitting, so treat architecture.md as something you reopen and grow:

- If one already exists, read it, then **extend and amend** it rather than rewriting from scratch. Preserve the structure and the prior reasoning.
- When a decision changes, **append a dated entry to the decisions log** and mark the superseded text as superseded in place, with a pointer to the new entry, rather than quietly deleting it. The trail of why things changed is part of the value.
- Keep the **open items** list current: move things from "to verify" into the body as they get settled, and add new unknowns as they surface.
- Always save to `architecture.md` and tell the builder where it is.

## A note on the example

`references/architecture-template.md` is generalized from a real, mature architecture document. Use its structure and its voice (plain-language, precise, honest about trade-offs and risk), but never copy its specific technology choices or its domain. Those were right for one product. Derive fresh ones for the product in front of you.
