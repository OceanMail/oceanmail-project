# ADR-007 — HF Link-Capacity Tiers and Survival Mode

Status: ACCEPTED
Date: 2026-09-14

## Context

OceanMail must schedule useful work across HF links whose delivered throughput can vary by more than an order of magnitude with propagation, modem mode, retransmission burden, and channel quality. Current project documentation intentionally does not preserve old point-in-time modem throughput figures as architectural truth, so the scheduler needs an explicit design assumption rather than inheriting historical measurements.

For current design work, OceanMail assumes that normally useful constrained HF links span approximately **0.1–3 kbps delivered throughput**. This is a scheduler/design range, not a claim that all supported modems or deployments will remain inside it.

Links below **0.1 kbps** are treated as degraded enough to require a distinct survival behavior.

## Decision

OceanMail will classify constrained-link capacity into operational tiers. Falling capacity progressively reduces which traffic is eligible or preferred rather than treating every message type equally.

Initial scheduler tiers are:

- **Tier 4 — >= 3 kbps:** unrestricted normal constrained-link operation. Ordinary mail, larger payloads, relay work, manifests, telemetry, OChat, and background synchronization may all be scheduled subject to normal policy.
- **Tier 3 — 1 to <3 kbps:** normal constrained operation. Most ordinary work remains eligible, while large/background objects receive lower preference.
- **Tier 2 — 0.3 to <1 kbps:** constrained mode. Prefer small ordinary messages, acknowledgements, manifests, receipts, control traffic, and high-value relay work. Large payloads normally wait unless explicitly selected or already substantially transferred.
- **Tier 1 — 0.1 to <0.3 kbps:** severe mode. Prefer small user mail, Emergency traffic, delivery evidence, tombstones/stop-transmit requests, routing/control state, and only unusually valuable relay work.
- **Tier 0 — <0.1 kbps:** survival mode. Minimize transmitted bytes and airtime while preserving the traffic required for safety, delivery progress, repair, and eventual network recovery.

These thresholds are initial policy values and may later be tuned from measured field evidence without changing the architectural principle.

## Survival-mode behavior

Survival mode does **not** mean local-only traffic and does **not** impose an absolute relay prohibition.

### Always or strongly eligible

- Emergency traffic when the Station is technically capable and legally/operationally permitted to assist.
- ACK/NACK and compact receipt/delivery evidence.
- Tombstones and stop-transmit requests.
- Minimal manifests and reconciliation/control state needed to prevent duplicate or wasted transmission.
- Minimal route/hop information required to keep the Grid functional.
- Very small locally originated or locally destined messages.
- Enough control traffic to allow normal operation to recover as link conditions improve.

### Normally suppressed or deferred

- OChat.
- Non-urgent telemetry that can wait.
- News/content feeds and other background content.
- Large attachments and large ordinary payloads.
- Speculative/background synchronization.
- Routine topology chatter beyond the minimum required for current forwarding decisions.
- Bulk accounting reconciliation that can safely wait for a better link.

## Survival-mode relay rule

Below 0.1 kbps, a Station should normally avoid accepting new ordinary relay payload, but relay remains eligible when withholding it would materially reduce the recipient's chance of delivery.

Examples of relay work that may remain eligible include:

1. Emergency traffic when the Station is technically capable and legally/operationally permitted to assist.
2. Traffic for a recipient that is directly reachable, or was recently reachable, through this Station.
3. A partially transferred message where completing the transfer is cheaper than abandoning and restarting elsewhere.
4. A very small message whose airtime cost is low.
5. Stranded or excessively aged traffic.
6. Traffic for which no plausible alternate route is currently known.

The intent is to prevent a degraded Station from becoming a bulk transit carrier while still allowing it to complete high-value deliveries that may otherwise fail.

## Scheduler principle

Capacity tier should primarily alter scheduler cost/eligibility rather than act only as a binary gate. As available throughput falls, **payload-size cost** and **relay cost** should increase sharply. This lets small, high-value traffic continue to move while large or speculative work naturally falls out of the schedule.

Emergency precedence remains governed by the existing Emergency/Ordinary decision. Capacity tier and an Emergency label do not themselves authorize transmission, unattended operation, or store-and-forward relay; the Station must also be technically capable and legally/operationally permitted to assist. This ADR does not create a new user-selectable priority class.

## Rationale

An absolute "no relay below 0.1 kbps" rule can make the Grid less useful precisely when propagation is poorest. Conversely, treating all queued work as equally eligible wastes scarce airtime on large, low-value, or deferrable traffic.

The selected model therefore uses **minimum airtime for maximum delivery value** as the survival objective while retaining enough control and repair traffic for the Grid to remain coherent.

## Consequences

- Station scheduling must eventually estimate or observe effective constrained-link throughput well enough to assign a capacity tier.
- Traffic classes and object sizes must be visible to the scheduler before transmission begins.
- Relay acceptance and scheduling policy must be able to distinguish ordinary bulk transit from high-value/stranded delivery opportunities.
- Control-plane encodings used in Tier 0 should be aggressively compact and avoid redundant chatter.
- Field testing may revise numeric boundaries and weighting functions, but should preserve the progressive-degradation model unless a later architecture decision supersedes it.

## Affected components

- OceanMail Station scheduler.
- GRID / CONTROL relay and route selection.
- STORE / TRANSPORT execution and transfer accounting.
- Manifest, receipt, tombstone, and reconciliation formats.
- Future field-testing and throughput instrumentation.
