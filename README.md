# Ottawa County Flock archive

Public-record archive of [Flock Safety transparency portals](https://transparency.flocksafety.com/) for Ottawa County agencies:

- **Holland PD** — `https://transparency.flocksafety.com/holland-mi-pd`

Same idea as [west-michigan-dispatch](https://github.com/Cantica-Systems/west-michigan-dispatch) and [kent-co-mi-flock](https://github.com/Cantica-Systems/kent-co-mi-flock): **the git history is the time-series.** The portals only keep about 30 days of search audits. This repo keeps every search id we have seen, in the month it occurred.

Latest summary: [`SNAPSHOT.md`](SNAPSHOT.md).

## Layout

```
data/
  holland-city-pd/
    YYYY-MM.csv              search audits, append-only, deduped on Flock id
    unknown.csv              rows whose searchDate didn't parse (rare)
    sharing_outbound.csv     agencies granted access to this agency’s data
    sharing_inbound.csv      agencies sharing their data with this agency
    stats.csv                portal totals, one row per snapshot

raw/
  <agency>/YYYY/MM/DD/…      portal page text as published
```

Search-audit CSVs are partitioned by **search time**. A search from 31 August lives in `2026-08.csv` even if it first appeared here in September. Ids already stored are left as-is.

Share lists are the current portal snapshot. `git log -p data/holland-city-pd/sharing_outbound.csv` shows when partners were added or removed.

Agencies pick which summary widgets to publish. A blank `stats.csv` cell (shown as — in [`SNAPSHOT.md`](SNAPSHOT.md)) means that figure was not on the page. The public search-audit CSV is the record this archive is built from; a portal with no audit file is not a completed snapshot.

## Columns (search audits)

| Column | Meaning |
|---|---|
| `id` | Flock search UUID |
| `userId` | redacted by the portal (`***`) |
| `searchDate` | UTC timestamp of the search |
| `networkCount` | networks/devices included in that search |
| `offenseType` | stated search reason |
