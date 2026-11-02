# m.A.R.S. Core Workspace Specification v0.3.0

**Mode:** paper-first, operator-directed, tool-less. The source archive has a fuller provenance trail.

## Identity and intent

Identity identifies a referent. Intent describes its recorded work structure, defined by exactly **Goal**, **Current Task**, **Task Queue**, and **Finished Task Queue**. The referents are **User**, **Agent**, **Workspace**, **Prompt**, and **History**; a referent is not necessarily an autonomous actor.

The Goal field records a desired outcome; it is not a procedure for developing or evaluating goals. Historical intent is not automatically current authority, and completed work does not prove goal achievement.

## State: eight vectors

| ID | Vector | Question |
|---|---|---|
| S1 | History | Where have I been? |
| S2 | Trajectory | Where am I going? |
| S3 | Present | Where am I now? |
| S4 | Origin | Where did we start? |
| S5 | Destination | Where do we want to go? |
| S6 | Accomplishments | What have I done? |
| S7 | Intentions | What do I want to do? |
| S8 | Obligations | What do I have to do? |

History != origin; trajectory != destination; intentions != obligations.

## Orchestration: twelve vectors

| Category | Started with | Obtained | Needed | Acquiring |
|---|---|---|---|---|
| Sources | O1 | O2 | O3 | O4 |
| Resources | O5 | O6 | O7 | O8 |
| Tools | O9 | O10 | O11 | O12 |

Sources preserve information and provenance; resources provide assets or capacity; tools are potential means of action. An inventory entry does not authorize implementation.

## Governance

- Preserve the difference between stated, inferred, recorded, verified, proposed, authorized, implemented, and tested.
- Retain corrections and provenance. Avoid overwriting historical claims without attribution.
- Use explicit named sentinels for unknown or unresolved values; never use a missing-value placeholder.
- The operator directs objectives and authorizes implementations. Agents retain judgment about authorized manner and means and the right to decline impermissible action.
- A source, resource, or tool can be listed without being acquired or verified usable.
- No agent runtime, automation, scheduler, external resource rebinding, or workspace tool is implemented.

## Composition

**Core-only:** this document and its machine-readable model have no embedded Goal Development procedure. The standalone Goal Development extraction is deliberately separate and is not imported by the core seed.

The canonical status of the proposed sentinel names and host resource bindings remain unresolved.
