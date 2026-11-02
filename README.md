# Factorium

Factorium is a game-modification suite built around reusable AI skills. Its purpose is to let an agent inspect a real game project, learn how that specific project works, and then perform focused modification or quality passes without forcing the game into a rigid universal template.

The first Factorium module is **Dialogue Factory**.

## V0.1: Dialogue Factory

Dialogue Factory is split into two skills:

1. **Dialogue Investigator** — studies the target game before any broad dialogue pass. It discovers the game's dialogue systems, character model, triggers, state, knowledge/memory rules, tone, canonical speech patterns, procedural generation, and other conditions that materially affect what a character could plausibly say. It writes a game-specific dialogue envelope for the factory to use.
2. **Dialogue Factory** — walks the game's dialogue using that discovered envelope. It checks each line in the context of the character, scene, trigger conditions, reachable states, and established voice, then leaves good dialogue alone and repairs only what needs repair.

The intended workflow is:

```text
Target game repository
        |
        v
Dialogue Investigator
        |
        v
.factorium/dialogue/DIALOGUE_ENVELOPE.md
        |
        v
Dialogue Factory
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
- **Prefer semantic counterexamples over exhaustive permutations.** The goal is to find materially different legal contexts that expose dialogue problems, not enumerate millions of mechanically possible states.

## Repository structure

```text
factorium/
├── README.md
└── skills/
    ├── dialogue-investigator/
    │   └── SKILL.md
    └── dialogue-factory/
        └── SKILL.md
```

Future Factorium modules may add other Investigator and Factory skills, but V0.1 intentionally stays focused on dialogue until the workflow has been tested against real games.
