# Catalog export — exclusion notes (per collection)

The export carries public collections only. The identity gate scanned
every exported line for the principal's identifiers (name, personal
mailbox, program mailbox): **0 hits, 0 lines dropped**
(`../identity-gate.json`). A broader hand scan surfaced two false
positives, adjudicated and kept: a historical program participant's
name inside declassified STAR GATE document titles, and a museum name
in one declassified title — neither is the principal or his location.

- **stargate** — exported in full at the catalog's latest state per
  document. Held back: the catalog's internal run-status and
  harvest-status records (operational bookkeeping, not documents);
  one campaign's downloaded-but-not-yet-ingested items (they enter the
  export when their ingest lands). Superseded earlier records for the
  same document are not exported — the append-only source catalog
  keeps them; the export is the current state.
- **scholarly-papers** — exported in full (metadata + public source
  locations). Abstracts were not exported; they remain reachable at
  the source.
- **un-sc-resolutions / un-ga-resolutions** — exported in full from the
  official-record catalogs. Held back: the store's larger structured
  sets whose catalogs have not yet been normalized into this export's
  shape (they are listed in the transport report as queued and remain
  retrievable through the convener).
- **public-archive-items** — series-level entries for the two verified
  public archive items; their member files are the archive's own.
- **Not exported at all, by rule:** one knowledge base bound to the
  principal's own locale and advocacy (held back under the identity
  rule — its general subject matter is reachable through the scholarly
  papers instead); campaign research notes; and every operational,
  personal, and correspondence-derived store in the local index, which
  is private by construction and never travels.
