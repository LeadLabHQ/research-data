# The Lead Lab Research Data

The data behind The Lead Lab's published research into what AI assistants
recommend when someone asks for a local service business.

Published research: https://leadlabhq.com/research/

## What's in here

### `batteries/` — 104 answer batteries

One JSON file per city × trade pair: 13 US cities × 8 trades.

- **Cities:** Orlando (Oct 14, 2026); New York, Los Angeles, Chicago,
  Houston, Dallas, Phoenix, Atlanta, Miami, Denver, Seattle, Boston and
  Las Vegas (Oct 15, 2026)
- **Trades:** plumbing, hvac, roofing, pest-control, cleaning, drywall,
  painting, tree-service

Each battery asked a fixed set of prompts (for example: who are the best
plumbers in this city?) across several AI models and recorded every answer
**verbatim**.

### `batteries-index.csv`

One row per battery file, so you can scan the whole set without opening
104 JSON files.

### `grok/` — the Model Wars extract

`grok-orlando-plumbing.json` — the Grok answers behind the Model Wars:
Orlando piece (https://leadlabhq.com/research/model-wars-orlando/):
4 prompts, answers recorded verbatim on the Grok consumer chat surface
with live web search on, plus the per-business name counts and the
parametric open-weight baseline the piece compares them against.
Operator/process fields from the working file were removed; what remains
is the published substance.

## Data dictionary

Battery file fields:

| Field | Meaning |
| --- | --- |
| `trade` | The service trade asked about (e.g. `plumbing`). |
| `market` | The city and state asked about (e.g. `Orlando, FL`). |
| `run_date` | The date the battery ran (ISO timestamp). |
| `models_used` | The AI models that answered, as labelled by the run. |
| `total_checks` | How many prompt × model answers the battery contains. |
| `answers` | The answers, one object per prompt × model. |
| `answers[].prompt` | The exact question asked. |
| `answers[].model` | The model that gave this answer. |
| `answers[].text` | The answer, verbatim. |
| `answers[].named_here` | Business names the answer named, extracted from the text. |

Index CSV columns: `city`, `trade`, `market`, `run_date`, `models_used`
(pipe-separated), `total_checks`, `answers`, `file`.

Grok file fields: `battery`, `run_date`, `web_search_active`,
`model_label`, `measurement_note`, `prompts` (each with `id`, `prompt`,
`answer`, `names`, `searches`, `sources_shown`), `per_name_counts_of_4`,
`distinct_name_total`, `excluded_from_names`, and
`llama_baseline_for_comparison` (the parametric comparison run, with its
own note).

## A note on what this data is

These are snapshots: what the models answered on the day each battery ran.
AI answers change. Treat every file as a dated record, not a live ranking.

One edit was made before publication: phone numbers that appeared inside
some answers were replaced with `[phone removed]`, matching the standard
on leadlabhq.com, which never publishes phone numbers. Everything else is
verbatim.

## License

CC BY 4.0 — see `LICENSE`. Credit: The Lead Lab
(https://leadlabhq.com/research/).
