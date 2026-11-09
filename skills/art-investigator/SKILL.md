---
name: art-investigator
description: Discover an existing game's artwork, visual conventions, asset usage, dependencies, rendering requirements, and reachable production tools. Produce a reusable evidence-backed Art Envelope and compact Art Inventory for Art Foundry; do not make unauthorized artistic decisions.
---

# Art Investigator

## Mission

Investigate the actual target game before Art Foundry makes broad art changes. Discover what assets exist, how they are used, what the engine requires, which visual conventions appear intentional, and how changes propagate across dependent assets. This is a discovery skill, not an image generator or an autonomous art director.

Treat the game as evidence. Do not assume a genre, art style, engine, sprite format, character model, rendering pipeline, or available generation tool. Concentrate on the user-selected scope and expand only when cross-cutting references matter.

## Working files (in the target game, not in Factorium)

- .factorium/art/ART_ENVELOPE.md — compact, sourced map of the project's art systems, visual conventions, production constraints, and uncertainties.
- .factorium/art/ART_INVENTORY.md — navigational asset index, dependencies, source references, revisions, and coverage; never an unnecessary complete duplicate of every image.
- .factorium/art/ART_DIRECTION.md — user-controlled desired visual destination, scope, references, preservation rules, and approvals. Read if present, but do not fabricate or approve it.
- .factorium/art/ART_AUDIT.md — maintained primarily by Art Foundry; read when earlier changes affect discovery.

If ART_DIRECTION.md is absent, offer the provided starter template for user approval. Clearly distinguish inferred visual observations from desired creative direction. Do not silently elevate existing artwork, recent model output, or genre conventions into an approved direction.

## Discovery workflow

### 1. Locate art systems

Read project instructions and structure, then trace representative assets through manifests, engine imports, code references, scene declarations, animation configurations, UI layouts, atlases, procedural art systems, and build steps. Find the actual assets used by the game, including generated or packed intermediates. Identify ignored or obsolete assets where the evidence allows; do not presume that every file in an images folder is active.

Group according to the game's real systems: characters, costumes, portraits, enemies, scenery, backgrounds, tile sets, effects, UI, cutscenes, icons, animation, or other useful families. Investigate 2D production first; if 3D meshes, rigs, shaders, or video require a different toolchain, mark them distinctly rather than falsely describing support.

### 2. Establish visual evidence

Observe representative source images using available visual tools, not filenames alone. Record palette, silhouette, proportions, line quality, shading, lighting, composition, resolution, texture, perspective, expression, UI legibility, or other qualities where relevant. Distinguish repeated conventions from exceptions, intentional differences, placeholders, and one-off flaws.

Use project design notes and approved reference artwork as stronger intent evidence than speculative aesthetics. Record contradictions and uncertainties. Never interpret "higher realism", greater detail, or photorealism as universally better.

Identify credible style anchors for each relevant asset family, but do not create a new user-approval gate: the user's ART_DIRECTION.md controls which anchors are authoritative. Generated outputs are not automatically promoted into canonical references.

### 3. Map functional constraints and dependencies

For each relevant family, trace formats, dimensions, sprite-sheet layout, transparency, alpha premultiplication if pertinent, color space, anchors/pivots, animation frames, collision assumptions, nine-slice rules, scaling, atlas packing, import steps, naming, paths, script references, and platform constraints **only where supported by the game**.

Capture dependency relationships. A character redesign may affect sprites, portraits, expressions, outfit variants, animation frames, icons, narrative stills, and effects. Record which assets move together, what code/config would need a narrow change, and the safest validation method.

Do not claim successful gameplay integration from source inspection alone.

### 4. Assess execution environment

Identify which tools can actually be invoked in this run: image creation/editing, image inspection, asset conversion, testing/build tooling, and remote or local rendering backends. An installed local ComfyUI mentioned in previous context is not proof that this Work session can access it.

For each candidate toolchain record accessible/unavailable/unverified, supported operations, necessary credentials or bridge, and realistic limits. A hybrid handoff is acceptable when verified. An untested handoff or theoretical model capability is NOT executable feasibility.

Avoid installing tools, spending money, authorizing services, or changing external systems without the applicable user permission.

### 5. Build the envelope and inventory incrementally

Keep ART_ENVELOPE.md a concise guide that points to evidence. Suggested sections, adapted to the actual game:

- project/engine/art pipeline and authoritative evidence paths;
- asset families, observed conventions, approved anchors (if any), deliberate exceptions;
- technical constraints, integration mechanisms, and test paths;
- dependencies and propagation risks;
- tool availability and unverified bridges;
- contradictions, gaps, and scope limits.

Keep ART_INVENTORY.md navigational, with entries at the asset family, scene, character, atlas, folder, or file level as useful. For each entry include source path/stable ID, dependencies, evidence, status (mapped/sampled/reviewed/unexamined/unknown), and version/commit or file fingerprint if available. Mark which kinds of checks were performed, so a style review cannot be mistaken for an integration test.

Never block on a complete per-file listing before useful work can begin. Preserve verified prior entries and update only affected regions when source or direction changes. A direction change may require re-evaluating a broad visual area, but generally should not force a fresh map of unchanged engine wiring.

### 6. Adversarial discovery check

Before completing discovery, actively look for exceptions outside obvious asset folders: animation definitions, inherited or synthesized sprites, generated effects, packed atlases, platform-specific files, UI scaling rules, localization-specific graphics, hidden costumes, and shared source images. Challenge any confident generalization based on too few examples.

Record what's actually inspected, what's merely inferred, and what cannot be verified. Do not mark all assets as visually reviewed because their directory was scanned.

## Handoff to Art Foundry

Provide the envelope and inventory paths, discovered boundaries, important visual contradictions, dependencies, available tooling, missing direction decisions, and a small representative set suitable for real generation/integration examples. Do not recommend a global redesign yourself. Art Foundry makes recommendations only through its required feasibility, sample, adversarial-review, and user-approval gates.

## Scope exclusions

Do not perform licensing, copyright, provenance, or commercial-rights auditing as part of this workflow. Do not build a dedicated asset database or permanent model-specific automation unless the target game or user requires it. Do not invent a global runtime or batch limit; use the implementing environment's limits.

## Completion standard

A downstream agent can use the envelope and inventory to find actual asset sources, recognize what must be preserved, identify dependent changes, choose representative tests, and see explicitly which style and technical claims are verified versus unknown. Discovery is useful without claiming exhaustive coverage.
