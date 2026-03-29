# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file interactive vitals chart (`index.html`) hosted on GitHub Pages. No build step — open the file directly in a browser or push to `main` to deploy.

## Architecture

Everything lives in `index.html`:

- **Data section** (top of `<script>`) — `VITALS` array, one object per metric. Edit values here.
- **Chart logic** — D3 v7 (loaded from CDN). Each series is normalized independently to `[0, 1]` so different units can share the same Y axis.
- **Interaction** — click a line (or legend row) to select it: selected line brightens, others gray out, Y axis labels appear showing actual values for that series. Click background or same line to deselect.
- **Hover** — crosshair + dot snap to nearest data point; tooltip shows date and value.

## Data format

Each entry in `VITALS`:
```js
{
  id: 'uniqueId',
  label: 'Display Name',
  unit: 'unit string',
  color: '#hexcolor',
  data: [
    { day: 'YYYY-MM-DD', value: 123 },
    ...
  ]
}
```

The four built-in series are `breathing` (blue `#4a9eff`), `heartRate` (red `#ff4a4a`), `spo2` (white `#e8e8e8`), and `weight` (yellow `#ffd700`).

## GitHub Pages deployment

Push `index.html` to the `main` branch and enable Pages (Settings → Pages → deploy from `main` / root).
