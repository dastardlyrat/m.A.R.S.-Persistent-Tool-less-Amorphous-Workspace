# m.A.R.S. — Persistent Tool-less Amorphous Workspace

**Core specification:** v0.3.0 (extracted from portable v0.2.0)  
**Status:** conceptual, operator-directed, paper-first, non-executing  
**Repository visibility:** public (GitHub repository metadata, verified 2026-11-11). **Do not publish private operational records, sensitive data, or unreviewed source material here.**

## Purpose

A generic durable workspace specification for tracking identity, intent, state, orchestration, prompt evaluation, and historical provenance across agents and environments. The export is designed to remain intelligible in human-readable text, structured JSON, and declarative logic. It does **not** ship an agent runtime, automation, scheduler, tool executor, or integration code.

The name `m.A.R.S.` is retained as supplied; this repository does not invent an expansion.

## Architecture

### Identity versus intent

Identity identifies the referent; intent records its goal/work structure. The five referents examined are **User, Agent, Workspace, Prompt, and History**. Intent is determined by exactly four elements:

1. **Goal** — desired outcome
2. **Current Task** — active work
3. **Task Queue** — pending work
4. **Finished Task Queue** — completed work and recorded results

Finishing a task does not establish that its goal succeeded. Historical intent is evidence, not automatic current authority.

### State: eight vectors

| ID | Vector | Guiding question |
|---|---|---|
| S1 | History | Where have I been? |
| S2 | Trajectory | Where am I going? |
| S3 | Present | Where am I now? |
| S4 | Origin | Where did we start? |
| S5 | Destination | Where do we want to go? |
| S6 | Accomplishments | What have I done? |
| S7 | Intentions | What do I want to do? |
| S8 | Obligations | What do I have to do? |

Trajectory is not necessarily destination; intention is not obligation.

### Orchestration: twelve vectors

| Category | Started with | Obtained | Needed | Acquiring |
|---|---|---|---|---|
| Sources | O1 | O2 | O3 | O4 |
| Resources | O5 | O6 | O7 | O8 |
| Tools | O9 | O10 | O11 | O12 |

The tools row is an *inventory and design category*, not authorization to construct or invoke tools.

## Extracted component (not in core or seed)

The Goal Development protocol was extracted into an independent, non-executing specification. The core and `seed/WORKSPACE_SEED.json` retain only the four intent fields; they contain no prompt-evaluation procedure. The historical v0.2.0 source is retained separately as provenance.

## Sentinels and evidence

Missing, unknown, unestablished, and inapplicable values require explicit semantically distinguished **named sentinels**, never an untyped placeholder. The proposed names in `specification/SENTINELS.json` are not claimed to be an approved canonical registry. Preserve the distinctions among **proposed, approved, implemented, and verified**.

## Source package and files

The original v0.2.0 archive is a historical predecessor and has **not been committed to this repository**. The revised v0.3.0 core is published as individual files under `specification/` and `seed/`. The predecessor archive has a SHA-256 manifest. The local revised core v0.3.0 export also has its own manifest. Within the source archive, files retain their original relative structure:

- `PORTABLE_EXPORT.json`, `MANIFEST.json`, and `README.txt`
- `specification/HUMAN_SPEC.md`, `WORKSPACE.json`, `LOGIC_REDUX.txt`, `SENTINELS.json`, `PROMPT_HISTORY.md`, and `SOURCE_ORIGINAL.md`
- `records/STATE.json`, `ORCHESTRATION.json`, and `INTENT.json`
- `portability/RESOURCE_ALIASES.json` and `IMPORT_CONTRACT.txt`
- `history/PROVENANCE.md`

All paths in the source archive are archive-relative. The exported resource aliases are deliberately non-reversible; host-specific resources must be explicitly rebound in a receiving environment. A historical snapshot is **not** a claim of live deployment.

### Verification

1. Check the archive ZIP integrity.
2. Compare each content file's SHA-256 to `MANIFEST.json`.
3. Validate JSON syntax and verify required vector counts: State = 8, Orchestration = 12.
4. Inspect the sentinel vocabulary and unresolved values.
5. Read `portability/IMPORT_CONTRACT.txt` before attempting to interpret the snapshot in another environment.

The separate root `README.md` explains this GitHub repository and is **not** part of the original v0.2.0 manifest.

## External error and lesson registry — proposed resource

[External registry development plan](resources/EXTERNAL_ERROR_LESSON_REGISTRY.md) · [Machine-readable resource contract](resources/EXTERNAL_ERROR_LESSON_REGISTRY_CONTRACT.json) · [Resource index](resources/README.md).

A separately hosted microcontroller or developer-board evidence service is proposed to retain **errors, lessons, claim support, canonical conflicts and regression tests**, so a receiving expert-system orchestrator can retrieve and review relevant records **before production admission**. This is an **external resource plan**, not an implemented device, live capability, modified core seed, or production authorization. The core seed's `resource_bindings` remains `SENTINEL_UNRESOLVED`. Failed retrieval is a proposed reason to **keep production locked**, not to synthesize a missing lesson.

## Durable ≠ self-running

*Durable* means the records support retention, copying, integrity checking, and rehydration—not guaranteed physical retention. *Orchestrated* describes the decision framework—not live autonomous operation. *Universal* describes portability of the specification—not universal compatibility certification.

**Safety boundary:** No workspace tools are implemented or authorized by this package. Imports are data-only, with no automatic resource rebinding, authority elevation, or promotion of historical prompts into active instructions.

## Provenance

This export follows the original generic workspace discussion and its corrections. See `history/PROVENANCE.md` and `specification/PROMPT_HISTORY.md` for the summarized chronological history. Preserve prior versions on future revision rather than silently replacing history.
