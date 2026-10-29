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
- Commit or push only when explicitly authorized; inspect staged scope and use explicit paths.

## Remove redundancy before delivery

- Before adding or retaining a defensive check, state change, or cleanup step, identify the concrete failure path in the current implementation if it is omitted. If no current requirement or failure path supports it, omit it; hypothetical future changes such as delayed destruction do not justify extra nodes today.
- Establish what the engine already handles at the relevant lifecycle stage. Do not manually repeat engine-owned cleanup without a timing or ownership reason. For example, disabling collision or Tick immediately before synchronous Actor destruction is usually unnecessary if nothing in between observes or reenters the Actor; this is not a blanket rule for delayed destruction or callback-heavy teardown.
- Give each resource or registration one responsible cleanup implementation. Normal completion and EndPlay may both invoke that implementation when they cover distinct exit paths; make shared cleanup safe to repeat instead of copying it across graphs. Check ownership of timers, delegates, and external effects rather than assuming Destroy handles all of them.
- Preserve guards with a concrete purpose, such as marking completion before callbacks to prevent synchronous reentry or unregistering an Actor from an external manager. Explain the protected path rather than labeling every precaution necessary.
- Avoid an Is Valid node immediately before an execution-pin Cast when its only purpose is rejecting a null input and Cast Failed already handles that path; use the cast's success/failure outputs directly. Do not generalize this into "Cast proves object validity": casting checks type and nullness, not destruction/garbage state. Retain a validity or lifecycle check only where the current path requires a live object (for example, cached actors after teardown), and evaluate any object dereference used to obtain the cast input separately.
- Before handing off C++ or Blueprint wiring, make a deletion pass for repeated validation, duplicated cleanup, and state writes with no observable role. Resolve uncertain engine behavior through targeted source inspection or a focused test; do not substitute additional defensive nodes for understanding. Keep this pass proportionate to the change.

## Conditional references

- [Role contract](references/role-contract.md): only when gameplay, technical, or editor ownership is unclear.
- [Project adapters](references/project-adapters.md): when project-specific build, compatibility, authority, or asset rules are needed. For TopDownRoguelikeShooter, read its [adapter](adapters/topdown-roguelike-shooter.md) directly.
- [Evidence and templates](references/evidence-and-templates.md): read the relevant proposal, delegation, handoff, or acceptance section, not the entire file by default.
- Treat GAS, Lyra, Game Features, dedicated servers, and source builds as project choices, not universal requirements.
