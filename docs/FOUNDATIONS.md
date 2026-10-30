# Foundations: API Catalog

This document records the method the catalogue follows: cardinal scope,
exclusions, admission criteria, allocation, cross-catalogue policy, and the
decision register. The record documentation standard
([RECORD-STANDARD.md](RECORD-STANDARD.md)) and the schema projection carry
the operational contract.

## 1. Cardinal scope

**API** — A contract defining the request/response shape of a service interface. Per CR-021 (D-4 disposition 2026-10-16): audit-then-specifies posture. The existing relationship vocabulary was audited in CR-021 §3.1; no existing relationship has the exact semantic "API contract specifies an interaction boundary". The canonical entry therefore sources the new dea:specifies relationship with target dea:IntegrationInterface. dea:API remains a contract entity; the interaction boundary it specifies is a separate Digital Profile entity (dea:IntegrationInterface). EGV-004 identity continuity: existing dea:entity-api references continue to resolve after regeneration. Cited template precedent: CR-019 (the abstract kind flip on dea:SolutionComponent; mirrored here for the API / interface separation).

## 2. What is deliberately excluded

Boundaries against sibling entity types are governed by the metamodel
definitions; anything that is not a api record
belongs to its owning catalogue (see the metamodel's `catalog_repo`
allocations).

## 3. Admission criteria and evidence ladder

1. The record describes a api per the metamodel definition.
2. At least one evidence source verifiably exists at admission time
   (`repository-path`, `system-of-record`, or `published-document`).
3. Relationship instances are asserted only against canonical target ids
   that exist; absence is honest (no local substitutes).

Evidence ladder (asserted in `provenance.ladder_passage`):
candidate → corroborated → reviewed → canonical.

## 4. Allocation

`dea:entity-api` (alias `API`), layer L5 / L5-integration, pinned against
OpenDEAM v0.8.0. Validated remotely by `validate-allocation.yml`
and locally by Gate 2. Upstream pins live in `dependencies.yaml`.

## 5. Cross-catalogue reference policy

1. Crosswalks and references are recorded on the asserting record's side,
   as typed relationship instances (metamodel relationship-instance
   contract).
2. Assertions wait for canonical targets: no scheme invention where a
   sibling id scheme does not exist.
3. Gates never resolve remote repositories; vendored registry snapshots
   carry the offline contract where a specific target family is asserted.

## 6. Decision-points register

| # | Decision | Status |
|---|---|---|
| D-1 | Methodology-first bring-up: no records before the kit and population CR | Adopted (CR-API-CAT-01) |
| D-2 | Hybrid pointer: identity keys for the regenerator + `metamodel:` allocation block for the root-model validator | Adopted (CR-API-CAT-01) |
| D-3 | Record ids take the `dea:api-<slug>` form (information-classes `dea:`-prefix precedent) | Adopted (CR-API-CAT-01) |
| D-4 | Admission ladder: candidate → corroborated → reviewed → canonical | Adopted (CR-API-CAT-01) |
| D-5 | Evidence-only admission: no record without a verifiable source; population plans document the wait | Adopted (CR-API-CAT-01) |
| D-6 | `CATALOG.yaml` is committed, not ignored (template deviation): the freshness gate diffs the committed index | Adopted (CR-API-CAT-01) |

## 7. Population plan

Initial population is evidence-gated. Candidate seed sources are named in
the population CR; where none are verifiable today, the catalogue stays at
zero canonical records with this section recording why and what would
unlock population.
