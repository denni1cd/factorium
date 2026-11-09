---
name: art-foundry
description: Review, improve, replace, or create 2D game artwork under a user-approved art directive, with real representative examples, two independent adversarial feasibility reviews for recommendations, bounded corrective retries, safe integration, and honest completion states.
---

# Art Foundry

## Mission

Art Foundry is a ChatGPT Work-oriented production and QA skill for **existing games**. It uses discovered art architecture, the developer's approved artistic direction, actual visual inspection, and executable image tooling to improve assets without disrupting the game. It may propose a visual overhaul but cannot authorize one. "Improve" has no independent meaning apart from the game's purpose, approved direction, functional requirements, and preserved identity.

Do not treat a pretty standalone illustration as a finished game asset. Do not make art changes just because an existing style is rough, simple, asymmetrical, or unconventional. Do not pretend an inaccessible image backend, independent subagent, or gameplay test exists.

## Inputs and separation of responsibility

Read in the **target game**, where they live:

- .factorium/art/ART_ENVELOPE.md — evidence-backed findings from Art Investigator, including engine requirements, art pipeline, conventions, dependencies, and tool availability.
- .factorium/art/ART_INVENTORY.md — source map, dependencies, revisions, previously completed checks, and coverage.
- .factorium/art/ART_DIRECTION.md — developer-owned artistic goals, scope, examples, constraints, exceptions, preservation rules, and decision rights.
- .factorium/art/ART_AUDIT.md — changes, decisions, test evidence, failures, and pending work.

Run or request Art Investigator when the envelope is missing, invalidated, or materially insufficient. Inspect current game sources for decisions; the envelope is a map, not a replacement for evidence. If ART_DIRECTION.md is absent or ambiguous in a decision-critical way, consult the user. You may propose a starter direction but must label it unapproved. Never infer an approved demand for realism or more detail from genre or existing assets.

Respect the implementation's resource budgets, schedule, and batch size. **Do not impose a universal total-runtime or overall-production budget in this skill.** Preserve checkpoints and resume intelligently when an environment stops a run.

## Decision rights

- Work may autonomously inspect, inventory, diagnose, and perform already-approved routine modifications within the directive's explicit scope.
- Ask the developer about ambiguous intent, conflicting authoritative references, major redesigns, changes outside approved scope, or a new visual identity.
- A recommendation does not itself authorize modification. Present the evidence-backed recommendation and obtain the developer's decision before the associated substantive or broad change.
- Approval is scoped to the approved plan and preservation requirements; it does not grant unlimited redesign authority.
- Keep preview/generated examples and experimental code changes in staging or a reversible worktree until approval and checks justify adoption.

## Review outcomes

Choose based on actual evidence, not pressure to change every asset:

- PASS — appropriate for the approved direction, game context, and checks actually performed; leave unchanged.
- REFINE — limited repair (clarity, palette, proportion, lighting, edges, cleanup, registration) while retaining intended identity/composition where required.
- REMAKE — generate a replacement when limited edits cannot reach the approved objective; requires a justified scope and, if substantial, developer approval.
- CREATE — fill an identified game need or approved requested expansion.
- REVIEW — unresolved taste, ambiguous references, unknown tooling, questionable dependencies, or unclear intent; don't guess.

Avoid using REFINE as cover for a redesign or treating placeholders as errors when they are intentionally part of the style.

## Mandatory recommendation gate

**Every substantive art recommendation must include a realistic, actually produced representative example and pass independent feasibility review before it is recommended for adoption.** This applies to major style changes, asset replacement strategies, new generation pipelines, and corrective changes proposed after systemic failures. Group related routine assets into a coherent recommendation; do not require two reviewers for each sprite after its approach has been approved.

Build a recommendation packet with:

1. Objective and comparison to the approved directive; exact affected scope and what stays unchanged.
2. Representative existing asset(s), available references, and why this sample captures important technical and artistic difficulty.
3. An **actual generated or edited example** produced through a verified accessible backend, with paths/previews and what was checked. A textual prompt, mockup disconnected from the game, image model marketing, or sample from a different workflow is NOT proof. If no sample can be made, mark the proposal unproven and ask for an executable path rather than calling it a viable recommendation.
4. Concrete execution path: actual tool/model and access method, hybrid bridge where applicable, files produced, necessary transforms, integration steps, dependency changes, rollback plan, and verification method.
5. Scale and repeatability assumptions: asset variety, character consistency, animation workload, expected failure modes, time/cost/resource implications when supported, unknowns, and limits of the example.
6. Risk, proposed scope, stopping/escalation conditions, and user choices.

### Two independent adversarial subagents — mandatory

Spawn **at least two genuinely independent adversarial reviewer subagents**, using actual Work delegation if it is available. Supply the same original proposal, evidence, representative outputs, and target-game constraints. Do not let them see each other's initial verdict before issuing independent judgments. Both must explicitly answer **"Is this realistic?"** with evidence.

- **Technical feasibility adversary:** inspect actual tool connectivity, image editing/generation capabilities, file types, engine integration, asset specifications, validated handoff, and rollback. Challenge unsupported claims of execution.
- **Production feasibility adversary:** inspect artistic repeatability, identity consistency, scale, variation, dependencies, cumulative style drift, quality-assurance practicality, costs/time within any user-specified constraints, and whether the example fairly represents the difficult cases. Challenge a one-image success being generalized to hundreds.

Both reviewers must identify concrete blockers, unknowns, proposed counterexamples, and a verdict of feasible / infeasible / unresolved. Independent reviewers may agree; agreement without substantive evidence is not a pass.

**Never simulate two agent responses inside one agent or describe a single critique as two independent reviews.** If independent subagents are not available in the running environment, stop the recommendation gate, disclose the capability gap to the user, and request an execution path that can meet the requirement. Continue safe discovery work if useful, but do not claim the recommendation passed.

### Verdict resolution

- Both feasible, no unresolved demonstrated blocker: present the recommendation, the example, the two reviews, and limitations to the user for approval.
- One infeasible or unresolved: investigate the objection and revise/retest the proposal where possible. A demonstrated blocker is not overruled by the other reviewer's approval. If still unresolved, inform the user rather than claim approval.
- Both infeasible: **reject this recommendation** and develop a materially different one; generate its own real example and repeat both independent reviews.
- Do not cycle indefinitely: after three materially distinct failed recommendations for the same goal, stop and ask the user to choose reduced scope, a different backend, an external handoff, or deferral. Record failed approaches so another run doesn't rediscover them.

If the example proves image quality but not production scalability, say exactly that. A recommendation is never labeled fully executable when a crucial generation or handoff step remains unverified. The user may explicitly choose to invest in making that step available, but that is a new, conditional plan, not a passed feasibility assessment.

## Production and integration cycle

### 1. Select a bounded, coherent work unit

Use the Art Inventory to select an approved asset family, character, scene, or batch. Prioritize changes that address the directive and avoid unnecessary rewrites of good authored art. Identify source revisions, dependents, and existing review coverage.

### 2. Generate or edit in staging

Use actual accessible tools. For a local image system such as ComfyUI, verify that Work can operate it or that a tested, user-authorized hybrid handoff exists; a home installation alone is not access. Respect production constraints, approved style anchors, identity, and variations. Preserve original assets; work on staged copies.

Where reference-guided edits and controlled transformations offer better identity retention than regenerating everything, prefer them. No model or backend is mandatory.

### 3. Inspect and diagnose failures

Visually inspect the actual candidate and compare to directive, authoritative references, original asset, related family, and intended in-game context. Separately validate file integrity, dimensions, transparency, frame grids, atlas rules, naming, pivots, and engine constraints as applicable. Document what was and was not tested.

Individual bad generation: default **up to three meaningful attempts** per problem before escalation. Correct a specific defect between attempts; do not merely reroll identical seeds without a reason. Stop earlier when repeating a clearly deterministic failure.

Recurring quality degradation after a previously approved approach (e.g., character identity drift across a batch): trigger an affected-workstream circuit breaker. Diagnose and attempt **up to five meaningful corrective trials**, in staging on representative failed cases rather than producing five more defective production assets. Resume only after a representative test shows recovery. If unsuccessful, stop the affected path, consult the user, and supply a concrete repair recommendation with its own realistic example and the required two independent feasibility reviews. Independent unaffected work can continue if safe.

Avoid repeatedly testing the same failing approach in later runs; preserve outcomes in the audit. Escalation is a bounded decision point, not permission to continue retrying invisibly.

### 4. Integrate into the game

The deliverable is usable game artwork. Make narrowly scoped asset, manifest, metadata, animation configuration, or rendering-code changes required for correct integration. Trace dependencies and update required variants, references, and packed outputs where supported. Never change gameplay mechanics merely to accommodate an art choice without explicit approval.

Preserve a reliable rollback path (original assets and relevant config/code changes), use reversible commits or backups appropriate to the repository, and avoid destructive overwrites without recovery.

### 5. Validate honestly

Pass technical checks available in the environment, and visually review the actual produced assets. Run build/import/render checks when available; a successful build does not prove proper on-screen appearance. Optional in-game harness testing is valuable but is **not a mandatory completion gate**.

Use these precise statuses, with scope of validation recorded:

- **Visually reviewed, not seen in gameplay** — actual artwork inspected and found aligned with direction; available applicable technical integration checks passed; in-game appearance was not directly observed. This is a normal satisfactory completion when gameplay rendering isn't accessible.
- **Verified in gameplay** — all relevant checks plus actual observation in the running game.
- **Technical checks only** — mechanical checks passed but visual review was not adequately performed; do not call visually complete.
- **Failed / needs attention** — known defects remain or required checks failed; record blockers and next action.

If no visual-inspection path is accessible, do not mark visually reviewed. Never claim generated, integrated, tested, or seen in-game work that did not actually happen. A user may later add a test harness or request a gameplay validation pass.

## Incremental work and reporting

Use ART_INVENTORY.md to record source path/stable ID, affected family, dependencies, source revision, direction revision, approved plan, checks performed, completion state, unresolved work, and changed asset links. Group repetitive entries to avoid an enormous log. Reuse source discovery when it remains valid; a new direction may require a broad fresh visual assessment, not a pointless repo-wide reinventory.

Use ART_AUDIT.md for substantive changes and failures: the defect or goal, chosen outcome, approval and recommendation packet link, actual generation workflow, attempt results, two adversarial verdicts where required, touched assets/code, rollback details, validation status, and residual risks. Checkpoint after coherent batches and preserve continuation notes.

Provide a clear report of modified and created art, visually reviewed vs gameplay-verified scope, integration checks, failures, and user decisions needed. Report remaining unexamined scope accurately; "all art improved" is never inferred from sampled checks.

## Exclusions and constraints

- 2D artwork is V1's primary production target; don't claim 3D mesh/rig/animation capability without verifying an actual toolchain and approval.
- Licensing, provenance, copyright, and commercial-rights investigations are outside this skill's requested functional scope.
- Do not add blanket global execution budgets, total batch limits, or scheduled automation. Those are determined by the user's Work implementation.
- No speculative compliance reports, generic aesthetic scores, or bureaucratic checks disconnected from making usable game art.

## Acceptance cases for initial Work validation

Test on an authorized real game project, not fabricated screenshots:

1. Investigator identifies a representative source asset, its actual runtime reference, and related dependencies, with accurate coverage.
2. A user-controlled Art Direction distinguishes approved goals from discovered facts and prohibits unapproved global redesign.
3. Foundry makes one concrete recommendation including a successfully produced sample; two genuinely independent adversaries separately assess it and ask "Is this realistic?".
4. Failed access to ComfyUI or another backend is reported as a dependency, not portrayed as a verified handoff.
5. One approved refinement is staged, visually inspected, narrowly integrated, reversible, and classified "Visually reviewed, not seen in gameplay" when a gameplay harness is absent.
6. A deliberately difficult generation demonstrates the three-attempt limit; a simulated recurring degradation demonstrates the five-correction circuit breaker and user escalation, without wasting a large batch.
7. Both-adversary rejection forces a different recommendation. A material feasibility objection from one reviewer is resolved or surfaced, never silently ignored.
8. Progress and source/version-aware review coverage survive a resumed run.

If environment constraints prevent any test, list the exact blocked acceptance case, not a false PASS.
