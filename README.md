# DraftFM v1.0 — The Hobbit (HOB) pack-1-pick-1 forecast

This artifact is a **pre-release prediction**. It ranks every card in the
Magic: The Gathering set *The Hobbit* (HOB, released 2026-08-14)
by how strongly a draft-pick model would take it as the first pick of the
first pack — computed and sealed **before** the set was playable and
**before any human draft data for it existed**.

## What produced it

DraftFM is a draft-pick model trained on 169,932,378
public human draft picks across 32 Magic sets. It never sees a set-identity
label: a card reaches the model only as features derived from its printed
characteristics plus a text embedding of its rules text. That is what makes a
forecast for an unreleased set possible at all — HOB contributes **only its
public Scryfall card records** here. No HOB picks, outcomes, ratings, or
community grades exist anywhere in this pipeline.

## What the numbers mean

- `score` — the raw model logit at pack 1, pick 1, with an empty pool, over the
  full 193-card set list. Higher is a stronger first pick.
- `rank` — 1 is the highest score.
- `percentile` — `100 * (n - rank) / (n - 1)`; 100.0 top, 0.0 bottom.
- `letter` — **presentation only.** Letters are fixed percentile bands on a
  13-level ladder, assigned by rank. They are not thresholds on the score and
  carry no information the rank does not already carry.
- `n_printings` — how many Scryfall printings in HOB share this card name.
  All printings of a name score identically; the ranking is published over
  unique names.
- `display_only_basic` — basic lands. Included for completeness, not meant as
  a draft recommendation.

The forecast is the score, the rank, and the percentile. The letter is a
reading aid.

**Serving note.** This forecast is sealed at the expert skill slice (win-rate bucket >= 0.55, >= 100 games; encoder ids 28 / 4). The deployed draft assistant defaults to a different conditioning pair (ids 33 / 6, ~0.66 win rate and 1000 games), so live scores will not match these numbers exactly.

## Files

| file | sha256 |
|---|---|
| `hob_p1p1_forecast.csv` | `a16c34767aa382e7703f480207f8480484e29ad22bbab2142aa2195e9b9a94a9` |
| `hob_p1p1_forecast.parquet` | `4c539b9cd78d669c8b9d9b79745d8009f0fc65dc592cc6007bbba91767e20e25` |

`seal_manifest.json` records the model checkpoint hash, the frozen feature-space
hash, the card-list hash, the code revisions, and the exact deployment
conditioning, so the run can be audited after the set is played.

## Honest limits

- This is one model's opinion formed from printed card text. It has no access
  to play testing, set mechanics in context, or how the format actually plays.
- It scores cards in isolation at P1P1. Draft value is contextual; a card that
  ranks low here can be excellent in the right deck.
- The 13-level ladder is a fixed distribution. Exactly
  4 cards get A+ because the
  band is 2% wide, not because 4 cards earned it.

Generated 2026-08-09T23:33:45+00:00 (2026-08-09T19:33:45-04:00).

## License

The forecast files in this repository (`hob_p1p1_forecast.csv`, `hob_p1p1_forecast.parquet`, `seal_manifest.json`) are released under [CC BY 4.0](LICENSE). Redistribute freely with attribution to Brian Ward, "DraftFM: A Foundation Model for Day-Zero Drafting in Magic: The Gathering", arXiv:2608.19568. The sealed tag `draftfm-v1.0` and its contents are unchanged by this commit.
