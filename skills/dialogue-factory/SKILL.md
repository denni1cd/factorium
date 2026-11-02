---
name: dialogue-factory
description: Audit and repair dialogue in a target game using the game-specific Dialogue Envelope produced by Dialogue Investigator. Use to evaluate whether each line makes sense for the speaking character across materially different reachable contexts, preserving good authored work and distinguishing routing, variant, and rewrite problems.
---

# Dialogue Factory

## Purpose

Evaluate and improve game dialogue at scale without flattening character voice or rewriting good authored material.

Dialogue Factory consumes the target game's:

```text
.factorium/dialogue/DIALOGUE_ENVELOPE.md
```

produced by Dialogue Investigator.

Do not run a broad factory pass without a usable envelope. If the envelope is missing, obviously stale, or contradicted by the current project, invoke or request Dialogue Investigator first.

## Core question

For each dialogue item, ask:

> Given this speaker, the established character evidence, the immediate scene, and every materially different context that can legitimately reach this dialogue, is this utterance plausible for this character here?

Do not reduce the task to "is this sentence well written?"

## Evidence to gather for each dialogue item

Use the envelope to locate the relevant context. Gather enough evidence to judge the line, including as applicable:

- speaker identity
- character card, stats, traits, background, and relevant modeled attributes
- representative canonical speech from the same character
- immediate preceding/following dialogue or scene context
- narrative purpose or intended meaning of the line
- trigger/routing conditions
- materially different legal contexts that satisfy those triggers
- speaker knowledge, belief, memory, or misconception in those contexts
- relationship to the listener
- relevant emotional or physical state
- game-specific tone/content rules

Avoid loading irrelevant state simply because it exists.

## Materially different contexts

Do not attempt a Cartesian product of every game variable.

Instead, identify semantic differences that could reasonably change whether the line makes sense. Probe boundaries and contrasts such as:

- minimum versus high intelligence when intelligence affects expression or reasoning
- remembered versus uncertain/reconstructed knowledge
- direct witness versus second-hand knowledge
- weak versus strong relationship or hostility
- novice versus expert domain knowledge
- calm versus extreme emotional state
- materially different quest outcomes that share a route

The exact dimensions come from the Dialogue Envelope, not from this list.

The Factory should actively seek counterexamples: try to find a legal context where the candidate line stops making sense.

## What to judge

Judge dialogue against the target game's discovered rules. Relevant questions may include:

- Would this character know or believe what the line asserts?
- Does the reasoning or abstraction fit the character's modeled cognition and established behavior?
- Does the vocabulary, register, cadence, directness, humor, profanity, formality, or rhetorical style fit the speaker?
- Does the line sound like this character rather than generic AI prose?
- Does the emotional state fit the wording?
- Would the character say this to this listener?
- Does the line respond naturally to the scene rather than summarize information for the player?
- Is the speaker compressing facts into a sophisticated conclusion they could not plausibly reach?
- Is world/player knowledge leaking into the character?
- Does the line read like author exposition instead of spontaneous speech?
- If the game intentionally uses stylized dialogue, does the line fit that style?

Do not penalize profanity, violence, threats, cruelty, sexual language, dark humor, or other mature content merely because it is mature. Judge whether it fits the game's envelope, speaker, scene, and intended rating/content level.

## Outcomes

Classify each meaningful problem as one of four outcomes.

### PASS

The dialogue is plausible across the materially different reachable contexts examined.

Action: leave it alone.

### ROUTE

The line itself is good, but one or more current trigger paths can reach it in a context where it does not make sense.

Action: prefer changing/narrowing routing or conditions over rewriting the line.

### VARIANT

The current route legitimately covers multiple distinct contexts that should not share the exact same realization.

Action: preserve the existing line where it works and create the minimum additional dialogue variant(s) needed for the other context(s), with appropriate routing.

### REWRITE

The line itself does not plausibly work for the intended speaker/context, or is stilted, clinically phrased, exposition-heavy, voice-inconsistent, or otherwise defective even under the route where it was meant to work.

Action: replace it while preserving the narrative intent, facts that should be conveyed, scene function, and character voice.

If evidence is insufficient to choose reliably, mark it for review rather than inventing missing game facts.

## Repair rules

When modifying dialogue:

1. Preserve narrative intent before preserving wording.
2. Preserve good authored text whenever possible.
3. Prefer the smallest effective change.
4. Do not rewrite a line merely because an alternate phrasing is also good.
5. Do not homogenize characters toward a single "natural" voice.
6. Use canonical dialogue as behavioral evidence, not as text to imitate mechanically.
7. If a character's state justifies awkward, fragmented, repetitive, vulgar, formal, confused, or unusual speech, preserve that distinction.
8. Fix routing when routing is the defect.
9. Add variants only where materially different contexts require them.
10. Re-evaluate a newly written variant or rewrite against the same context before accepting it.

## Procedural dialogue

For runtime-generated dialogue, inspect the generation prompt/rules and the context supplied to them.

If many failures share the same cause, prefer repairing the generator or its supplied context rather than patching generated examples one at a time.

Examples:

- missing character intelligence/context -> improve generator context
- speaker knows world facts they were never given -> fix knowledge context
- every character uses the same rhetorical style -> strengthen character evidence/prompting
- one broad generated response is reused across incompatible states -> split routing or generation conditions

## Factory pass strategy

For large games, work iteratively rather than producing an enormous undifferentiated report.

A useful pass is:

1. select a coherent dialogue region, character, quest, or batch
2. gather context from the project and envelope
3. evaluate each item
4. leave PASS items untouched
5. repair ROUTE, VARIANT, and REWRITE items
6. re-check changed dialogue
7. continue to the next batch

Use a capable larger model when a case requires substantial contextual reasoning. Routine iteration over well-understood dialogue may use a faster model when available.

## Reporting

Maintain a concise audit trail in the workspace when useful. It should identify changed dialogue and why, but should not bury the project in commentary for PASS items.

For each changed item, record enough to understand:

- location/node
- outcome: ROUTE, VARIANT, or REWRITE
- triggering counterexample or defect
- change made

The finished game content is the primary output; the audit trail is secondary.

## Success standard

A successful Dialogue Factory pass should make the game's dialogue feel as though it came from the characters and situations that actually exist in the game—not from a generic dialogue model—while preserving the author's intended narrative and minimizing unnecessary edits.
