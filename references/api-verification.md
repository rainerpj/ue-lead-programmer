# UE API and Blueprint Node Verification

## Establish the target

Record the exact UE version/build, engine source or Installed Build, relevant plugin versions, modules, target platform, and graph kind. Do not assume latest documentation matches the project or that an enabled editor plugin is available in a runtime/server target.

## Primary evidence

- Inspect matching local engine/plugin headers and implementation for declarations, visibility, signatures, reflection metadata, lifecycle behavior, and module/export dependencies.
- Use version-matched Epic documentation and official plugin/vendor documentation or source. Browse when source evidence is unavailable or version/behavior remains uncertain. Community snippets and model memory are discovery leads only.
- For Blueprint exposure, inspect reflected declarations/metadata or the actual K2 node implementation and pin allocation. When available, verify in the matching Editor and graph context. A screenshot can establish the shown node/pins, not unobserved behavior.
- Record file/line or official URL, version, exact contract, and evidence limits. Conflicting sources or missing evidence remain unresolved until checked; never fill gaps with plausible names.

## C++ checks

For every new or uncertain engine/plugin symbol, verify owner, exact spelling, header/module, access, full signature and overload, return and parameter types, static/instance status, required configuration, and target availability. Check reflection specifiers, delegate signatures, lifecycle order, thread/authority constraints, units, cancellation, and cleanup when relevant.

Private/internal source is not automatically a supported public API. Do not suppress compiler errors, invent includes, or use speculative version guards to hide an unverified call. Mark deliberately proposed project-defined APIs separately and provide their implementation contract.

## Blueprint checks

For each new or uncertain node in a handoff, verify:

- exact searchable/display name and backing C++ symbol or node class;
- origin: engine, named plugin, existing project helper, or helper to create;
- owning/target type, plugin/module prerequisite, and graph context (such as Event Graph, Function, AnimGraph, or ability graph);
- whether reflection/node implementation actually exposes it there; an ordinary C++ method or delegate is not inherently a callable node or bindable dispatcher;
- execution pins, data pins, direction, type, defaults, reference/container semantics, and relevant advanced/hidden pins;
- pure/impure, latent/async restrictions, required world context, authority, and completion/cancellation behavior as applicable.

Do not derive a node name or pin layout solely by adding spaces to a C++ identifier. Do not treat BlueprintNativeEvent/ImplementableEvent, Custom Event, Event Dispatcher, interface message, function, and macro as interchangeable. Verify the applicable mechanism.

For project-defined helpers, give a single canonical name and explicit creation/implementation prerequisite. A helper listed in a plan is not an existing searchable node. If Editor search is unavailable, label node exposure/source verification separately from Editor confirmation. If exposure or pins themselves cannot be established, block the affected handoff step instead of publishing a guessed instruction.

## Evidence ledger and review

| Symbol/node/behavior | Origin | UE/plugin version | Primary source | Exact signature or pins/context | Status and limits |
|---|---|---|---|---|---|

Use explicit statuses: source verified, Editor confirmed, project-defined pending implementation, or unresolved. Verify new or uncertain symbols/nodes, including those introduced by a delegated author; resolve discrepancies directly or return them for correction. If no supported route is verified, report that dependency as blocked with researched alternatives; do not claim the feature is impossible merely because one search failed.
