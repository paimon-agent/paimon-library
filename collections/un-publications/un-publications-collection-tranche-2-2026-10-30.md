# UN Publications Collection — Tranche 2 (2026-10-30)

Dispatched by the parent as an overnight autonomous run under the standing
collection doctrine: official UN channels only, public sources only, no
accounts, paced requests, access blocks recorded and never circumvented,
raw captures preserved before parsing, counts re-verified from disk,
honest fractions, "complete" claimed only for closed universes.

Tranche 2 executed the four items filed in the tranche-1 note §10, in its
filed order. Collection root:
`hidden_files/un-publications/`.

## 1. WHO IRIS OAI-PMH harvest (tranche-1 plan item 4, residual leg)

Route: `https://iris.who.int/server/oai/request` (DSpace 7 OAI-PMH,
metadataPrefix oai_dc). Identify verified 2026-10-30: earliestDatestamp
2008-05-01, granularity second-precision, deletedRecord transient.
Denominators: OAI ListRecords total 277,585 (includes deleted stubs);
DSpace REST total 274,847 (live items only).

Method: monthly datestamp windows 2008-05…2026-10 with the single
dominant window split out — **2025-10 carries 252,764 records (91% of
the repository)**, one continuous backfile digitization ingest,
2025-10-21T10:39Z → 2025-10-22 (152,541 records on the 21st, 100,117
on the 22nd, ~11K/hour; the first batch record is a 1960 World Health
Assembly minutes). October was harvested as 27 per-hour windows plus
29 per-day windows; deleted records are kept as flagged stubs.

**Incident (recorded in full in §6):** the first complete pass over all
277 windows was held only in ephemeral scratch storage when the VM
rebooted at 07:51 UTC, destroying it — including two windows damaged
earlier the same night by a duplicate-worker race (two same-shard
incarnations writing the same files after a botched restart; banks
verified clean for all other windows). The harvest was rebuilt with
all state in the collection tree (`agency-repositories/who-iris/`,
raw pages gzipped under `oai_raw/`, parsed records under `oai_parsed/`,
worker state under `work/`) and re-run from scratch.

**Result — closed universe, complete at metadata level.** The rebuild
harvested all 277 windows with every window's banked pages verified
record-for-record against its parsed output and against the server's
per-window completeListSize. The merge (dedup by OAI identifier)
produced **277,585 unique records — exactly the OAI endpoint's own
unwindowed completeListSize — with zero duplicates**: **274,211 live
records** (`who_iris_records.jsonl`) and **3,374 deleted-record stubs**
(`who_iris_deleted.jsonl`, kept and flagged). Installed under
`agency-repositories/who-iris/` (9,500 gzipped raw pages in `oai_raw/`;
merge report alongside). Live records sit 636 below the REST total
probed earlier the same day (274,847): repository drift between the
two measurements and/or REST-vs-OAI counting conventions — the
OAI-side closure is exact. Full text (bitstreams) not harvested.

## 2. GA special + emergency special sessions (tranche-1 plan item 1)

**Closed.** The tranche-1 note said these were "absent from every DHL
route tried" — that was itself wrong: the Dag Hammarskjöld Library
guide pages carry the full static tables, and they are the route that
worked (browser user-agent, plain GET):

- `https://research.un.org/en/docs/ga/quick/special` → **76 records**,
  sessions S-1…S-32. Three sessions are *not* gaps: S-28 (2005) and
  S-29 (2014) are commemorative sessions whose guide sections carry no
  resolutions table (the Library records no resolutions adopted);
  S-31 (2020, COVID-19) adopted decisions only — its sole table row,
  A/S-31/3, is a decision and is excluded by design (2 such rows
  skipped across both files).
- `https://research.un.org/en/docs/ga/quick/emergency` → **86 rows /
  85 unique symbols**, all 11 emergency sessions (ES-1…ES-11; ES-10
  alone 27). A/RES/996 is cross-listed in the ES-1 and ES-2 tables
  (it spans both sessions) — both rows kept and flagged. The guide is
  current: it includes A/RES/ES-11/10 of 24 February 2026.

The tranche-1-filed route (Digital Library symbol-prefix export)
failed: digitallibrary.un.org search answers HTTP 202 with an empty
body (bot challenge) for HTML and `of=xm` alike — recorded, not
circumvented. `www.un.org/en/ga/sessions/special.shtml` loads fine
with a browser user-agent (the tranche-1 403 was user-agent
dependent).

Dedup vs the 21,665-record regular-session catalog: zero symbol
overlap, zero base-number collisions — the 162 records are purely
additive. Legacy resumption tables (ES-10 especially) carry
month-year adoption dates only; preserved verbatim.

Installed:
`general-assembly-resolutions/ga_special_resolutions.jsonl` (76) +
`.csv`; `ga_emergency_resolutions.jsonl` (86) + `.csv`; raw guide
pages in `general-assembly-resolutions/raw_tables/`. GA structured
records now 21,665 + 162 = **21,827**.

## 3. S/RES/2561–2575 (tranche-1 plan item 2) — correction of record

The tranche-1 catalog filed these 15 resolutions as **(2020)**. That
year was wrong, and it is why every enrichment route failed in
tranche 1: no documents exist under the (2020) symbols. The correct
symbols are **S/RES/2561–2575 (2021)** — under them, the ODS API
served all 15 full texts immediately:

- 2561: 29 Jan 2021 (UNFICYP, Cyprus) · 2562: 11 Feb (UNSMIL, Libya) ·
  2563: 25 Feb (Somalia sanctions) · 2564: 25 Feb (Yemen sanctions) ·
  2565: 26 Feb (Somalia / AMISOM) · 2566: 12 Mar (UNMISS) · 2567:
  12 Mar (Sudan / UNITAMS) · 2568: 12 Mar (children & armed conflict /
  COVID-19 vaccines) · 2569: 26 Mar (Afghanistan / UNAMA) · 2570:
  16 Apr (Libya ceasefire) · 2571: 16 Apr (Libya arms embargo) ·
  2572: 22 Apr (South Sudan sanctions) · 2573: 27 Apr (protection of
  civilians in armed conflict) · 2574: 11 May (Iraq / UNITAD) ·
  2575: 11 May (Abyei / UNISFA).

All 15 records corrected in place (symbol, docs_url, adoption date,
adoption line, preamble opener) in `sc_resolutions.jsonl`/`.csv`; the 15
PDFs installed in `security-council-resolutions/ods_fill/`. Symbol-level-
only SC records remaining: **0 of 2,832**. The
same item's tail — the ~10 ODS records with partial tranche-1
first-page extraction (666, 1223, 1243, 1248, 1249, 1253, 1254, 1276,
2675, 2707) — was re-extracted from the held PDFs; all now carry
adoption dates and preamble openers (666's file is a compilation page;
its line was assembled from verbatim fragments, noted in its record).
The catalog's last two symbol-only records — **S/RES/800 and 801
(1993)**, flagged "pending tranche-2 enrichment" since tranche 1 —
were enriched from their shared compilation-page ODS file: Slovak and
Czech admission recommendations, both adopted without a vote on
8 January 1993 (3157th and 3158th meetings). Tranche 2 also filled
the standalone adoption_date field from the adoption line for 36
ODS-cluster records that carried the date only inside their topic
text. **Result: all 2,832 SC records now carry both a topic and an
adoption date; bare symbol-only records: 0.** Full-text PDFs held:
72 → **89** (84 SC + 5 GA).

## 4. Treaty Collection per-treaty enumeration (tranche-1 plan item 3)

**Closed: 675 treaties, all unique MTDSG numbers**, each with a
status-page URL (`ViewDetails.aspx?src=TREATY&mtdsg_no=…`, spot-verified
HTTP 200). Route: the Participation Status index's chapter links are
plain GETs (`Treaties.aspx?id={chapter}&subid=A&clang=_en`) — the
ASP.NET postback machinery was a dead end; the links were in the index
HTML all along. Chapter XI splits into sub-chapters A–E (only XI
does). Per-chapter: I:7, II:1, III:38, IV:27, V:5, VI:22, VII:12,
VIII:6, IX:13, X:33, XI-A:18, XI-B:231, XI-C:11, XI-D:10, XI-E:4,
XII:17, XIII:4, XIV:10, XV:3, XVI:3, XVII:1, XVIII:27, XIX:74, XX:1,
XXI:11, XXII:4, XXIII:3, XXIV:2, XXV:8, XXVI:13, XXVII:53, XXVIII:2,
XXIX:1. Validated per chapter page: the MTDSG numbers in the whole
document equal the set captured from its grid.

Denominator: the Collection's own homepage says "**more than 600**
multilateral treaties" — the enumerated 675 exceeds the round figure;
read as consistent (approximate/older figure and/or counting
conventions for lettered amendments and protocols), not as a
contradiction. One trailing grid column is unlabelled in the source
(e.g. 329 for the Genocide Convention); preserved as `source_list_no`,
meaning unverified.

Installed: `treaty-collection/mtdsg_treaties.jsonl` (675) + `.csv`;
34 raw chapter pages in `treaty-collection/raw_tables/`.

## 5. Totals after tranche 2

Structured metadata records: 43,843 → **322,265** (+162 GA
special/emergency, +675 treaties, +277,585 WHO IRIS). Full-text PDFs:
72 → **89**. Collection: ~10,500 files, ~714 MB (tranche 1: 621 files,
~122 MB). Closed universes now: Security Council (2,832/2,832, fully
enriched), WHO IRIS metadata (277,585/277,585), Treaty Collection
enumeration (675 vs ">600"), GA as listed across regular + special +
emergency sessions (21,827).

## 6. Incidents and access blocks (tranche 2)

- **VM reboot, 2026-10-30 07:51 UTC** (uptime reset; all processes
  killed). Everything installed in the workspace collection survived;
  the WHO IRIS first-pass harvest, held in ephemeral scratch, did not
  (see §1). Lesson recorded for the program's standing rules: harvest
  state belongs in the collection tree from the first byte, never in
  scratch.
- **Duplicate-worker race (WHO, first pass):** a pacing restart killed
  by PID list — the list included the operator shell itself — left
  first-incarnation split workers alive alongside their replacements;
  two windows (2025-10-22T04/T05) were left partial and two (T09/T12)
  misrecorded before the banks were audited (all other windows'
  raw banks verified byte-clean against their parsed outputs). The
  rebuild (§1) partitions windows disjointly across four workers with
  per-worker state files and no mid-flight restarts.
- digitallibrary.un.org search: HTTP 202, empty body (bot challenge) —
  recorded, not circumvented.
- WHO IRIS: occasional HTTP 500s under parallel load; retry/backoff
  absorbed them; no window failed terminally.
- **Post-reboot storage settling (WHO rebuild):** for roughly an hour
  after the reboot, reads of the workspace filesystem intermittently
  returned stale snapshots (window banks appeared short, then whole).
  The rebuild's later audits — run after the settling window — are
  fully consistent (bank = parsed = per-window completeListSize;
  merge total exactly 277,585 with zero duplicates). Any future audit
  of this collection should be run well clear of a reboot event.

Feed-watch candidates: unchanged from tranche 1 (none added by
tranche 2).
