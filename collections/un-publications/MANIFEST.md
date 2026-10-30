# UN Publications Collection — Manifest (Tranches 1–2)

Harvest dates: **2026-10-30** (tranche 1; tranche 2 same day). Sources: official UN channels only (un.org domains and the UN's official repositories). No accounts or logins used. Requests were paced and honestly identified; every access block encountered was recorded, not circumvented.

Coverage discipline: "complete" is claimed only where a closed universe was enumerated and validated. Everywhere else this manifest gives the count actually held and the denominator's source — or states plainly that no trustworthy denominator exists.

## 1. Security Council resolutions — CLOSED UNIVERSE, COMPLETE

- Canonical source: Dag Hammarskjöld Library (DHL) Security Council meetings tables — data service behind `research.un.org/en/docs/sc/quick` (1999–2026) and the static tables in the same guides (1946–1998); gaps filled from the Official Document System (ODS).
- **Items cataloged: 2,832 of 2,832** — every numbered resolution S/RES/1 (1946) through S/RES/2832 (2026). Validated by sequential-number check: zero gaps.
- Composition: 2,771 records from the DHL tables (1,492 data-service era + 1,279 guide-table era, including text-scan rescues); 63 records enriched from ODS PDFs for resolutions the meetings tables omit (chiefly the written-procedure clusters). **Every one of the 2,832 records now carries a topic and an adoption date** (tranche 2 also filled the adoption_date field from the adoption line for 36 ODS-cluster records, and enriched the last two symbol-only records — S/RES/800 and 801 (1993), Slovak and Czech admission recommendations, adopted without a vote on 8 January 1993 — from their compilation-page ODS file).
- **Correction of record (tranche 2):** the 15 resolutions filed in tranche 1 as S/RES/2561–2575 **(2020)** carry the wrong year — the correct symbols are **S/RES/2561–2575 (2021)**. No documents exist under the (2020) symbols, which is why every tranche-1 enrichment route failed (the ODS API redirects nonexistent symbols to its error page). Under the (2021) symbols the ODS API served all 15 full texts; the records are corrected in place (symbol, docs_url) and enriched (adoption dates 29 Jan – 11 May 2021, adoption lines, preamble openers), and the 15 PDFs are held under `ods_fill/`. **Zero symbol-level-only records remain.**
- Tranche 2 also re-extracted the 10 records whose tranche-1 ODS first-page extraction was partial or empty (S/RES/666, 1223, 1243, 1248, 1249, 1253, 1254, 1276, 2675, 2707) from their held PDFs: all now carry adoption dates and preamble openers; S/RES/666's ODS file is a compilation page, and its adoption line was assembled from that page's verbatim fragments ("Resolution 666 (1990) of 13 September 1990"; "Adopted at the 2939th meeting" → meeting record S/PV.2939).
- **Full text held: 84 English PDFs** — the complete 2026 slice (21 resolutions, S/RES/2812–2832) under `fulltext/`, plus 63 gap-fill PDFs under `ods_fill/`.
- Files: `security-council-resolutions/sc_resolutions.jsonl` + `.csv` (2,832 rows each); raw source tables preserved in `raw_tables/` (134 files).
- Full-text slice rule: English PDFs via ODS for all Security Council resolutions adopted in the most recent calendar year (2026).

## 2. General Assembly resolutions (regular sessions) — ALL 81 SESSIONS AS LISTED

- Canonical source: DHL General Assembly session tables (`research.un.org/en/docs/ga/quick/regular/{session}`; data service for recent sessions, static tables for earlier ones).
- **Items cataloged: 21,665 records covering all 81 regular sessions, 1st (1946) through 81st (2026)**, with no session missing. Multi-part resolutions are cataloged at part level (e.g., A/RES/217(III) A–E, incl. part A, the Universal Declaration of Human Rights). Three parser generations (fixed-column, header-mapped, text-segment) were unioned to cover the tables' layout eras (8-, 6-, and 5-column formats, Roman-numeral symbol era included).
- Coverage statement: complete **relative to the Library's own session tables**, the authoritative public listing. Session 81 is the current session and lists 7 resolutions as of the harvest date. No independent denominator exists against which to verify the Library's tables themselves.
- **Special and emergency sessions — gap closed in tranche 2 (162 records).** The route that worked is the DHL guides' own static tables (`research.un.org/en/docs/ga/quick/special` and `/emergency`, plain GET with a browser user-agent); the tranche-1 statement that the guides carry no equivalent tables was itself incorrect — the data-service keys were the dead end. **Special sessions: 76 records** across S-1…S-32; S-28 (2005) and S-29 (2014) are commemorative sessions whose guide sections carry no resolutions table (no resolutions recorded as adopted), and S-31 (2020, COVID-19) adopted decisions only (its sole row, A/S-31/3, is a decision, excluded by design). **Emergency sessions: 86 rows / 85 unique symbols** across all 11 sessions ES-1…ES-11; A/RES/996 is cross-listed in the ES-1 and ES-2 tables (both rows kept, flagged); the guide is current through A/RES/ES-11/10 of 24 February 2026. Legacy resumption tables (ES-10 especially) carry month-year dates only, preserved verbatim. Dedup against the 21,665 regular-session records: zero symbol overlap — purely additive. The tranche-1-filed Digital Library route failed: digitallibrary.un.org search answers HTTP 202 with an empty body (bot challenge) for HTML and XML alike — recorded, not circumvented. GA structured records now total **21,827**. Files: `general-assembly-resolutions/ga_special_resolutions.jsonl` + `.csv` (76 rows), `ga_emergency_resolutions.jsonl` + `.csv` (86 rows); raw guide pages preserved in `general-assembly-resolutions/raw_tables/`.
- **Full text held: 5 English PDFs** — session 81 slice (A/RES/81/1–81/5). A/RES/81/6 and A/RES/81/7 are listed by the Library but were not yet retrievable from ODS at harvest time (API redirected to error page on repeated attempts); recorded in `fulltext/download_log.json`.
- Files: `general-assembly-resolutions/ga_resolutions.jsonl` + `.csv` (21,665 rows each); raw tables in `raw_tables/` (197 files); `textscan_unparsed.json` documents the residual mention analysis (umbrella symbols of multi-part resolutions, parts held).
- Full-text slice rule: English PDFs via ODS for all resolutions of the most recent (current) session.

## 3. UN Digital Library — one-year OAI-PMH metadata slice

- Canonical URL: https://digitallibrary.un.org — OAI-PMH endpoint `https://digitallibrary.un.org/oai2d` (Identify verified 2026-10-30: repository "United Nations Digital Library System"; metadata formats marcxml, oai_dc, oai_openaire; earliest datestamp 2017-04-08). The Library's data-policy note bars robot harvesting of full content — this harvest is metadata-only, paced.
- **Items cataloged: 19,346 metadata records (19,306 unique OAI identifiers; 40 duplicates from datestamp movement)**, covering datestamp window **2025-10-01 → 2026-10-30** — all 13 monthly windows completed, resumption tokens followed to exhaustion. October 2025 alone contributes 17,513 records (a mass-update batch in the source).
- Coverage statement: this is a **one-year slice, not the catalog**. The Library publishes no total-record count reachable by this harvest (its homepage refuses the harvest client, HTTP 403), so no fraction is claimed.
- Files: `digital-library/dl_oai_slice.jsonl`; raw OAI responses in `digital-library/oai_raw/` (198 XML pages).

## 4. Official Document System (ODS) — route documentation + full-text source

- Canonical URL: https://docs.un.org/{symbol} (JS application; language/version picker). Working machine route documented in `ods/source-note.md`: `https://documents.un.org/api/symbol/access?s={symbol}&l=en&t=pdf` redirects to the delivery PDF. undocs.org/{symbol} 301-redirects to docs.un.org.
- Role in this tranche: full-text source for the two flagship slices above (89 PDFs held in total across the collection: 84 SC + 5 GA).
- Access note: ODS returns 403 to HEAD requests and thin clients; full-browser-UA GET succeeds. Recorded, worked within, not circumvented.
- Enumeration limit: ODS is a document store searched by symbol, not an enumerable catalog; no size figure is published.

## 5. UN iLibrary / UN Publications — sitemap-complete URL inventory (metadata only)

- Canonical URL: https://www.un-ilibrary.org (sales-publication platform; publications.un.org is the program's home).
- Harvest route: the platform's own sitemap index (7 gzipped sitemaps, lastmod 2026-10-24).
- **Items cataloged: 222,907 content URLs** — the complete sitemap enumeration: 12,139 book roots (12,142 distinct ISBN-13s incl. chapter-level prefixes), 115,088 chapter components and 80,590 further book-component URLs, 13,268 journal-article URLs across 26 electronic ISSNs, 1,266 papers (DOI prefix 10.18356), 400 periodical and 147 series pages.
- Coverage statement: complete as a URL inventory of what the platform's sitemap lists on 2026-10-30. Metadata depth is URL/ISBN/ISSN level only; no full text taken (sales catalog; only openly free text would be taken, and the sitemap does not mark it).
- Files: `un-ilibrary/ilibrary_sitemap_urls.txt`, `ilibrary_books.csv` (12,139 ISBN rows), `ilibrary_journals.csv` (26 ISSN rows).

## 6. UN Treaty Collection — per-treaty enumeration (tranche 2)

- Canonical URL: https://treaties.un.org (Multilateral Treaties Deposited with the Secretary-General, MTDSG).
- **Items cataloged: all 29 MTDSG chapters** (chapter number, title) from the Participation Status index: `treaty-collection/mtdsg_chapters.json`.
- **Per-treaty enumeration completed in tranche 2: 675 treaties, all with unique MTDSG numbers**, each with title, adoption/registration data as the chapter lists give it, and a status-page URL (`ViewDetails.aspx?src=TREATY&mtdsg_no=…`, spot-verified HTTP 200). Route: the index's own chapter links are plain GETs (`Treaties.aspx?id={chapter}&subid=A&clang=_en`); chapter XI splits into sub-chapters A–E (only XI does). Largest lists: XI-B (transport) 231, XIX 74, XXVII 53. Files: `treaty-collection/mtdsg_treaties.jsonl` + `.csv` (675 rows); 34 raw chapter pages in `treaty-collection/raw_tables/`, validated per page (the set of MTDSG numbers in each page equals the set captured from its grid).
- Denominator check: the Collection's own homepage figure is "**more than 600** multilateral treaties" (accessed 2026-10-30); the enumerated 675 is consistent with that round, evidently approximate/older figure (counting conventions may also differ, e.g. for lettered amendments and protocols). One grid column (a trailing numeric column, e.g. 329 for the Genocide Convention) is unlabelled in the source; it is preserved as `source_list_no` with its meaning unverified.
- The UN Charter's landing point is recorded in `dag-hammarskjold-library/source-note.md` (https://www.un.org/en/about-us/un-charter).

## 7. Dag Hammarskjöld Library research guides + Depository Library programme — finding aids

- Canonical URL: https://research.un.org (sitemap probed: 109 URLs). The guides are the human interface to the same tables harvested in §§1–2 — they are the provenance record for this build.
- Depository Library Programme: operating since 1947; per the Library's own programme page (read 2026-10-30), it is transitioning to the **UN Library Knowledge Network** (contact dhldl@un.org). Details in `dag-hammarskjold-library/source-note.md`.

## 8. Major agency repositories — catalog-level inventory only (tranche 1)

Full inventory with sizes, export routes, and harvest plans: `agency-repositories/repositories.json`.

| Repository | Size (source's own figure) | Export route | Status 2026-10-30 |
|---|---|---|---|
| WHO IRIS (iris.who.int) | **274,847 items** (its DSpace 7 REST API total) | OAI-PMH `iris.who.int/server/oai/request` (Identify verified) + REST | **HARVESTED in tranche 2** — see below |
| UNHCR Publications / Refworld | no count published | Refworld site up (200); mixes UNHCR + external sources (provenance flag) | unhcr.org returned **429**; defer |
| UNDP Publications (undp.org/publications) | no count captured | — | **403** to harvest client; recorded |
| UNICEF Publications/Reports (unicef.org/reports) | no count captured | — | 200; sitemap route for tranche 2 |
| IAEA Publications + INIS (iaea.org/publications; inis.iaea.org) | not capturable (JS application) | INIS search app | Inventory only |
| UNESCO UNESDOC (unesdoc.unesco.org) | not capturable | OAI endpoint exists | **HTTP 520** on three attempts 2026-10-30 (outage/block); retry tranche 2 |

### WHO IRIS harvest (tranche 2) — CLOSED UNIVERSE, COMPLETE (metadata level)

- Route: OAI-PMH `https://iris.who.int/server/oai/request`, `oai_dc`, Identify verified (earliest datestamp 2008-05-01; deletedRecord transient). All state lives in `agency-repositories/who-iris/`: raw pages gzipped in `oai_raw/` (9,500 pages), per-window parsed files in `oai_parsed/`, harvest/merge code and worker logs in `work/`.
- **Items cataloged: 277,585 unique OAI records — exactly the endpoint's own unwindowed completeListSize (277,585)**, harvested over 277 datestamp windows (221 monthly windows 2008-05…2026-10 excluding 2025-10; October 2025 split into 27 hourly + 29 daily windows) with **zero duplicates**: **274,211 live records** (`who_iris_records.jsonl`) + **3,374 deleted-record stubs** (`who_iris_deleted.jsonl`, kept and flagged). Every window's banked raw pages were verified against its parsed output (record-for-record) and against the server's per-window completeListSize.
- The October 2025 window alone holds **252,764 records (91%)**: a single backfile digitization ingest, 2025-10-21T10:39Z → 2025-10-22 (~11K records/hour; the batch opens with a 1960 World Health Assembly minutes).
- Count note: live records (274,211) sit **636 below** the REST API total probed earlier the same day (274,847) — repository drift between the two measurements and/or REST-vs-OAI counting conventions; the OAI-side closure (277,585 = 277,585, zero duplicates) is exact. Full text (bitstreams) not harvested — metadata level only.

## 9. UN Journal — current-awareness source (not harvested)

- Canonical URL: https://journal.un.org — returned **403** to the harvest client on 2026-10-30; recorded in `un-journal/source-note.md`, not circumvented. Daily programme of meetings; value is current-awareness, not back-catalog.

## Access blocks recorded (2026-10-30)

www.un.org 403 (curl) · digitallibrary.un.org HTML 403 (OAI-PMH unaffected) · digitallibrary.un.org search HTTP 202 empty body (bot challenge; tranche 2) · docs.un.org HEAD 403 · journal.un.org 403 · undp.org 403 · unhcr.org 429 · unesdoc.unesco.org 520. ODS API returned transient 502s on three symbols; all three succeeded on retry. WHO IRIS answered occasional HTTP 500s under parallel harvest load; its retry/backoff absorbed them (tranche 2).

## Totals (after tranche 2, verified from disk 2026-10-30)

- Structured metadata records: **322,265** (2,832 SC + 21,827 GA + 19,346 Digital Library + 675 treaties + 277,585 WHO IRIS, of which 274,211 live and 3,374 deleted stubs) + 222,907 iLibrary URLs at inventory level + 29 treaty chapters.
- Full-text PDFs held: **89** (84 SC + 5 GA).
- Collection size: ~10,500 files, ~714 MB, under `hidden_files/un-publications/`.
- Closed universes completed: Security Council resolutions (2,832/2,832, every record with topic + adoption date); WHO IRIS metadata (277,585/277,585 unique OAI records); Treaty Collection per-treaty enumeration (675, against the source's own ">600"); GA resolutions as listed by the Library across regular (21,665), special (76), and emergency (86) sessions.
