# UE Lead Programmer

A Codex skill for leading Unreal Engine requirement intake, technical planning, C++ implementation, Blueprint and asset handoff, diagnosis, validation, and scoped Git delivery.

## Core workflow

- Classify chat-delivered requests against the live project state and design authority.
- Establish intended behavior from the user request and applicable design authority for new features and material scope expansions.
- Resolve material product conflicts before implementation; continue independent work while decisions are pending.
- Obtain approval for a proportionate proposal for new features or material scope expansions; continue already approved work without restarting approval.
- Separate product decisions and game feel from technical ownership, lifecycle, interfaces, and C++ architecture.
- Deliver exact Blueprint and asset integration instructions while protecting user-owned binary assets.
- Report compilation, PIE, target-platform, multiplayer, presentation, and feel evidence as separate validation levels.
- Keep commits path-scoped and preserve unrelated staged or working-tree changes.

## Install

Clone the repository into the Codex skills directory:

```bash
git clone https://github.com/rainerpj/ue-lead-programmer.git "${CODEX_HOME:-$HOME/.codex}/skills/ue-lead-programmer"
```

Restart or reload Codex after installation. The skill supports automatic discovery and can also be invoked explicitly as `$ue-lead-programmer`.

This repository is public and can be cloned without repository membership.

## Delivery gates

Use the smallest workflow appropriate to the change. Substantial cross-module, lifecycle, serialization, or asset-contract changes use the full module workflow; routine fixes and documentation edits use proportionate checks.

The authoritative details live in `SKILL.md` and `references/module-workflow.md`.

## Repository structure

```text
ue-lead-programmer/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
|-- references/
|   |-- role-contract.md
|   |-- api-verification.md
|   |-- module-workflow.md
|   |-- evidence-and-templates.md
|   `-- project-adapters.md
`-- adapters/
    `-- topdown-roguelike-shooter.md
```

The project adapter contains durable routing, ownership, evidence, and asset-protection constraints for that project profile. It does not include the Unreal Engine project, Blueprint assets, game source, project design documents, or build output.

## Scope

This repository contains the reusable Codex skill and its adapter instructions only. It is not an Unreal Engine plugin, game project, gameplay framework, or asset package. Concrete implementation remains in the user's UE repository and follows that project's explicit authority and approval boundaries.

