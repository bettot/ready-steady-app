# Ready & Steady — App Prototype
**Built:** 7 July 2026 · from `HANDOFF_App_Prototype_Brief.md` · concept exploration for the phase-3 product

## What this is
A self-contained, tappable mobile prototype. No backend, no accounts, no app stores —
everything runs in the browser and saves your taps locally on the device (localStorage).

- **Tap it on a phone:** https://bettot.github.io/ready-steady-app/ (tip: "Add to Home Screen" makes it feel installed)
- **Backup link (same app):** https://claude.ai/code/artifact/5f105b33-299c-4265-991f-9ff950fbf1cc
- **Code lives at:** https://github.com/bettot/ready-steady-app (public)
- **Or open locally:** double-click `index.html` (same app; `ready-steady-app.html` is the
  source file the artifact is published from — edit that one, `index.html` is a generated wrapper).

## What's inside
| Tab | What it does |
|---|---|
| **Today** | The jar shelf: "Stocked for X days" toward 72 h → 1 week (MSB), per-category status, "use these soon" reminders, Ready Day ritual |
| **Pantry** | The hero feature. Food, water and gear log with dates. Add via **real camera scanning** — barcode → product name, photo of the printed date → suggested best-before (see below) — or type it in. Water containers get an automatic refresh-by date (+6 months). Tap an item → "Eaten & replaced" rotates it with a fresh date |
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

## The camera scanner (real since 5 Aug 2026)
"Add to the shelf" now uses the phone's actual camera, in two steps — and every reading
lands in the form for checking; the camera never saves anything by itself.

1. **Barcode → product name.** Android Chrome uses the phone's built-in `BarcodeDetector`
   (nothing to download). iPhone Safari has no such API, so it falls back to a local
   WebAssembly build of ZXing (`vendor/zxing/`, ~1.1 MB, fetched only when scanning).
   The code is looked up in **Open Food Facts** (free, no key, needs internet) and the
   name + quantity are pre-filled.
2. **Photo → best-before date.** The date is photographed (cropped to the frame guide);
   the photo stays visible next to the date field while confirming — even when the text
   reading fails, the date can be read off the photo instead of walking back to the shelf.
   OCR is local Tesseract (`vendor/tesseract/`, ~6 MB, fetched on first use, cached by the
   browser). Understands European formats (`10.03.2027`, `10/03/27`, `MAR 2027`, `03 2027`,
   `2027-03-10`; Swedish/Norwegian/Danish/Finnish month names). Month + year only → last
   day of that month. Day-first always — never American month-first. The photo is not
   stored after saving the item (localStorage is small); that's a deliberate v1 choice.

Failure is a first-class path: camera blocked/missing/busy, no internet, unknown barcode,
unreadable stamp — each lands straight in manual entry with a plain explanation. Camera
permission is requested only when a scan button is tapped, never on page load.

**Needs HTTPS:** camera APIs only run on secure pages, so the scanner works on the GitHub
Pages link (and localhost), not on the claude.ai artifact copy or via `file://`.

**Vendored libraries** (local files, no CDN — the app stays independent of anyone's uptime):
| Library | Version | Licence | On disk | A phone downloads |
|---|---|---|---|---|
| zxing-wasm (reader) | 3.1.2 | MIT (bindings) / Apache-2.0 (zxing-cpp) | 1.1 MB | ~1.1 MB, iPhone barcode only, lazy |
| tesseract.js | 6.0.1 | Apache-2.0 | 0.2 MB | with core+lang below, first date photo only |
| tesseract.js-core (LSTM) | 6.1.2 | Apache-2.0 | 7.9 MB (2 CPU variants) | ~4 MB (one variant) |
| tessdata_fast `eng` | — | Apache-2.0 | 2.0 MB | 2.0 MB |

The base page itself stays a single ~90 KB HTML file; nothing above loads until a scan
button is tapped.

## Regenerating index.html
`ready-steady-app.html` is the source (also what the artifact is published from).
`index.html` = the same file with this exact wrapper bolted on — regenerate, don't hand-edit:
```
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#f3eadb">
</head>
<body>
…ready-steady-app.html, verbatim…
</body>
</html>
```

## What the real app would add (phase 3, after validation)
React Native/Expo (one codebase → iOS + Android), push notifications for expiry/Ready Day,
offline-first storage with optional cloud sync, household sharing, Swedish/English toggle,
keeping date photos with items (needs IndexedDB, not localStorage). Deliberately out of
scope now per the launch decision.
