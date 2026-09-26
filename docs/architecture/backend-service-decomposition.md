# OceanMail Backend Logical Service Decomposition

Status: CURRENT architectural direction.

OceanMail hosted infrastructure should be designed as independent logical services with explicit APIs/data ownership, while allowing several or all services to run together on one VPS during early deployment. Scaling to separate VPSs/services must be a deployment change rather than an architectural rewrite.

## Logical service domains

1. **Internet mail conversion/gateway service** — conventional SMTP/Internet email ↔ OMail conversion and external Internet-mail handoff. OceanMail-operated hosted infrastructure is the public Internet-mail boundary; Stations are not arbitrary public Internet MTAs.
2. **Account / identity / authentication service** — hosted accounts, identity, credentials, enrollment, authorization, recovery, and related authoritative account state.
3. **Encrypted telemetry/log processing and reputation analytics** — ingest structured Station events, support abuse/AUP monitoring, relay/gateway contribution/reputation, reliability/network statistics, and operational analysis. At scale this may move to dedicated VPS/service infrastructure.
4. **Grid coordination and authoritative data publishing** — aggregate Station observations, maintain authoritative registries/selected network state, compute/publish permitted reputation or coordination data, and distribute signed Grid/region datasets.
5. **Software health, update, configuration, and dataset distribution** — Station software health, staged software updates, signed configuration/data releases, regional/Grid data files, and other operational datasets.
6. **Internal administrative/control plane** — operator tooling spanning the above services without becoming the sole source of component truth.

## What remains Station-owned

Do not centralize native OMail transport into the hosted backend. Stations own autonomous transport behavior including durable local transfer state/coordination, retries, acknowledgements/evidence, store-and-forward/relay execution, local mailbox/state where applicable, and enough Grid/routing/peer/gateway/region intelligence to continue useful native OMail operation while disconnected from OceanMail servers.

The hosted Grid service coordinates, aggregates, and publishes selected authoritative data; it does not become a mandatory real-time routing engine for native boat-to-boat OMail.

## Telemetry/logging boundary

Station telemetry synchronized to hosted infrastructure must be protected cryptographically in transit and by the accepted storage/security model at rest. Centralized telemetry is not merely debug output: it is input to reputation/contribution accounting, abuse detection, network health, reliability/statistics, and operational analysis.

Stations should retain durable telemetry locally until confirmed ingestion, then age/delete synchronized records according to policy. Detailed diagnostic/debug logs are a distinct category with bounded local retention and selective upload. Prefer structured events over shipping unbounded raw log files.

## Deployment consequence

Initial deployment may place these services on one VPS or a small number of VPSs. Service boundaries, APIs, data ownership, security boundaries, retention, and backup requirements should nevertheless remain explicit so individual domains can later be separated independently.

## Shared-data urgency boundary

Under [ADR-008](../decisions/ADR-008-four-band-scheduling-and-channel-use.md), the authoritative data/update services may designate urgent shared data for Band 1 instead of ordinary Band 3 background broadcast. Authenticate designation scope/freshness; preserve Station scheduling and its normal Band 1 cap. Promotion is not Emergency classification, route-establishment authority, or permission for an ordinary sender to buy priority. The service contract remains unimplemented.
