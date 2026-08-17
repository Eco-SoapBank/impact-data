# Eco-Soap Bank — Impact Data

Published impact figures for [ecosoap.org](https://www.ecosoap.org), served as a small JSON file.

**Data:** [impact.json](impact.json) · **Live URL:** https://eco-soapbank.github.io/impact-data/impact.json

## What this is

The website displays a handful of impact figures — bars delivered, people reached, tons upcycled, women employed, countries reached. This repository publishes the current values so the site can read them at page load instead of having them typed into each page by hand.

The file is written automatically by a scheduled job in the private `eco-soap` repository, which reads the Global Impact rollup in AirTable, formats each figure for display, and commits the result here.

## Why it is public

GitHub Pages does not serve from private repositories on the free plan, and the site needs to fetch this file from a browser.

Nothing sensitive lives here. Every number in `impact.json` is already printed on the public homepage. **This repository must never contain anything else** — no credentials, no AirTable exports, no personal data, no partner or donor information.

## Format

```json
{
  "bars_delivered": "86.7M",
  "beneficiaries": "22.1M",
  "countries_reached": "42",
  "tons_upcycled": "8,400",
  "women_employed": "175",
  "updated": "2026-08-17"
}
```

Values are **display strings, not raw numbers** — already rounded and formatted, so the website renders them exactly as written with no client-side maths. `updated` is the date the job last wrote the file.

## How the website uses it

A script in the Webflow site footer fetches this file and fills any element carrying a matching `data-stat` attribute:

```html
<div data-stat="bars_delivered">86.7M</div>
```

The number typed into Webflow acts as a fallback. If this file is unreachable, the page keeps showing the last value published in the site itself rather than breaking or going blank.

## Editing by hand

Don't, as a rule — the scheduled job overwrites it. If a number is wrong, fix the source in AirTable.
