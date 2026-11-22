# rtofs-model-currents-repo

The RTOFS **currents** — a data repository of the oceansensing ocean map system: its own
Pages site, its own schedule, its own gigabyte, holding no code of its own.

**Built, rehearsed and taken live 2026-09-27** — published to Pages and R2,
not drawn on the website's map. `PLAN.md` is the founding plan;
`CLAUDE.md` carries what must not be got wrong and the shared doc doctrine.

## What it publishes

NOAA's Global Real-Time Ocean Forecast System's **surface currents**.

| root | quantity | grid |
| --- | --- | --- |
| `cur-rtofs-useast.json` | surface currents, a vector pair | US East, 0.08 degree, `regional: true` |

About 7 MB (measured 2026-09-27).

These products are published **operationally but not drawn on the website's
map** — the owner's call, 2026-09-27. The map's status
line reports those Pages carries when they fall behind; those R2 alone carries
are in the status on R2 and on the `published` branch, not Pages'.

## Published to R2 alone (since 2026-10-10)

Declared `r2_only` in `pipeline/products.toml`: the same run builds these,
they are left out of this repository's Pages site and its status, and the R2
job publishes them beside the rest (the site pipeline's D13, its note of
2026-10-09). Their roots stay on the `published` branch, as every product's do.

| root | quantity | grid |
| --- | --- | --- |
| `cur-rtofs-useast-nearbottom.json` | the current at each column's deepest wet level of the 40 depths | US East, 0.08 degree, `regional: true` |

## The times either side (declared 2026-11-22; no run had published them when this was written)

Both roots are declared to publish two days ahead and one
behind (DECISIONS D3), six-hourly. A root's header lists every time in `moreFrames`, its own
among them; none lists `frames`. An hour read while ahead is `<root>.v<time>.json`, and
keeps that name once behind; an hour read when it is already behind is
`<root>.v<time>.r<run>.json`, from the newest cycle's nowcast up to
the cycle, its forecast after. Every dated file is R2's alone: none is on Pages
or the `published` branch.

## Where the data comes from

**Source**: NOAA's open-data bucket on AWS, registry entry
<https://registry.opendata.aws/noaa-rtofs/>. The fetcher is the site's
`scripts/fetch-rtofs.py`; its budget is in `pipeline/products.toml` and its
traps in `CLAUDE.md`.

## How it runs

The orchestrator (the site's private `pipeline/`), the fetchers and the
published-file contract all come from `oceansensing.github.io`, checked out at
run time. This repository carries `pipeline/products.toml` and its publish
workflow, and nothing else executable. Each run publishes to GitHub Pages and
to Cloudflare R2 from one build. Sibling repositories of the same model:
`rtofs-model-fields-repo`.

**Which document gets what, and what "update docs" means across every
repository of this project, is the doctrine block at the top of `CLAUDE.md`** —
the same text in each, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
