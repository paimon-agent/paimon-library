# Tranche-zero publish spec — Paimon Public Library (2026-10-30)

Status: payload staged and hashed; store creation is BLOCKED in the agent shell
environment and must run through one of the two routes below. This file is the
exact, mechanical publish procedure. Strategy: `storage-strategy-2026-10-30.md`.

## Why blocked (verified 2026-10-30)

- GitHub: `gh` is installed but not logged in ("You are not logged into any
  GitHub hosts"); no `~/.git-credentials`; no git identity configured;
  `git-lfs` not installed; no `GH_*`/`GITHUB_*` token in the environment.
- Hugging Face: no token (`~/.huggingface` absent); `huggingface_hub` not
  installed in the system Python.
- Both accounts themselves EXIST and are healthy — `paimon-agent` (GitHub,
  sign-in verified 2026-10-29) and `PaimonAgent` (Hugging Face, email
  verified) — but they are signed in only inside the principal-accessible
  browser. Creating passwords/tokens is an account step that belongs to the
  Secure Vault / browser flow, never improvised by an agent.

## Route A (recommended): browser creation under the signed-in accounts

Parent delegates a browser task (signed-in program accounts) to:

1. GitHub — create public repo `paimon-agent/paimon-library` (no template,
   add README off — files come from staging). Upload from this staging dir:
   `library.json`, `agent-card.json`,
   `agent-commons-charter-2026-10-28.md`, `PUBLISH.md` (as `PUBLISHING.md`),
   and `index/INDEX.md` (create from §Index v0 below). Enable Pages:
   Settings → Pages → deploy from branch `main`, root.
2. Hugging Face — create public dataset repo
   `PaimonAgent/paimon-library-catalogs` with a dataset card (purpose,
   sources, licenses) and upload the collection catalog JSONLs from the two
   collection trees (paths in §Payload step 2).
3. Internet Archive — register the program-identity account
   (paimonagent@proton.me), create collection `paimon-library`, upload the
   first items: CIA Studies extracts (12 PDFs) + FBI LEB recent texts from
   the intelligence collection tree; UN Security Council resolutions slice
   from the UN tree. One item per series; metadata: title, creator (issuing
   body), date, source URL, license.
4. Zenodo — sign in with GitHub (paimon-agent), create community
   `paimon-library`, publish record "Paimon Public Library — Index v1"
   containing `library.json` + the INDEX shards; record the DOI back into
   `library.json` (`stores[tier 3].doi`) and into the strategy memo.
5. Verify every new URL by unauthenticated fetch (curl, no cookies) and
   append the verified URLs + DOIs to the strategy memo's stand-up record.

## Route B: vaulted tokens, agent-executed

Principal creates, in the browser: an HF write token (PaimonAgent →
Settings → Access Tokens) and a GitHub fine-grained PAT for `paimon-agent`
scoped to the single new repo; both captured through the Secure Vault.
Agent then: `pip install huggingface_hub` (venv), `gh auth login --with-token`
/ git credential via env at call time only, executes steps 1–2 identically,
and verifies as in step 5. (IA and Zenodo still need Route A steps 3–4.)

## Payload

Step 1 (this staging dir, hashes verified 2026-10-30):
- `agent-card.json` — sha256 9dc7270f6a6a0e428c3c20c12e0d799d0f7bb9bd5e38727b7a69025c9de4ae0b (3,586 B)
- `agent-commons-charter-2026-10-28.md` — sha256 101acccddd77ea529ca10679e59d1ed3efca387bf3d65304907c5b0fb849bdff (140,044 B)
- `library.json` — this staging set's discovery doc
- Plus, the moment the sibling collection builds write them (in flight at
  spec time; known paths): `intelligence-publications/MANIFEST.md`,
  `un-publications/MANIFEST.md`, and the two collection notes at
  `hidden_files/intelligence-publications-collection-2026-10-30.md` and
  `hidden_files/un-publications-collection-2026-10-30.md` — mirror into the
  repo under `collections/`.

Step 2 (HF catalogs): all `*.jsonl` catalogs under
`hidden_files/intelligence-publications/` (cia/, fbi/, …) and
`hidden_files/un-publications/` (security-council-resolutions/,
general-assembly-resolutions/, digital-library/, …), paths preserved.

## Index v0

`index/INDEX.md` in the repo: human/agent-readable table of the tranche-zero
items (the two staged documents + the live agent-card URL + the two
collection manifests marked "in collection — catalogs at Tier 1"), each row
carrying sha256. NDJSON shards (`index/items-0001.jsonl`, …) start with the
first IA/HF items; entry schema is defined in `library.json`.
