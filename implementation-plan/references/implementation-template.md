# Implementation Plan: <product name>

> Built from `architecture.md` (<version or date>). Reader: a non-technical builder working with <build tool>. Last updated <date>.

## How to use this
- Build top to bottom: first the screens (with placeholder data), then each feature made real, one at a time.
- Each chunk is one thing to hand to your build tool. Give it the "What to implement" text.
- After each chunk, run the "How to tell it worked" check before moving on.
- Tick the box when a chunk is done, and keep this file updated as you build.

## Features by screen
Every feature, grouped by the screen it lives on, taken straight from `architecture.md`. This is the spine of the build: first you build these screens, then you make each feature real, top to bottom.

| Screen | Features on it |
|---|---|
| <Home / dashboard> | <feature A>, <feature B> |
| <Browse / search> | <feature C> |
| <Detail / profile> | <feature D>, <feature E> |
| <Settings> | <feature F> |

## You are here
> Currently on: <feature or screen>. Last finished: <chunk name>.

---

## Build pass 1: the screens (UI first)

Build every screen in the table above with placeholder data. Nothing is saved or wired up yet; this is so you can see and click the whole product before any backend exists.

- [ ] **Create the project and build all the screens**
  - What to do: Stand up the app and every screen in the features-by-screen table, with placeholder content.
  - What to implement: In <build tool>, start a new project and build these screens: <Home>, <Browse>, <Detail>, <Settings>. Show mock or placeholder data on each so they are visible and clickable. No real saving or logic yet.
  - How to tell it worked: You can open the app and click through every screen, even though the data showing is fake.
  - Builds: `architecture.md` § Client / front end

## Build pass 2: make each feature real (one at a time)

For each feature in the table, make it work end to end: its data, its sign-in, its logic, the integration it needs, and the rule that protects it. Recommended order is below, core feature first since the rest lean on it. Adjust if this product needs it, and say why.

- [ ] **<Core feature, e.g. Booking a walk> — make it real**
  - On screen: <which screen(s) it lives on>
  - What to do: Make <core feature> work end to end on its screen.
  - What to implement: Add what it needs: <auth provider, e.g. Supabase Auth> for accounts, the <X> and <Y> tables (with the rule that each person sees only their own rows, called row-level security), and the logic for <the core action>. Switch its screen from placeholder data to this real data.
  - How to tell it worked: <e.g. "Sign in, book a walk on its screen, and see it saved in your bookings; a second test user cannot see it.">
  - Builds: `architecture.md` § Identity and access, § Data and storage, § The core logic

### ▶ Now it runs for real
> By here, the first feature works on real saved data instead of placeholders. Sign in and try it before continuing, so you catch problems while the build is still small.

- [ ] **<Feature 2> — make it real**
  - On screen: <screen(s)>
  - What to do: <one line>
  - What to implement: <its data, its logic, and any integration, e.g. "connect Stripe so walkers get paid">
  - How to tell it worked: <a manual check with a visible result>
  - General note: If you are not on <build tool>, <how this differs>.
  - Builds: `architecture.md` § <sections>

- [ ] **<Feature 3> — make it real**
  - On screen: <screen(s)>
  - What to do: <one line>
  - What to implement: <its data, its logic, and any integration>
  - How to tell it worked: <a manual check with a visible result>
  - Builds: `architecture.md` § <sections>

> Repeat for every feature in the table above. Fold any background jobs and final security rules into the feature they belong to.

---

## Before you call it a first working version
A quick end-to-end pass. Every feature in the table should run from start to finish:
- [ ] <Feature A runs end to end>
- [ ] <Feature B runs end to end>
- [ ] <Feature C runs end to end>

## To confirm or watch
- <Open item, e.g. "Confirm <tool>'s free tier covers <X> before launch.">
- <Integration or limit to test early.>

## Changelog
- <date> — Plan created from `architecture.md` <version>.
- <date> — <what changed and why>.
