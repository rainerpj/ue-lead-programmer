# TopDownRoguelikeShooter Adapter

Apply only when the live repository is `TopDownRoguelikeShooter` or its authority documents explicitly identify it as that project.

## Authority and routing

- Read `UE_IMPLEMENTATION_PROGRESS.md` and the active `UE_DEVELOPMENT_TASK_*.md` before changing implementation.
- Use the project GDD/index and gameplay or development memos for design and technical decisions; do not promote implementation notes over their declared authority.
- Keep one active UE module task when the project documents require that workflow; archive it only after the recorded acceptance gate.

## Current project constraints

- Confirm the live `.uproject` EngineAssociation before building; the current established implementation line uses UE 5.5.
- Preserve the project-owned Lyra compatibility layer, migrated animation assets, Pawn-owned ASC prototype boundary, and existing user Blueprint work unless the active authority explicitly changes them.
- Treat concrete `TDRS*` classes, gameplay tags, sockets, DataAssets, weapon/enemy rules, maps, and asset paths as project implementation, never as universal UE architecture.

## Source control and evidence

- UE binary assets use Git LFS; inspect attributes and staged scope before committing.
- Preserve unrelated staged planning, PDF, spreadsheet, and delivery files. Prefer explicit project paths and path-limited commits.
- Keep UHT/UBT, automated checks, user PIE acceptance, audio/feel acceptance, and multiplayer or target-platform validation as separate evidence.

## Maintenance

Apply the automatic check and synchronization process in `references/project-adapters.md` whenever this adapter is used.

For this project, explicitly compare:

- the live `.uproject` EngineAssociation and build targets;
- the existence and authority of `UE_IMPLEMENTATION_PROGRESS.md`, the active `UE_DEVELOPMENT_TASK_*.md`, the GDD/index, and gameplay/development memos;
- the Lyra compatibility boundary, ASC ownership model, module layout, networking/persistence decisions, and Blueprint/editor ownership;
- migrated or user-owned asset protections, Git LFS coverage, generated paths, and scoped-delivery conventions.

Module progress, the current weapon or enemy task, milestone completion, individual `TDRS*` implementation details, asset selections, and PIE results remain in project documents. Synchronize them here only if they establish or replace a durable project-wide constraint.
