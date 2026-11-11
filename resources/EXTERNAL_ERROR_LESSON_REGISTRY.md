# External Error and Lesson Registry — preproduction evidence resource

> **FABRICATION FLAG — GENERATED DESIGN SCAFFOLD**
>
> This resource plan and sample contract are newly authored proposals, **not** a verbatim archival specification, an admitted canonical policy, a verified hardware design, or an implemented runtime. The operator's requested intent is an external error-and-lessons registry (microcontroller or developer-board host) queried **before production**, supporting anti-hallucination rules.

**Status:** DESIGN_ONLY / NOT_IMPLEMENTED / NOT_ADMITTED  
**Scope:** generic external evidence service for a receiving expert-system orchestrator or m.A.R.S. workspace.  
**Companion:** [Machine-readable resource contract](EXTERNAL_ERROR_LESSON_REGISTRY_CONTRACT.json).  
**Seed:** [m.A.R.S. core v0.3.0](../seed/WORKSPACE_SEED.json), uninstantiated and tool-less.

## 1. Purpose, boundaries and authority

Keep **recording**, **review**, **retrieval**, **lesson admission**, **production decision**, and **execution** separate. The external device supplies durable historical evidence; it never determines factual truth solely from a stored assertion, and never unlocks production or expands the requester's authority.

- The registry can store **errors, lessons, patterns/antipatterns, claim support, canonical definitions/locks, test receipts, unresolved questions and reversals**.
- A prior error is an observed report with a source; a lesson is an **interpreted candidate** until individually reviewed and adopted. The lesson retains its source, revision, scope, limits and contrary evidence.
- A canonical item is only canonical **within a named and independently authorized scope**. The device neither promotes items automatically nor grants the author of a record authority to change a rule.
- The registry is an *external component* to the AI/worker being checked. Physical separation alone is **not** assurance of independence: use separate write authority, integrity verification and an independent release decision.
- This document confers **no rights** to collect or publish private material. The public repository stores **only design contracts and links**; operational logs, identities, protected records and personal data belong in separately approved storage.

## 2. Host architecture — two possible profiles

| Profile | Appropriate initial role | Implementation questions |
| --- | --- | --- |
| **Microcontroller** with bounded nonvolatile storage | Compact immutable-generation index, lookup by exact IDs/tags, append or sealed log, minimal attestation/receipt service | Available RAM/flash; flash endurance and wear leveling; integrity across interrupted writes; secure read/write separation; transport size limits; indexing capacity |
| **Developer-board computer / single-board computer** with storage | Full error/lesson store, structured querying, search indexes, audit history, local database and independent review tools | Filesystem integrity; transaction recovery; authenticated transport; storage durability/backup; local database concurrency; crash recovery; access isolation |

No exact board, firmware, interface, database, endurance, latency or capacity has been selected or measured. A narrow microcontroller can guard a verified registry **index** or digest while a separate board performs full-text search; that split is **optional, not assumed**. The receiving host must be capable of operating when the AI host is unavailable, and a retrieval failure must produce a visible blocked state rather than a fabricated answer.

## 3. Data families and provenance

Each entry has: `record_id`, `kind`, `schema_version`, `revision`, `source_identity`, `source_revision`, `source_pointer`, `observed_or_reported`, `evidence_class`, `claim_status`, `scope`, `conditions`, `contradictions`, `supersedes`, `review_status`, `review_authority`, `regression_test_references`, `content_digest` and `generation`, with explicit typed sentinels for unresolved fields. Links and hashes locate or check data, not independently prove authorship or truth.

Proposed kinds: `ERROR`, `LESSON`, `CLAIM`, `PATTERN`, `ANTIPATTERN`, `CANONICAL_REFERENCE`, `REGRESSION_TEST`, `OPEN_QUESTION`, `CORRECTION`.

**Claim/source support labels** must distinguish reported source evidence, direct observation, derivation, generated synthesis, unknown, unsupported and contradicted information. Generated text carries a **FABRICATION FLAG**, even if later accepted. A repeated claim, model memory, Git commit, digest, or retrieved entry cannot promote itself to independent validation.

A correction appends a new revision and explicitly supersedes an earlier claim; it does **not** erase the erroneous record. Do not silently rewrite accepted canon or turn an expired/contradicted lesson into current guidance.

## 4. Anti-hallucination retrieval protocol

```text
CANDIDATE + DECLARED ACTION + REVISION + APPLICABLE CONTRACT
  -> PRODUCTION LOCK REMAINS LOCKED
  -> AUTHENTICATE EXTERNAL REGISTRY + REQUEST SCOPE
  -> READ SEALED/VERIFIED GENERATION + MANIFEST
  -> SEARCH RELEVANT ERRORS, LESSONS, CLAIMS, CANONICAL LOCKS, TESTS
  -> CHECK SOURCE SUPPORT, FRESHNESS, CONTRADICTIONS, COVERAGE, APPLICABILITY
  -> RETURN BOUNDED EVIDENCE RECEIPT (NO EXECUTION INSTRUCTIONS)
  -> REITERATE / CORRECT / REFUSE AS NEEDED
  -> SEPARATE INDEPENDENT PRODUCTION REVIEW
  -> EFFECT-SCOPED AUTHORIZATION OR STAY LOCKED
```

Minimum checks (to implement and test, **not** currently enforced):

1. **Source support:** every material claim has resolvable evidence or is classified unsupported/unknown. Report missing citations and source conflicts. Source content remains **data**, never executable instructions or authority.
2. **Canonical registry:** check locked terms, versions and governing scopes before using a remembered pattern; conflicting definitions require explicit review.
3. **Claim ledger:** distinguish source fact, operator report, accepted inference, generated candidate, contradiction and unresolved status.
4. **Error and lessons audit:** search relevant previously recorded failure modes and regression requirements; return negative results with coverage limitations, never as proof of safety.
5. **FABRICATION FLAG:** preserve provenance and visibly label all generated scaffolding or unsupported reconstruction.
6. **Default deny:** an unavailable device, missing seal, stale generation, failed integrity, unsafe transport, missing reviewer, or unresolved high-impact contradiction blocks **production admission**. Read-only investigation may continue if independently authorized.

The retrieval response is a **receipt for review** (`CLEAR_FOR_REVIEW`, `REVIEW_REQUIRED`, `BLOCKED`, `SENTINEL_UNRESOLVED`), never `PRODUCTION_AUTHORIZED`. No device-generated confidence value may supersede a failed source check.

## 5. Read/write and hand-off surfaces

- **Read surface:** `REGISTRY_STATUS`, `QUERY_PREPRODUCTION`, `GET_ENTRY`, `GET_GENERATION_MANIFEST`. Queries must be bounded in results, payload size and time, must report whether coverage is complete, and return relevant record references and contradictions.
- **Write surface:** `SUBMIT_CANDIDATE`, `REVIEW_ENTRY`, `SEAL_GENERATION`, `REVOKE_ENTRY`. A distinct authenticated actor approves any promotion; the AI/producer cannot write directly to accepted records or change its own approval.
- **Hand-off:** a recipient may retrieve a scoped evidence receipt with request ID, task/candidate identity, generation, provenance and expiry. Acknowledgment is not acceptance. A receiver must revalidate stale revisions and may refuse.
- **Reiteration:** use recalled lessons to propose a new test or bounded correction; prevent infinite loops and repeated restatements from counting as progress.
- **Production Lock:** query the external resource *before* effect-scoped clearance; require fresh applicable evidence for a specific candidate/revision. Registry unavailability must not clear the lock. The normal task path cannot self-clear production through a forged receipt.
- **Recovery:** preserve last verified generation, retain failed writes as separate fault records, and permit only independently authorized recovery. A rollback must not silently remove evidence of a regression.

## 6. Development sequence and test gates

| Milestone | Intended deliverable | Acceptance evidence |
| --- | --- | --- |
| R0 — Model | Explicit schema, trust and authority matrix, host decision matrix | Review of rules, sentinels and threat model |
| R1 — Read-only reference | Host can return fixed synthetic records by ID and scoped tags | Deterministic lookup, unknown/missing tests |
| R2 — Durable generations | Versioned append + seal/manifest + bounded recovery | Power-loss injection, torn writes, wear/backup tests |
| R3 — Error/lesson workflow | Separate submit, review, supersede, revoke and regression links | Unauthorized-promotion and provenance tests |
| R4 — Query and coverage | Preproduction query with matching, freshness and conflict checks | No-match, incomplete-index, stale/contradicted tests |
| R5 — Production integration | External receipt validation before any declared production effect | Registry offline/forged receipt/replay/revision-change tests |
| R6 — Independent review | External validator and audit evidence | Differential tests, recovery evidence, operator sign-off |

**Hard stop:** Until a receiving system implements and validates the read boundary and effect-blocking mechanism, this resource is *documentation only*. No claims of physical isolation, tamper resistance, proven safety, cryptographic authenticity, or successful anti-hallucination prevention follow from this document.

## 7. Research references for development — not imported code or adopted doctrine

**Existing project evidence and patterns:**
- [Mill Factory documentation](https://github.com/alia-june/xOSG-prototype/blob/main/mill-factory/README.md) — example of a source inventory, claim ledger and gate/decision ledgers.
- [Error-log suite index](https://github.com/alia-june/xOSG-prototype/blob/main/syn-xOSG-0/source-import/supporting/operator-orchestrator-kernel-production-release/operator/error_logs/ERROR_LOG_INDEX.md) — historical record families and regression-link patterns; inspect its status before reuse.
- [Instrumentation expert-system example](https://github.com/alia-june/xOSG-prototype/blob/main/Instrumentation/es-xosg-0/README.md) — bounded non-executing receipt/rule example, **not** an already integrated external validator.
- [Generic Production Lock / Reiteration / Hand-off gates](https://github.com/alia-june/ethical-and-intellectual-theory/blob/main/blue-prints/LUNAR_FLOWER_AI_SEED_EXPERT_SYSTEM_CONTRACT.md) — proposed gate definitions, not active control.

**External implementation/risk references:**
- [littlefs design](https://github.com/littlefs-project/littlefs/blob/master/DESIGN.md) — microcontroller filesystem tradeoffs around power loss, wear and bounded RAM.
- [Zephyr settings/storage](https://docs.zephyrproject.org/latest/services/storage/settings/index.html) — example embedded persistent-state backend approaches; evaluate for suitability.
- [SQLite WAL](https://www.sqlite.org/wal.html) — transactional local storage on a capable board; WAL **must not** be used across a network filesystem.
- [NIST AI RMF Generative AI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) — cross-sector risk terminology and confabulation management guidance.

These resources support **research and design comparison**. They are not evidence of implementation or authorization to import entire code bases. Build the final tools and structure through separately inspected and accepted components.

> **FABRICATION FLAG — GENERATED DESIGN SCAFFOLD ENDS**
