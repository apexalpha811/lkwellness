# Private investments: what these two briefs are, and how they differ

Written 2026-08-17. Read this before changing anything in this folder.

## What this folder is

Two investor briefs for L&K Wellness with **no lender anywhere in them**. Same business as the
briefs in `ample/` and `surgical/`: same rooms, same menu, same volumes, same revenue, same
operating income. What changes is the right-hand side of the balance sheet. The whole project cost
is raised as equity, so there is no loan, no debt service, no coverage ratio, no rate sensitivity
and no SBA program language.

| | Ample, private | Surgical, private |
|---|---|---|
| Project cost | $4,750,000 | **$5,000,000** |
| Equity raised | $4,750,000 | $5,000,000 |
| Senior debt | none | none |
| Working capital reserve | $1,105,800 | **$1,054,800** |
| Modelled cash trough | $42,467 at month 9 | $607,422 at month 11 |
| Operating income, stabilized | $224,801 /mo, $2,697,611 /yr | $189,541 /mo, $2,274,497 /yr |
| Unlevered yield on equity | 56.8% | 45.5% |
| Cumulative cash by month 36 | $4,589,439 | $3,154,780 |
| Equity payback | month 37, extrapolated | month 46, extrapolated |
| Footprint | 4,925 SF | 5,825 SF |
| Slides | 40 | 41 |

**The two briefs diverged on 2026-08-18.** Ample now carries a priced round with a ratchet,
follow-on rights and an exit thesis. Surgical is still a flat all-equity ask with no ownership
percentage, no valuation and no exit path. Read the next section before comparing them.

## Ample's priced round, added 2026-08-18

Surgical has none of this. Every slide, section and paragraph below is gated on a `deal` object
that exists on the `ampleEquity` scenario alone, and the self-check fails the build if any other
scenario acquires one.

| | Value |
|---|---|
| Raise | $4,750,000 |
| Starting stake | 30% |
| Pre-money / post-money at 30% | $11,083,333 / $15,833,333 |
| Entry multiple, base case | 5.87x operating income |
| Ratchet cap | 40%, reached at the low case of $1,244,500 |
| Pre-money / post-money at 40% | $7,125,000 / $11,875,000 |
| Ratchet threshold | $2,200,000 trailing twelve-month operating income |
| Expansion reserve | 25% of operating income |
| Buyback window | years 3 to 5, multiple to be agreed |

**Three corrections were made to the brief as specified, and they should not be quietly reverted.**

The two valuations originally given, $7,125,000 pre and $11,875,000 post, are the **40%** endpoint,
not the 25% start. $4,750,000 / 0.25 is $19,000,000 post and $14,250,000 pre. The pair was
mislabelled, not miscalculated.

**The starting stake moved from 25% to 30%.** At 25% the round prices at 7.04x base-case operating
income, above every published single-location band and inside the range for multi-location
platforms. A brief that asks a platform multiple for one building that does not exist yet, two
pages from a table citing those comps, hands a reader the objection. 30% prices at 5.87x, inside
the 5.0x to 6.5x band for a single location under a strong operator.

**Founder retained income is therefore 70%, not 75%:** $1,888,328 a year at base case. The 75%
figure followed from the 25% stake that was replaced.

**The exit multiples cite a real source and are narrower than first specified.** Breakwater M&A,
20 February 2026, gives 3.5x to 6.5x for a single location and 6.0x to 9.0x for a multi-location
platform, with a +0.5x to 1.0x membership premium. The 7x to 12x+ spread originally asked for is
not supported by that source; 10x to 12x appears only in secondary sources describing top-tier
platforms. Quoting 12x against a primary source that stops at 9.0x would be exactly the unsourced
inflation this project refuses everywhere else. One sourced fact does land in L&K's favour and is
used: membership and access revenue is 41.9% of the total, above the 30% to 40% band the source
names as a premium driver.

**What the brief admits rather than hides.** The ratchet cushions the downside without making the
investor whole: at the low case, 40% of $1,244,500 pays $497,800, less than the $809,283 that 30%
of base case pays. A build assert holds that inequality true, so if the terms ever change to make
the protection complete, the build fails and the copy gets corrected rather than quietly becoming
a lie. Investor cash yield is shown at two distribution assumptions, full distribution and after
the 25% expansion reserve, because the follow-on rights depend on retaining cash and one column
alone would contradict the other page.

## The three decisions behind them

1. **All equity, no debt at all.** Decided in conversation on 2026-08-17. The alternative
   considered was keeping the same loan and simply renaming it "senior debt", which would have left
   every number untouched. That was rejected: the brief is for investors who are funding the whole
   thing.
2. **Surgical lands on $5,000,000 flat**, achieved by taking $300,000 out of its working capital
   reserve rather than out of any construction, equipment or pre-opening line. Nothing about the
   building changed.
3. **Ample stays at $4,750,000** with its reserve untouched.

## Two things a reader will notice, so they are disclosed rather than buried

**Ample's reserve is far larger than it needs to be.** Removing the debt service shrinks its
modelled cash trough from $269,054 to $42,467, so a $1,105,800 reserve now covers the trough 26
times over. That is roughly $1.1M of a $4.75M raise sitting idle. It is defensible as a cushion
that funds a much slower ramp than the one modelled, without going back for a second raise, and
that is exactly how the disclosures page and the register describe it. If the ask should be lower
instead, cut `EQUITY_RESERVE.ample` in `deck-build/model.js` and the project cost follows.

Surgical does not have this problem: its $1,054,800 reserve covers a $607,422 trough 1.7 times.

**The yield figures are large and narrowly defined.** 56.8% and 45.5% are stabilized annual
operating income divided by the amount raised. They are stated before tax, before any distribution
policy, before maintenance capital and before any assumption about a sale, so they are **not
investor returns**. Every artifact says so in those words. No IRR and no exit multiple appears
anywhere, because nothing in this model supports a terminal value that could be sourced, and
inventing one would be the single easiest thing in these documents to attack.

## How they are built

Exactly the same way as the other five briefs, from the same model. Nothing is retyped, so no
figure here can disagree with the lender version except where the capital stack genuinely differs.

```bash
node deck-build/model.js && node deck-build/build-sites.js && node deck-build/build-assumptions.js && node deck-build/build-deck.js
```

The two scenarios are `ampleEquity` and `surgicalEquity` in `deck-build/model.js`, derived from
`ample` and `surgical` with `Object.assign` and a `dataKey` back to the base, the same pattern the
private-equity variants use. They carry one flag, `allEquity: true`, and every difference in every
artifact hangs off that flag:

- `model.js` drives all debt fields to zero, sets `dscr` to null and an empty `rateBand`, and adds
  `unleveredYield`, `cumulativeCash36` and `paybackMonth`.
- `build-deck.js` swaps the SBA package slide for a capital-and-returns slide, and branches the
  cover, footer, ask, use of funds, ramp, sensitivity band, disclosures, timeline, risks and close.
- `site-template.html` hides the lender framing and renders the same capital section in its place.
  All seven sites still share this one template.
- `build-assumptions.js` swaps the capital-stack table and the rent sensitivity column.

**Do not fork the deck or the template to make a change here.** The whole point of the derivation
is that a fix to the business lands in both versions on the next build. The self-check asserts that
these two scenarios still describe the same building as their base: same revenue, same operating
income, same footprint, same space program, same menu, and no capital line other than the reserve
moved.

## Known gap

Surgical's copy of this memo, inside `private investments/surgical/` and its published repo, is
the 2026-08-17 version and does not describe ample's priced round. It was left alone because that
pass was scoped to ample only. Re-copy this file into that folder when you next touch surgical.

## What is unchanged and still open

The rent assumption of $5.50/SF/month NNN still has no broker letter behind it, the surgical
facility fee schedule is still constructed, and the surgeon principal relationship still needs an
operating agreement. All three are disclosed in these registers exactly as they are in the others.
