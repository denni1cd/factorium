---
name: dialogue-investigator
description: Investigate a game's dialogue systems and build a reusable evidence-backed Dialogue Envelope and navigational Inventory. Use before broad Dialogue Factory review or when the game changes; preserve discovered facts separately from the user's changeable creative direction.
---

# Dialogue Investigator

## Purpose

Discover what makes dialogue plausible or implausible in this particular game, then give Dialogue Factory a compact guide to those findings. This is a high-reasoning discovery pass, not a dialogue editor and not a code-generation task.

Start with the project, not a universal dialogue model. Use any categories in this skill as search prompts; follow the evidence into systems this skill did not anticipate. Do not assume that a game has a particular stat, character schema, dialogue format, or separation between world, player, and character knowledge.

## When to use

- Before Dialogue Factory reviews a game for the first time.
- After a dialogue, character-state, quest, memory/knowledge, routing, or generation change could invalidate the existing envelope.
- When the existing envelope is missing, stale, too vague for the current review, or contradicted by the project.

If an envelope already exists, read it as a hypothesis to verify against the current project, not as authoritative source material.

## Primary output

Create or update this file in the target game project:

```text
.factorium/dialogue/DIALOGUE_ENVELOPE.md
```

Organize it around the target game's actual systems. Do not force every suggested topic below into a section when it does not apply. Keep it compact enough for repeated use during a large dialogue pass, but include enough detail that the Factory can judge a line's speaker, knowledge, trigger, and relevant situation without rediscovering basic game behavior. Point to the best evidence locations, using repository-relative paths and useful symbols, nodes, or file patterns where known.

## Persist discoveries for future passes

Investigation is expensive; preserve the map so later direction changes do not require rediscovering the whole project. Alongside the envelope, create or update:

- `.factorium/dialogue/DIALOGUE_INVENTORY.md` — a **navigational index**, not a second copy of the game or an exhaustive per-line database. Start with an entry per useful unit (file, scene, quest, character, generator, or dialogue cluster); refine to nodes only where useful. Link to source paths or stable identifiers, important speakers and trigger/context dependencies, canonical-voice evidence, and procedural entry points.
- For each indexed unit, make **coverage** explicit (mapped, sampled, reviewed, not yet examined, or unclear). Note last inspected source revision/commit or file reference when available and what remains unknown. Do not equate 'found the file' with 'understood all routes.'
- Reuse existing inventory entries when still supported by source; update only impacted areas and record new paths or contradicted assumptions. Do not repeatedly inventory unchanged areas just to produce a newer timestamp.
- Keep the inventory compact. Group repetitive content and link back to actual source. Avoid requiring a full inventory of every line before the Factory can start; the Factory can refine it during review.

Keep **creative direction** separate from discovered game mechanics:

- `.factorium/dialogue/DIALOGUE_DIRECTION.md` records the user's current explicit artistic goals and scope, for example naturalistic versus heightened speech, pacing, exposition tolerance, or character-specific exceptions.
- Do not infer a permanent preference for 'realism' or another style from the game genre or from one example. If no direction has been provided, leave it explicitly unspecified (or draft a clearly marked, unapproved starter for the user); never silently treat an inferred direction as a requirement.
- A direction change usually calls for a **Factory style-impact pass**, not a new full Investigator run. Reinvestigate only when dialogue architecture, character facts, trigger logic, voice evidence, or other underlying discoveries are stale.
- If evidence about the game conflicts with an explicit creative direction, record the tension; do not silently rewrite lore or character state as a shortcut to matching style.

These are lightweight Markdown artifacts maintained **in the target game workspace**, not in Factorium itself. No new database, parser, schema, or standing agent is required.
## Investigation sequence

### 1. Orient in the project

Read the game's README and any project guidance that explains layout, build/runtime behavior, or content conventions. Identify the engine and likely content formats from the repository itself. If the project is large, use its directory structure, manifests, search, and references from code to narrow the search; do not mistake the first obvious `dialogue` folder for the whole system.

Build a working map of where dialogue is authored, invoked, selected, transformed, localized, or generated. Search for representative content and follow references outward into scripts, quest/event logic, character definitions, prompts, and data. Explore unfamiliar formats through their surrounding code or documentation. Read enough examples to understand the system, then expand where a new path or exception appears.

### 2. Establish evidence and its limits

Prefer direct, current project evidence, and match the evidence to the claim:

- For what can happen, trace runtime logic, conditions, and data.
- For how a character speaks, use that character's canonical dialogue in context.
- For intended meaning, consult character definitions, design notes, and documentation, then compare them with implementation and authored content.
- Use setting, genre, or small-sample inference only when direct evidence is missing, and label it as inference.

Cross-check sources when they disagree. For example, a character bio may describe a restrained speaker while their dialogue becomes profane when frightened; record the situational pattern rather than choosing one source and erasing the other. Do not convert a few lines into a confident, universal voice rule. Say when dialogue is sparse, contradictory, placeholder text, or likely outdated.

Use evidence to explain a finding, not just to decorate it with a path. The envelope should make clear which files establish a trigger, which samples establish a voice pattern, and which conclusions remain uncertain.

### 3. Trace dialogue paths and triggers

Follow dialogue from its source to the point where a speaker can say it. Determine, as applicable, whether it is reached through conversation trees, barks, quests, ambient events, combat, cutscenes, item interactions, authored scripts, runtime prompts, or other project-specific paths. Look for conditions, fallbacks, shared nodes, substitutions, cached/generated text, and alternate routes.

The goal is to identify materially different legal contexts, not enumerate every state combination. Ask what distinctions could change the line's truth, inference, emotional plausibility, intended effect, or voice. In particular, examine broad conditions that group states a writer or generator may need to treat differently.

Example: one route may require that the player completed an investigation, while the speaker's witness flag is optional. The line can then reach a character who knows the culprit and one who only knows that the player returned. The shared route is a knowledge boundary worth exposing, even if both characters occupy the same dialogue node.

Example: one conversation node may be reachable both before and after a character has reconstructed a suppressed memory. A line that assumes the recovered memory works only for one group. Record the split and how the Factory can recognize it; do not enumerate unrelated combinations of inventory, weather, and relationship state unless they also change plausibility.

### 4. Discover state, knowledge, and memory as implemented

Trace any state that can materially affect what a speaker can know, believe, infer, remember, feel, intend, or say. Candidate search topics may include attributes, expertise, social role, faction, relationship, reputation, quest and choice history, injuries, status effects, location, possessions, secrets, or prior conversations. These are prompts, not a required schema.

For each relevant system, explain what its values mean in this game and how they affect dialogue or reachability. Do not import generic meanings. If the game models intelligence, for example, inspect what its code and authored dialogue connect it to: inference, abstraction, vocabulary, attention, schooling, or something else. Do not infer that a low value means childish wording unless project evidence supports that reading.

Keep these concepts distinct wherever the game does:

- what is true in the world;
- what the player has learned;
- what information is available to this speaker;
- what the speaker believes, including mistaken beliefs;
- what the speaker remembers, has forgotten, or has reconstructed.

Trace the actual information flow. A quest completion flag may describe player progress, not a character's knowledge. A world fact may be available to code without ever being presented to the speaker. Likewise, memory loss may restrict recall without erasing the character's skills or every belief. Do not collapse these states unless the implementation does.

### 5. Learn character voice and content conventions

For important speakers, sample canonical dialogue across enough scenes to distinguish recurring habits from one-off reactions. Where evidence permits, note meaningful patterns in sentence shape, cadence, directness, abstraction, vocabulary, formality, humor, profanity, emotional expression, and rhetorical habits. Include situational shifts, contradictions, development, and uncertainty. Do not turn the result into a formula to imitate mechanically.

Determine the game's tone and content envelope from its actual writing and stated conventions. Mature language, violence, cruelty, sexual material, offensive characters, dark humor, and other adult content are not defects by themselves. Explain how the game uses such material and what context makes it fit or clash. Do not sanitize or moralize the source material.

### 6. Investigate procedural dialogue when present

Follow the generation path from prompt/instructions to supplied context, generation, selection or filtering, storage/reuse, and routing. Determine what the generator receives, what it lacks, whether context is transformed or summarized, and whether one output can appear in materially different situations.

When examples are available, compare recurring failures and locate their likely cause: missing or misleading context, a prompt rule, generation quality, reuse, or routing. If a generator never receives speaker knowledge, patching individual lines will not repair the information leak. Record where the Factory should inspect upstream instructions and context before treating outputs as isolated authored lines.

If no procedural system is found after a reasonable search of runtime entry points and project references, say that none was found in the inspected paths; do not claim that no such system exists everywhere without evidence.

### 7. Draft a useful envelope and inventory

Include the findings the Factory will need repeatedly. Depending on the project, this may cover architecture, key speakers and canonical voice evidence, dialogue-affecting state, knowledge/belief/memory, trigger boundaries, procedural generation, tone, recurring review rules, and unresolved questions. The exact organization and terminology should fit the game.

For each significant conclusion, make it actionable: explain the rule or distinction, why it matters to dialogue review, and where to verify it. Highlight high-impact counterexamples and shared routes. Separate observed behavior from design intent and inference when those differ.

Keep the envelope a guide, not a substitute for source inspection. It should direct the Factory to representative evidence and warn it where cases need a deeper source-level check.

Update the inventory from paths and content actually inspected: index dialogue areas, recurring entry points, relevant voice sources, and trigger dependencies, identifying sampled versus unexamined areas. Preserve useful previous entries unless source evidence invalidates them. A large game may begin with a coarse index; do not block completion on line-level enumeration.

### 8. Make an adversarial second pass

After drafting, try to disprove the envelope. Search beyond the directories and file types used in the first pass. Follow unusual speaker definitions, event or quest entry points, indirect/derived state, alternate conversation paths, hidden branches, memory and knowledge mechanics, runtime prompt construction, special-case routing, and references from systems that did not initially look dialogue-related.

Ask concretely:

- Is there a way into dialogue that bypasses the route I traced?
- Can the same trigger admit speakers or states with meaningfully different knowledge, belief, memory, cognition, relationships, or emotional condition?
- Is a variable only a proxy for player progress, while the dialogue treats it as speaker knowledge?
- Are there exceptions to a voice or tone pattern, or evidence that changes its meaning?
- Could generated text be reused under context different from the one that produced it?
- What plausible project evidence would make a key claim in this envelope false?

Update the envelope when this pass finds a missed system or narrows a claim. If evidence cannot settle an important question, state the uncertainty and its practical effect instead of guessing.

## What makes an envelope trustworthy

The envelope is ready when it gives the Factory a reliable starting model of:

- where dialogue originates and how important paths reach it;
- which game-specific state distinctions can change a line's plausibility;
- how world/player/speaker knowledge, belief, and memory actually relate;
- what canonical speech establishes for important characters, with limits called out;
- how the game's tone and mature content function;
- how procedural generation works, if present, and where systemic defects can arise;
- the materially different contexts hidden by broad/shared triggers;
- the strongest evidence locations and unresolved issues that could change a verdict.

Stop when those areas have evidence-backed coverage appropriate to the project's size and scope, and the adversarial pass no longer changes the core model. Do not imply exhaustive coverage. For a very large project, describe which systems, characters, or content areas were sampled and why they represent the relevant paths. Keep an uncertainty visible if it could alter a Factory decision; defer only details unlikely to affect dialogue plausibility.

## Output review

Before finishing, read the envelope as if you were the faster model receiving only that file and its evidence links. Could you identify where to inspect the speaker, line, route, and relevant state? Could you find a counterexample in which the line stops making sense? Does the envelope distinguish what the project proves from what it suggests? If not, tighten the relevant explanation or mark the gap.

The final update should briefly report the envelope and inventory paths, the major systems and context boundaries discovered, uncovered or unexamined areas, any material uncertainty, and the scope of the adversarial second pass. Do not claim the target game's dialogue was audited or repaired; this skill prepares that later work.
