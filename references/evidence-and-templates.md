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

Record API/source verification and Blueprint Editor confirmation separately, with the exact symbols/nodes covered. Record delegated authorship only when it matters to traceability. A handoff file's existence proves documentation was written, not that a Blueprint asset was implemented.

## Technical proposal

Use this detailed template for substantial module or contract changes before implementation approval. Small proposals need only behavior, affected interfaces, ownership, risks, and completion checks. Include applicable sections and public/reflected/serialized contracts; omit unaffected fields, private helper inventories, and empty tables. Pseudocode is optional.

```markdown
# Technical Proposal <ID>: <outcome>

- Requirement authority and exact decision:
- Classification and current implementation evidence:
- Goal, scope, exclusions, assumptions, risks:
- Exact UE/plugin versions, modules, engine distribution, target:

## Object inventory
| Exact name | Class/component/object/interface kind | Base type | File/asset path | Create/change | Responsibility | Owner and lifetime |
|---|---|---|---|---|---|---|

## Object contract: <exact name>
- Creation/registration/initialization order and destruction owner:
- Static definition versus mutable instance state:
- C++/Blueprint division and reflection requirements:

| Variable | Exact type | Visibility/reflection | Default or decision pending | Config/runtime/serialized | Validity/units | Writer/readers | Replication/persistence |
|---|---|---|---|---|---|---|---|

| Function | Exact signature and I/O | Visibility/exposure | Caller/trigger | Preconditions | Main logic | Side effects/failure |
|---|---|---|---|---|---|---|

| Interface/event | Kind and origin | Exact signature/payload | Producer | Consumer | Call/bind point | Unbind/cancel point | Authority |
|---|---|---|---|---|---|---|---|

## Lifecycle and main logic
- Applicable lifecycle callbacks and source evidence:
- Initialization and reference acquisition order:
- Main execution pseudocode or state-transition table:
- Data/event flow and C++/Blueprint crossing:
- Invalid data, repeat calls, interruption, cancellation, cleanup:
- Ownership changes, teardown, reload, and async/timer/delegate cleanup where applicable:
- Authority, replication, prediction, and target boundaries where applicable:

## Blueprint and asset contract
- Parent classes, component hierarchy, assets, graph locations:
- Existing nodes versus project helpers to implement/create:
- Default values, references, tags, and editor assignments:
- Migration impact and rollback:

## API/node evidence
| Symbol/node/behavior | Origin | Target version | Primary evidence | Exact contract/context | Status and limits |
|---|---|---|---|---|---|

## Implementation and acceptance
- Implementation slices, allowed paths, and any Blueprint handoff destinations:
- Build/static/Editor/PIE/packaged/network/device acceptance matrix:
- Open decisions, evidence gaps, and dependent stop conditions:
```

## Optional delegated coding and handoff packet

```markdown
# Delegated Packet <ID>

- Accepted proposal and approval evidence:
- Engine/plugin versions and relevant project instructions:
- Exact allowed code/test/document paths:
- Protected assets, generated files, and unrelated changes:
- Objects, variables, functions, interfaces, and events to implement:
- Frozen signatures, reflection, serialization, and Blueprint contracts:
- Main logic, lifecycle, authority, failure, and cleanup:
- Verified API/node ledger and primary sources:
- Existing source patterns to follow:
- Blueprint handoff Markdown destination and required template:
- Required proportionate checks and available build/editor tools:
- Explicit exclusions and conditions requiring lead review:
- Return: changed paths, code/handoff summary, commands/results, newly researched API/node evidence, unresolved gaps, and pending editor/target acceptance.
```

Delegated authors must preserve the accepted contract and verify API/node instructions. The lead reviews the result and may correct directly or return work; delegation and a particular model are not required.

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

### Handoff baseline and execution walkthrough

Before writing, establish which affected assets/functions already exist from current evidence. For implemented graphs, identify the retained entry, exact insertion/replacement point, and removed chain; for unimplemented graphs, give only the final construction steps. Use actual class/asset names. Keep one current instruction source and link shared procedures instead of duplicating them across supplements.

Before delivery, walk the affected instructions from the recipient's current baseline to an observable result:

- Can the stated variable type actually be selected in Blueprint, and is the node really Pure or executable? Verify reflection flags, actual event/function context, node overload, target and relevant pins; an EventGraph cannot use function locals. Mark unavailable evidence explicitly instead of inventing the editor result.
- Are required Class Defaults, inherited/instance overrides, component settings and asset assignments included? Trace the changed gate with existing asset values, not only ideal new defaults. Inspect only assets/settings affected by the change; summarize broad migration scope when all instances cannot be checked.
- Does each new helper have a real caller at the specified branch, with result/failure propagation? Trace initialization, activation, retry and teardown as applicable. An available function is not a connected workflow, and “retry supported” requires a trigger that can still execute after failure.
- Are explanations consistent with the actual branches and supported node outputs? Apply the shared necessity review to the resulting graph, including configuration/record fields and duplicated cleanup. Preserve compact comparisons and the formatting rules below; precision does not require expanding every trivial operator.

Fix known missing steps before calling the affected handoff executable. Report the walkthrough as static inspection unless editor operations were actually performed. Link/format validation alone does not satisfy this walkthrough.

### Handoff formatting rules

Apply these rules to Blueprint, editor, build, and validation handoffs:

- Write ordinary instructions and headings in Chinese; preserve exact API, node, pin, type, variable, and asset names.
- Separate actions from cautions and explanations. For longer documents, use distinct `操作步骤` and `注意事项` sections. For short handoffs or cautions tied to a specific step, use a separate `> **注意（步骤 N）：** ...` block outside the numbered action text. Do not rely on color alone.
- Number actions in execution order. Each step identifies where to operate, what to do, exact settings or connections, and the expected result where useful. Keep background, limitations, and pitfalls out of the action sequence.
- For Blueprint wiring, use numbered steps followed by indented `text` code blocks with arrow connections and explicit branch paths. Put data-pin sources and defaults beside the receiving node. Keep cautions in separate prose or callouts. Do not replace this format with node-by-node tables unless the user explicitly requests tables; asset, variable, and signature inventories may still use tables.
- Prefer compact expressions for ordinary comparisons (`==`, `!=`, `>`, `<`, `>=`, `<=`), arithmetic, and Boolean conditions. Write `Branch(CurrentTarget == Entry.InTarget)` or `Branch(Distance < MinDistance)` directly; do not separately list Equal/Less nodes, A/B pins, Return Value, and Branch.Condition for the same expression. Likewise, use `Set Count = Count + 1` and `Branch(A AND B)` when types and operands are clear. These are wiring shorthand, not new helper functions or executable code.
- Expand a data chain only when it resolves a real ambiguity: a special equality/tolerance node, overload or conversion, non-obvious output pin, or evaluation/lifetime ordering. Boolean shorthand does not imply Blueprint short-circuit evaluation; retain separate validity branches before dereferencing an object. Continue to name exact custom functions, target references, important parameters, and True/False destinations.
- Preserve the established wiring format when revising a section. If the user has not implemented it yet, present the final instructions directly rather than adding old-node deletion/migration steps.
- Put prerequisites before the steps. Place any caution that must be read before an action ahead of that action or in the prerequisites, with a reference to its step number; do not bury it at the end.
- Keep acceptance checks and verification status in their own section. Distinguish checks the recipient must perform from evidence already obtained.
- The lead reviews this separation as part of handoff review; return mixed action/caution prose to the author for correction.

````markdown
# 蓝图交接：<功能名称>

## 前置条件与交接范围
- Required parent class/component/interface:
- UE/plugin version, implementation prerequisites, and handoff status:
- Asset locations and naming:
- Class Defaults, tags, and data assignments:
- Exact events, nodes, variables, and bindings:
- Animation/VFX/audio/UI/camera/haptic hooks:

## 名称索引
| Canonical name | Kind (variable/function/macro/Custom Event/dispatcher/interface/node) | Origin | Owning class/Blueprint and graph | Exists or must be created | Purpose |
|---|---|---|---|---|---|

## 辅助项契约：<canonical name>
- Kind and owning Blueprint/graph:
- Inputs/outputs with exact names, types, defaults, and reference/container semantics:
- Variables with exact names, types, defaults, visibility, and owner:
- Caller, responsibility, side effects, failure, and cleanup:

## 操作步骤

操作位置：`<完整资产路径> → <函数或事件图>`。

1. <按依赖顺序创建变量、辅助函数或事件；已有项直接复用，写清类型、默认值和归属。>
2. <写明本段接线的目的，然后给出执行链；每个分支明确下一节点或结束位置。>

```text
<入口事件／函数>
 → <准确节点名>
   Target=<对象引用来源>
   <输入引脚>=<源节点.输出引脚或固定值>
 → Branch(CurrentTarget == Entry.InTarget)
   True → <下一节点及输入>
        → Return <输出引脚>=<值>
   False → <失败处理节点及输入>
         → Return <输出引脚>=<值>
```

3. <下一段接线；明确承接上一段哪个输出。简单 Pure 表达式直接写在使用处，不展开重复数据线；仅复杂或有歧义的数据链单列，且不画成执行线。>

```text
仅在需要展开复杂数据链时（Pure，无执行线）：
<源节点.输出引脚> → <目标节点.输入引脚>
<Pure节点.返回值> → <执行节点.数据输入>

执行连接：
<前段指定执行输出> → <下一节点>
```

## 注意事项
- <适用步骤编号；限制、易错点及其影响。操作前必须了解的事项应移至前置条件或对应步骤之前。>

## 验收与验证状态
- Debug filters, watches, and expected runtime values:
- Normal, invalid, cancellation, interruption, cleanup, and repeat checks:
- Evidence the programmer has supplied:
- PIE/target evidence still owned by the user or QA:
````

- Distinguish repeated nodes with local labels only when the inline condition does not already identify them; do not require global P01/D01 inventories. Use concise expressions or adjacent pin assignments to identify data sources; reserve explicit source-pin -> destination-pin lists for connections that need clarification. In execution chains, an ordinary arrow means the previous node's Then output connects to the next node's execution input; explicitly name other execution pins such as True/False, Loop Body, Completed, and Break.
- Show branches, return paths, asynchronous completion/cancellation, bind/unbind, and lifetime cleanup where relevant.
- Mark custom helpers as user-to-create or code-generated, with prerequisites before their first use.
- Record node exposure/source verification separately from actual Editor search/compile confirmation.

Use one canonical name per helper throughout the file; do not interchange function, macro, Custom Event, dispatcher, or interface message. If a required node or pin is unresolved, mark that step blocked and explain the missing evidence rather than writing a speculative wiring recipe.

### Handoff pre-delivery check

Before the first delivery and after substantive revisions, review the affected instructions and their dependencies against the rules above:

Apply the `Common implementation gate` in SKILL.md as well: correctness and necessity are separate logic-review passes, shared with C++ and Blueprint implementation. This formatting/completeness check does not replace them. Use the shared review checklist's compact coverage record rather than introducing a separate handoff review ledger.

- Can the recipient identify each owning asset/graph, existing versus new/replaced content, and helper/variable ownership without guessing? Create helper signatures before their first use.
- Does the wiring retain numbered steps, indented arrow blocks, and separate cautions? Are operands, types, object references, important defaults, branch exits, and return values clear? Accept ordinary comparisons, arithmetic, and Boolean expressions inline; do not require their expansion into operator nodes and pin lists merely for completeness. Check ambiguous or lifetime-sensitive data chains explicitly, without treating Boolean expressions as short-circuit guards. Remove redundant expanded data lines when the inline expression already specifies the connection; do not convert the section into node-by-node tables.
- Are prerequisites, numbered actions, cautions, and acceptance evidence separated as specified? Check that cautions needed before an action appear before it.
- Are unresolved API/pin details explicitly identified, and are static evidence, Editor compilation, and PIE results distinguished? Do not label unresolved steps executable or the whole handoff ready.

Correct omissions before delivery; do not defer format compliance until the user requests a rewrite. In the delivery reply, briefly state the scope actually checked and any remaining gaps. A heading/keyword check or template presence alone cannot establish wiring completeness. This check concerns document readiness, not implementation or runtime acceptance.

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
