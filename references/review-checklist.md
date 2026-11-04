# Conditional review checklist

Use the sections relevant to the change. Patterns below require investigation, not automatic rejection.

## Common implementation review gate

Apply to C++ implementations, Blueprint graphs, and executable handoff instructions. Review the changed functions and the callers, callees, callbacks, and cleanup paths needed to establish their contracts; do not expand routine work into a whole-project audit.

1. Before implementation, establish ownership, the authoritative state, input guarantees, the boundary responsible for validation, and responsibility for failure and cleanup. Reuse existing capabilities; justify new abstractions by a current unmet need.
2. After implementation, perform a correctness pass: follow inputs and execution order through success, real failure, repetition, cancellation, callbacks/reentry, and teardown where applicable. Check partial side effects, state publication, and ownership transfer across the call chain, not only within each function.
3. Perform a separate necessity pass using `Initialization, state writes, and guards` below and the relevant responsibility/reuse checks. For each guard, assignment/reset, cached state, registration/cleanup, retry/fallback, or new wrapper, identify its observable purpose and whether another layer already guarantees or performs it. Writing the implementation while checking it is not a substitute for this pass.
4. Resolve findings within the authorized scope. Changes invalidate the affected review conclusions: recheck the changed paths and dependent guarantees, then run proportionate verification on the final version. Tests may inform either pass; passing tests does not replace them. Test required behavior and meaningful failure paths, not redundant implementation details merely to justify retaining them.
5. Record the actual coverage and remaining gaps. For nontrivial work, use a compact record in the existing review/task/status location; a small change may use one sentence. Include scope (functions/call chains), correctness result, necessity result, fixes/recheck, and validation limits. Do not create a second project status authority or a mandatory standalone report.

| Scope / functions and dependencies | Correctness result | Necessity result | Fixes and recheck | Verification / remaining gaps |
|---|---|---|---|---|
| Actual inspected scope | Findings or none found | Findings or none found | What changed and was rechecked | Commands/scenarios actually run; unreviewed or unverified areas |

Only call the stated scope reviewed when both passes are complete and unresolved findings or evidence gaps are disclosed. A complete delivery claim requires applicable blocking findings resolved; a review may finish with findings still open. Keep document preparation, static logic review, UHT/build, automated tests, Blueprint compilation, and PIE as separate claims. Mechanical format/link checks establish none of the logic-review results. A second reviewer is optional when authorized, not a prerequisite or implied delegation permission.

## Responsibility and reuse

### Project-owned shared capability index

Apply when adding or changing classes, functions, or Blueprint flows, and when creating, extracting, changing, or retiring project-owned shared libraries and reusable entry points.

- Keep one concise index in the project's existing architecture or development documentation. If no suitable home exists, create a small project document following repository conventions when registering the first relevant shared capability. Point to its location from the project-level `AGENTS.md`; use the established project instruction entry point if the repository uses another convention. Keep project-specific entries out of this reusable skill and do not create a second progress/status authority.
- On creating or extracting a shared capability, register its entry point, purpose and applicability, definition location, and a representative actual caller. Update affected rows when contracts or locations change. Mark retired entries with their replacement when needed for migration; do not present them as available. Maintain only task-relevant entries rather than requiring a whole-project inventory.

| 公共库／入口 | 用途与适用条件 | 定义位置 | 代表性调用位置 |
|---|---|---|---|
| 库名及函数或节点名 | 解决的问题、适用前提及重要限制 | 源文件与符号，或蓝图资产与函数路径 | 实际调用类／函数／图表；尚未接入则明确注明 |

- Before implementation, consult relevant index rows, then verify the current implementation and representative callers for parameter/result semantics, side effects, ownership, and lifecycle. Search by responsibility and behavior as well as names. A missing or incomplete index does not prove that no reusable implementation exists; perform a focused source/asset search. Keep signatures and implementation details in their owning source or Blueprint rather than copying them into the table.
- Call an existing capability when its contract fits. For a partial fit, assess a minimal extension against its existing consumers; do not force reuse across incompatible contracts or add a forwarding wrapper merely to appear compliant. Explain a concrete mismatch when retaining separate behavior.
- Before delivery, trace the affected new or changed callers to confirm applicable shared entry points are actually used and equivalent duplicate logic is not left behind. When extracting a library, verify migration of the original callers within the agreed scope as well. Registration, includes, imports, or a mention in the plan are not evidence of integration.
- For Blueprint handoffs, identify the intended call and its wiring, but mark the caller as pending until saved-graph evidence establishes integration. Keep any pending implementation status in the existing status authority and link it if needed. No caller yet is a disclosed integration gap, not a reason to invent a caller or broaden scope without authorization.
- Include decisive reuse or contract-mismatch evidence in the existing compact review record where material; no separate reuse report is required. Review-only tasks inspect and report missing reuse or stale entries without editing project documents or code unless authorized.

### Necessity and migration evidence

Use for changed data schemas, abstractions, configuration, and Blueprint integration. Apply to affected items; do not create an exhaustive project inventory or a new mandatory report.

- For each added or retained field in a changed record, trace its producer, actual later consumer, and required lifetime. Prefer a local value when only the current invocation consumes it; retain snapshots only for a concrete later read, timing guarantee, persistence, or diagnostic requirement. Writing a field without a consumer does not justify storage. Check the whole changed record, not only one conspicuous field.
- Before adding a Definition subclass, wrapper, manager, or configuration asset, compare the existing type/instance defaults and existing configuration owner. A different content effect alone does not require a new native type. A wrapper needs responsibility beyond renaming a call; a shared helper needs a coherent operation or genuinely shared behavior. Examine long Blueprint flows by responsibility and duplicated failure/cleanup chains, not a fixed node-count limit.
- Follow configuration from the author's actual asset through initialization to its consumer. Check relevant inherited defaults, child/instance overrides, enabled flags, and required assignments when changing a gate. For tagged/variant data, validate active fields according to the contract; do not reject inactive fields unless their presence has a real semantic consequence. Do not narrow supported content types merely to simplify implementation or tests.
- Compare behavior rather than names when reconciling a handoff with saved graphs. A direct native call may already satisfy a documented wrapper's responsibility. Verify its arguments, ordering, result and failure handling before reporting missing functionality; do not recreate a layer the user has explicitly removed.
- For each questioned guard, name the earlier guarantee and the next operation that could invalidate it. If there is no intervening invalidation and no distinct failure behavior, remove or report the duplication. For necessary guards, retain the concrete callback, lifetime, external-input, or failure rationale; do not replace all checks with blind trust.
- Recheck affected explicit user decisions after fixes or document rewrites: reuse, rejected wrappers/guards, C++/BP ownership, supported content, and configuration ownership. Use current task context and relevant owning documents; retrieve history only for an unresolved conflict. Correct the owning contract when a decision changes, rather than maintaining a second preference ledger.

Record a few decisive evidence points in the existing coverage record: actual consumer/guarantee, configuration migration checked, and any unavailable graph/default evidence. “Necessity reviewed” without an inspected scope and these relevant facts is not a sufficient result. Static walkthroughs do not establish editor usability or PIE behavior.

- Character/Pawn: physical representation, movement, components, animation-facing state, and appropriate ASC integration. Investigate unrelated gameplay systems accumulating in one class.
- PlayerController: ownership, possession, controller-level input, local control, and suitable UI interactions. Verify ownership before placing reusable mechanics here.
- PlayerState/ASC: evaluate persistent attributes and abilities across death, possession, and Pawn replacement. Pawn-owned and PlayerState-owned ASCs can both be valid; verify owner/avatar initialization and teardown.
- Components: reusable Actor-owned functionality with coherent initialization and lifetime, when not naturally an Ability.
- Subsystems: require scope and lifetime that fit the feature; avoid global managers for local responsibilities.
- GameFeature/Experience/modular gameplay: reuse existing grants, input mapping, component injection, and initialization where adopted. Do not require this architecture in projects that do not need it.
- Search for existing damage, interaction, weapon, targeting, cooldown, status, input, and animation-event paths. Prove duplicated ownership before recommending consolidation.

## GameplayAbility and AbilityTask lifecycle

- Trace activation eligibility: required/blocked tags, cooldown, cost, authority/local control, target validity, and invalid gameplay states.
- Trace commitment, including intentional split cost/cooldown commits. Check failed commit behavior, irreversible effects before successful commitment, and charging before the action can occur.
- Trace success, failure, cancellation, input release, target loss, timeout, state changes, montage completion/interruption, death, and destruction. Persistent abilities may remain active intentionally; require a defined shutdown path.
- Check cleanup of owned delegates, timers, tags, spawned actors, targeting, input/movement restrictions, temporary components, and cosmetic state. Determine which resources are automatically cleaned up, externally owned, or intended to persist.
- Test reasoning against cancellation between setup steps, reactivation, repeated completion, and late callbacks. Cleanup should not undo state now owned by a later activation or another system.
- Check cancellation/blocking tags and their interactions with death, stun, weapon changes, movement modes, and montage interruption.
- Prefer suitable existing AbilityTasks over polling or custom callback chains. Candidate concepts include montage waiting, gameplay-event waiting, target data, input release, delays, and tag changes; verify exact task names and contracts in the project version.
- For custom tasks inspect activation, delegate registration, task destruction, owner lifetime, prediction/replication, and ability termination.

## Tags, effects, attributes, and events

- Tags: use semantic gameplay state where activation, blocking, cancellation, cross-system queries, replication, or effect application benefits. Local booleans/enums need not become tags. Check source ownership and balanced addition/removal.
- Effects: inspect Instant/Duration/Infinite semantics, stacking, executions, modifier operations, SetByCaller values, granted tags, cooldowns, and costs. Question direct health mutation when it bypasses the project's intended damage pipeline; verify legitimate initialization or controlled attribute operations before reporting.
- Attributes: inspect replication/RepNotify, base/current values, clamping, PreAttributeChange, PostGameplayEffectExecute, max/current relationships, invalid values, and death thresholds. Determine whether multiple representations of death/health have distinct roles or can diverge.
- Events: verify tag and payload contract, Instigator, Target, OptionalObject, magnitude, delivery timing, and handler lifetime. Check whether repeated delivery or multiple listeners can duplicate gameplay execution.

## C++ / Blueprint boundary — mandatory

- Determine whether C++ replaces, supports, or accidentally duplicates an existing Blueprint flow. Check state machines, damage, weapons, interactions, montage timing, and events. Seek one authoritative execution path.
- Preserve C++ infrastructure for reusable primitives, GAS integration, engine integration, safe lifetime/async behavior, and appropriate authority/replication/prediction handling.
- Preserve intentional Blueprint/data composition for content-specific ability flows, encounter sequencing, cosmetics, asset selection, and tuning. Moving it to C++ requires a concrete benefit.
- Treat Blueprint-facing APIs as public contracts: small, explicit, semantically named, safe under repetition, and clear about preconditions and lifecycle.
- For BlueprintCallable, check invalid states and call order. Prefer fewer higher-level operations or enforced internal state over undocumented Initialize/Setup/Start/Update/Finish sequences.
- For BlueprintPure, inspect mutation and repeated evaluation cost: world searches, traces, asset loads, expensive queries, and large allocations. Evaluate actual use before assigning impact.
- Choose BlueprintImplementableEvent, BlueprintNativeEvent, BlueprintAssignable delegates, GameplayEvents, tags, RepNotify, or lifecycle callbacks according to the extension/notification contract.
- Verify how Blueprint observes success, failure, cancellation, completion, and state changes. Silent early returns are defects only when the caller needs a result or state becomes inconsistent.
- Prefer meaningful state-change notifications over polling. Check partial changes on failure and stale notifications after cancellation.
- Expose appropriate montage, Niagara, sound, GE/Ability/projectile/weapon classes, damage, cooldown, timing, and tuning configuration. Native tag declarations, constants, and fixed collision contracts can be intentional; do not label every hardcoded value a defect.

## Networking and prediction

- Verify the supported network mode, server authority, owning client, simulated proxies, RPC ownership, replicated state, OnRep behavior, and ability execution policy.
- Distinguish authoritative damage/spawn/effects from cosmetic feedback. Trace predicted execution, server execution, confirmation, multicast, OnRep, GameplayEvents, and C++/Blueprint callbacks for duplicate or missing outcomes.
- For predicted abilities examine prediction windows, rejection/rollback, reconciliation, predicted spawning, FX duplication, and confirmation. Do not assume a GameplayEvent automatically crosses the network.
- Check persistent state for late join/relevancy needs; transient multicasts may not represent it. Avoid needless replication of cosmetics while preserving required remote feedback.
- Recommend additional prediction only for a demonstrated responsiveness need.

## Animation, movement, spawn, and collision

- Montage: completion, blend-out, interruption, cancellation, root motion, AnimNotify/AnimNotifyState, event timing, movement locks, and ability end timing. Prefer animation-driven timing when that is the contract; independent timing can be intentional.
- Movement: assess CharacterMovement, animation root motion, root motion sources, appropriate tasks, and LaunchCharacter before custom per-frame transforms. Check collision, authority/prediction, cancellation, interruption, and restoration of movement mode.
- Spawn: authority, Owner, Instigator, transform, collision, replication, lifespan, cleanup, and spawn failure. Verify projectile damage is applied exactly once per intended hit to a valid target.
- Collision: channels, object types, hit versus overlap, query/physics settings, ignored owner, friendly fire, trace complexity, and repeated overlaps/hits. Distinguish intentional multi-hit attacks from accidental repeated damage.

## Input and UI

- Prefer a coherent Enhanced Input to input-tag/ASC/Ability path where it fits the project. Custom routing is not itself a defect.
- Check repeated bindings, mapping-context ownership, Pawn replacement, unbinding, press/release semantics, UI blocking, and input restoration after cancellation.
- Common UI: ActivatableWidget activation/deactivation, routing, focus, bindings, Pawn reference availability, teardown, and restoration of gameplay input.
- Keep gameplay authority in gameplay systems; UI normally conveys intent and displays state.

## Object lifetime, delegates, async, death, and respawn

- Identify who owns each UObject/Actor/component and when it can disappear. Inspect reflected references, raw pointers, strong/weak references, GC reachability, destruction, and validity at callback time.
- Inspect AddDynamic/AddUObject/AddWeakLambda/AddLambda and handle cleanup according to their actual semantics. Check duplicate registration, unsafe captures, and activation-to-activation accumulation.
- Async/timers: consider owner or widget destruction, ability end, level transition, cancellation, and completion from an obsolete operation. Valid object pointers alone do not prove a callback is still semantically current.
- Death/respawn: trace cancellation, ragdoll, possession, Pawn/ASC avatar replacement, and destruction. Verify owned tags/effects, input, montages, equipment, targeting, movement, and bindings are restored or retained intentionally.

## Performance and unnecessary complexity

### Initialization, state writes, and guards

Apply to code, Blueprint graphs, and executable handoff instructions in the agreed review scope. Trace each Clear/Reset, Set/assignment, and conditional check in execution order:

1. Establish the variable's owner, lifetime, actual default, and incoming value on every path. Distinguish function locals from members, reference parameters, static storage, and persistent event-graph temporaries. Verify initialization semantics rather than assuming every local starts empty or zero; uninitialized C++ scalars are not equivalent to default-initialized Blueprint locals.
2. Identify earlier writes and later readers, including loop iterations, callbacks, repeated calls, and reentry. Ask what current behavior changes if this operation is removed. Flag a reset of a fresh empty local container or empty local string before its first write when it adds no effect; inspect sibling initializations for the same root cause rather than stopping at the first example. Keep resets needed between iterations or uses within one invocation.
3. For each guard, identify the failure it catches and whether a caller, type, initialization boundary, or preceding branch already guarantees the condition. Check whether an intervening external call, callback, or lifetime transition can invalidate that guarantee before treating the guard as redundant.
4. Check observable side effects before recommending removal: setters may notify, replicate, release resources, or synchronize other state even when the stored value is unchanged. Preserve operations with a concrete current purpose; hypothetical future changes alone do not justify redundant nodes.
5. Validate at the responsible boundary. Preserve checks for external input, genuinely fallible operations, and actual object-lifetime risks. For internal guarantees, prefer direct use or project-appropriate development assertions for programmer errors rather than repeated recoverable-failure branches. An assertion is not a substitute for runtime handling of external input; a cast does not prove that an object is still alive.
6. For state variables, flags, and caches, identify the authoritative source, all writers/readers, and why separate storage is required. Remove duplicated truth only after checking its distinct timing, snapshot, or performance purpose; do not reject every cache or flag by form.
7. For Bind/Unbind, resource release, Destroy, and cleanup helpers, identify the owner and what the engine or an existing path already handles. Keep distinct normal/failure/cancellation/teardown paths where required, but give each resource one cleanup responsibility. Check intervening callbacks before removing collision/state changes around destruction.
8. For retries, fallbacks, functions, classes, and wrappers, identify a current trigger or responsibility that existing systems cannot satisfy. Reject speculative recovery that hides invalid configuration or violates the caller contract; do not add a layer solely for hypothetical future reuse.

Group proven no-effect operations as a scoped simplification finding with locations and the reason removal preserves behavior. Distinguish unnecessary wiring/maintenance cost from a runtime bug or measured performance issue. Do not claim a complete redundancy pass when only a sample of functions or branches was examined; review permission alone does not authorize deleting the operations.

- For Tick/polling, establish why continuous evaluation is needed. Consider delegates, timers, tag events, AbilityTasks, animation events, OnRep, overlap/hit events, movement callbacks, and explicit state transitions.
- Investigate world searches, repeated component/object lookup, synchronous asset loading, string tag lookup, expensive traces, allocations, and casts only in realistic hot paths and actor counts.
- Question parallel cooldown/status/attribute/ability systems, event buses, one-use managers, wrappers, factories, interfaces, and speculative generic frameworks. Recommend deletion or simplification only after identifying all consumers and behavior that must remain.
- Prefer project conventions unless evidence shows correctness, lifetime, replication, or material duplication problems. Do not report speculative micro-optimizations.
