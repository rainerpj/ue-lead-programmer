# Evidence and Delivery Templates

Use the smallest applicable template. Keep project facts in project documents; these formats define reusable fields and evidence semantics.

## Evidence levels

Evidence is cumulative only when each level was actually observed:

1. `[Designed]`: ownership, interfaces, scope, and acceptance are defined.
2. `[Implemented]`: source, Blueprint, data, or assets exist in the inspected workspace.
3. `[Build Passed]`: the relevant UHT, compilation, link, cook, or package command passed; name the command and target.
4. `[Automated Test Passed]`: named tests or deterministic validations passed.
5. `[PIE User Confirmed]`: the user observed the stated behavior in PIE or Standalone; record the scenario and boundary.
6. `[Target Confirmed]`: required device, packaged build, client/server topology, platform, performance scene, listening, or feel acceptance passed.
7. `[Delivered]`: approved scope was documented and committed or packaged; record the identifier and remaining workspace state.

Do not infer a higher level from a lower one. A build does not prove Blueprint wiring, presentation, feel, audio, networking, target-device behavior, or content completeness.

## Minimum acceptance slice

Use before expanding a new module:

```markdown
# Slice <ID>: <player-observable outcome>

- Authority/spec:
- Player-visible goal:
- Minimum configured example:
- Included:
- Explicitly excluded:
- Preconditions and dependencies:
- Input and trigger:
- Authority/runtime result:
- Presentation result:
- Failure, cancellation, cleanup, and repeat paths:
- Required evidence levels:
- Expansion decisions intentionally deferred:
```

The configured example proves the contract only within its stated boundary; it does not automatically become the future content parent, final balance, or production architecture.

## Feature contract

Use when design and implementation need one traceable interface:

```markdown
# Feature Contract <ID>: <name>

- Product/design authority:
- Target version and status:
- Player value and intended decision:
- Rules and invariants:
- Included / excluded:
- Definition data and owner:
- Runtime state and owner:
- Authority/execution owner:
- Blueprint/editor owner:
- Presentation triggers and asset owner:
- Persistence, replication, interruption, cleanup:
- Debug and telemetry surface:
- Acceptance matrix:
- Current evidence:
- Open decisions, owner, deadline, fallback:
- Change impact and migration:
```

## Blueprint and asset handoff

```markdown
# Blueprint Handoff <ID>

- Required parent class/component/interface:
- Asset locations and naming:
- Class Defaults, tags, and data assignments:
- Exact events, nodes, variables, and bindings:
- Animation/VFX/audio/UI/camera/haptic hooks:
- Debug filters, watches, and expected runtime values:
- Normal, invalid, cancellation, interruption, cleanup, and repeat checks:
- Evidence the programmer has supplied:
- PIE/target evidence still owned by the user or QA:
```

## Delivery evidence

```markdown
# Delivery Evidence <ID>

| Claim | Evidence level | Command/scenario | Result | Owner/date |
|---|---|---|---|---|

- Delivered paths:
- Commit/package identifier:
- LFS/generated-path checks:
- Pre-existing staged or unstaged state preserved:
- Known exclusions and deferred validation:
```
