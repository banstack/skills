---
name: to-system-design
description: Turn a grill-me'd conversation into a full system-design PRD rendered as an interactive HTML artifact — no interview, just synthesis of what's already been discussed and decided.
disable-model-invocation: true
---

# To System Design

Synthesizes the current conversation — ideally one that has already been through `grill-me` — into a PRD that includes system-design decisions (architecture, data flow, module boundaries), rendered as an interactive Claude Code Artifact. Do NOT interview the user; that's `grill-me`'s job. This skill only synthesizes what you already know.

If the conversation hasn't been through a `grill-me` session yet and the design has open branches (unresolved dependencies between decisions), recommend running `grill-me` first rather than guessing at unresolved questions.

If the issue tracker and triage label vocabulary for this repo aren't already established in conversation context or in a `docs/agents/` config, ask the user once: where do issues live (GitHub Issues, GitLab, local markdown under `.scratch/`, other), and what triage label should mark an issue as ready for an AFK agent to pick up. Default to GitHub Issues with a `ready-for-agent` label if the user has no preference. Remember the answer for the rest of the conversation.

## Process

### 1. Gather context

Work from whatever is already in the conversation. If the user passes a reference to an existing PRD artifact (a file path under `docs/prds/`), read it and treat this as a revision rather than a fresh PRD.

### 2. Explore the codebase

Explore to understand the current state of the code, if you haven't already. Use the project's domain glossary vocabulary throughout, and respect ADRs in the area you're touching.

If there's no existing codebase (a greenfield build), skip this step — there's nothing to explore yet.

### 3. Confirm seams

Sketch the seams at which you're going to test the feature. Prefer existing seams over new ones, and the highest seam possible — the fewer seams across the codebase, the better; ideally one. Check with the user that these seams match their expectations before writing the PRD.

### 4. Draft system design decisions

This is what distinguishes this skill from a plain PRD: work out and record the architectural shape of the solution — module boundaries, data flow, state ownership, API/schema contracts, sequencing/dependencies between components. Where a diagram clarifies the shape faster than prose (data flow, state machine, sequence of steps), include one (inline SVG or a simple box-and-arrow diagram in HTML/CSS — no external diagram services).

### 5. Write and publish the artifact

Fill in the template below as structured data, then render it two ways from the same data:

1. **A Claude Code Artifact** (via the `Artifact` tool) — the interactive, shareable view a human reads.
2. **A local file at `docs/prds/<slug>.html`** — the durable copy `to-issues` reads from later. This must be the same document, not a re-derivation.

Both must follow the **fixed structure** below exactly, because `to-issues` depends on it. Embed the PRD content twice in the file: once as rendered HTML for humans, and once as a `<script type="application/json" id="prd-data">` block containing the same content as structured JSON (matching the section keys below) for reliable machine parsing. Never let the two drift — generate the HTML from the JSON, not the other way around.

<prd-template>

JSON keys (`docs/prds/<slug>.html`'s `#prd-data` block) and their rendered sections:

- `problemStatement` (string) — ## Problem Statement — the problem from the user's perspective.
- `solution` (string) — ## Solution — the solution from the user's perspective.
- `userStories` (string[]) — ## User Stories — an extensive numbered list, each `As a <actor>, I want a <feature>, so that <benefit>`. Cover the feature exhaustively, not just the happy path.
- `systemDesign` (object) — ## System Design Decisions
  - `modules` (string[]) — modules/components built or modified, and their responsibilities
  - `dataFlow` (string) — how data moves through the system for this feature; include a diagram if it clarifies
  - `interfaces` (string[]) — API/schema contracts, function signatures, or event shapes that are part of the decision (not implementation detail)
  - `decisions` (string[]) — architectural calls made and why (e.g. "chose X over Y because Z")
- `testingDecisions` (object) — ## Testing Decisions
  - `philosophy` (string) — what makes a good test here (external behavior, not implementation)
  - `seams` (string[]) — the confirmed seams from step 3
  - `priorArt` (string[]) — similar tests already in the codebase to model after
- `outOfScope` (string[]) — ## Out of Scope
- `furtherNotes` (string) — ## Further Notes

Do NOT include specific file paths or code snippets in prose fields. Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it in the relevant field and note briefly that it came from a prototype.

</prd-template>

### 6. Hand off

Tell the user the artifact URL and the local file path. `to-issues` reads the `#prd-data` block from `docs/prds/<slug>.html` directly — no issue-tracker publish step is required for this PRD itself, though `to-issues` will still publish the resulting vertical-slice issues to the tracker as usual.
