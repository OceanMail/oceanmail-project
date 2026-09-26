# OceanMail AI Development Workflow

Status: ACTIVE PROCESS

This specification defines the default division of responsibility among the human owner, ChatGPT, Codex, Claude, Git/GitHub, local development machines, and CI for OceanMail development work. It is an operating process, not product architecture.

## Authority

- The human owner is the final decision-maker for product direction, architecture, security/privacy, merge/release, regulatory, and safety-sensitive choices.
- Git/GitHub is the durable convergence point and authoritative project record.
- AI output is advisory or implementation work until reconciled into the repository and accepted through the normal project workflow.
- Passing tests or CI is implementation evidence, not permission to redefine architecture or proof that live product behavior was verified.

## Roles

### ChatGPT — primary architect, designer, planner, and director

ChatGPT owns cross-repository architectural continuity and the default planning/directing role for OceanMail work.

Responsibilities include:

- defining and maintaining system architecture and product behavior;
- reconciling new work with accepted project decisions and repository truth;
- decomposing work into bounded implementation tasks;
- defining constraints, acceptance criteria, required tests, and non-goals;
- preparing implementation-ready Codex handoffs;
- independently reviewing actual Git/PR/CI state rather than accepting an implementation-agent handoff at face value;
- deciding when an independent Claude architecture/review pass is useful;
- evaluating Claude review findings and deciding which suggestions should be adopted;
- directing accepted follow-up implementation work;
- identifying when a proposed implementation would silently redefine architecture.

ChatGPT may proactively ask Claude to critique an architectural decision and suggest improvements. Claude's response is advisory input; ChatGPT remains the primary architect/designer and is responsible for reconciling accepted suggestions with existing Git truth before implementation.

### Codex — primary implementation/coding agent

Codex is the default agent for actual repository implementation work, normally from the Linux client/bash environment.

Use Codex for:

- feature implementation;
- repository-wide changes and refactors;
- debugging;
- tests and CI repair;
- migrations;
- dependency/build changes;
- Git operations and PR preparation;
- applying concrete accepted review findings.

Codex should normally:

1. inspect the repository and relevant project/component documentation before editing;
2. implement against explicit requirements rather than inventing architecture;
3. preserve unrelated work;
4. run relevant tests, static checks, and integration checks available in scope;
5. investigate and fix regressions caused by its changes;
6. report assumptions, evidence, remaining gaps, and branch/PR state truthfully;
7. leave work in a reviewable state.

Codex may edit, test, commit, push, and prepare/update PRs within the assigned scope. Codex does not merge by default; merge requires owner authorization under the owning repository's workflow.

### Claude — supporting architecture/review agent and independent critic

Claude is used for independent critique and review, including:

- second opinions on architecture;
- identifying risks, alternatives, and missing considerations;
- design/specification critique;
- consequential implementation/PR review;
- integration-risk analysis;
- detection of architectural drift, omitted requirements, hidden coupling, insufficient tests, or unintended consequences.

Claude does not own OceanMail architecture and is not a competing source of truth or mandatory approval layer. Claude should review against the accepted architecture unless explicitly asked to explore redesign alternatives.

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

### 1. Design and planning

The owner and ChatGPT establish or update the design. ChatGPT checks current Git truth and defines the intended behavior, affected boundaries, constraints, acceptance criteria, required evidence/tests, and explicit non-goals.

### 2. Optional independent architecture critique

When useful, ChatGPT asks Claude to review the proposed decision for risks, alternatives, missing considerations, and possible improvements.

Claude's suggestions are not automatically accepted. ChatGPT reconciles them against current repository truth and the owner's direction, then updates the design or rejects the suggestion explicitly as appropriate.

### 3. Implementation handoff

ChatGPT gives Codex an implementation-ready task that should include, as applicable:

- objective;
- relevant authoritative files/specifications/ADRs;
- architecture that must remain intact;
- required behavior;
- acceptance criteria;
- required tests/evidence;
- integration points;
- non-goals;
- constraints Codex must not redesign around.

The handoff should normally be concise because Codex can inspect the repository directly; do not restate the entire project architecture when durable repository instructions already provide it.

### 4. Implementation and verification

Codex implements in the Linux/bash development environment, runs relevant checks, fixes regressions, and reports the evidence obtained without overstating it.

### 5. Independent project-lead review

After Codex returns a handoff, ChatGPT should inspect the actual repository/PR when possible:

1. confirm repository, branch, and HEAD;
2. inspect changed files/diff;
3. compare the change against accepted architecture and task acceptance criteria;
4. inspect CI status/logs where relevant;
5. distinguish tested facts from agent claims;
6. require live verification when the changed behavior cannot be proven by static/integration tests;
7. accept, issue a narrow correction, or escalate an architecture decision.

Implementation-agent confidence is not merge evidence by itself.

### 6. Optional independent implementation review

For consequential changes, ChatGPT may ask Claude to review the implementation or PR for architectural drift, security/integration problems, requirement omissions, edge cases, and insufficient tests.

### 7. Review triage

ChatGPT evaluates review findings against accepted architecture and repository evidence. Findings should be treated as one of:

- must fix;
- should fix;
- optional improvement;
- incorrect/not applicable;
- architectural question requiring owner decision.

Codex implements accepted code/documentation fixes. Claude findings are not blindly applied.

### 8. Live/product verification when required

When the requirement concerns actual UI, application startup/profile behavior, a live Station, RF/hardware, or other behavior that cannot be proven by unit/integration evidence, perform a live check in an appropriate environment before claiming completion.

For Desktop UI-affecting work, use this default visual QA loop:

```text
Codex
  -> implements
  -> launches the pinned Thunderbird/OceanMail Desktop build where practical
  -> captures affected surfaces/screenshots
  -> performs first-pass visual QA
  -> fixes obvious visual/interaction regressions

ChatGPT
  -> independently reviews actual diff/CI
  -> reviews selected final screenshots/captures
  -> requires additional live verification when screenshots cannot prove the behavior

Owner
  -> provides final product judgment for consequential UX choices
  -> performs/observes live acceptance only when interaction, timing, feel, hardware,
     platform behavior, or another requirement cannot be established reliably otherwise
```

The owner does not need to manually inspect every minor visual change when Codex first-pass QA plus independent ChatGPT review provides sufficient evidence. Conversely, screenshots do not replace live verification for interaction, timing, focus, startup/profile lifecycle, platform behavior, hardware, or other runtime behavior that cannot be proven from a static capture.

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

When Codex discovers that an accepted design is impossible, materially unsafe, incompatible with upstream behavior, or likely to require a major architectural change, it must stop rather than quietly improvise.

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

The owner and ChatGPT resolve the question and record the resulting decision before implementation resumes.

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

Recommended Codex completion handoff:

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

Do not merge unless explicitly authorized.
```

## Cross-repository work

When a change spans Desktop, Station, Server, or Infrastructure:

- ChatGPT defines/reconciles the service or contract boundary before implementation;
- Codex may implement across multiple repositories only when the assignment explicitly scopes that work;
- each repository's local instructions apply;
- API/contract changes must be documented at the authoritative boundary;
- do not solve a missing API by fabricating equivalent behavior in the wrong component;
- test each side separately and together where possible.

## Governing rules

- Established Git decisions take precedence over suggestions from any AI agent unless deliberately changed.
- Neither Claude review text nor Codex implementation silently changes architecture.
- Architectural changes should be recorded in the appropriate decision/specification documents before or with implementation.
- Small, obvious changes do not require an independent Claude pass.
- Consequential or cross-component changes should receive stronger independent review when it materially reduces risk, but Claude is advisory rather than an approval gate.
- When Claude and Codex disagree, ChatGPT reconciles the disagreement using repository truth, tests/evidence, accepted decisions, and the owner's direction.
- Security, privacy, safety, and evidence-truthfulness constraints are architecture boundaries, not implementation conveniences.

## Operating principle

> ChatGPT designs and directs. Codex implements. Git preserves. CI verifies deterministic behavior. Local/live environments verify reality. Claude independently critiques when warranted. The owner retains final authority.

Implementation success, automated-test success, and actual product correctness are separate claims and must be evidenced separately.

## Scoped CI retrofit review requirement

For every PR in the [CI retrofit rollout](ci-quality-retrofit.md), independent Claude review of the exact base/head is required, including governance and small changes. This overrides the optional implementation-review default only for this rollout. Claude provides findings and a recommendation, ChatGPT triages, and the owner retains merge and branch-protection authority. No review or green check authorizes advancement beyond the assigned task.

