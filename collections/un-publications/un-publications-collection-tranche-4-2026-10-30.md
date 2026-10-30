# UN Publications Collection — Tranche 4 (2026-10-30)

Dispatched by the parent as an autonomous run under the standing
collection doctrine: official UN channels only, public sources only, no
accounts, paced requests, access blocks recorded (with `valid_as_of` +
`next_trigger`) and never circumvented, raw captures preserved before
parsing, per-window raw banks verified against parsed output, counts
re-verified from disk, honest fractions, "complete" claimed only for
closed universes.

Tranche 4 executed the six legs filed in the tranche-3 note's residue,
in its filed order (1)–(6), run as four disjoint parallel partitions of
the collection tree (state in the tree from the first byte; no shared
shards). Collection root: `hidden_files/un-publications/`. Identity
check on the finished tranche: **zero matches for the principal's
surname across the entire collection tree** (text formats and an
all-file-types pass; 0 hits).

Headline: full-text PDFs **378 → 1,171** (+793, all WHO IRIS,
MD5-verified); structured records unchanged at **322,316** (the DL
backfill's honest yield was 0 new); agency catalogs 26,797 → **28,109**
(UNICEF /documents/ delta); collection **11,207 files / ~1.5 GB →
14,556 files / 4,006,285,483 bytes (~4.0 GB)**. The tranche's two
attempted page-level harvests against agency HTML (UNDP flagship,
UNHCR) were blocked outright; everything blocked is recorded with its
evidence, nothing was circumvented.

## (1) WHO IRIS bitstreams — re-attempts, dedup-by-work, extension to 1,000 works

**Re-attempt of the 6 restricted handles — all 6 still restricted.**
Exactly one attempt per handle through the tranche-3 `process()` code
path (2026-10-30T12:22:16Z): 10665/387961, 387937, 387783, 387932,
387875, 387865 each returned **HTTP 401 on the bitstream content
endpoint only** (metadata public). Outcomes in
`bitstreams/reattempt_tranche4.jsonl`; the manifest rows were
consolidated in place with the tranche-3 error text preserved under
`tranche3_error`. Observation: for 10665/387932 and 10665/387875 the
content-endpoint bitstream UUID differs from tranche 3 (the bitstream
was replaced upstream) — still 401. Not circumvented; the remedy
remains a later re-attempt if embargoes lift (≤1 attempt per tranche).

**Deduplicated-by-work slice — the tranche's methodological step.**
Tranche 3's slice was the 300 most recent *records*, dominated by
language editions. Tranche 4 first built a work-level candidate list.
Slice rule as applied: group key = (issued date, sorted subject set,
sorted collection set) from each candidate's OAI record — WHO indexes
subjects in English across language editions, so editions of one work
share all three — with (issued, normalized title) as fallback for the
1,262 groups whose records carry no subjects; representative =
English-language record if one exists (27,127 groups), else the
earliest-ranked member; representatives keep most-recent-first order.
All 51,316 candidates joined to an OAI record (0 unmatched; `sets`
agreed in 100% of cases). Result: **36,450 distinct works; 6,298
multi-edition groups**. English preference changed the representative
in 38 of the first 1,000 works.

**The dedup key's measured failure (filed, not hidden):** it
false-merges sibling documents that share boilerplate subject sets.
Title-level inspection of the largest groups found FCTC
participant-guide clusters (63/59/52 members) of *distinct* documents,
a 63-record EURO "country profile for healthy ageing and care" cluster
(no loss — tranche 3 already held all 63), and a 7-report SEARO
communicable-disease country series (10665/386892–386898, issued
2026-08-07) collapsed to 1 work, of which only the representative
(Thailand) entered the slice. Genuine editions merge correctly (e.g.
the 5-edition medical-oxygen specifications group). **The 36,450
works figure is therefore a lower bound**, and the tranche-5 seed
below adds title discrimination before any further extension.

**Extension harvest — first 1,000 works complete.** Tooling:
`work/harvest_bitstreams_t4.py`, a copy of the tranche-3 script with
exactly two changes (candidate list → `candidates_dedup_t4.jsonl`;
report → `harvest_report_tranche4.json`; diff-verified). The slice's
issued cutoff is **2025-12-18** (the walk consumed 1,217 raw ranked
records to reach 1,000 works; the 1,000th work is 10665/384541). Of
the 1,000 representatives: 206 already in the manifest (skipped,
including the 6 restricted — not re-attempted a second time); **794
new attempts → 786 downloaded, 7 skipped-no-pdf** (10665/387103,
386385, 385075, 384699 xlsx; 386532 pptx; 384811 docx; 385272 no
ORIGINAL bundle), **1 failed** (10665/386730, `IncompleteRead` after
the script's internal retries — transient truncation, not a block).
Every one of the 786 was independently re-verified from disk: %PDF
magic, byte size, sha256, and **computed MD5 == DSpace's listed MD5,
786/786**.

**Coordinator follow-ups (both worker-flagged decisions, taken):**
(i) 10665/386730 re-attempted once — **downloaded** (5,106,235 bytes);
its manifest row preserves the extension error. (ii) The 6 SEARO
siblings (10665/386892–386897 — Sri Lanka, Nepal, Myanmar, Maldives,
Bhutan, Bangladesh) harvested individually, each row flagged with a
`dedup_note`; all 6 downloaded and verified. Follow-up outcomes in
`bitstreams/coordinator_followup_t4.jsonl`.

**Cumulative bitstream store (disk-verified): 1,082 PDFs,
3,024,888,265 bytes; manifest 1,100 rows (1,082 downloaded /
12 skipped-no-pdf / 6 failed-restricted); 1,100 unique handle_ids;
manifest byte sum == disk byte sum exactly; 0 orphans, 0 missing.**

Execution note: both a `nohup` launch and a tracked-background
relaunch of the harvest were silently reaped mid-run by the
environment (at [348/1000] and [434/1000]; logs end cleanly, no
partial rows — the script's per-row resumability absorbed both). The
leg completed via foreground chunk-resumption of the identical
command. See Issues — this pattern recurred across the tranche.

## (2) UNDP flagship sub-harvest — attempted in full, blocked in full

Subset recomputed independently: **2,502 URLs** under
`www.undp.org/publications/` in `undp/sitemap_urls.txt` (2,480
single-slug + 22 nested) — matches the tranche-3 estimate (~2,503).
All 2,502 landing pages were fetched (2026-10-30T12:23:19Z–13:31:23Z,
paced 1.5s between request starts, tranche-3 Chrome UA, raw body
preserved before parsing, resumable skip-existing fetcher):
**200 ×0 — 403 ×2,501 — status 0 ×1.** Every 403 body is the Akamai
"Access Denied" (edgesuite) page; all 2,501 are preserved in
`undp/flagship_raw_pages/`. Probes confirmed the block is HTML-route
wide (homepage, /publications, /about-us all 403 via curl, urllib,
and requests) while robots/sitemaps still return 200 from the same
host/UA — so **the tranche-1 403 did recur, for landing pages only**;
the tranche-3 inventory succeeded precisely because it needed only
sitemaps. The one status-0 row (idx 1123, an indigenous-peoples
handbook page) exhausted its single permitted retry on a proxy
connection error and stands recorded with next_trigger "next tranche
retry". Enrichment is 0 across all fields as a consequence of the
block — the extractor was self-tested on synthetic fixtures pre-run
(title, meta description, meta-date priority, `<time>` fallback, PDF
dedup/resolution all correct), so the zero is the block, not the
tooling. No throttle events (no 429/5xx/timeouts); the
stop-cool-down machinery never triggered. The fetcher was killed
twice by host restarts (at rows 926 and 1,425) and resumed
skip-existing both times with the catalog verified duplicate-free
before each relaunch. Reconciliation: `flagship_catalog.jsonl` =
2,502 rows = the subset, order and URL set equal. **Flagship
enrichment is BLOCKED, not unfinished** — next trigger: unblocked
egress or a verified official UNDP API/feed route; do not re-run
direct-HTML fetches from this host. The 25,804-URL inventory stands.

## (3) UNICEF follow-ups — retries (0 recovered) + /documents/ delta harvested

**(a) Sitemap retries.** Libya: the tranche-4 capture was 0 bytes;
the recovery leg's fresh paced attempt returned **HTTP 401, 0 bytes**
again (`libya__sitemap_tranche4b.xml`) — still blocked, zero URLs.
rosa/eap/azerbaijan: HTML pages again in both tranche-3 and tranche-4
captures — zero URLs extractable. No new publication-pattern URLs
came from any of the four.

**(b) Page retries.** All 31 tranche-3 non-200 records re-fetched
once (each annotated in place: `tranche3_fetch_status` preserved,
`tranche4_retry` added): **0 recovered — 403 ×28, status 0 ×3.**
The unicef.cn/subsites 403 band did not move.

**(c) /documents/ delta — computed from preserved sitemaps, ruled,
harvested.** Independent recomputation over all 165 preserved sitemap
files (157 valid XML; the non-XML are the HTML captures + Libya's
0-byte captures): **1,327 /documents/ URLs, 15 already in the
catalog, delta = 1,312** (www.unicef.org 1,309 + www.unicef.cn 3;
**all 1,312 landing-page-shaped, 0 direct-file**). The recompute
matched two other computations of the same delta exactly. Under the
coordinator's ruling (delta ≤ 2,000 → add + harvest under the sized
rule), all 1,312 were appended (`pattern: "documents"`,
`source_tranche: 4`; URLs in `sitemap_urls_tranche4_additions.txt`)
and their landing pages fetched: **1,274 × 200** with full captured
enrichment (titles 1,273, descriptions 1,172, **3,042 PDF links**
recorded across the records — links only), **10 × 403, 25 × status 0,
3 × 404**. The status-0s concentrate in a Moldova band whose pages
truncated mid-body (IncompleteRead at 81–168 KB) across ~1h of
retries; recorded as-is, not circumvented.

**Final UNICEF catalog (disk-verified): 2,305 records** — the 993
tranche-3 rows intact (URL set == `sitemap_urls.txt`) + 1,312
documents records; fetch_status **200 ×2,236, 403 ×38, 0 ×28,
404 ×3**; all URLs unique; catalog-vs-last-logged-retry mismatches 0.
`harvest_report_tranche4.json` carries the leg's full accounting
including a recovery addendum.

Process note (detail in Issues): this leg needed a recovery worker —
see the cross-leg process findings below.

## (4) UNHCR — 429 a third consecutive time; stand-down honored

Exactly one paced probe (`GET https://www.unhcr.org/publications`,
browser Chrome UA, 2026-10-30T12:21:58Z): **HTTP 429**,
`{"error": "too_many_requests", …, "retry_after": 600}` — the same
body as tranches 1 and 3, the stated 10-minute window again long past
in practice. `block_record.json` updated (all probes now preserved in
a `probes[]` history + `tranche4_probe`; valid_as_of 2026-10-30;
next_trigger: next tranche). **Catalog remains 0 records.** No
sitemap attempt, no pagination, no Refworld bulk harvest. Three
consecutive tranche-series 429s across a full day read as IP-level
throttling stricter than the site's own message (observation; the
mechanism is medium-confidence, not directly observable).

## (5) UNESDOC — one probe, STILL-BLOCKED

Exactly one paced probe (`GET
https://unesdoc.unesco.org/oai/request?verb=Identify`,
2026-10-30T12:22:07Z): **HTTP 200, `text/html`, 1,361 bytes — an HTML
SPA shell**, programmatically confirmed to contain neither `<OAI-PMH`
nor `<Identify>`. Same failure mode as tranche 3 (1,000-byte shell),
changed from the 520s of tranches 1–2. Verdict **STILL-BLOCKED** in
`agency-repositories/unesdoc/probe_tranche4.json` (valid_as_of
2026-10-30; next_trigger: next tranche or a unesdoc.unesco.org
uptime signal). No second probe; no harvest. Why the OAI path serves
the shell remains unestablished.

## (6) Digital Library backfill 2023-10 → 2024-09 — complete; 0 new; anomaly reconfirmed

The tranche-3 backfill's discipline mirrored exactly (its `harvest.py`
adapted only for the window range + the mandatory anomaly method
note; diff-verified): 12 monthly windows, full-datestamp form,
oai_dc, ≥1.5s pacing, raw banked before parsing, per-window
verification. **All 12 windows complete; raw `<record>` count ==
parsed lines in every window** (4/5/5/5/6/6/7/12/20/20/21/21 = 132
parsed lines). Merge: **21 unique identifiers, 111 cross-window
duplicate lines, overlap with the tranche-3 backfill 21/21 (a subset
of its 51), overlap with the tranche-1 slice 0 — unique NEW records:
0.**

The anomaly is reconfirmed programmatically, exactly as the method
note predicted: **no resumptionToken and no completeListSize in any
window**; **all 21 unique records carry the single datestamp
2025-07-22T15:33:49Z**, which lies outside every requested window;
and each window's identifier set is a superset of the previous
window's (perfect nesting). Window counts **must not** be read as
monthly activity. The 0-new outcome is a legitimate result, and the
filed recommendation stands: **no further pre-2024-10 backfill
windows without a new rationale** — the nesting evidence predicts the
returned set only shrinks going backward. Files:
`digital-library/backfill-2023-10_2024-09/` (`state.json` carries the
method note, per-window observations, and the merge record).

## Totals after tranche 4 (verified from disk 2026-10-30)

Structured metadata records: **322,316** (unchanged — DL backfill 2
added 0) + agency sitemap catalogs: UNDP 25,804 (inventory) + UNICEF
**2,305** = **28,109** (+1,312) + UNDP flagship attempt record (2,502
rows, all blocked) + 25 Refworld sample records (provenance-flagged;
UNHCR catalog = 0) + 222,907 iLibrary URLs (inventory level) + 29
treaty chapters. Full-text PDFs: 89 → **1,171** (+1,082 WHO IRIS,
i.e. +793 net over tranche 3's 378). Collection: **14,556 files,
4,006,285,483 bytes (~4.0 GB)**. Closed universes unchanged: Security
Council (2,832/2,832), WHO IRIS metadata (277,585/277,585), Treaty
Collection enumeration (675), GA as listed (21,827). WHO full text:
1,082 PDFs against 51,316 candidates / 36,450 deduplicated works
(lower bound) — first-1,000-works slice complete.

## Access blocks recorded (tranche 4)

unhcr.org — 429 (third consecutive probe; valid_as_of 2026-10-30;
next_trigger: next tranche) · unesdoc.unesco.org OAI — 200-with-
HTML-shell, 1,361 bytes (STILL-BLOCKED; next_trigger: next tranche
or uptime signal) · undp.org HTML routes — Akamai 403 ×2,501
flagship pages + homepage spot checks (robots/sitemaps unaffected;
next_trigger: unblocked egress or a verified official API/feed) ·
UNICEF Libya child sitemap — 401 (again) · UNICEF page retries —
403 ×28, 0 ×3 · UNICEF /documents/ non-200s — 403 ×10, 0 ×25,
404 ×3 · WHO IRIS bitstreams — 401 ×6 on re-attempt (content
restricted, metadata public; next_trigger: ≤1 re-attempt per
tranche).

## Issues (cross-leg, filed for the record)

1. **Detached/background processes were reaped repeatedly across the
   whole tranche** — WHO harvest (×2), UNDP fetcher (×2, host
   restarts), UNICEF v3 (host restart ~13:02 UTC). In every case the
   in-tree, resumable state absorbed the kill with **zero data
   loss** (verified duplicate-free before every resume). Standing
   consequence: long harvests in this environment must be resumable
   by construction and verified at each resume — all tranche-4
   tooling was, and the tranche's results rest on post-resume disk
   verification, not on process survival.
2. **UNICEF leg concurrent-writer collisions (×3).** The original
   leg's processes outlived its "interrupted" status: the
   coordinator's recovery brief was written against a live,
   still-appending `retry_tranche4.jsonl` (a mid-flight read of 107
   rows; 35 rows were on disk when the recovery leg started), a
   sibling process died in the 13:02 UTC host restart mid-fetch, and
   a finalizer raced the recovery leg's last minutes, producing 13
   duplicate log entries. All collisions were reconciled:
   catalog-vs-last-logged-retry mismatches = 0, the catalog's 993
   original rows verified intact, and every count in §(3) is from
   post-hoc disk verification. Lessons: an "interrupted" worker is
   not necessarily a dead one — verify writer liveness before
   dispatching a recovery, and snapshot shared-file counts at leg
   start. (One coordinator premise also corrected by the recovery
   leg: the tranche-4 UNICEF fetches captured full enrichment —
   titles, descriptions, PDF links — not the title+count-only shape
   the mid-flight file suggested.)
3. **A transient status-0 band** (UNICEF resume run) recorded 165
   connection-class failures while near-contemporaneous diagnostics
   returned 200; those rows were stripped (backup preserved) and
   re-attempted rather than filed as blocks. The Moldova truncation
   band, by contrast, reproduced over ~1h and stands as recorded.

## Residue — tranche 5 seeds (in order)

1. **WHO IRIS bitstreams:** before any extension beyond 1,000 works,
   refine the dedup key (add title discrimination for same-subject
   sibling series — series/country siblings are the measured
   false-merge class); the 36,450-works figure is a lower bound
   until then. Re-check the 6 restricted handles at most once per
   tranche. The remaining ~35,450 works are unharvested by slice
   design, not blocked.
2. **UNDP:** flagship enrichment stays blocked from this host — next
   attempt only via unblocked egress or a verified official UNDP
   API/feed route (establish the route's existence first). Do not
   re-run direct-HTML fetches from this host. The 25,804 inventory
   and the 2,502-row blocked-attempt record stand as the evidence.
3. **UNICEF:** the /documents/ pattern is now part of the catalog
   (2,305 records); future sitemap refreshes should include it in
   the pattern set from the start. Libya sitemap: retry next
   tranche. The Moldova status-0 band could be retried under a
   partial-body-acceptance method — that is a method change and
   needs its own ruling, not a silent retry.
4. **UNHCR:** one paced probe next tranche (the pattern is three
   consecutive 429s across a full day; a multi-day cool-down is the
   only untried variable — do not increase request volume).
5. **UNESDOC:** one paced Identify probe on an uptime signal or at
   the next tranche; harvest only on valid OAI XML.
6. **Digital Library:** no further pre-2024-10 backfill without a
   new rationale (nested-subset evidence predicts 0 new); never cite
   the 2023-10→2025-09 window counts as monthly activity.
