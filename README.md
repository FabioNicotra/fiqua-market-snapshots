# fiqua-market-snapshots

Auto-published market-data snapshots for [fiqua](https://pypi.org/project/fiqua/).

`treasury_cmt_curve.json` holds a rolling window (about ten trading days) of the
U.S. Treasury par yield curve, sourced from `home.treasury.gov`. It is written by
fiqua's `publish-treasury-curve` GitHub Actions workflow after each trading day and
read at runtime by `fiqua.market.TreasuryMirrorMarketDataProvider`, which keeps the
slow live Treasury fetch off the request path.

This is a cache, not an archive. Only the recent window is kept; older curves drop
off as new ones arrive. For full history, query the Treasury feed directly (see
`fiqua.market.TreasuryFeedMarketDataProvider`).

Served raw, with no credential, at:

    https://raw.githubusercontent.com/FabioNicotra/fiqua-market-snapshots/main/treasury_cmt_curve.json

Design notes: `docs/market-data-provider-design.md` in the fiqua repository.
