# DraftFM's Reality Fracture first-pick ratings

Here is the [complete 295-name forecast](fra_p1p1_forecast.csv) for *Reality
Fracture* (FRA). It was computed on September 20 from a September 19 card
snapshot, using the same frozen DraftFM checkpoint that produced the [Hobbit
forecast](https://github.com/brianward92/draftfm/releases/tag/draftfm-v1.0).
We are publishing it on September 25, **after prerelease events began** and
before the September 29 MTG Arena release. This is a dated public prediction,
not a claim that we sealed it before anyone could play the set.

The highest-ranked card is **Garruk, Veiled Butcher**. The model's highest
uncommon is **Terminal Criticism**, at overall rank 49. That second choice is
especially easy to disagree with: it is conditional removal, and the model
has no direct picture of the decks people will build. We are leaving the
ranking as generated so it can be checked later.

## What the file covers

The CSV has 285 unique FRA names (including five basic lands marked
`display_only_basic`) and the ten Special Guests associated with this release.
Alternate printings are collapsed by name. The separate Commander product is
excluded. The [uncommon list](fra_uncommons.csv) filters the original ranking;
it does not rescore or regrade any card.

Each `score` is a model logit for pack 1, pick 1 of a Premier Draft, with an
empty pool and the same expert-player conditioning used for the Hobbit
forecast (win-rate ID 28, games ID 4). Higher scores mean stronger first-pick
preferences. `rank` orders those scores. `percentile` and `letter` summarize
the rank across all 295 names, including the display-only basics. The 13
letter bands have fixed sizes: **an A is not a measured win rate**, and the
number of A cards says nothing about how many bombs the set contains.

These ratings are for first picks, not Sealed deck building or later picks.
Card value changes with your pool and the format. The forecast has not been
tested against FRA picks or game outcomes. DraftFM's structured keyword
vocabulary does not contain Replicate; the printed rules text still enters
through its fixed text encoder.

The local MTGA Draft Assistant uses the same model and saved card features,
but its default skill conditioning differs from this CSV. Its live letter
grades may therefore differ from the published first-pick letters.

## Provenance and later evaluation

The [generation manifest](fra_forecast_manifest.json) records the card
snapshot, checkpoint and feature hashes, scoring condition, coverage, and
output digests. Its `status` says “local candidate” because it was written
at generation time; this publication is the public timestamp. The
[verification record](fra_verification.json) reports two byte-identical
exports. No FRA draft picks, outcomes, or post-release ratings were used to
fit or select this forecast.

For a later first-pick comparison, take the highest raw `score` among every
offered non-basic card. Exclude a pack if any offered non-basic card lacks a
score; do not silently shrink the pack. Report coverage and tie handling.
Keep the original CSV fixed when comparing to observed selections or game
results. Agreement with human picks is a behavioral measure, not evidence
that a card causes wins.

| File | SHA-256 |
| --- | --- |
| [`fra_p1p1_forecast.csv`](fra_p1p1_forecast.csv) | `116fc528acd83843e283daa73492fa01041f167daebe92103d9f9a52617a348e` |
| [`fra_uncommons.csv`](fra_uncommons.csv) | `301db981e2a2968aa4143ac642706dabb643cf0068208ea6eda1001ec78deada` |
| [`fra_forecast_manifest.json`](fra_forecast_manifest.json) | `0394f8c62a98573d048f2d1283e192dbe05217466129d1625af8c935a235f6b0` |
| [`fra_verification.json`](fra_verification.json) | `a4bc5432aa53f572ab90b5f152e777456c5b282400621dc32ffbf370ccb8722c` |

Forecast files are released under [CC BY 4.0](LICENSE). Please credit Brian
Ward and DraftFM when redistributing them. Card records came from Scryfall.
[Wizards' release schedule](https://magic.wizards.com/en/news/feature/collecting-reality-fracture)
lists prerelease beginning September 25 and MTG Arena release September 29.
