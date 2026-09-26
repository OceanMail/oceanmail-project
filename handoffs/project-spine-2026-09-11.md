# Project Spine Implementation Handoff — 2026-09-11

Status: INITIAL SPINE IMPLEMENTATION COMPLETE

## Objective

Establish `OceanMail/oceanmail-project` as durable organization-level project memory, repoint active component repositories to it, and prepare the organization for conversation-by-conversation reconciliation before old chat history is deleted.

## Completed

- inspected every repository in the OceanMail organization and classified active versus historical/frozen;
- established `PROJECT.md`, `CURRENT_STATE.md`, `DECISIONS.md`, `AGENTS.md`, `REPOSITORIES.md`, project ADRs, system/interface/terminology/history documentation, workstream summaries, scoped handoff conventions, and conversation reconciliation procedure;
- centralized organization-level authority in `OceanMail/oceanmail-project`;
- preserved component-local implementation documentation rather than copying it into the spine;
- updated Desktop, Station, Server, and Infrastructure documentation/agent instructions to point to the central spine;
- explicitly marked Desktop Decision 0001's former program-authority assignment superseded;
- corrected Station `CURRENT_STATUS.md` to reflect the accepted Available foundation;
- integrated the project spine into Desktop, Station, Server and Infrastructure;
- replaced the component-specific governance proposal with the central governance model;
- left historical/frozen 0.1 and BEMPIC repositories intact because they are already clearly labeled and remain useful evidence.

## Current authority model

- `OceanMail/oceanmail-project` — organization-wide definition, architecture, terminology, decisions, repository inventory, current state, workstreams, governance, and reconciliation process.
- active component repositories — source code and component-specific implementation documentation/evidence.
- historical/frozen repositories — history/research only unless material is deliberately reconciled forward.

## Next phase

Run the existing OceanMail conversation threads through [`docs/specifications/chat-reconciliation.md`](../docs/specifications/chat-reconciliation.md).

Each thread should identify durable decisions/context missing from Git and place them in the correct authoritative repository. Do not paste raw transcripts or recreate already-documented facts.

When that reconciliation phase is complete, this handoff can be archived/deleted after any remaining durable information has been absorbed into normal project documents.

## Completion test for this phase

A new contributor with GitHub access only can now determine the current project definition, active repositories, major architecture, HERMES/Mercury transition, current Station/Desktop state, historical/frozen paths, authority/read order, and where to put future decisions. The remaining risk is intentionally the next reconciliation phase: chat-only decisions not yet captured in Git.