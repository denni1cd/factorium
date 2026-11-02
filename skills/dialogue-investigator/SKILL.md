---
name: dialogue-investigator
description: Inspect a target game project and discover the game-specific conditions that determine whether dialogue is plausible. Use before running Dialogue Factory on a new game or after major dialogue-system changes. Produce a dialogue envelope from the actual project rather than relying on a fixed universal template.
---

# Dialogue Investigator

## Purpose

Understand how dialogue actually works in the target game before Factorium judges or rewrites it.

The Investigator is a discovery skill, not a dialogue editor. Its job is to inspect the project broadly, identify what can materially affect a spoken line, and create a game-specific **Dialogue Envelope** that the Dialogue Factory can trust.

Do not begin with a rigid predefined list and assume it is complete. Use the categories below as prompts for investigation only. Follow the target game's implementation and authored material wherever they lead.

## Primary output

Write or update:

```text
.factorium/dialogue/DIALOGUE_ENVELOPE.md
```

inside the target game workspace unless the user specifies another location.

The envelope should be concise enough for repeated use by the Dialogue Factory but detailed enough to prevent important context from being lost.

## Investigation process

### 1. Locate the dialogue system

Inspect the project to determine where dialogue lives and how it is selected or generated. Find, as applicable:

- authored dialogue files
- scripts and scene files
- dialogue trees or node graphs
- procedural dialogue generators
- event and quest systems that invoke dialogue
- character/NPC definitions
- localization or string tables
- prompt templates used by runtime AI systems
- conditions, predicates, tags, or flags that control dialogue selection

Do not assume one format. A game may spread dialogue behavior across code, data, scripts, prompts, and content files.

### 2. Discover dialogue-affecting state

Identify the state that can materially change what a character should know, believe, feel, intend, or plausibly say.

Examples may include intelligence, education, profession, expertise, personality, faction, relationship, reputation, quest state, prior choices, memory, knowledge flags, injuries, intoxication, fear, grief, status effects, location, time, inventory, secrets, or prior conversations.

These are examples only. Include systems because the target game uses them, not because they appear on this list.

For each important factor, explain how the game represents it and how it can affect dialogue.

### 3. Separate kinds of truth

Explicitly determine how the game distinguishes, or fails to distinguish, among:

- world truth
- player knowledge
- speaker knowledge
- speaker belief or misconception
- memory available to the speaker

A character must not be treated as knowing a fact merely because the game state contains that fact.

### 4. Learn character voice from evidence

Determine what evidence exists for how characters speak. Prefer, in order of usefulness:

1. existing canonical dialogue from the character
2. character cards, biographies, stats, traits, and authored notes
3. established setting and social context
4. inferred patterns, clearly labeled as inference

Record relevant patterns without reducing a character to simplistic rules. Intelligence, for example, may influence abstraction, inference depth, causal synthesis, vocabulary, or rhetorical complexity in a game, but should not automatically be translated into "low intelligence = short words" unless the authored game actually establishes that pattern.

### 5. Understand triggers and reachable contexts

Inspect how a line or dialogue node can be reached. The envelope should teach the Factory how to reason about trigger conditions and identify **materially different reachable contexts** rather than enumerating every possible state combination.

Pay special attention to boundary conditions and broad routes that can admit characters with substantially different knowledge, cognition, relationships, memories, or emotional states.

### 6. Establish tone and content envelope

Determine the game's intended tone, genre, rating/content level, and how mature material is used.

Do not treat profanity, violence, cruelty, threats, sexual language, dark humor, or offensive characters as dialogue defects merely because they are mature or unpleasant. Record how such material functions in this game so the Factory can judge consistency rather than morality.

### 7. Inspect procedural generation

If dialogue is procedurally generated, determine:

- what inputs the generator receives
- what character/state context is available to it
- what context is missing
- where prompts or generation rules live
- whether generated text is later filtered, selected, routed, or rewritten
- whether the same generated line can be reused across materially different contexts

### 8. Challenge the first-pass envelope

Before finalizing the envelope, perform an adversarial second pass over the project with the explicit goal of proving the draft incomplete.

Search for:

- dialogue calls outside the obvious dialogue directories
- indirect or derived state
- special-case NPCs
- alternate quest/event paths
- hidden knowledge or memory systems
- runtime-generated prompts
- unusual routing rules
- state that changes how a character speaks without being labeled as a dialogue variable

If an important area remains unclear, record it under **Unresolved / Needs Review** rather than silently guessing.

## Required Dialogue Envelope sections

Use whatever additional structure best fits the game, but include at least:

```markdown
# Dialogue Envelope — <Game>

## Dialogue Architecture
Where dialogue comes from and how it is selected/generated.

## Character and Voice Evidence
What defines characters and how canonical speech should be inferred.

## Dialogue-Affecting State
Game-specific variables/systems that materially alter plausible dialogue.

## Knowledge, Belief, and Memory
How speaker knowledge differs from world/player knowledge.

## Trigger and Context Rules
How dialogue becomes reachable and what materially different contexts matter.

## Procedural Dialogue
How generated dialogue works, if present.

## Tone and Content Envelope
Genre, maturity, profanity/violence conventions, and other relevant tone rules.

## Game-Specific Review Rules
Important conclusions the Dialogue Factory should apply repeatedly.

## Unresolved / Needs Review
Anything the investigation could not determine reliably.

## Evidence Map
Key files/directories/systems used to derive the envelope.
```

## Completion standard

The Investigator is complete when it can explain, with project evidence, what contextual dimensions the Dialogue Factory must consider and where that evidence comes from.

Do not claim exhaustive certainty when the project is ambiguous. The goal is a strong, game-specific operating model that can be revised as the game changes.
