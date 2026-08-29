# UE Lead Programmer

A Codex skill for leading Unreal Engine requirement intake, technical planning, C++ implementation, Blueprint and asset handoff, diagnosis, validation, and scoped Git delivery.

## Core workflow

- Classify chat-delivered requests against the live project state and design authority.
- Require every new feature, system, module, player-facing rule, or material scope expansion to have an explicit design-document source.
- Stop and request a product decision when the chat request is missing from, ambiguous against, or inconsistent with the design authority.
- Produce a traceable technical proposal and obtain user acceptance before implementation begins.
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

This is currently a private repository, so cloning requires a GitHub account with repository access.

## Delivery gates

The module workflow uses a gated path:

1. Gate 0 — requirement authority and proposal approval.
2. Gate A — baseline and scope.
3. Gate B — ownership and interface freeze.
4. Gate C — C++ implementation and build evidence.
5. Gate D — Blueprint and asset handoff.
6. Gate E — acceptance, documentation, and scoped delivery.

The authoritative details live in `SKILL.md` and `references/module-workflow.md`.

## Repository structure

```text
ue-lead-programmer/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
|-- references/
|   |-- role-contract.md
|   |-- module-workflow.md
|   |-- evidence-and-templates.md
|   `-- project-adapters.md
`-- adapters/
    `-- topdown-roguelike-shooter.md
```

The project adapter contains durable routing, ownership, evidence, and asset-protection constraints for that project profile. It does not include the Unreal Engine project, Blueprint assets, game source, project design documents, or build output.

## Scope

This repository contains the reusable Codex skill and its adapter instructions only. It is not an Unreal Engine plugin, game project, gameplay framework, or asset package. Concrete implementation remains in the user's UE repository and follows that project's explicit authority and approval boundaries.

