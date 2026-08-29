# Project Adapters

Use a project adapter to preserve repository-specific rules without forking the lead-programmer skill.

## Discovery

1. Read repository `AGENTS.md`, `.agents`, `.codex`, project indexes, active implementation documents, and the `.uproject` before selecting an adapter.
2. Match an adapter by explicit project root, project name, or authority documents. Do not apply an adapter merely because two projects share a genre or plugin.
3. The live repository remains authoritative. If an adapter conflicts with current files, report the drift and follow the current approved project authority.
4. If no adapter matches, build a temporary project profile in the response or work notes. Do not create a persistent adapter unless the user asks.

## Automatic maintenance

When a matching adapter is used, automatically compare it with the live project at task start and again after an engine migration, architecture decision, module acceptance, authority-document change, or delivery-workflow change.

Synchronize the adapter during the same task only when a durable project rule is confirmed by the current authoritative files or an explicit user decision. Durable adapter facts include:

- engine association, targets, stable build entrypoints, and project roots;
- authority-document locations and precedence;
- framework, module, networking, persistence, compatibility, and ownership boundaries;
- protected asset categories and editor responsibilities;
- source-control, LFS, generated-path, validation, and delivery conventions.

Do not copy transient state into an adapter, including the active feature, completion percentage, current branch, staged-file counts, temporary defects or workarounds, one-off asset choices, tuning values, test captures, or milestone results. Those belong in project progress, task, decision, handoff, defect, or evidence documents.

Maintenance sequence:

1. Treat the live project authority as the source of truth; never change project rules merely to match an adapter.
2. Classify each difference as durable, transient, proposed, or uncertain.
3. Update the adapter only for verified durable differences. If the difference is proposed, inferred, conflicting, or not yet authoritative, report it and leave the adapter unchanged.
4. Keep the edit limited to the matching adapter unless the change is genuinely universal across materially different UE projects.
5. After synchronization, verify links and skill structure, then report what changed and which live authority supported it.

## Adapter contents

An adapter may define:

- project roots, `.uproject`, engine association, targets, and build commands;
- design, implementation-progress, active-task, and decision authorities;
- module, plugin, framework, networking, persistence, and compatibility constraints;
- user-owned Blueprint, map, animation, audio, VFX, migrated, or binary asset boundaries;
- source-control layout, LFS rules, generated paths, and delivery conventions;
- project-specific evidence requirements and known external blockers.

An adapter must not duplicate the generic role contract, module gates, evidence vocabulary, or Git safety rules.

## Installed adapters

- [TopDownRoguelikeShooter](../adapters/topdown-roguelike-shooter.md)
