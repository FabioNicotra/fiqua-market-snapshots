# fiqua-market-snapshots

The published slice of fiqua's market data store, read at runtime by
`fiqua.market.MirrorMarketDataProvider` and
`fiqua.market.MirrorReferenceDataProvider` (the `mirror` preset). It keeps
slow or browser-blocked sources off the request path.

| File | Contents | Written by |
| --- | --- | --- |
| `store/v<schema>/mirror.sqlite.gz` | A gzipped SQLite market data store holding the last month of end-of-day U.S. Treasury data: the par yield curve from `home.treasury.gov`, the TreasuryDirect FedInvest list and prices of every marketable Treasury, and the contract terms of every listed security | fiqua's `publish-treasury-snapshots` workflow, each weekday evening, rebuilt in full each run |

Each fiqua release reads the folder for its own store schema version. A
folder for an older version is no longer updated.

The slice is a cache, not an archive: only the last month is kept. For older
data, query the live providers (`fiqua.market.TreasuryFeedMarketDataProvider`,
`fiqua.market.TreasuryDirectMarketDataProvider`).

Served raw, with no credential, under:

    https://raw.githubusercontent.com/FabioNicotra/fiqua-market-snapshots/main/

Design notes: the "Mirror data providers" section of `docs/market-data.md` in
the fiqua repository.

Until 2026-11-27 this repository also held three JSON snapshots
(`treasury_cmt_curve.json`, `treasury_bond_quotes.json`,
`treasury_bond_terms.json`), read by fiqua 0.5.0 and 0.6.0. They are kept in
the git history.
