# Simple Calendar for Even G2

A hands-free month-view calendar for [Even Realities G2](https://www.evenrealities.com/) smart glasses, designed to be operated entirely from the R1 ring. Always opens at the current month — no setup required.

> **Status:** v1.0.4 — [available on Even Hub](https://hub.evenrealities.com/).

## Features

- **At-a-glance month view** — full 6-week grid that fits inside the G2's 9-line text container
- **Today shown in the header** — current month always opens with `MMM D, YYYY`; other months show `MMM YYYY`
- **R1-only navigation** — swipe to move the cursor through Today / Next / Prev, tap to switch months. Cursor starts on Today so an accidental first tap is a no-op.
- **Always opens at today** — no persisted state; every launch starts on the current month
- **Lightweight text rendering** — single-frame on-glass updates, no image upload
- **Mixed-width font alignment** — fullwidth weekday header and digits keep columns aligned despite the proportional G2 font

## Preview (on-glass)

Current month (header carries the date):

```
May 4, 2026
Ｓｕ Ｍｏ Ｔｕ Ｗｅ Ｔｈ Ｆｒ Ｓａ
　　 　　 　　 　　 　　 　１ 　２
　３ 　４ 　５ 　６ 　７ 　８ 　９
１０ １１ １２ １３ １４ １５ １６
１７ １８ １９ ２０ ２１ ２２ ２３
２４ ２５ ２６ ２７ ２８ ２９ ３０
３１
▷ Today  ▒ Next  ▒ Prev
```

Browsing a different month (header drops the day):

```
Apr 2026
Ｓｕ Ｍｏ Ｔｕ Ｗｅ Ｔｈ Ｆｒ Ｓａ
　　 　　 　　 　１ 　２ 　３ 　４
　５ 　６ 　７ 　８ 　９ １０ １１
１２ １３ １４ １５ １６ １７ １８
１９ ２０ ２１ ２２ ２３ ２４ ２５
２６ ２７ ２８ ２９ ３０
　
▒ Today  ▷ Next  ▒ Prev
```

## Controls

| Input | Action |
|---|---|
| Swipe up / down | Move cursor through Today → Next → Prev (cycles) |
| Tap | Execute the cursor action (switch month) |
| Double-tap | Exit confirmation dialog (Even Hub page-lifecycle convention) |

### Navigation row

1. **Swipe** to move the `▷` cursor across `Today` / `Next` / `Prev`. Launch always starts on `Today`, so an accidental tap right after opening leaves the month unchanged.
2. **Tap** to apply:
   - `▷ Today` — jump back to today's month (no-op if already there)
   - `▷ Next` — go forward one month
   - `▷ Prev` — go back one month
3. While viewing the current month, the header reads `MMM D, YYYY`; other months show `MMM YYYY` only.

## Try it

- **Browser dev:** `npm run dev`, then open http://localhost:5177 — the in-browser UI mirrors what the glasses show, with on-screen Today / Next / Prev buttons.
- **On-glass:** install via Even Hub once approved, or build & sideload your own `.ehpk` (see [Development](#development)).

## Development

### Requirements

- Node.js 20+
- `@evenrealities/evenhub-cli` 0.1.13 or later (installed as a devDependency)

### Build & run

```bash
npm install
npm run dev        # browser dev at :5177
npm run typecheck  # tsc --noEmit
npm run build      # production build into dist/
npm run pack       # build + package into simple-calendar.ehpk
```

## Tech stack

- TypeScript + Vite (flat asset output, required by `evenhub-cli`)
- React + [even-toolkit](https://www.npmjs.com/package/even-toolkit) for the smartphone UI
- `@evenrealities/even_hub_sdk`
- Pure JS `Date` arithmetic for month/year boundary handling — no calendar library

## Author

Built by **TakeMotions**.
