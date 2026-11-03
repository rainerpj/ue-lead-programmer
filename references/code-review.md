# Requested code and architecture review

Review correctness, necessity, ownership, and maintainability against the actual project. Blueprint is a production layer; Lyra is a reference, not a required architecture.

## Evidence and scope

- Identify the requested diff/files and inspect relevant instructions, Git state, engine version, and project conventions.
- Review callers, grants, tags, initialization, cancellation, teardown, and similar implementations as needed. Do not expand a scoped review into a full rewrite.
- Use editor inspection or readable exports for Blueprint behavior. Asset names or C++ declarations alone do not prove graph behavior.
- Verify uncertain engine/GAS APIs against the installed version or official documentation.
- Investigate missing facts first; ask only when a material uncertainty cannot be resolved. Separate evidence gaps from defects.
- Review authorizes inspection and non-mutating validation, not fixes, asset edits, commits, or external comments unless separately requested.

## Review priorities

1. Does this code need to exist, and does its responsibility already belong to GAS, Unreal, project C++, or Blueprint?
2. Is the design the simplest suitable option, with clear ownership and C++/Blueprint boundaries?
3. Are activation, commit, cancellation, authority, object lifetime, cleanup, and reentry correct?
4. Are implementation costs material at the project's actual gameplay scale?

Read relevant sections of [review-checklist.md](review-checklist.md) when deeper inspection is needed. Apply networking only where in scope; label unknown requirements rather than inventing multiplayer obligations.

For C++, Blueprint, and executable handoff reviews, read and apply the checklist's `Common implementation review gate` and `Initialization, state writes, and guards` sections. Perform correctness and necessity as separate passes over the agreed scope and relevant call-chain dependencies. Inspect each guard, state write/reset, registration/cleanup, retry/fallback, and new abstraction; checking only conspicuous defensive branches is insufficient. Follow the gate's coverage record and change-invalidation rules. Review-only authorization still does not authorize fixes.

## Findings threshold

For data/schema, abstraction, configuration, or Blueprint integration reviews, also apply `Necessity and migration evidence` in the checklist. Check actual consumers, saved defaults and semantic equivalence with existing calls; do not infer a defect solely from a missing wrapper name or a mismatch with obsolete instructions.

Report concrete defects or material maintenance problems with a realistic trigger and consequence. Check existing safeguards and intentional conventions first.

- Separate new defects from pre-existing conditions.
- Do not flag Tick, booleans, raw pointers, managers, or one-implementation interfaces solely for their form.
- Prefer reuse where it fits; avoid imposing new subsystems, tags, prediction, GameFeatures, or Blueprint-to-C++ migration just to resemble Lyra.
- Exclude cosmetic preferences, speculative performance claims, duplicate root causes, and findings added to meet a quota.

## Output

Follow the user's requested format; otherwise provide a short scope summary, findings ordered by severity, and important validation limits.

For each finding, give a verified location, triggering condition, impact, and smallest adequate remedy. Use HIGH/MEDIUM/LOW unless the host requests another scale: major gameplay/crash/corruption risks, meaningful lifecycle or maintenance problems, then limited-impact actionable issues.

Use [final questions](final-questions.md) as an internal, relevance-based check for substantial reviews. Do not print all 20 answers unless requested; expose only actionable findings and material uncertainties. No findings means none found within the inspected scope, not proof of complete correctness.

Distinguish static inspection, UHT/build, automated tests, Blueprint/PIE, network, and device evidence. Avoid repeating findings as both narrative and inline comments unless the output format requires it.
