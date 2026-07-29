# Ready & Steady — App Prototype
**Built:** 7 July 2026 · from `HANDOFF_App_Prototype_Brief.md` · concept exploration for the phase-3 product

## What this is
A self-contained, tappable mobile prototype. No backend, no accounts, no app stores —
everything runs in the browser and saves your taps locally on the device (localStorage).

- **Tap it on a phone:** https://claude.ai/code/artifact/5f105b33-299c-4265-991f-9ff950fbf1cc
- **Or open locally:** double-click `index.html` (same app; `ready-steady-app.html` is the
  source file the artifact is published from — edit that one, `index.html` is a generated wrapper).

## What's inside
| Tab | What it does |
|---|---|
| **Today** | The jar shelf: "Stocked for X days" toward 72 h → 1 week (MSB), per-category status, "use these soon" reminders, Ready Day ritual |
| **Pantry** | The hero feature. Food, water and gear log with dates. Add via **simulated camera scan** of a date label, or type it in. Water containers get an automatic refresh-by date (+6 months). Tap an item → "Eaten & replaced" rotates it with a fresh date |
| **Checklists** | The 25-point "Are You Ready?" check with live score + the three first actions; the two-level Weekend-Ready (72 h) → Week-Ready (7 days) master list; household setup (people, allergies, pets) that drives the water math (3 L/person/day) |
| **Steady** | "If something happens" — four offline quick sheets (power outage, storm, water disruption, leave in 10 minutes) set in calm, high-contrast lights-out styling; 112 / 113 13 / 1177; the ten power's-out games; talking-with-kids by age |

Demo data is seeded relative to today's date, so the demo never looks stale.
"Reset the demo" lives at the bottom of the Today tab.

## Design decisions
- Palette from the logo: charcoal `#202020` on cream `#f3eadb`; slate `#323232` for the
  lights-out pages; one warm accent: **marmalade `#c17817`** (honey/preserves — deliberately
  not terracotta, never alarm-red). Status colors: dill green / marmalade / paprika rust.
- Georgia serif for display + italic "friend's note" moments; system sans for UI.
- Signature element: the readiness meter is a **shelf of seven jars** — one jar per day of
  self-sufficiency, 72 h and 1-week marks drawn on the shelf.
- The Steady tab is designed for a stressed person in a dark house: one tap from anywhere,
  big type, short sentences, no decisions required.
- English UI, Swedish-ready: all strings live in one place in the JS; numbers (112/113 13/1177),
  P4 and MSB framing are already Sweden-first.

## What the real app would add (phase 3, after validation)
React Native/Expo (one codebase → iOS + Android), true camera scanning (barcode + OCR of
date stamps), push notifications for expiry/Ready Day, offline-first storage with optional
cloud sync, household sharing, Swedish/English toggle. Deliberately out of scope now per
the launch decision.
