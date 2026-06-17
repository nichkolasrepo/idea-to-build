# architecture.md: structure and writing guide

The canonical structure for the `architecture.md` this skill produces, generalized from a real, mature architecture document. Use the structure and the voice. Never reuse the source's specific technologies or domain.

## How to use this template

- **Two readers, every line, and match the register to the builder.** A developer or AI build tool must always be able to act on it, so the precise technical terms are always present. For a non-technical builder, the prose must also be followable by them: say things in everyday words first, with the precise term in parentheses. For a technical builder, write at their level and skip the glosses.
- **Scale depth to maturity.** Not every section is required. A first draft needs sections 1 through 5, plus 9 (cost, lightly) and 11 (open items). The deeper sections (10, 12, and the advanced ones) are earned by products that have real decisions and constraints behind them. Leaving a section out is fine: note it as "not yet decided" in open items instead of padding it.
- **Prose over bullets in the body.** The stack table, the build-versus-buy table, and the diagram are the structured parts. The layer explanations and the trust model read better as short prose with the reasoning visible.
- **Show the why and the alternative, everywhere.** Every significant choice carries its reasoning in plain terms and the realistic alternative the builder could consider, with the situation under which they would switch. Not just what was picked, but why, and what else exists. This is what makes the document honest advice a non-technical builder can understand and revisit, rather than a list of nouns to take on faith.

## The sections

### Title + register line

A title naming the product and stating this is its architecture, plus a one-line statement of what the document is for. Optionally a short pointer block listing sibling documents (a product spec, a cost model, a design doc) if they exist.

### 1. The mental model (read this first)

One short paragraph that captures the whole system in a way the builder could repeat to a friend: what the thing is, and the central idea everything else hangs off. Follow it with two or three consequences that fall out of that idea (the things that are true because of it). This section is the anchor. If a reader reads only this, they should still get the shape of the system. Write it once the picture is clear, but place it first.

### Stack at a glance

A table giving the one-screen summary, one row per layer:

| Layer | Tech / vendor | Responsibility |
|---|---|---|
| Front end | (the framework) | what the user touches |
| Hosting / compute | (the platform) | where it runs |
| Database | (the store) | the source of truth |
| Auth | (the provider) | identity |
| Payments, email, etc. | (the providers) | what each one does |

Keep "Responsibility" in plain language. The "Tech / vendor" column must name the specific product or service you recommend (the default), not a category, a requirement, or a hedge: write "Convex", not "a HIPAA-eligible database"; "Stripe Connect", not "a payments provider". A non-technical builder reads this table to learn exactly what they will use, so every row commits to a real name, even when the choice is constrained or carries caveats; the constraint, the reasoning, and the alternatives belong in the section 3 write-ups, not in a cell. Keep the table lean and scannable. This table is what a build tool scans first.

### 2. System diagram

A simple ASCII diagram showing the main pieces and how a request flows between them (client, the server or compute, the database, the third-party services, with money and monitoring off to the side). Keep it readable over impressive: labeled boxes and arrows. Follow it with a **one-line data flow** sentence tracing a single user action from tap to response. ASCII is deliberate: it survives in any text box, any tool, and any coding agent's context.

### 3. The layers

A short subsection per layer from the stack table, written so a non-technical builder can grasp three things at a glance for every choice: what is chosen, why, and what else they could pick. Do not bury these in a flowing paragraph; make them legible. A reliable format for each layer is one plain sentence on what it is and does, then three short labeled lines:
- **Recommended:** the specific named product or service.
- **Why this:** the reason in plain, product-grounded terms.
- **Other options:** one or two *named* alternatives (never a vague "or an open-source option"), each with a recognizable "choose it if ..." situation.

Name real alternatives even when you are confident in the pick; letting the builder understand the alternatives is the whole point. This is where a developer gets enough to start, and where a non-technical builder learns not just what each piece is, but why it was chosen and what else exists.

### 4. What you build vs. what you get off the shelf

A table splitting the capabilities the product needs into "already solved by something off the shelf" versus "you have to build this". One of the most useful sections for a non-technical builder: it shows where the real work (and the moat) is, versus where to just buy.

| Capability the product needs | Off the shelf today | Your job |
|---|---|---|
| (e.g. sign-in) | (the auth provider does it) | wire it up |
| (the thing that makes the product special) | nothing | build it |

### 5. Integrations / third-party services

How the product talks to outside services (payments, email, calendar, messaging, search, and so on): the specific provider for each, how authentication to it works at a high level, and the fallback if a provider fails or does not fit a given user. Flag anything that sits on the launch critical path, such as an approval or verification process a provider requires.

### 6. The core logic / engine (domain-specific)

The deep section for whatever the product actually does under the hood, named for the product. If there is AI, this is where model usage lives: which models do which jobs, how calls are routed so a model can be swapped without a rewrite, and how usage is capped and metered. If there is a complex domain process, describe it here. Depth should match how central this is to the product.

### 7. Background work and scheduling

If the product does anything when the user is not present (reminders, scans, digests, syncs): how that work is triggered, and the rule that it must never fail silently (catch up on the next run, safe to retry). Skip if the product is purely request and response.

### 8. Security, isolation, and data lifecycle (the trust model)

In plain terms: how the system keeps users' data separate, where secrets live, how it treats input from the outside world (the rule that incoming content is data and never instructions is worth stating explicitly for anything agentic), the main ways the system could be abused and how each is blocked, and what happens to data across its life: retention, deletion (and what deletion really guarantees), export, and backups. For sensitive-data products this is the most important section. Write it as a contract, not an aspiration.

### 9. Cost shape

The handful of things that actually drive the bill (often the always-on infrastructure more than the per-use costs), the biggest levers to control them, and, for a paid product, rough per-user economics. Keep it directional and flag the numbers to confirm with real measurement.

### 10. Build-to-extend constraints

The few decisions to honor now so they do not cap the product later (for example: model tenancy as multi-user-ready from day one even if launching single-user). Short and specific.

### 11. Open items to verify

An honest list of what is not settled and what to test before relying on it: the assumptions, the numbers to measure, the provider terms to confirm. This section keeps the document trustworthy and is the natural backlog for the next session.

### 12. Operations and lifecycle (for maturing products)

For products past the earliest stage: how a request actually reaches the running code and back; how a new user or tenant is provisioned end to end; how updates are built and rolled out safely; and how data is backed up and restored. Skip for a v0.1.

### Advanced sections (earned by mature products)

- **Invariants**: a numbered list of properties the system must always hold (isolation, exactly-once actions, deletion guarantees), each with the part of the system accountable for it and the test that proves it. Only meaningful once the system is real enough to test.
- **Residual risk**: stated plainly, what the chosen design does not fully protect against, so no one is surprised later. The willingness to write this section is what separates a credible architecture from a sales pitch.

### Decisions log

Dated entries recording each significant decision and the reason for it. When a decision is reversed, add a new dated entry and mark the old text as superseded in place (with a pointer to the new entry) rather than deleting it. The history of why the architecture changed is part of its value.
