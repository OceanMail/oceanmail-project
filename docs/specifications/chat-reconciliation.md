# Conversation-to-Git Reconciliation Procedure

Status: ACTIVE PROCESS

Use this procedure before deleting or retiring an OceanMail ChatGPT/Codex/Claude conversation.

## Goal

Extract durable project knowledge that is missing from Git without turning Git into a transcript archive.

## Procedure

1. Read this project's `PROJECT.md`, `CURRENT_STATE.md`, `DECISIONS.md`, `REPOSITORIES.md`, relevant workstream/ADR/interface docs, and the owning component repository docs/source.
2. Review the conversation for information not already represented in Git.
3. Classify each useful item as one of:
   - current architecture/definition;
   - decision/clarification/rationale;
   - current implementation/workstream state;
   - cross-component contract/interface;
   - component-specific implementation knowledge;
   - unresolved question/risk;
   - historical rationale;
   - temporary active handoff state.
4. Write each item to its authoritative home:
   - organization-wide → `oceanmail-project`;
   - component-specific → owning component repository;
   - temporary current work → scoped `handoffs/` entry, with permanent knowledge also placed in normal docs.
5. Reconcile conflicts. Do not preserve both as equally current; mark supersession/history explicitly.
6. Update `CURRENT_STATE.md` only for material current-state changes; do not append diary entries.
7. Add small settled semantics to `DECISIONS.md`; create/update an ADR for major architecture decisions.
8. Update `REPOSITORIES.md`, terminology, interfaces, or workstream docs only if the conversation materially changes them.
9. Verify links and ensure no important decision exists only in the conversation or handoff.
10. Record the reconciliation in Git through the repository's normal workflow.

## Temporal precedence and retired-thread safety

Conversation age is evidence about authority. A retired conversation must never become newer project truth merely because its reconciliation commit is newer.

Apply these rules whenever reconciling old or uncertain-age threads:

- **Current Git wins over older chat.** If current project-spine, component `main`, merged decisions, tests, or accepted implementation evidence postdate a conversation decision, preserve the newer Git truth and classify the chat material as superseded/history if it is still useful.
- **A new reconciliation commit does not reset the decision date.** Preserve the original decision/event date where known. Do not use today's reconciliation date to make an old idea appear newly accepted.
- **Default uncertain legacy material downward, not upward.** If an old thread contains a plausible requirement that is not corroborated by current authority and its acceptance status cannot be established, record it as HISTORICAL, RESEARCH, CANDIDATE, or UNRESOLVED. Do not label it ACTIVE/CURRENT.
- **Promotion to current truth requires evidence.** Chat-only material may become ACTIVE/CURRENT only when it is clearly a later owner/project decision than the Git material it changes, or when it is strictly additive and demonstrably compatible with current architecture. The reconciliation should preserve enough provenance/rationale to establish that basis.
- **Do not reopen superseded architectures by implication.** Historical BEMPIC/M4P/OMGP, 0.1, old Priority semantics, old product splits, prototype server/infrastructure behavior, or other retired designs remain non-authoritative unless a new explicit architecture decision reactivates them.
- **Research stays research.** Historical protocol, hardware, regulatory, modem, routing, frequency, or interoperability findings may be retained for future evaluation, but their presence in Git does not put them on the implementation critical path.
- **Implementation evidence outranks recollection.** Where an old conversation conflicts with merged code/tests/current component status, do not overwrite the implementation truth without an explicit current decision explaining why it is being changed.
- **When chronology is unclear, do not guess.** Record the conflict or candidate separately and leave current truth unchanged pending deliberate review.

Before changing `PROJECT.md`, `CURRENT_STATE.md`, an ACTIVE entry in `DECISIONS.md`, or a CURRENT ADR/specification from a retired thread, explicitly perform this temporal-precedence check.

## What not to do

- Do not paste raw chat transcripts into Git.
- Do not copy implementation docs into the project spine when a component repository owns them.
- Do not treat an AI suggestion as accepted architecture merely because it appeared in a long thread.
- Do not rewrite history to make an old design look current.
- Do not promote an unresolved idea into a decision.
- Do not treat the timestamp of a reconciliation commit as the timestamp or authority of the underlying decision.

## Completion check

Ask: if this conversation vanished now, would a new capable contributor know the current truth, the settled decision, and the next active step from Git alone? If not, reconciliation is incomplete.

Then ask the inverse safety question: if this conversation were from an obsolete development phase, did this reconciliation change any current truth solely because the old chat said so? If yes, correct the reconciliation before considering it complete.
