# Agent instructions for metadatafixer/snapback

This repository uses provider-neutral instructions and project state.

## Product constraints

Read [README.md](README.md) and [PERMISSIONS.md](PERMISSIONS.md) before changing
permissions, network access, data flow, backup, restore, or deletion behavior.
Keep user media and metadata on-device, preserve the documented narrow Google
host access, and treat moving Google Photos items to trash as a destructive
user-authorized action.

<!-- project-continuity:managed:start -->
## Project continuity

Use this repository as the project resume point. Before substantial work, read
`PROJECT_STATE.md` and any linked plan or workstream file. A new agent should
be able to identify the objective, verified state, next action, and material
constraints without needing a provider-specific chat transcript or memory.

When a verified GitHub origin exists, use its issues and pull requests as the
shared execution, discussion, and review record. `PROJECT_STATE.md` is a
concise index and resume point: link the active issue or PR instead of
duplicating its backlog or conversation. Do not guess or create a remote. Add
new GitHub tracking only when it adds independent value and the requested scope
authorizes that external write.

Treat recorded state as a dated observation, not live truth. Reconcile it with
the current branch, commit, working tree, tests, and relevant external systems
before acting. Preserve unrelated work and surface discrepancies explicitly.

Update `PROJECT_STATE.md` in place after a material decision, verified result,
changed next action, or incomplete stopping point. Keep it concise and link to
plans, logs, issues, PRs, and durable decisions instead of copying them. Record
what was actually checked, when, and against which revision or environment.
Do not infer implementation, passing tests, deployment, or live outcomes from
a summary or timestamp alone.

For concurrent efforts, use one state file per independent workstream and list
each from the root state file. Record ownership, branch, and affected paths.
The lead maintains the root index; workers update only their assigned stream.
State files coordinate work but are neither locks nor authorization.

Record consequential user authorization with its source and exact scope.
Preserve valid approval across handoffs, recheck material preconditions, and
request new authorization only when scope or conditions materially change. A
completed one-time approval does not authorize repetition. Read back uncertain
external actions before retrying.

Keep secrets, credentials, signed URLs, private transcripts, and unnecessary
personal or customer data out of tracked state. Use safe evidence references.

## Orchestration

Keep instructions and continuity records usable by any capable LLM. The lead
owns scope, work allocation, integration, and final verification. Delegate
only bounded, independently useful work with explicit inputs, owned paths,
authorization limits, and acceptance evidence. Keep delegation flat and avoid
overlapping writers. Handle small tasks directly when delegation costs more
than it saves.

Use the active provider's installed model policy for model names and reasoning
effort. Choose the least costly supported role that can reach a verified result;
reserve stronger reasoning and independent review for consequential judgment.
Honor explicit user choices and documented project-specific exceptions. Do not
copy provider model mappings into this shared project-continuity block.
<!-- project-continuity:managed:end -->
