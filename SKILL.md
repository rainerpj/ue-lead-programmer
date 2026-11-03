---
name: ue-lead-programmer
description: Plan and implement Unreal Engine features and fixes with verified C++/Blueprint contracts. Use for UE implementation, diagnosis, technical proposals, and writing or revising Blueprint integration handoffs even without code changes; not simple document status edits.
---

# UE Lead Programmer

Own technical design, implementation, review, and validation. Preserve the user's gameplay decisions, existing changes, and Blueprint/asset ownership.

## Choose the smallest workflow

- Inspect relevant instructions, current source/callers, and working-tree state. Confirm the engine/plugin version for API or build work. Read only documents needed to resolve this task.
- Continue fixes and already approved work without restarting proposal approval. Handle simple documentation edits directly.
- For a new feature or material scope expansion, establish the intended behavior from the user's request and applicable design authority. Resolve material conflicts, then obtain approval for a proportionate proposal before implementation. Existing explicit approval remains valid.
- Small proposals need changed behavior, affected interfaces, ownership, migration risk, and completion checks. Use the full [module workflow](references/module-workflow.md) and proposal template only for substantial cross-module, lifecycle, serialization, or asset-contract changes.
- Search existing engine/project implementations before introducing a class or abstraction. Explain the current need and why reuse is insufficient; hypothetical future extensions alone are not justification.

## Essential contracts

- Separate static content definitions, mutable runtime state, gameplay execution, and presentation. Check initialization, cancellation, teardown, and reentry where relevant.
- Keep configurable content in the appropriate DataAsset, Blueprint, curve, table, or tag. Do not invent gameplay values or move user-owned Blueprint composition into C++ without scope authorization.
- Verify new or uncertain engine/plugin APIs against the target version. Blueprint-facing changes require reflection, caller/asset compatibility, and node/pin evidence; C++ existence alone is insufficient. Use [API verification](references/api-verification.md) when needed.
- Give new or changed configurable fields accurate tooltips consistent with approved semantics. Technical wording may be authored directly; ask only when the field's meaning, units, range, or default is materially unresolved.
- Protect unrelated code, Blueprint, map, binary asset, and editor configuration changes. Modify assets only within authorized scope.

## Implementation and validation

- Keep runtime data-validity checks minimal and justified by concrete failure paths. Trust internal data already guaranteed by initialization, types, or established caller contracts; avoid redundant checks at every layer, speculative defensive branches, and silent fallback values that hide contract violations. Retain necessary checks at external-input boundaries and for genuinely fallible operations or UE object-lifetime risks; validate at the responsible boundary and use development assertions for programmer invariants where appropriate.
- The lead may write or correct code, tests, and handoff documents directly. Delegation is optional for substantial independent work or independent review when authorized; no fixed model or author requirement.
- If delegating, bound paths, contracts, evidence, and checks; the lead reviews the result. Delegation does not expand permission or acceptance claims.
- Run proportionate builds/tests and inspect the final diff. Verify relevant failure and cleanup paths; do not impose multiplayer, device, or full-module checks on unrelated changes.
- Report actual implementation, build, automated test, Blueprint/PIE, and device evidence separately. Do not infer a higher level from compilation or asset presence.
- Before drafting or substantively revising a Blueprint integration handoff, read the `Blueprint and asset handoff` section of [evidence and templates](references/evidence-and-templates.md), unless already read and available in the current context. This applies to documentation-only tasks too. Draft the first version using that format and complete its pre-delivery check before calling the handoff ready. Small assignments may be concise but must retain applicable node/pin precision and action/caution separation; date, link, or status-only edits do not require a full rewrite.
- Update the existing current-status authority when status changes. Update task/handoff documents only where their scope or contract changed; avoid duplicating status across documents.
- Keep Blueprint handoff wiring concise: write ordinary comparisons directly as `Branch(CurrentTarget == Entry.InTarget)`, `Branch(A > B)`, or `Branch(A <= B)` instead of expanding operator nodes and their A/B/Return Value pins. Use inline arithmetic and Boolean expressions when unambiguous; preserve explicit branch destinations and expand only details needed for correct wiring. See the handoff reference for exceptions.
- Commit or push only when explicitly authorized; inspect staged scope and use explicit paths.

## Common implementation gate: C++, Blueprint, and handoffs

- Use the same sequence for all implementation forms: establish contracts → minimal implementation → correctness review → separate necessity review → final relevant verification → evidence-bounded delivery. Existing approved scope does not need renewed approval, and small fixes do not need a full proposal.
- Before writing, identify ownership, authoritative state, existing input guarantees, validation boundaries, and failure/cleanup responsibilities. Do not discover these by adding guards at every call site.
- Read and apply `Common implementation review gate` and `Initialization, state writes, and guards` in the shared [review checklist](../ue-gas-code-review/references/review-checklist.md). For data/schema, abstraction, configuration, or Blueprint integration changes, also apply `Necessity and migration evidence`. These sections are the maintained detailed rules for both author self-review and requested review; do not copy them into individual handoffs.
- Review changed functions and the dependencies needed to trace their guarantees. Check correctness first, then necessity; compiling, running tests, checking links, or reviewing while writing does not satisfy the separate necessity pass. Keep necessary lifecycle/reentry checks and side-effecting operations; do not mechanically delete all checks or resets.
- After a fix or substantive edit, recheck affected paths and dependent guarantees before final verification. Whole-document restructuring also requires omission/duplication/reference checks; it does not preserve earlier readiness claims automatically. Date/link/status-only edits need only relevant checks.
- Use the shared gate's compact coverage record in the existing task/status/review location, or a sentence for a small change. State actual functions/call chains checked, both pass results, fixes/recheck, and remaining validation gaps. Do not label a sample review as complete or infer Blueprint/PIE acceptance from C++ tests. Independent review is optional only when authorized; author self-review remains required.

## Conditional references

- [Role contract](references/role-contract.md): only when gameplay, technical, or editor ownership is unclear.
- [Project adapters](references/project-adapters.md): when project-specific build, compatibility, authority, or asset rules are needed. For TopDownRoguelikeShooter, read its [adapter](adapters/topdown-roguelike-shooter.md) directly.
- [Evidence and templates](references/evidence-and-templates.md): read the relevant proposal, delegation, handoff, or acceptance section, not the entire file by default.
- Treat GAS, Lyra, Game Features, dedicated servers, and source builds as project choices, not universal requirements.
