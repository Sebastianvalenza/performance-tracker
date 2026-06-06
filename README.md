# VIP Performance Tracker

A client-side operations dashboard that turns a flat ticketing export (Zendesk, or any CSV) into a filterable, gamified view of agent productivity across markets, shifts and operations.

## The Problem

Performance for a large multi-market support team was tracked in a manually maintained spreadsheet: someone exported the day's ticket data, copied it into tabs, and rebuilt the same charts by hand every morning. It was slow, error-prone, and gave no live view of who was on pace, which operation was lagging, or how the month was trending until it was already over.

## The Solution

VIP Performance Tracker ingests the ticket export and renders it as an interactive dashboard with five views:

- **Overview** — team KPIs, a gamified tier board per operation (a "floor" model: an operation only turns fully gold when *every* agent clears the gold threshold), the daily points trend, and a sortable, groupable agent leaderboard.
- **Projection** — linear month-to-date extrapolation of each agent's points to end of month, against the gold target.
- **Individual** — a full per-agent profile: operation, markets, shift rotation, tier progress and daily trend.
- **Compare** — normalized radar comparison of up to four agents across points, volume, SLA and QA.
- **History** — weekly and monthly trends for volume and quality over the full period.

Points are computed as `public comments × 1 + internal comments × 0.25`. Agents earn 🥉 bronze (800), 🥈 silver (1,200) and 🥇 gold (1,600) tiers; operation and team tiers inherit the lowest agent tier beneath them.

It ships with a deterministic synthetic dataset (48 agents, 4 operations, 10 markets, 90 days) so the live demo works with zero setup, and a **column-mapping CSV uploader** that auto-detects agent, date and metric columns from an arbitrary export — falling back to manual mapping and graceful error states when a file isn't in the expected shape. Optional metrics (SLA, QA, resolution time) are hidden automatically when absent. Dark/light themes persist per user; the current view is shareable via URL.

## Stack

- Vanilla **HTML + CSS + JavaScript** — single file, no build step, no framework
- **Chart.js** for line, bar and radar visualizations
- **PapaParse** for client-side CSV parsing and column detection
- Deterministic seeded PRNG for reproducible synthetic data
- Fully static — runs on GitHub Pages with no backend, no credentials, no data leaving the browser

## Demo

**Live:** https://sebastianvalenza.github.io/vip-performance-tracker/

![Overview — operation tiers and agent leaderboard](https://github.com/Sebastianvalenza/vip-performance-tracker/blob/main/VPT%20History%20tab.png)
![History tab — Weekly and monthly performance](https://github.com/Sebastianvalenza/vip-performance-tracker/blob/main/VPT%20Overview.png)

## Impact

Replaced a manual daily reporting spreadsheet with a live, self-serve dashboard — eliminating the morning rebuild and giving team leads real-time visibility into pacing, tier progress and at-risk agents.
