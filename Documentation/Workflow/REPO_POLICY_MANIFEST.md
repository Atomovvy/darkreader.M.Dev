# REPO_POLICY_MANIFEST.md

Repository: `Atomovvy/darkreader.M.Dev`
Policy mode: Atomovvy local overlay on external copy
Central policy repository: `Atomovvy/Atomovvy`
Repository role: `external-copy`

## External source boundary

The product code and upstream history belong to the Dark Reader project and its contributors. The current repository carries the MIT license. Atomovvy-local policy files do not replace upstream licensing, authorship, contribution or release rules.

## Required Atomovvy central policy

Read current applicable versions of:

```text
Documentation/Workflow/AGENTS_BASE.md
Documentation/Workflow/GIT_POLICY.md
Documentation/Workflow/PROMPT_POLICY.md
Documentation/Workflow/MULTI_AGENT_LOCK_POLICY.md
Documentation/Workflow/P2C_SIMPLE_LOCK_V2_RUNBOOK.md
Documentation/Workflow/VALIDATION_POLICY.md
Documentation/Workflow/HANDOFF_POLICY.md
```

If required current central policy is unavailable, Atomovvy-directed repository-changing work fails closed as `CENTRAL_POLICY_UNAVAILABLE`.

## Repository writer coordination

```text
P2C_SIMPLE_LOCK_V2_STATUS=ACTIVE
COORDINATION_MODE=P2C_SIMPLE_LOCK_V2
LOCK_REF=coordination/write-lock-v2
LOCK_FILE=LOCK.json
CLAIM_PRIMITIVE=GITHUB_CONTENTS_FILE_SHA_CAS
READ_ONLY_LOCK_REQUIRED=NO
P2C_LEGACY_STRONG_STATUS=FROZEN_REFERENCE
LEGACY_STRONG_DEFAULT_FOR_ORDINARY_WRITES=NO
RUNTIME_ACTIVATION_COMMIT=b2bec365cdcf972fe34669608a062c07f77c95f6
```

For ordinary hosted Atomovvy mutations, freshly fetch and validate the live lock, retain the exact returned file SHA, acquire by exact file-SHA compare-and-swap, and verify exact ownership before crossing the target-mutation boundary.

Coordination failure fails closed without silent Legacy Strong fallback.

## Scope boundary

This rollout changes only Atomovvy-local coordination/policy metadata. It does not modify Dark Reader source, package metadata, build, tests, release configuration, browser-extension behavior, upstream synchronization strategy or licensing.

The lock coordinates conforming Atomovvy writers only. It does not grant authority to rewrite upstream history, publish releases, change licensing or merge changes.

## Handoff

Atomovvy-local repository-changing work uses `Documentation/Workflow/AGENT_LAST_RUN.md`. Live lock state is always read from `coordination/write-lock-v2:LOCK.json`.
