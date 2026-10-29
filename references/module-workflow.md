# Substantial Module Delivery

Use for new or materially restructured modules and significant cross-module or asset-contract changes. Small approved fixes do not require these gates or a full proposal.

## Requirement and proposal

- Establish scope from the user request and relevant project authority. Resolve material conflicts; do not ask the user to reapprove already accepted work.
- For new development, present behavior, ownership, affected interfaces, lifecycle, migration risks, and acceptance before implementation. Record confirmed product decisions in the existing authority when needed.
- Use only applicable sections of the technical proposal template. Inventory public/reflected/serialized contracts and lifecycle-critical internals; do not enumerate every private helper or unaffected member.
- Implementation starts once the proposal is accepted.

## Baseline and contracts

- Inspect relevant source, callers, assets/references, and Git state; preserve pre-existing changes.
- Assign rule, definition, runtime state, execution, and presentation owners. Cover persistence/replication only when relevant.
- Search for reusable implementations. Add the minimum structure needed by the accepted scope.
- Identify failure, interruption, cleanup, and compatibility conditions that matter to this change.

## Implementation

- Implement directly or delegate bounded work when authorized. The lead remains responsible for integration and review; there is no mandatory author/model.
- Verify new or uncertain dependencies under [API verification](api-verification.md).
- Keep changes scoped, expose safe Blueprint interfaces, and protect unrelated assets.
- Build with the project toolchain; report UHT, compilation/linking, and runtime checks distinctly.

## Blueprint handoff

- Only changes affecting integration need a handoff. For a trivial assignment, provide concise exact instructions.
- For substantial integration, use the relevant [handoff template](evidence-and-templates.md): prerequisites, numbered steps, cautions, and validation.
- Include exact classes, nodes, targets, pins, tags, assets, and expected behavior. Distinguish engine nodes from helpers the user must create; identify unverified editor details.
- Editor changes and subjective feel remain user-owned unless authorized otherwise.

## Acceptance and delivery

- Verify relevant normal, invalid-data, resource, cancellation, reentry, ownership-change, and cleanup scenarios.
- Do not add network, packaging, or device acceptance when it is outside the approved task.
- Update the current-status authority; change task/handoff documents where contracts or scope actually changed.
- Report performed checks, results, and limits. Build success does not prove Blueprint or PIE behavior.
- Commit/push only when explicitly requested; inspect staged scope, exclude unrelated/generated files, and check LFS for binary assets when applicable.
