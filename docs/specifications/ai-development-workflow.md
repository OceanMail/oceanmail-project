# OceanMail AI Development Workflow

Status: ACTIVE PROCESS

This specification defines the default division of responsibility among the human owner, Claude, ChatGPT, Git/GitHub, local development machines, and CI for OceanMail development work. It is an operating process, not product architecture.

Updated 2026-10-27: Claude replaced Codex as primary programmer. ChatGPT moved from day-to-day planner/director to a big-picture decision and occasional review role. Codex has no standing role. See `DECISIONS.md`.

## Authority

- The human owner is the final decision-maker for product direction, architecture, security/privacy, merge/release, regulatory, and safety-sensitive choices.
- Git/GitHub is the durable convergence point and authoritative project record.
- OceanMail's purpose, plan and mission are foundational. Accepted architecture changes only when needed, especially for law/regulation or verified technical limits (code, upstream, platform, hardware), through the architecture escalation gate. Claude may raise such changes; the owner decides, with or without ChatGPT.
- AI output is advisory or implementation work until reconciled into the repository and accepted through the normal project workflow.
- Passing tests or CI is implementation evidence, not permission to redefine architecture or proof that live product behavior was verified.

## Roles

### Claude — primary programmer

Claude is the default agent for OceanMail repository work, normally from the owner's Linux client/bash environment.

Use Claude for:

- feature implementation;
- maintenance, troubleshooting, and debugging;
- repository-wide changes and refactors;
- tests and CI repair;
- migrations;
- dependency/build changes;
- Git operations and PR preparation;
- applying concrete accepted review findings;
- keeping component status docs, `CURRENT_STATE.md`, workstreams, and active handoffs current with the work.

Within the settled architecture, Claude also plans its own bounded tasks from tracked issues and owner direction: it defines acceptance criteria, required tests, and non-goals before implementing.

Claude has architectural latitude. When it sees the need for an architecture change, it proposes the change to the owner using the escalation format. The owner and Claude may decide without ChatGPT. The decision is recorded in Git before implementation proceeds.

Claude should normally:

1. inspect the repository and relevant project/component documentation before editing;
2. implement against accepted requirements rather than inventing architecture;
3. preserve unrelated work;
4. run relevant tests, static checks, and integration checks available in scope;
5. investigate and fix regressions caused by its changes;
6. review its own actual diff and CI before handoff, and report assumptions, evidence, remaining gaps, and branch/PR state truthfully;
7. leave work in a reviewable state.

Claude may edit, test, commit, push, and prepare/update PRs within scope. Claude merges a PR only when the owner explicitly instructs it to merge that specific PR; otherwise the PR waits for the owner. One instruction does not authorize later merges. Claude's self-review is not independent review evidence.

### ChatGPT — big-picture decisions and independent review

ChatGPT is used when needed for:

- big-picture architecture or product decisions the owner wants a second view on (optional; the owner and Claude may decide without it);
- critique of a proposed architecture change raised through the escalation gate;
- independent bug-finding review of Claude's implementation or PR, at the owner's request.

ChatGPT is not a day-to-day planner or approval gate. Its findings are advisory until triaged under the review rules below.

### Codex — no standing role

Codex was the primary implementation agent until 2026-10-27. The owner may still assign it a specific task. Any such work follows the same branch/PR, evidence, and review rules.

### Independent review

An independent reviewer is anyone other than the session that authored the change: ChatGPT at the owner's request, or a separate Claude review session started with fresh context against the exact base/head. Independent review covers:

- architectural drift and omitted requirements;
- bugs, edge cases, and insufficient tests;
- security/integration problems, hidden coupling, and unintended consequences.

### Git/GitHub — durable convergence point

Git/GitHub preserve source code, authoritative documentation, decision history, PR review state, CI evidence, and merge history. Repository content and actual PR state take precedence over an agent's memory or self-report.

### Local development machines

Local development machines are the preferred place for interactive or hardware-dependent verification that cloud/sandbox environments cannot faithfully prove.

A local Debian/KDE environment provides interactive Linux Desktop verification. Use local environments when appropriate for:

- real Thunderbird GUI and profile/startup behavior;
- visual UX and native-chrome integration;
- local Docker/service labs;
- actual Station processes;
- future radio/hardware interaction.

A sandbox failure to launch a GUI is not evidence that the product code is broken if the same code can be isolated and verified elsewhere. Conversely, static review does not substitute for a live check when the requirement is visual, lifecycle-, platform-, or hardware-dependent.

### OceanMail organization self-hosted runners

Organization self-hosted runners are shared CI resources across OceanMail repositories, not dedicated interactive workstations for one component.

Rules:

- do not assume exclusive or immediate availability; queueing can be normal;
- keep self-hosted jobs bounded and use timeouts for potentially long-running work;
- prefer compact jobs over unnecessary parallel occupation of shared runners;
- clean up Docker containers, servers, browser/GUI processes, temporary daemons, and other persistent state even after failures;
- do not use a shared runner as a permanent interactive Thunderbird or hardware lab;
- run inexpensive deterministic checks locally before push when practical;
- do not claim Windows/macOS coverage from a Linux-only run.

## Default workflow

### 1. Task definition

Claude checks current Git truth and defines the task from the tracked issue or owner direction: intended behavior, affected boundaries, constraints, acceptance criteria, required evidence/tests, and explicit non-goals, all within the accepted architecture. Architecture questions go to the owner, who may decide with Claude alone or involve ChatGPT.

### 2. Architecture changes and optional critique

When a task needs an architecture change, Claude proposes it to the owner and they decide together. The owner may also ask ChatGPT to critique it. Its suggestions are not automatically accepted. They are reconciled against current repository truth, and the owner decides.

### 3. Task shape

An implementation-ready task should include, as applicable:

- objective;
- relevant authoritative files/specifications/ADRs;
- architecture that must remain intact;
- required behavior;
- acceptance criteria;
- required tests/evidence;
- integration points;
- non-goals;
- constraints the implementation must not redesign around.

Keep it concise; durable repository instructions already provide the architecture.

### 4. Implementation and verification

Claude implements in the Linux/bash development environment, runs relevant checks, fixes regressions, and reports the evidence obtained without overstating it.

### 5. Self-review against Git truth

Before handoff, Claude inspects the actual repository/PR:

1. confirm repository, branch, and HEAD;
2. inspect changed files/diff;
3. compare the change against accepted architecture and task acceptance criteria;
4. inspect CI status/logs where relevant;
5. distinguish tested facts from assumptions;
6. require live verification when the changed behavior cannot be proven by static/integration tests;
7. finish, issue a narrow correction, or escalate an architecture decision.

Implementation-agent confidence is not merge evidence by itself.

### 6. Optional independent review

For consequential changes, the owner may ask ChatGPT, or Claude may start a separate fresh-context review session, to review the implementation or PR for bugs, architectural drift, security/integration problems, requirement omissions, edge cases, and insufficient tests.

### 7. Review triage

Claude proposes a disposition for each finding, against accepted architecture and repository evidence:

- must fix;
- should fix;
- optional improvement;
- incorrect/not applicable;
- architectural question requiring owner decision.

The owner decides disputed findings and architectural questions. Claude implements accepted fixes. Findings are not blindly applied.

### 8. Live/product verification when required

When the requirement concerns actual UI, application startup/profile behavior, a live Station, RF/hardware, or other behavior that cannot be proven by unit/integration evidence, perform a live check in an appropriate environment before claiming completion.

For Desktop UI-affecting work, use this default visual QA loop:

```text
Claude
  -> implements
  -> launches the pinned Thunderbird/OceanMail Desktop build where practical
  -> captures affected surfaces/screenshots
  -> performs first-pass visual QA
  -> fixes obvious visual/interaction regressions

Independent reviewer (when consequential)
  -> reviews actual diff/CI
  -> reviews selected final screenshots/captures
  -> requires additional live verification when screenshots cannot prove the behavior

Owner
  -> provides final product judgment for consequential UX choices
  -> performs/observes live acceptance only when interaction, timing, feel, hardware,
     platform behavior, or another requirement cannot be established reliably otherwise
```

The owner does not need to manually inspect every minor visual change when Claude first-pass QA plus, for consequential changes, independent review provides sufficient evidence. Conversely, screenshots do not replace live verification for interaction, timing, focus, startup/profile lifecycle, platform behavior, hardware, or other runtime behavior that cannot be proven from a static capture.

Stale screenshots should not be retained as current product evidence. Retained visual evidence should identify the verified build/HEAD when practical.

### 9. Completion

A change is ready to advance when the required behavior and evidence are present, material accepted review findings are resolved, the implementation remains consistent with accepted OceanMail architecture, and the owner authorizes merge under the repository's workflow.

## Verification classes

Every substantial implementation/review handoff must distinguish three kinds of evidence.

### STATIC / UNIT

Examples: lint, unit tests, static/type checks, source-regression checks, build/package validation.

### INTEGRATION

Examples: Docker labs, SMTP/IMAP interaction, protocol/service integration, CI, bounded service tests.

### LIVE / PRODUCT

Examples: actual Thunderbird UI, real application startup/profile behavior, actual Station process, real RF/radio hardware, human visual/UX verification, and field behavior.

A green unit test or CI run must never be described as proof that a live GUI/hardware behavior was verified.

## Architecture escalation gate

When Claude sees the need for an architecture change, or discovers that an accepted design is impossible, materially unsafe, incompatible with upstream behavior, or likely to require a major architectural change, it must stop rather than quietly improvise, and bring the proposal to the owner.

Required escalation format:

```text
BLOCKED / ARCHITECTURAL DECISION REQUIRED

Observed:
Why current design is problematic:
Evidence:
Options:
Recommended option:
Affected repositories/files:
```

The owner and Claude resolve the question, with ChatGPT only when the owner wants it, and record the resulting decision before implementation resumes.

## Assignment and handoff shape

Recommended implementation assignment:

```text
TASK:
Repository:
Branch / starting HEAD:
Authority / required reading:
Objective:
Observed evidence / context:
Acceptance criteria:
Do not / non-goals:
Required validation:
Return:
```

Recommended completion handoff:

```text
Repository:
Branch:
Starting HEAD:
Ending HEAD:

Objective:
Root cause / implementation:
Files changed:

STATIC / UNIT:
- tests:
- lint/static:

INTEGRATION:
- labs/services:
- CI:

LIVE / PRODUCT:
- performed:
- not performed:

Architecture questions:
- NONE
or exact escalation

Outstanding gaps/blockers:
PR status:

Do not merge unless the owner explicitly instructs a merge of this PR.
```

## Cross-repository work

When a change spans Desktop, Station, Server, or Infrastructure:

- an unsettled service or contract boundary is proposed by Claude and decided by the owner before implementation;
- Claude may implement across multiple repositories when the task explicitly scopes that work;
- each repository's local instructions apply;
- API/contract changes must be documented at the authoritative boundary;
- do not solve a missing API by fabricating equivalent behavior in the wrong component;
- test each side separately and together where possible.

## Governing rules

- Established Git decisions take precedence over suggestions from any AI agent unless deliberately changed.
- Neither review text nor implementation by any agent silently changes architecture.
- Architectural changes should be recorded in the appropriate decision/specification documents before or with implementation.
- Small, obvious changes do not require an independent review pass.
- Consequential or cross-component changes should receive stronger independent review when it materially reduces risk, but review is advisory rather than an approval gate.
- When a reviewer and Claude disagree, the owner decides, using repository truth, tests/evidence, accepted decisions, and the owner's direction.
- Security, privacy, safety, and evidence-truthfulness constraints are architecture boundaries, not implementation conveniences.

## Operating principle

> The settled architecture sets direction. Claude implements and maintains. Claude proposes needed architecture changes and the owner decides. ChatGPT advises and reviews for bugs when asked. Git preserves. CI verifies deterministic behavior. Local/live environments verify reality. The owner retains final authority.

Implementation success, automated-test success, and actual product correctness are separate claims and must be evidenced separately.

## Scoped CI retrofit review requirement

For every PR in the [CI retrofit rollout](ci-quality-retrofit.md), independent review of the exact base/head by a reviewer other than the authoring session (a separate fresh-context Claude review session, or ChatGPT at the owner's request) is required, including governance and small changes. This overrides the optional implementation-review default only for this rollout. The reviewer provides findings and a recommendation, Claude proposes dispositions, the owner decides disputed ones, and the owner retains merge and branch-protection authority. No review or green check authorizes advancement beyond the assigned task.

