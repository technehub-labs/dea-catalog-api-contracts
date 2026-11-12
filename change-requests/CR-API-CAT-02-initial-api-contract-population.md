# CR-API-CAT-02: Initial API Contract Population

| Field | Value |
|---|---|
| **CR** | CR-API-CAT-02 |
| **Title** | Initial API contract population (627 records) |
| **Status** | Landed (this PR) |
| **Layer** | Catalogue (L5) |
| **Programme** | Ontology grounding (IS semantic architecture) |
| **Repository** | `technehub-labs/dea-catalog-api-contracts` |
| **Author** | Emmanuel A. Otchere |
| **Date** | 2026-11-12 |
| **Depends on** | CR-API-CAT-01 (kit bring-up); CR-IS-CAT-04B in `technehub-labs/dea-catalog-integration-interfaces` (the pinned Integration Interface population) |
| **Trigger** | Evidence-gated seed population per FOUNDATIONS section 7; the Integration Interface catalogue admitted 627 vendor-neutral boundary records, giving this catalogue its first verifiable seed source. |

## 1. Executive summary

This CR admits the initial population of the API catalogue: 627 canonical
API records (`dea:api-<slug>`), one per canonical Integration Interface
record of the pinned seed source, each asserting exactly one typed
relationship instance `specifies` against its Integration Interface id
(OpenDEAM v0.8.0 contract relationship, per the CR-021 D-4 disposition).
The catalogue moves from 0 to 627 canonical records; `CATALOG.yaml` is
regenerated and committed (D-6); the catalog version advances 0.1.0 to
0.2.0.

## 2. Scope

In scope: 627 record subtrees under `entities/v1-alpha/` (record YAML plus
per-record README per docs/RECORD-STANDARD.md), the deterministic
generator `scripts/generate_api_population.py`, the vendored inventory
`scripts/api_population_data.json`, `CATALOG.yaml` (regenerated),
`metamodel-pointer.yaml` (version bump only), `CHANGELOG.md`, this CR and
the register.

Out of scope: schema, gate, workflow or FOUNDATIONS changes; metamodel
changes; sibling catalogues; any API record without a canonical
Integration Interface target (none exists; every IF record at the pin
has one).

## 3. Method (derived, not asserted)

Per the CR-021 D-4 disposition, an API record is the contract that
specifies an interaction boundary; the boundary is owned by the
Integration Interface catalogue. The population is therefore derived
from the boundary evidence, not discretionary:

1. The seed source is the Integration Interface population admitted by
   CR-IS-CAT-04B in `technehub-labs/dea-catalog-integration-interfaces`,
   vendored at commit
   `35afd57443e4aab376dfc456cdef93fb39e7a22d`
   (`scripts/api_population_data.json`; 627 interfaces, each carrying 3
   distinct vendor corroborations as evidence only, per G-12).
2. One API record is emitted per interface: `dea:api-<slug>` where
   `<slug>` is the interface slug; name derived from the interface name
   (trailing ` Interface` becomes ` API Contract`; an already-API-named
   boundary becomes `... API Contract` via the ` Contract` suffix);
   description, tags and external references derived from the interface
   record fields (interface kind, interaction pattern, consumer class,
   sector, system class, 3 vendor corroborations).
3. Each record asserts exactly one relationship instance:
   `specifies` from the API id to the Integration Interface id, direction
   source-to-target, status active, with structured provenance (manual
   assertion, verified). No other relationship vocabulary is used.
4. Evidence is a repository-path source: the pinned Integration
   Interface record path in the seed repo. Gates never resolve remote
   repositories (FOUNDATIONS section 5); the reference is verifiable at
   admission time by any reader with access to the seed repo.
5. Admission ladder per FOUNDATIONS D-4 is recorded per record
   (candidate, corroborated, reviewed, canonical; all 2026-11-12, actor
   Emmanuel A. Otchere).

Interface kind coverage at the pin: 406 rest-api, 157 file-transfer, 36
message-topic, 27 event-stream, 1 rpc; interaction patterns 407
request-response, 157 batch, 27 streaming, 27 event-push, 9
event-subscribe. Every interface kind obtains its contract record; the
request/response shape wording follows the metamodel definition of
dea:entity-api (a contract defining the request/response shape of a
service interface), reading the shape as the contract the boundary
exposes whatever its interaction pattern.

## 4. Repository deliverables (this PR)

- `entities/v1-alpha/dea:api-<slug>/dea:api-<slug>.yaml` plus sibling
  `README.md`: 627 record subtrees (1254 files).
- `scripts/generate_api_population.py`: the deterministic, idempotent
  generator (per G-10; stdlib only; byte-identical re-runs; hard-fails
  on inventory anomalies and on D-004/D-005 glyph embargo violations).
- `scripts/api_population_data.json`: the machine-readable vendored
  inventory at the pin (with the seed repo, the seed CR and per-interface
  paths).
- `CATALOG.yaml`: regenerated (627 entities, all canonical,
  open_change_requests 0).
- `metamodel-pointer.yaml`: catalog version 0.1.0 to 0.2.0 (identity
  keys consumed by the regenerator; the `metamodel:` allocation block is
  untouched).
- `CHANGELOG.md` and `change-requests/README.md` index row.

## 5. CI requirements

All three existing workflows must pass without modification. Local
pre-flight (hand-rolled, full tree):

- validate-catalogue gate 1 (check_parse.py): every YAML and JSON file in
  the tree parses; 1279 yaml files checked, 0 findings. PASS.
- gate 2 (check_pointer.py): pointer identity keys consistent; version
  bump only. PASS.
- gate 3 (check_record_posture.py): 627 records, every id matches
  `dea:api-[a-z0-9-]+`, every type is API. PASS.
- gate 4 (regenerate_catalog.py --check plus check_catalog_index.py
  --strict): committed CATALOG.yaml equals the regenerator output for the
  in-repo environment (the repository field resolves from the git origin
  URL, which CI sets to the canonical https URL; the committed file
  carries that value); 627 entities, counts consistent, no orphans. PASS.
- gate 5 (check_schema.py): every record validates against
  schemas/entity.schema.json and its relationship instance against
  schemas/relationship-instance.schema.json (required fields, authorized
  relationship type `specifies`, id patterns, enums, closed field sets).
  PASS.
- gate 6 (check_record_documentation.py): description at least 40 chars
  with verbatim README blockquote; evidence rationale at least 20 chars
  with a known source kind; all five README sections present; every
  record carries relationships. PASS.
- validate-allocation: metamodel-pointer.yaml `metamodel:` block
  unchanged against OpenDEAM v0.8.0. PASS.
- validate-authorship: no new authorship-bearing fields outside the
  allowlist; CR metadata author is Emmanuel A. Otchere. PASS.

## 6. Acceptance criteria

1. 627 canonical API records exist, one per Integration Interface record
   at the vendored pin, each id of the form `dea:api-<slug>`.
2. Every record asserts exactly one `specifies` relationship instance
   whose target is the pinned Integration Interface id (direction
   source-to-target).
3. Every record carries at least one verifiable evidence source and a
   rationale; the evidence source is the pinned record path in
   `technehub-labs/dea-catalog-integration-interfaces`.
4. Re-running `scripts/generate_api_population.py` reproduces every
   record byte-identically (G-10).
5. `CATALOG.yaml` validates against the catalog index schema and equals
   the regenerator output in CI (D-6 freshness).
6. The D-004/D-005 glyph and punctuation embargo holds over every
   emitted record, README, script, data file, report and doc (no em dash,
   no en dash, no ellipsis, no triple semicolon in new text). The
   pre-existing em dash in the CR-API-CAT-01 CHANGELOG heading and in the
   metamodel-pointer.yaml title comment are untouched pre-existing text,
   not emitted by this CR.

## 7. NOT-list

1. No schema, gate, workflow or FOUNDATIONS edits.
2. No relationship vocabulary beyond `specifies`.
3. No vendor product admitted as canonical; vendor systems appear as
   corroboration evidence only (per G-12).
4. No remote resolution in any gate.

## 8. Risks

- The `repository` field of `CATALOG.yaml` is environment-dependent (it
  resolves from the git origin URL); CI sets the canonical https URL
  before the freshness gate runs, and the committed file carries that
  value. A clone with a different origin would regenerate a different
  value; this is the documented CR-CATALOG-STRUCT-06a behavior, not a
  drift introduced here.
- The seed repo is private; the evidence reference is verifiable to any
  reader with access, and the gates never resolve it (FOUNDATIONS
  section 5).

## 9. Definition of done

All three CI workflows green on the PR; merged to main; the register row
moved to Landed; the catalog version at 0.2.0 with 627 canonical records.
