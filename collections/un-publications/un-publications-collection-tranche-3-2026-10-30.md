# UN Publications Collection — Tranche 3 (2026-10-30)

Dispatched by the parent as an autonomous run under the standing
collection doctrine: official UN channels only, public sources only, no
accounts, paced requests, access blocks recorded (with `valid_as_of` +
`next_trigger`) and never circumvented, raw captures preserved before
parsing, per-window raw banks verified against parsed output, counts
re-verified from disk, honest fractions, "complete" claimed only for
closed universes.

Tranche 3 executed the five legs filed in the dispatch, in its filed
order (a)–(e), run as five disjoint parallel partitions of the
collection tree per the tranche-2 §6 lessons (state in the tree from
the first byte; no shared shards; no mid-flight restarts). Collection
root: `hidden_files/un-publications/`. Identity check on the finished
tranche: zero matches for the principal's surname across the
collection's text files.

## (a) UNESDOC OAI retry — STILL-BLOCKED (failure mode changed)

One paced probe of `https://unesdoc.unesco.org/oai/request?verb=Identify`
(browser user-agent, 2026-10-30T09:20:06Z): **HTTP 200 — but the body
is a 1,000-byte HTML app shell** (`<div id="app">`), not an OAI-PMH
Identify XML response. The tranche-1/2 failure was HTTP 520; the site
now answers, but the OAI path serves the SPA fallback, so repository
name / earliest datestamp / size could not be extracted and
harvestability is unconfirmed. Under the leg's one-probe rule the
second probe (ListMetadataFormats/ListRecords) was correctly not run —
it was conditioned on a *valid* Identify response. Recorded in
`agency-repositories/unesdoc/probe-tranche3.json`: verdict
**STILL-BLOCKED**, valid_as_of 2026-10-30T09:20:06Z, next_trigger =
next tranche or a unesdoc.unesco.org uptime signal. Why the endpoint
serves the shell (endpoint moved/retired vs. site still recovering vs.
route intercepted) is **not established** — filed as observation, no
mechanism claimed (confidence high on the observation itself).

## (b) UNDP + UNICEF — sitemap routes; one inventory, one full sized harvest

**UNDP — inventory complete (25,804 publication URLs).** The
tranche-1 HTTP 403 did **not** recur with the full browser-style
user-agent: robots.txt and the sitemap index answered 200, and all 7
paginated urlsets were fetched and preserved raw (82 MB under
`undp/raw_sitemaps/`). Of 138,929 unique sitemap URLs, **25,804 are
publication URLs** (`/publications/` 25,732; `/evaluation/` adds 72
non-overlapping). 25,804 > the leg's 2,000 sized-harvest threshold →
**no landing pages fetched**, by rule: `catalog.jsonl` carries all
25,804 records at sitemap level (titles null by design, `date` =
sitemap lastmod, `source: "sitemap"`), reconciled line-for-line
against `sitemap_urls.txt`.

**UNICEF — inventory + full page-level harvest (993 records).**
Sitemap index + 158 child sitemaps: 157 fetched 200 (raw preserved);
the **Libya child sitemap returned 401** and the `rosa`/`eap`/
`azerbaijan` routes returned HTML instead of XML (0 URLs extractable;
captures preserved) — all recorded as blocks with
valid_as_of 2026-10-30, next_trigger = next tranche retry. Of 63,188
unique URLs, **993 are publication URLs** (`/reports/` 799,
`/evaluation/` 193, `/publications/` 1). 993 ≤ 2,000 → **all 993
landing pages fetched**: **962 × 200** (titles and descriptions on
962, page dates on 800, **1,604 PDF links recorded across 770 records
— links only, no PDFs downloaded**), **30 × 403** (15 on unicef.cn,
15 on unicef.org subsites; recorded per record as `fetch_status=403`,
not retried), 1 disconnect (a Pakistan child-marriage research page,
after one retry). Raw HTML preserved for the first 200 pages (198
files; 2 of the 200 were the 403/disconnect cases with no body).
**Throttle incident:** after ~667 paced fetches the host answered 9
consecutive 30s timeouts; the harvester was stopped, cooled down ~3
minutes, probed once (200 in 1.0s), and resumed at slower 2.0s pacing
to completion — the standing pacing discipline working as designed.
Judgment call flagged for a follow-up decision: `/documents/` paths
were excluded by the leg's pattern set, though the global sitemap
alone carries 401 such URLs that may be publication-adjacent; a
documents-only delta can be computed from the preserved raw sitemaps
without re-fetching.

## (c) UNHCR — 429 persists; Refworld inventoried, sample flagged

**unhcr.org:** a single paced probe of `/publications` after several
hours' cool-down returned **HTTP 429** again, body
`{"error":"too_many_requests", …, "retry_after":600}` — the stated
10-minute window had long passed, so the throttle reads as IP-level
and stricter than its own message (observation, not mechanism). No
sitemap/pagination attempt, no circumvention. Block recorded in
`agency-repositories/unhcr/block_record.json` (valid_as_of
2026-10-30, next_trigger: next tranche). **UNHCR catalog remains 0
records** (`catalog.jsonl` empty; the 3,000 cap unused).

**Refworld:** inventoried as scoped — routes all 200 (home, `/search`,
`/sitemap.xml` with 78 sub-sitemaps, browse by country /
document-source / documents-type / keywords / thematic-areas, 4
collections, the UNHCR section). Two structural findings: search
results are JS/federated-Solr-driven with no server-rendered rows,
and **`robots.txt` disallows `/search`** — the sample therefore used
only robots-allowed document/browse pages. Published facet counts
were extracted verbatim: 46 document types (Annual/Sessional Reports
44,137; Country Reports 20,952; Case Law 13,181; Resolutions/
Recommendations/Declarations/Decisions 11,661) and 475 document
sources with counts — **"UN High Commissioner for Refugees (UNHCR)"
= 5,829 documents, behind the US Department of State (13,679), the
UN General Assembly (7,498), and Amnesty International (7,025)**.
No global total is published; facet counts overlap and were never
summed. **Sample: 25 records** (13 most-recent homepage-linked + 10
core instruments + 2 UNHCR handbooks), each fetched individually and
carrying **`provenance: "refworld-mirror"`** with its stated issuer
preserved verbatim — **only 5 of 25 are UNHCR-issued as stated**;
the rest are national authorities, the General Assembly, OAU/AU,
and others. The sample is evidence for the provenance rule, not a
UNHCR catalog: **no record in this tranche carries
`provenance: "unhcr"`**. (Facet term list of 475 is a rendered-page
lower bound — the counts shown are verbatim, completeness of the
term list is medium-confidence.)

## (d) Digital Library OAI backfill 2024-10 → 2025-09 — harvested; major server anomaly

All 12 disjoint monthly windows harvested with the tranche-1
discipline (full-datestamp form, oai_dc, ≥1.5s pacing, raw pages
banked under `digital-library/backfill-2024-10_2025-09/raw/` before
parsing). Per-window verification: raw `<record>` count = parsed
lines in every window (21/21/21/21/34/36/45/51/51/51, then 0/0 —
2025-08 and 2025-09 answered `noRecordsMatch`). Merge: 352 parsed
lines → **51 unique OAI identifiers, zero overlap with tranche 1's
slice**; **41 of the 51 are deleted-record stubs** (kept, flagged);
10 carry full metadata (1997–2000 documents).

**Anomaly (the leg's real finding; recorded in the backfill
`state.json` and in MANIFEST §3):** the server returned **no
resumptionToken and no completeListSize for any backfill window**,
and all 51 unique records carry the **identical datestamp
2025-07-22T15:33:49Z** — a single purge/sanctions batch. Windows
2024-10…2025-01 return the identical 21-record subset; the set grows
monotonically to the full 51 by 2025-05 — i.e., **records are
returned for windows that do not contain their datestamp**, contrary
to OAI-PMH semantics. A single-day probe of 2025-07-22 returns all
51; 2025-07-23→31, all of 2025-08, and all of 2025-09 return
`noRecordsMatch`. Independently confirmed via ListIdentifiers, and
the tranche-1 October-2025 control window still returns
completeListSize=17,513 with in-window datestamps — the endpoint is
healthy; the anomaly is specific to pre-Oct-2025 datestamps
(plausibly an index/migration artifact of the repository's Oct 2025
mass update — that explanation is low-confidence; the behavior is
high-confidence, observed across 10+ probes and two verbs).

**Implication, stated plainly:** this backfill cannot evidence what
changed in the Digital Library during 2024-10→2025-09 beyond that one
batch. Either the repository genuinely had almost no OAI-visible
datestamp activity that year (activity concentrated in the Oct 2025
migration batch tranche 1 already holds), or its historical
datestamp index is incomplete; the endpoint alone cannot distinguish
the two. With no completeListSize and no resumptionToken,
completeness of the single-page windows is medium-confidence (OAI
semantics say each list is complete; ListIdentifiers corroborated
spot-checked windows; a silently truncated list cannot be ruled out
from the response alone). **Any future historical backfill
(pre-2024-10) should expect the same July-batch subsets for windows
before 2025-07 and must not read per-window counts as monthly
activity.**

## (e) WHO IRIS bitstreams — selective full text for the publication series

**Scope first (no downloads before the definition existed).** All 21
distinct `dc.type` values in the 274,211 live records were tabulated.
Adopted definition — **publication series proper** = the WHO
publication / technical-document / technical-report family:
Publications 16,293; Technical Documents 34,104; Technical documents
903; Technical Reports 8; Technical reports 6; Technical document 1;
Country Cooperation Strategy 1 → **51,316 candidate records =
18.7% of live records**. Excluded: Governing Bodies documents
(126,669 incl. case variants), Journal articles (62,490), untyped
(29,550), Meeting reports (2,448), press releases/fact sheets
(1,326), speeches (406), multimedia (3), and the singleton ephemeral
bulletins; one mis-typed Regional Committee document
(`Technical Documents [EM/RC63/R.6]`) was excluded on inspection.
DSpace REST corroboration (paced): 68 communities and 720
collections enumerated — per-office `Publications` and
`Technical Documents` collections corroborate the type scope;
journal articles live in separate collections. Full per-type
rationale in `bitstreams/series_scope.json`. Confidence: the
case/plural variant grouping is high (>0.9); the n=1 judgment calls
(Country Cooperation Strategy in; the two singleton bulletin types
and the EM/RC63 mis-type out) are ~0.7 each and documented per type.
Excluding the 29,550 untyped records is conservative and **known to
undercount** (at least one untyped record sits in a Publications
collection) — the true series is somewhat larger than 51,316.

**Harvest (bounded slice):** the most recent 300 candidates by
issued date — the slice's cutoff is **2026-09-16 → 2026-10-29**.
Attempted 300 · **downloaded 289** · skipped-no-pdf 5 · failed 6 ·
**569,487,781 bytes (544 MB)**. Verification was independent and
total: every PDF re-read — %PDF magic ✓, byte size ✓, sha256 against
the manifest ✓, and **computed MD5 equals DSpace's own listed
bitstream MD5 for 289/289**. The 5 skipped are genuine: 3 XLSX-only
ORIGINAL bundles (10665/387572, 387883, 387882) and 2 records with
no ORIGINAL bundle (10665/387861, 387736). The **6 failures are
HTTP 401 on bitstream content only** ("Authentication is required";
metadata and bitstream listing are public): handles 10665/387961,
387937, 387783, 387932, 387875, 387865 — read as restricted/
embargoed bitstreams (confidence ~0.85), reproduced on direct
re-test (not transient), recorded `failed` in the manifest, **not**
circumvented; a later re-attempt is the remedy if embargoes lift.
For multi-PDF ORIGINAL bundles the first PDF by filename was taken;
the other bitstream names are recorded per manifest row.

**Incident (found, fixed, recovered in-run):** 9,626 candidate
records (22 in the slice) carry `dc.identifier` as a bare string
with no handle URI; the first handle parser's OAI fallback produced
`10665/10665/<id>` → 404s. The parser was fixed, the bogus manifest
rows removed, and a recovery pass re-attempted all 22 → **22/22
downloaded**. Final counts above are post-recovery; candidate count
and date cutoff were unchanged by the fix. Slice character (stated
for honesty): dominated by the newest HQ/regional releases incl.
many language editions and multi-module course documents — a
faithful "most recent 300 records," not a deduplicated-by-work
selection. Tooling is resumable (`who-iris/work/harvest_bitstreams.py`;
full 51,316-row ranking in `work/candidates_sorted.jsonl`).

## Totals after tranche 3 (verified from disk 2026-10-30)

Structured metadata records: 322,265 → **322,316** (+51 DL backfill)
+ agency sitemap catalogs at inventory/catalog level: UNDP 25,804 +
UNICEF 993 = **26,797** (UNICEF page-enriched) + 25 Refworld sample
records (provenance-flagged; UNHCR catalog = 0). Full-text PDFs:
89 → **378** (+289 WHO IRIS). Collection: **11,207 files, ~1.5 GB**
(tranche 2: ~10,500 files, ~714 MB). Closed universes unchanged:
Security Council (2,832/2,832, fully enriched), WHO IRIS metadata
(277,585/277,585), Treaty Collection enumeration (675 vs ">600"),
GA as listed across regular + special + emergency sessions (21,827).
New in tranche 3: the WHO publication-series full-text slice
(289 of the most recent 300 candidates, MD5-verified) against a
scoped universe of 51,316.

## Access blocks recorded (tranche 3)

unesdoc.unesco.org OAI — 200-with-HTML-shell (STILL-BLOCKED;
valid_as_of 2026-10-30; next_trigger: next tranche or uptime
signal) · unhcr.org — 429 post-cool-down (valid_as_of 2026-10-30;
next_trigger: next tranche) · UNICEF Libya child sitemap — 401 ·
30 UNICEF page-level 403s + 1 disconnect (per-record) · 6 WHO IRIS
bitstreams — 401 content-restricted (per-handle, in the bitstream
manifest). Digital Library historical-datestamp anomaly (§d) is a
data-behavior finding, not an access block.

## Residue — tranche 4 seeds (in order)

1. **WHO IRIS bitstreams:** re-attempt only the 6 restricted handles;
   then extend the slice — `python3 work/harvest_bitstreams.py 1000`
   (most recent 1,000 candidates; expect ~2–3 h, ~1.8 GB, pacing
   ≥1.5s). Consider a deduplicated-by-work variant so language
   editions don't dominate.
2. **UNDP selective harvest:** the full 25,804 exceeds the page-fetch
   threshold; harvest the flagship/global subset instead
   (`https://www.undp.org/publications/*` top-level ≈ 2,503 URLs in
   `undp/sitemap_urls.txt`) as a sized sub-harvest.
3. **UNICEF follow-ups:** retry the recorded blocks (Libya 401;
   rosa/eap/azerbaijan HTML sitemaps; the 31 non-200 pages — URLs in
   `unicef/catalog.jsonl` where `fetch_status != 200`); decide
   whether `/documents/` URLs join the publication pattern set and,
   if yes, compute the delta from the preserved raw sitemaps (no
   re-fetch needed).
4. **UNHCR:** single paced probe of
   `https://www.unhcr.org/publications` (browser UA, ≥2s pacing). If
   200: map sitemap/pagination and harvest metadata into
   `unhcr/catalog.jsonl` (cap 3,000, `provenance="unhcr"` only for
   UNHCR-issued documents, raw pages first 100, reconciled report).
   If 429 again: update `block_record.json` valid_as_of and stand
   down. Do not bulk-harvest Refworld (robots disallows `/search`;
   sample-only, `provenance="refworld-mirror"`).
5. **UNESDOC:** one paced Identify probe at the next tranche or on
   an uptime signal; harvest only on a valid OAI response.
6. **Digital Library:** deeper backfill (pre-2024-10) only with the
   §(d) anomaly expectations written into its tasking; do not cite
   the 2024-10→2025-09 window counts as monthly activity.
