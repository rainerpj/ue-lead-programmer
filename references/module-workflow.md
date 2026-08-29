# Module Delivery Workflow

## Gate 0: Requirement authority and proposal approval

- Classify each chat-delivered request against the conversation, live project state, progress/task documents, and design authority: new development, continuation of an accepted scope, bug fix, diagnosis, or documentation-only work.
- For new features, systems, modules, player-facing rules, or material scope expansions, cite the named design authority and the exact requirement or decision that authorizes the work.
- If the chat request is absent from, ambiguous against, or inconsistent with the design authority, stop before solution design or implementation. Ask the user to choose the intended requirement and record the resolved decision in the appropriate authority document.
- Once the requirement is aligned, produce a traceable technical proposal covering scope and non-goals, ownership, interfaces and data, lifecycle and failure paths, Blueprint/assets, migration risk, acceptance evidence, and implementation stages.
- Do not edit implementation code/assets or freeze a new interface until the user accepts that proposal.

Exit: the requirement has an explicit design-document source, conflicts are resolved and recorded, and the user has accepted the technical proposal. Only then enter Gate A.

## Gate A: Baseline and scope

- Read the live progress document, active task specification, relevant design authority and current source.
- Inspect Git status before edits; identify user changes and pre-existing staged content.
- State the player-facing goal, included/excluded scope, dependencies, input, output, failure, interruption and acceptance evidence.
- Use the minimum acceptance slice template when a small independently testable result will prevent premature architecture or content expansion.
- Label confirmed facts, proposals, prototype questions and deferred work.

Exit: the module goal and non-goals are clear enough to avoid accidental expansion.

## Gate B: Ownership and interface freeze

- Produce a concern-to-owner map: rule, definition, runtime instance, execution, presentation, persistence and debug.
- Assign a stable Feature Contract ID when design, engineering, Blueprint/assets, and acceptance need cross-document traceability.
- Draft the minimal reflected schema and Blueprint-facing API.
- Ask the user only for design fields, meanings, values or presentation choices that materially affect the contract.
- Keep concrete content names out of generic execution branches; prefer tags, definitions, interfaces, policies or strategies.

Exit: lifecycle-critical types and asset contracts are agreed; tuning values may remain editable.

## Gate C: C++ implementation

- Modify only approved files and preserve user-owned Blueprint/assets.
- Add the smallest reusable foundation that satisfies the accepted scope.
- Handle authority, initialization order, cancellation, cleanup, invalid references and duplicate grants/listeners.
- Expose safe Blueprint entrypoints and avoid exposing mutable internals unnecessarily.
- Compile with the project engine/toolchain. Distinguish header generation, compilation, linking and runtime validation.

Exit: C++ builds, or a concrete external blocker is reported with completed evidence.

## Gate D: Blueprint and asset handoff

Provide exact instructions for:

- parent class and asset location;
- Class Defaults and required tags;
- nodes, events, variables and data assignments;
- animation, VFX, audio, UI or cue hooks;
- debug filters, runtime watches and expected values.

The user performs editor changes and reports PIE evidence. Do not claim Blueprint or feel acceptance from C++ compilation alone.
Use the Blueprint and asset handoff template when the integration contains more than a trivial assignment.

Exit: the user can integrate without inferring missing technical steps.

## Gate E: Acceptance and delivery

Test or direct tests for:

- normal success;
- invalid or missing data;
- resource exhaustion;
- input release and repeated input;
- cancellation and interruption;
- equip/unequip, death, respawn or ownership changes when relevant;
- missing presentation assets without gameplay failure;
- authority/client boundaries when in scope.

Update implementation progress and the active task document. Before commit:

Record each completion claim with the evidence levels in `evidence-and-templates.md`; do not collapse build, PIE, target, feel, and delivery evidence into one status.

1. inspect staged and unstaged paths;
2. exclude generated directories and unrelated user changes;
3. verify LFS handling for UE binary assets;
4. use a path-limited commit if unrelated files are already staged;
5. report the commit hash and remaining workspace state.
