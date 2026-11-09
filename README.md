# Factorium

Factorium is a game-modification suite built around reusable AI skills. Its purpose is to let an agent inspect a real game project, learn how that specific project works, and then perform focused modification or quality passes without forcing the game into a rigid universal template.

Factorium currently defines two reusable modules: **Dialogue Factory** and **Art Foundry**.

## V0.1: Dialogue Factory

Dialogue Factory is split into two skills:

1. **Dialogue Investigator** — studies the target game before any broad dialogue pass. It discovers the game's dialogue systems, character model, triggers, state, knowledge/memory rules, tone, canonical speech patterns, procedural generation, and other conditions that materially affect what a character could plausibly say. It writes a game-specific dialogue envelope and reusable source inventory for the factory to use.
2. **Dialogue Factory** — walks the game's dialogue using that discovered envelope. It checks each line in the context of the character, scene, trigger conditions, reachable states, established voice, and the user's current creative direction, then leaves good dialogue alone and repairs only what needs repair. It records coverage so future passes can resume intelligently.

The intended workflow is:

```text
Target game repository
        |
        v
Dialogue Investigator
        |
        v
.factorium/dialogue/DIALOGUE_ENVELOPE.md
.factorium/dialogue/DIALOGUE_INVENTORY.md
        |
        v
Dialogue Factory + DIALOGUE_DIRECTION.md
        |
        +-- PASS
        +-- ROUTE
        +-- VARIANT
        +-- REWRITE
```

## Design principles

- **Discover before modifying.** Factorium should learn the target game's actual rules rather than begin with a generic checklist and assume it is complete.
- **Use the game as evidence.** Character cards, implementation, existing dialogue, event logic, and procedural systems are stronger evidence than assumptions about how a game "should" work.
- **Preserve authored work.** Good existing dialogue should remain untouched. A routing problem should not become a rewrite problem.
- **Judge the reachable context.** The important question is not merely whether a line is well written, but whether the speaker would plausibly say it in every materially different context that can legitimately reach it.
- **Separate world truth from character knowledge.** A character should not know something merely because the game or player knows it.
- **Treat modeled attributes as real constraints.** If a game models intelligence, education, memory, intoxication, relationships, personality, injuries, or similar state, the investigator determines how those systems matter for dialogue in that game.
- **Do not moralize mature material.** Profanity, violence, cruelty, threats, sexual language, or other mature content should be judged for character, scene, tone, rating target, and narrative consistency—not penalized simply for being mature.
- **Reuse discovery; vary direction.** Keep source facts and dialogue locations in the Envelope and Inventory, separate from the user's changeable creative direction. Review only affected areas when evidence supports doing so; do not claim a direction change is free of re-reading.
- **Checkpoint long runs.** Record batch coverage and dependencies as work proceeds so later runs can resume without repeating all discovery.
- **Prefer semantic counterexamples over exhaustive permutations.** The goal is to find materially different legal contexts that expose dialogue problems, not enumerate millions of mechanically possible states.

## Repository structure

```text
factorium/
├── README.md
├── docs/
│   └── WORK_ART_FOUNDRY_HANDOFF.md
└── skills/
    ├── dialogue-investigator/
    │   └── SKILL.md
    ├── dialogue-factory/
    │   └── SKILL.md
    ├── art-investigator/
    │   └── SKILL.md
    └── art-foundry/
        ├── SKILL.md
        └── ART_DIRECTION_TEMPLATE.md
```

The target game, not the Factorium skills repository, holds optional working artifacts under `.factorium/dialogue/`: `DIALOGUE_ENVELOPE.md` (discovered logic), `DIALOGUE_INVENTORY.md` (source map and coverage), `DIALOGUE_DIRECTION.md` (user-controlled artistic goals), and `FACTORY_AUDIT.md` (changes and unresolved cases). Build these progressively; a full per-line index is not a prerequisite.

V0.1 established the dialogue workflow. The art module below is a separate skill system and should be tested in the actual Work execution environment before claiming full production readiness.

## V0.2: Art Foundry (skill definitions; Work validation pending)

Art Foundry extends Factorium to existing game art. It uses two skills:

1. **Art Investigator** — discover active artwork, visual conventions, authoritative references, engine/import requirements, asset dependencies, and actually available generation tools; write a compact Art Envelope and source Inventory.
2. **Art Foundry** — audit assets against a developer-approved art direction, refine/remake/create artwork through real image tooling, preserve originals, integrate only necessary asset/config/code changes, and verify visual and technical results.

The target game's working files are:

- .factorium/art/ART_ENVELOPE.md — discovered evidence, constraints, and unknowns.
- .factorium/art/ART_INVENTORY.md — source map, dependencies, revisions, and review coverage.
- .factorium/art/ART_DIRECTION.md — the **developer's** approved artistic objectives, references, scope, preservation rules, and decisions.
- .factorium/art/ART_AUDIT.md — actual changes, generation attempts, adversarial reviews, validations, and unresolved issues.

A starter for the direction is at skills/art-foundry/ART_DIRECTION_TEMPLATE.md. The user controls creative direction; the system can recommend an overhaul but cannot authorize one.

### Art Foundry safeguards

- Every substantive art recommendation requires a **real, representative generated/edited example**, a verified execution path, and at least **two genuinely independent adversarial Work subagents**. The technical and production reviewers both ask "Is this realistic?". Both rejecting feasibility forces a different recommendation; a demonstrated blocker from either reviewer must be resolved or surfaced. Do not pretend to have independent reviews if the runtime cannot provide them.
- Run changes only within approved artistic scope. Use a default maximum of **three meaningful attempts** for an individual generation problem and **five corrective staging attempts** for recurring quality degradation before escalating with alternatives.
- Actual image inspection and relevant technical integration checks are required for **"Visually reviewed, not seen in gameplay"**. Gameplay observation is optional and must be claimed only when performed.
- Work must verify access to any backend (including local ComfyUI/hybrid bridges). A prompt or marketing demonstration does not prove execution.
- The implementation determines overall production budgets and batch size. V1 does not perform art licensing/provenance audits or claim unverified 3D production support.

See docs/WORK_ART_FOUNDRY_HANDOFF.md for Work-native acceptance tests. **These repository changes define the workflow; they do not mean the Work environment, subagents, generation backend, or in-game integration have already been tested.**
