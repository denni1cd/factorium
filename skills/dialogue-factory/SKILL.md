---
name: dialogue-factory
description: Audit and conservatively repair dialogue in a target game using its game-specific Dialogue Envelope. Evaluate character, scene, knowledge, voice, and materially different reachable contexts; distinguish routing, variant, and rewrite defects.
---

# Dialogue Factory

## Purpose and prerequisite

Dialogue Factory is the high-volume dialogue QA and repair stage of Factorium. Its primary input is the target game's:

```text
.factorium/dialogue/DIALOGUE_ENVELOPE.md
```

Use the envelope together with the actual game repository. The envelope explains what to look for; the repository provides evidence about the specific line, its speaker, scene, implementation, and reachable states.

Do not begin a broad pass without a usable, current envelope. If it is missing, stale, or contradicted by the project, stop the broad pass and run or request Dialogue Investigator. Do not fill gaps with generic assumptions.

## Governing question

For every item under review, ask:

> Given who this character is, how they normally speak, what they know or believe, what is happening in the scene, and every materially different legal context that can reach this dialogue, does this line make sense for this character here?

This is a character-and-context QA pass, not generic copyediting. Existing dialogue is evidence of authored voice. Awkwardness, vulgarity, terseness, verbosity, confusion, repetition, pomposity, formality, limited abstraction, or emotional instability may be intentional. Do not polish these traits away. A stylistically different alternative is not proof of a defect.

## Work a batch

Choose a coherent unit such as a character, scene, quest, chapter, dialogue file, or generator. Keep its bounds clear so coverage is visible. For each item:

1. **Locate the source and purpose.** Identify its speaker, listener, scene, narrative job, and nearby canonical dialogue. If generated at runtime, locate the generator and the inputs that produce it.
2. **Check the envelope's relevant rules.** Use the game-specific voice evidence, knowledge and memory model, state, trigger rules, and tone. Inspect the actual implementation or authored data for the predicates and evidence that decide reachability; do not rely on a summary when the source can settle the question.
3. **Identify what the line presupposes.** Note the facts, memories, observations, inferences, expertise, relationship, emotion, and prior exchange a character would need for this exact utterance. Include implications and certainty, not only explicit claims.
4. **Probe for counterexamples.** Find materially different legal contexts admitted by the route that could change the judgment. In particular, check the context boundaries the envelope identifies: for example, remembered versus unavailable memories, witness versus hearsay, low versus high expertise, or different relationship or quest states. Establish whether each context is genuinely reachable; do not enumerate every theoretical combination.
5. **Choose an outcome only when evidence supports it.** Leave a plausible line untouched. If defective, identify whether the defect is routing, a need for distinct realizations, or the wording/content itself. If the evidence is missing, contradictory, or too difficult to resolve reliably at the current model's capability, flag the case for review or escalation rather than guessing.
6. **Make the smallest effective repair and re-evaluate it.** Recheck new or changed text against the same intended contexts and counterexample that exposed the defect. Generation is not self-validating.

Look for evidence in the places relevant to the item: surrounding dialogue, character files, scene and quest scripts, dialogue data, conditionals, event/state logic, knowledge or memory systems, and generator prompts or supplied context. Avoid loading unrelated systems simply because they exist.

## Reachable context and judgment

Do not ask only whether an imagined context makes a line work. Try to disprove the line's fit by finding a legitimate context the game allows to reach it where it stops making sense. Reason from actual conditions and the Dialogue Envelope; do not assume world truth or player knowledge is available to the speaker.

Judge only dimensions the game establishes as relevant. These can include:

- what the speaker witnessed, learned, remembers, believes, misunderstands, or has forgotten;
- whether the speaker can form the line's inference or level of abstraction from available observations;
- intelligence, education, profession, expertise, or other modeled traits as the game defines them;
- canonical vocabulary, register, cadence, rhetoric, repetition, humor, or other voice patterns;
- emotion, physical state, relationship, social role, prior choices, or recent interaction;
- whether the line responds to the immediate exchange or instead sounds like player-facing exposition, a system summary, or clinical AI prose;
- whether a generic line erases a meaningful distinction between states.

Do not translate modeled intelligence into a crude word-length rule. It may affect inference depth, causal synthesis, abstraction, recognition of contradiction, or another behavior established by this game. Use canonical speech and implementation as evidence. Label uncertain inference as uncertain.

Profanity, violence, threats, cruelty, sexual language, dark humor, offensive characters, and disturbing themes are not defects merely because they are mature or unpleasant. Judge whether they fit the speaker, scene, game envelope, and intended content level. Do not sanitize the game.

## Outcomes

Apply the outcome to the defect, not as a forced label for every reviewed line. If a line has independent defects, record them separately.

### PASS

The line plausibly works across the materially different reachable contexts examined, and matches its intended scene and speaker. PASS is a supported judgment, not simply the absence of an obvious problem during a skim. Leave the line unchanged. Routine PASS items need little or no individual reporting.

### ROUTE

The line is good for its intended context, but the current conditions also allow it to appear in a context where it does not belong. Narrow or correct the trigger, condition, state supplied, or other routing. Preserve the line where it works.

### VARIANT

Multiple contexts are intentionally meant to reach the same dialogue beat, but they need different realizations to preserve character plausibility. Keep the existing line in the context where it works and add only the needed variant or variants, with conditions that select them correctly. Do not create variants for merely stylistic alternatives.

### REWRITE

The line itself is defective for its intended context, even with correct routing. Replace it while preserving its semantic purpose: relevant facts, scene function, and what the character is trying to do. Express that purpose in this character's voice; do not impose generic polished prose.

### Review / escalation

Do not force PASS, ROUTE, VARIANT, or REWRITE when key evidence is unresolved, project sources conflict, reachability is unclear, or the case requires reasoning the current model cannot do reliably. Record the exact uncertainty and the evidence needed. Escalate difficult or ambiguous cases to a stronger model or a human reviewer when available; keep the clear routine items moving.

## A compact distinction

Suppose the envelope says a character remembers only events they personally witnessed, and the quest's shared dialogue beat is intended to work whether or not they witnessed the gate attack.

- **Bad line — REWRITE:** “I saw the captain order the attack,” although the character has no observation or evidence of that order in any intended context. The assertion is unsupported even on the route where the line was meant to play. Rewrite it to serve the beat using only what the character could know.
- **Good line, bad routing — ROUTE:** “I saw the gate fall” is established, appropriate witness dialogue, but its current trigger also admits characters who were elsewhere. Restrict this line to witnesses; do not rewrite good witness dialogue to accommodate the faulty condition.
- **Legitimate variant — VARIANT:** Both witness and absent-character contexts should reach the beat. Preserve “I saw the gate fall” for witnesses and add a response such as “I found the gate already down; I don't know how it fell” for an absent character who observed the aftermath. Do not route the absent character out if the scene is meant to include them.

The same suspicious wording can therefore call for different repairs depending on intended reachability and scene purpose. Verify those from the game.

## Repair rules

- Preserve good authored dialogue, including unusual or rough voices.
- Prefer the smallest change that actually fixes the defect.
- For ROUTE, fix the condition rather than changing good prose.
- For VARIANT, split only the line or branch that needs a different realization; do not duplicate a conversation unnecessarily.
- For REWRITE, understand the semantic job first, then preserve relevant facts, intent, and character identity.
- Use the same character's canonical dialogue as behavioral evidence when available; do not mechanically imitate a sample.
- Do not invent character facts, memories, motivations, or game rules to justify a preferred rewrite.
- After editing, evaluate the new line or routing against the same counterexample. Reject a repair that creates a new implausibility.

## Procedural dialogue and repeated failures

For generated or templated dialogue, inspect the source instructions, context supplied to the generator, state/knowledge inputs, selection rules, and output routing. Consider whether the individual output is the right repair target.

As the batch proceeds, keep a compact working note of recurring causes and affected locations. If several failures share a source—missing character context, incorrect knowledge, broad conditions, reused output across incompatible states, or flattened voice instructions—address that source before patching every instance. Then review or regenerate affected outputs and sample them in their actual contexts. Do not claim a systemic fix without checking its downstream results.

## Scale and escalation

Use a fast capable model for routine items when available, relying on the envelope's evidence map and focused source reads. Reserve deeper reasoning for items with ambiguous knowledge or memory, subtle cognitive demands, conflicting routes, major narrative consequences, or uncertain repair choices. Escalate those cases individually where possible; do not let a few hard items turn a large batch into guesses or stall clear work.

Keep review overhead proportional to risk: inspect enough context to support each PASS, but do not write an essay for it. Spend analysis and output on actual defects, uncertain cases, and repeated patterns. Keep a compact batch progress note during long runs so reviewed regions, open cases, and systemic findings are not lost.

## Audit trail

The changed game content is the primary output. For meaningful modifications, maintain a concise audit note in the project's existing work log or, if none is in use, `.factorium/dialogue/FACTORY_AUDIT.md`. Record only what is needed to understand:

- location or stable dialogue/node identifier;
- outcome: ROUTE, VARIANT, or REWRITE;
- the counterexample or defect that warranted the change;
- what was changed.

Do not list every PASS unless requested. For a generator or routing fix affecting many lines, record the shared cause and affected scope rather than repeating the same explanation per line.

## Completion standard

A successful Factory pass leaves working dialogue alone, repairs only evidenced defects, catches materially different legal contexts through counterexample-driven review, and preserves the game's own character voices and content. Every accepted repair has been checked again; unresolved cases are clearly surfaced; repeated failures are addressed at their source where practical.
