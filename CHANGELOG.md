# Changelog

## [Unreleased]

### `CR-API-CAT-02` initial API contract population (627 records)

Evidence-gated seed population derived from the Integration Interface
catalogue vendored at commit 35afd57443e4aab376dfc456cdef93fb39e7a22d
(CR-IS-CAT-04B): one canonical API record per interface, each asserting one
`specifies` relationship instance to its boundary; deterministic generator
(scripts/generate_api_population.py, G-10) plus vendored inventory
(scripts/api_population_data.json); CATALOG.yaml regenerated (627 canonical);
catalog version 0.2.0.

### `CR-API-CAT-01` — catalogue foundation (kit bring-up)

Standard kit generated from the metamodel (org-wide catalog advancement
programme): hybrid pointer pinned to OpenDEAM v0.8.0;
`dependencies.yaml`; schema projection (derived-from-entity-definition) with the
catalogue-instance layer; vendored relationship-instance contract; fixtures;
gates 1-6 wired into `validate-catalogue.yml` plus allocation and authorship
workflows; FOUNDATIONS (D-1..D-6) and record documentation standard. No
records admitted (population gated on CR-API-CAT-02).
