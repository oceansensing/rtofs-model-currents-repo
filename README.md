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
map** — the owner's call, 2026-09-27. The map's status line still reports
them when they fall behind, which is how their health stays visible.

## Published to R2 alone (since 2026-10-10)

Declared `r2_only` in `pipeline/products.toml`: the same run builds these,
they are left out of this repository's Pages site and its status, and the R2
job publishes them beside the rest (the site pipeline's D13, its note of
2026-10-09). Their roots stay on the `published` branch, as every product's do.

| root | quantity | grid |
| --- | --- | --- |
| `cur-rtofs-useast-nearbottom.json` | the current at each column's deepest wet level of the 40 depths | US East, 0.08 degree, `regional: true` |

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

**Which document gets what, and what "update docs" means across all
twenty repositories, is the doctrine block at the top of `CLAUDE.md`** —
the same text in all twenty, held equal by the site's `check:docs`.

## Structure

```
README.md       what this is
CLAUDE.md       what must not be got wrong, and the shared doc doctrine
PLAN.md         the founding plan and running record
DECISIONS.md    dated one-way decisions, D1 onward
pipeline/       products.toml, the declaration the orchestrator reads
.github/        the publish workflow
```
