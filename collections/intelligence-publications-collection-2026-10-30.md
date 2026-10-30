# Intelligence Publications Collection — Tranche 1 Note (2026-10-30)

**What was built.** A standing library of the U.S. intelligence community's *own* public publication output, plus its official declassification/FOIA channels, under `hidden_files/intelligence-publications/` with a per-source subdirectory and a full `MANIFEST.md`. Method: verify each source at its official home, enumerate through the agency's own sitemap or index (never a mirror), harvest the metadata catalog for everything enumerable, and hold full text for a stated recent slice. **29,366 catalog records and 86 full-text items** were collected. Six sources (ODNI, NSA, DIA, NRO, IARPA, NIU) refused automated access (HTTP 403 bot filtering) and were recorded as blocked with zero harvested — no circumvention was attempted.

## Per-source results (one line each)
- **CIA CSI** — complete sitemap catalog (1,987 records: Studies in Intelligence articles 1955–present, 60 books/monographs); 13 recent full-issue extract PDFs held (Vols. 65–70). **The book PDFs themselves 404 on the agency's own site** (see below).
- **FBI LEB** — 198 issue pages → 1,356 article records; all 67 articles from 2025–2026 issues held as full text.
- **FBI Vault** (declass group) — 9,944 sitemap URLs across 1,886 subjects; metadata only (holdings are massive scanned PDFs).
- **NIJ** — the collection's biggest catalog: 15,752 publications (the site's full sitemap-exposed library), 30 newest enriched, 5 PDFs held.
- **State FRUS** — 237 digital-edition volumes from the Historian's administration indexes.
- **State FOIA Library** — route-level only (ASP.NET search portal; not statically enumerable).
- **CIA Reading Room / CREST** — 6 named collections at collection level; document level is search-only by design.
- **DHS I&A** — 67 items (the official library's I&A filter, all pages).
- **NARA NDC** — 10 release-list files cataloged (each an entry-level index of declassified records); most recent quarter's list held in full.
- **NGA** — verified to have no publications library (products are data/services); 2 route records.
- **State INR** — verified-absent: no public publication catalog exists.
- **ODNI / NSA / DIA / NRO / IARPA / NIU** — blocked (403), 0 harvested.
- **IC on the Record** — official status *verified* from ODNI's own CLPT Transparency Tracker (agency-published catalog of the channel, 2013–2017), but not harvested: the tracker PDF sits on the blocked ODNI domains and the channel itself is a third-party platform. Carried as a verified-official candidate.
- **Allied (CSIS, GCHQ)** — not harvested (host unreachable / path unverified); candidates only.

## Notable findings and series
1. **CIA's broken book shelf.** CSI's books & monographs pages link full-text PDFs under `cia.gov/csi/wp-content/uploads/…`; every sampled link returns HTTP 404 from the origin (site-migration breakage). The catalog and the broken-link evidence are preserved (`cia/book_pdfs.json`); if CIA repairs the path, tranche 2 can pull ~40 monographs immediately. This is the single largest recoverable full-text gap.
2. **Studies in Intelligence** remains the community's flagship open journal — unclassified extracts now run to Vol. 70 No. 3 (Sep 2026); the recent slice is held in full.
3. **The declassification layer is catalog-shaped, not document-shaped.** NARA NDC quarterly release lists and the FBI Vault sitemap each act as ready-made entry-level indexes — harvesting the *lists* captures the catalog layer of millions of pages without touching the documents.
4. **NIJ is a publications firehose next to the IC's trickle** — 15,752 items vs. DHS I&A's 67 genuinely public products; most finished intelligence simply has no public arm.
5. Series worth watching: DIA *Military Power* country studies and NSA's *Cryptologic History* series (both behind the 403 wall), ODNI's *Annual Threat Assessment* and *Statistical Transparency Reports*, ISCAP release decisions (archives.gov), and FRUS's ongoing digital-edition expansion.

## Feed-watch candidates (candidates only — no cron edited)
- **FBI LEB RSS** — https://leb.fbi.gov/RSS (verified present on the site). Strongest candidate: a real journal feed.
- **CIA newsroom/CSI** — cia.gov publishes RSS for news releases; a CSI-specific feed was not verified at harvest. Candidate pending verification.
- **NIJ / OJP** — OJP operates news/publication RSS feeds; the NIJ publications list itself had no verified feed at harvest. Candidate pending verification.
- **NARA NDC release lists** — quarterly web postings, no feed found; a quarterly manual/poll check would do.
- **ODNI / NSA / DIA newsroom feeds** — presumably exist behind the same 403 wall; candidates once access is retested.

## Indexing
`~/workspace/bin/library-index build` indexes Markdown under goal workspaces — so `MANIFEST.md` and this note **will** be picked up by a normal build with no changes. It does **not** index JSONL catalogs or PDFs, so the 29,366 records are not full-text searchable through it as-is. Parent step (not run here — a full build rebuilds the global index): run `~/workspace/bin/library-index build`. If catalog search is wanted later, the cheap route is a one-off conversion of the JSONL catalogs to a single Markdown table per source (the manifest already summarizes them).

## Tranche-2 plan
1. **Retest the 403 wall** (ODNI, NSA, DIA, NRO, IARPA, NIU) — if access opens, harvest in this order: ODNI reports/threat assessments → NSA CCH series → DIA Military Power → NRO declassified collections → IARPA/NIU. Cross-check DTIC and govinfo (official repositories) for the same series in parallel.
2. **CIA books repair watch** — re-probe the wp-content PDF paths; pull all monographs if repaired. Also backfill Studies article PDFs pre-2021.
3. **Full-text backfill** — FBI Vault by priority subjects; DHS I&A's 67 PDFs; NIJ PDF backfill via publication viewer pages + NCJ-number extraction fix (current markup defeated the regex).
4. **Reading-room depth** — CIA Reading Room full collections list via its search facets; State FOIA Library if an enumerable view exists; FRUS reconciliation against the Historian's volume search (237 → full digital edition).
5. **IC on the Record** — harvest the catalog from ODNI's CLPT Transparency Tracker PDF if/when odni.gov is reachable.
6. **NARA Catalog API** — retry with proper API negotiation for series-level declassified holdings (RG 263/457/59 first).
7. **Allied tranche** — CSIS commentaries and UK official intelligence-history publications, with canonical URLs verified first.
8. **Cadence** — LEB and NIJ are living catalogs (monthly/continuous): quarterly refresh; NDC lists quarterly; the rest annually or on change.

*Discipline note: every item in this collection was published by the agency itself or an official government repository. Nothing leaked, nothing mirrored, nothing behind a login.*
