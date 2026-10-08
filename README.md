# fiqua-market-snapshots

Auto-published market-data snapshots for [fiqua](https://pypi.org/project/fiqua/),
read at runtime by `fiqua.market.MirrorMarketDataProvider` and
`fiqua.market.MirrorReferenceDataProvider`. They keep slow or browser-blocked
sources off the request path.

| File | Contents | Written by |
| --- | --- | --- |
| `treasury_cmt_curve.json` | The U.S. Treasury par yield curve over about the last ten trading days, from `home.treasury.gov` | fiqua's `publish-treasury-curve` workflow, after each trading day |
| `treasury_bond_quotes.json` | TreasuryDirect FedInvest prices of every marketable Treasury over the last ten priced days, with each day's on-the-run securities; each security's type, coupon, maturity and call date are written once | fiqua's `publish-treasury-bonds` workflow, the morning after each trading day |
| `treasury_bond_terms.json` | The contract terms of every Treasury bill, note and bond maturing on or after a cutoff (2025-01-01 by default), matured ones included, from the TreasuryDirect securities API | the same `publish-treasury-bonds` workflow, rebuilt in full each run |

The curve and quotes files are a cache, not an archive: only the recent window
is kept. For older prices, query the live providers
(`fiqua.market.TreasuryFeedMarketDataProvider`,
`fiqua.market.TreasuryDirectMarketDataProvider`).

Served raw, with no credential, under:

    https://raw.githubusercontent.com/FabioNicotra/fiqua-market-snapshots/main/

Design notes: the "Mirror data providers" section of `docs/architecture.md` in
the fiqua repository.
