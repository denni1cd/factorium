# Work acceptance-test handoff: Art Factory V1

Use this when testing the Art Investigator and Art Factory skills in the ChatGPT Work execution environment.

## Starting point

Repository: denni1cd/factorium

Read:
- skills/art-investigator/SKILL.md
- skills/art-factory/SKILL.md
- skills/art-factory/ART_DIRECTION_TEMPLATE.md

These are skill instructions, not evidence that Work can actually generate images, spawn two independent subagents, reach local ComfyUI, or edit a target game's files. Verify all claimed capabilities in this **actual** session.

Choose a target game that the user has authorized for this test, and confirm the authorized art scope. Keep Factorium's reusable skill definitions in Factorium; write project-specific .factorium/art/ working files into the target game only.

## Suggested Work task

> Implement a real V1 acceptance test of Factorium's Art Investigator and Art Factory skills on the authorized target game. Use its actual artwork, code references, and engine constraints. First produce the Art Envelope and Inventory; consult the developer for any needed Art Direction. Develop one feasible, narrowly scoped art improvement recommendation with a real representative example generated or edited using tools actually available to this Work session. Spawn at least two genuine independent adversarial reviewer subagents: one challenges technical execution/integration, the other challenges artistic repeatability at production scale. Each must explicitly answer "Is this realistic?" based on evidence and independently report objections. If Work cannot spawn independent subagents, cannot render a sample, or cannot reach a proposed backend, report that blocker rather than simulating a pass. Seek approval for the substantive change, then implement a limited and reversible asset update, inspect the actual result, complete available integration checks, and report the correct visual/gameplay completion status. Record revisions, dependencies, attempts, failures, and audited changes. Do not rewrite the entire game's art for this initial test.

## Acceptance checks

1. Investigator maps a real asset and code/runtime entry point, relevant dependencies, and uncertainties.
2. ART_DIRECTION.md reflects actual user-approved creative goals; unspecified decisions aren't invented.
3. The recommendation includes a genuinely produced representative example and verified execution path.
4. Two independent adversaries produce separate evidence-based assessments, explicitly asking "Is this realistic?".
5. The review gate enforces both-reject => new recommendation; one demonstrated blocker => investigate or escalate.
6. Modifications stay inside approved scope, stage/recover originals, and make necessary narrow game integration changes.
7. Technical checks and actual image review are distinguished from seeing the asset during gameplay.
8. Per-asset failure budget of three and recurring-degradation corrective budget of five are demonstrable without wasting a whole batch.
9. The inventory/audit enable a resumed incremental run without redoing unaffected discovery.
10. No licensing/provenance audit or universal production-runtime budget has been added.

## Failure reporting format

For each acceptance check, report PASS / FAIL / BLOCKED, the evidence path or specific tool observation, what was genuinely exercised, and the minimal fix needed. Do not call an instruction in SKILL.md a tested runtime capability.

## Delivery

Keep reusable changes in a reviewable branch/PR against Factorium. Make target-game asset changes only in that game's authorized workspace. Return a brief summary: generated sample location, adversarial verdicts, integrated changes, validation status, failures, and recommended changes to the reusable skill definitions.
