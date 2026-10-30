# Intelligence Publications Collection — Manifest (Tranche 1)

Harvest date: **2026-10-30**. Scope rule: **publicly released publications from official agency channels or official government repositories only.** No leaked/classified material, no document dumps, no third-party mirrors were harvested. Federation of American Scientists pages were not used as a source. Where a site refused automated access (HTTP 403 bot filtering), harvesting stopped and the block is recorded — no circumvention.

Collection root: `hidden_files/intelligence-publications/` · Total size at tranche 1: ~61 MB · Catalog format: JSONL, one record per item (`source, title, url, format`, plus type/date/doc-id where the source exposes them; `title_source` states whether a title came from the page or was derived from the URL slug).

---

## Group 1 — Agency publication libraries

### CIA — Center for the Study of Intelligence (CSI)
- Canonical home: https://www.cia.gov/resources/csi/ (verified HTTP 200)
- Enumeration: CSI sitemap (`/resources/csi/sitemap/sitemap-0.xml`) — complete URL inventory of the CSI subsite.
- **Cataloged: 1,987** (`cia/csi_catalog.jsonl`) — 674 journal-article archive pages (Studies in Intelligence vols. 1–~64), 154 recent-issue extract articles, 1,093 other journal pages (current/recent-issue articles and indexes), 60 books & monographs detail pages, 6 index pages.
- **Full text held: 13 PDFs** (`cia/studies_recent/`) — the unclassified full-issue *Studies in Intelligence* extracts for the most recent slice (Vols. 65–70, 2021–2026), the slice rule used. Map of all PDF links found on recent issue pages: `cia/studies_issue_pdfs.json`.
- **Gap (documented): CSI book/monograph full texts could not be held.** The book pages' own "Download PDF" links (under `cia.gov/csi/wp-content/uploads/…`) return HTTP 404 from the origin — verified on multiple sampled titles on 2026-10-30; several book pages expose no static download link at all. Linked-but-broken PDF URLs are preserved in `cia/book_pdfs.json` (4 pages, 23 links sampled before the pattern was confirmed dead). This is an agency-side breakage, recorded as the collection's largest single full-text gap.
- *Studies in Intelligence* back-run: article-level metadata is complete via the sitemap; article PDFs for pre-2021 issues are tranche 2.

### FBI — Law Enforcement Bulletin (LEB)
- Canonical home: https://leb.fbi.gov/ (verified 200); archive index https://leb.fbi.gov/archives
- Enumeration: issue archive pages spanning 2010–2026 (monthly issues; some early years partial).
- **Cataloged: 198 issues** (`fbi/leb_issues.json`) and **1,356 article/notice records** (`fbi/leb_articles.jsonl`) harvested from 198/198 issue pages (april-2011 recovered on retry). 494 titles from page anchor text; 862 derived from URL slugs (labeled in the data). Issue attribution = the archive page where a link was first encountered; issue pages cross-link recent content, so attribution is approximate for a minority of records.
- **Full text held: 67 items** (`fbi/leb_recent_text/*.txt`) — every article in the most recent slice (issues dated 2025–2026), cleaned HTML-to-text.
- Feed: the site publishes an RSS feed (https://leb.fbi.gov/RSS) — feed-watch candidate (see collection note).

### NIJ — National Institute of Justice
- Canonical home: https://nij.ojp.gov/ ; publications library https://nij.ojp.gov/library/publications/list (verified 200)
- Enumeration: NIJ's own XML sitemap (16 sitemap pages) — every `/library/publications/*` URL on the site.
- **Cataloged: 15,752 publications** (`nij/catalog.jsonl`) — the full enumerable public catalog of the NIJ library as exposed by the site sitemap (research reports, journal articles incl. the *NIJ Journal*, annual reports, topical items; titles slug-derived except the newest ~80, which carry page titles). This is "all" of what the site's sitemap exposes; items delisted from the sitemap, if any, are invisible to this method.
- **Enriched slice:** the 30 newest publications were fetched individually (`nij/recent_enriched.jsonl`) — 19 with publication dates recovered; NCJ-number extraction failed against current page markup (0 recovered — known gap, tranche 2).
- **Full text held: 5 PDFs** (`nij/recent_pdfs/`) — of the enriched 30, only 5 expose a direct official PDF link (ojp.gov) that downloaded cleanly; the rest link PDFs through viewer pages (tranche 2 backfill).

### ODNI — Office of the Director of National Intelligence
- Canonical home: https://www.dni.gov/ (also https://www.intelligence.gov/)
- **Cataloged: 0 — BLOCKED.** Both hosts return HTTP 403 (bot filtering) to direct fetch and to the text-fetch service on 2026-10-30. No circumvention attempted.
- Known public series (not harvested): Annual Threat Assessment of the U.S. Intelligence Community; Statistical Transparency Reports; CLPT transparency documents. Tranche 2: retry, and cross-check DTIC/govinfo holdings (official repositories).

### NSA — National Security Agency
- Canonical home: https://www.nsa.gov/
- **Cataloged: 0 — BLOCKED** (HTTP 403 bot filtering, same pattern).
- Known public series (not harvested): Center for Cryptologic History publications (Cryptologic History Series, Cryptologic Quarterly selections, historical monographs), NSA historical/declassified releases. Tranche 2: retry; many CCH titles are also in the NARA Catalog and DTIC.

### DIA — Defense Intelligence Agency
- Canonical home: https://www.dia.mil/
- **Cataloged: 0 — BLOCKED** (HTTP 403).
- Known public series (not harvested): the Military Power publications series (country studies), DIA public reports. Tranche 2: retry / DTIC cross-check.

### NGA — National Geospatial-Intelligence Agency
- Canonical home: https://www.nga.mil/ (verified 200)
- **Cataloged: 2 route records** (`nga/routes.jsonl`). NGA operates no enumerable publications library on its public site; its public products are chiefly data/services (GEOINT products, geographic names) and news-format items (incl. *Pathfinder* magazine via the news section). Recorded as verified-but-not-a-publication-library.

### DHS — Office of Intelligence & Analysis
- Canonical home: https://www.dhs.gov/office-intelligence-and-analysis ; filtered library https://www.dhs.gov/publications-library/intelligence-and-analysis
- Enumeration: the DHS Publications Library's own I&A filter (7 result pages).
- **Cataloged: 67 publications** (`dhs/catalog.jsonl`) — all items the library's I&A filter returns (assessments, oversight program documents, threat-awareness products, program announcements). Metadata only in tranche 1; the underlying PDFs sit on dhs.gov and are a tranche-2 full-text backfill. Note: DHS I&A's finished intelligence is largely FOUO/law-enforcement-sensitive and never public; this catalog is the genuinely public residue.

### State Department — Bureau of Intelligence and Research (INR)
- Canonical home: https://www.state.gov/ (bureau pages under /bureaus-offices/; the legacy INR bureau URL returns 404)
- **Cataloged: 0.** INR maintains no public publications library; it publishes essentially nothing under its own name publicly (its public footprint runs through ODNI products and FRUS). Recorded as verified-absent, not an access failure.

### National Intelligence University / IARPA
- Canonical homes: https://ni-u.edu/ (NIU), https://www.iarpa.gov/ (IARPA)
- **Cataloged: 0 — both BLOCKED** (HTTP 403 bot filtering). NIU Press titles and IARPA program publications are tranche-2 retries.

---

## Group 2 — Declassification & FOIA reading rooms (agency-published)

### CIA FOIA Electronic Reading Room (incl. CREST)
- Canonical home: https://www.cia.gov/readingroom/ (verified 200); CREST collection: https://www.cia.gov/readingroom/collection/crest-25-year-program-archive (verified 200)
- **Cataloged: 6 named collections** (`cia/readingroom_collections.jsonl`) — the collections linked from the reading-room home (CREST 25-Year Program Archive; Presidents Daily Brief 1961–1969; Nixon Collection; Current/Central Intelligence Bulletin; AQUILINE; Collapse of Communism in Eastern Europe). The collections index itself is JavaScript-rendered and not statically enumerable; the full collections list is larger (~dozens of special collections) — tranche 2 via the reading room's own search facets.
- Documents: the reading room is a **search interface over ~millions of declassified pages** (CREST alone was ~13 million pages at transfer to NARA); document-level harvest is not enumerable without query fan-out and was not attempted. Metadata-only at collection level, by design.

### FBI Vault
- Canonical home: https://vault.fbi.gov/ (verified 200)
- Enumeration: the Vault's own XML sitemap.
- **Cataloged: 9,944 URLs** (`fbi/vault_catalog.jsonl`) spanning **1,886 distinct top-level subjects/collections** — overwhelmingly individual file "part" view pages (released file sets, incl. proactive disclosures and FOIA releases). Titles slug-derived (labeled).
- Full text: none held in tranche 1 (the Vault's holdings are very large scanned PDFs; subject-level full-text backfill is tranche 2, prioritized by subject).

### State Department — FRUS (Office of the Historian)
- Canonical home: https://history.state.gov/historicaldocuments (verified 200)
- Enumeration: the per-administration volume index pages (29 pages).
- **Cataloged: 237 FRUS volumes** (`state/frus_volumes.jsonl`) — every volume linked from the administration indexes. The full FRUS series (1861– ) runs to ~580 volumes in print; the Historian's digital edition is a subset and this enumeration reflects what the administration pages link — tranche 2 reconciles against the Historian's own volume search. Volumes are HTML/XML-native; no bulk full text in tranche 1.

### State Department — FOIA Reading Room / FOIA Library
- Canonical home: https://foia.state.gov/ (verified 200)
- **Cataloged: 5 route records** (`state/foia_routes.jsonl`) — FOIA Library, Collections, MDR section, FOIA logs/reports. The portal is an ASP.NET search application; its Collections page renders via postback and is not statically enumerable. Search-only at document level; recorded as a route, tranche 2 if an enumerable view is found.

### NSA Declassification & Transparency
- Canonical home: https://www.nsa.gov/ (declassification/transparency and FOIA sections under it)
- **Cataloged: 0 — BLOCKED** with the rest of nsa.gov (HTTP 403). Tranche 2: retry; NSA releases are also partially discoverable via the NARA Catalog (RG 457).

### ODNI — IC on the Record
- Channel: icontherecord.tumblr.com (launched by ODNI 2013-08-21)
- **Status determination: official historically, NOT harvested in tranche 1.** ODNI's own Civil Liberties, Privacy and Transparency office published a "Transparency Tracker" cataloging IC on the Record releases (Jan 2013 – May 2017), and ODNI statements describe it as "ODNI's public Tumblr site" — official status is documented by the agency itself. However: (a) the channel is dormant (tracker coverage ends May 2017), (b) the official tracker PDF itself is hosted on the bot-blocked odni.gov/dni.gov domains and could not be downloaded at harvest (a 479-byte stub was returned), and (c) harvesting the catalog from Tumblr directly would mean harvesting from a third-party platform rather than the agency's own record. Recorded as a **verified-official candidate** for tranche 2, catalog source = the ODNI CLPT tracker once reachable.

### NARA — National Declassification Center (NDC) + Catalog
- Canonical homes: https://www.archives.gov/declassification/ndc/ ; release lists https://www.archives.gov/declassification/ndc/release-lists ; Catalog https://catalog.archives.gov/
- **Cataloged: 10 release-list files** (`nara/release_lists.jsonl`) — the NDC's posted quarterly/annual release lists (XLSX/PDF) enumerated from the release-lists pages and their era sub-pages. Each list is itself an entry-level index of hundreds–thousands of declassified records, so the collection holds the NDC's catalog layer without re-keying it.
- **Full text held: 1 file** — the FY26 Q4 release list PDF (`nara/fy26-q4-release-list.pdf`), the most recent list, as the held sample.
- NARA Catalog proper: the public API endpoint probed returned the web-app shell rather than JSON from this vantage; series-level declassified-record harvesting via the Catalog API is tranche 2. ISCAP releases (linked from archives.gov/declassification) noted as an adjacent official series for tranche 2.

---

## Group 3 — Allied / official-adjacent (candidates only in tranche 1)

- **Canada — CSIS** (csis-scrs.gc.ca / canada.ca): connection to the agency host failed at harvest (no HTTP response); **not harvested**. Candidate: CSIS Commentary / annual public reports, tranche 2.
- **United Kingdom — GCHQ / official intelligence history**: the probed GCHQ path returned 404 (wrong path, not a block); **not harvested**. Candidates: GCHQ published historical papers and The National Archives' official-history releases, tranche 2 with verified canonical URLs.

---

## Totals (tranche 1)

| Measure | Count |
|---|---|
| Catalog records, all sources | **29,366** |
| — CIA CSI | 1,987 |
| — FBI Vault | 9,944 |
| — FBI LEB | 1,356 (+198 issue records) |
| — NIJ | 15,752 (+30 enriched) |
| — FRUS volumes | 237 |
| — DHS I&A | 67 |
| — CIA Reading Room collections | 6 |
| — NARA NDC release lists | 10 |
| — NGA / State FOIA routes | 7 |
| Full-text items held | **86** (13 CIA Studies issue PDFs · 5 NIJ PDFs · 67 LEB article texts · 1 NARA release-list PDF) |
| Sources blocked by site bot-filtering (0 harvested) | ODNI, NSA, DIA, NRO*, IARPA, NIU |

\* NRO (https://www.nro.gov/) — probed in the first recon batch: HTTP 403, same blocked cluster as ODNI/NSA/DIA. NRO's public/declassified releases (e.g., satellite program histories) are tranche-2 retries; several NRO declassified collections are also described in the NARA Catalog.

## Coverage honesty statement
"All" in this manifest means *all of the public catalog as the agency's own site enumerates it* (sitemap or official index), for CIA CSI, FBI Vault, FBI LEB, and NIJ. For FRUS it means all volumes linked from the Historian's administration indexes (a subset of the digital edition, which is itself a subset of the print series). For DHS I&A it means all items the official library filter returns. For the reading rooms (CIA, State FOIA) only the collection level is cataloged — document level is search-only by the agencies' own design. Six IC sources returned nothing at all due to bot filtering; their absence is a harvest-access fact, not evidence about the size of their public catalogs (NSA's and ODNI's are substantial).
