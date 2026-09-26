# Infrastructure Workstream

## Purpose

Provide reproducible, secure deployment and operations for OceanMail hosted services and future gateway infrastructure.

## Repository

`OceanMail/oceanmail-infrastructure`

## Current state

The active 0.2 repository is bootstrap-level and primarily defines its boundary. The historical infrastructure prototype contains useful deployment, PostgreSQL, backup, monitoring, and supply-chain lessons but is not current deployment authority.

OceanMail uses a dedicated GitHub organization. Shared self-hosted CI runners are organization-scoped infrastructure rather than repository-owned machines.

Private runner inventories and operational procedures are excluded from public documentation. Administrative exclusion of public repositories from trusted execution is an ongoing security requirement.

OceanMail-operated Server/infrastructure is the sole public SMTP/MX boundary. Internet-connected Stations and gateway Stations do not become independent public MTAs or deliver directly to arbitrary Internet SMTP systems. Native OMail remains decentralized and may continue without central Internet-mail infrastructure.

## Responsibilities

- environments and topology;
- CI/CD and release acceptance;
- GitHub Actions runner governance, runner-group access, and self-hosted runner lifecycle;
- DNS/TLS/network infrastructure;
- public SMTP/MX deployment, IP/reputation operations, and mail-boundary availability/recovery;
- monitoring/alerting;
- backup/restore/disaster recovery;
- secret-management boundaries and secret-free templates;
- deployment supply-chain controls;
- operational runbooks;
- deployment support for managed permanent OceanMail Stations/gateways;
- hosted-service layouts that allow independent logical services to begin co-located and later move to separate VPSs without architectural redesign.

## CI runner policy

- Register reusable OceanMail self-hosted runners at `OceanMail` organization scope by default.
- Use runner groups/repository access controls to limit which active repositories may consume them.
- Workflows should request required platform/capability labels, not a specific host name, unless machine affinity is deliberate. Public PR checks use GitHub-hosted runners.
- Repository-scoped registration is an exception for deliberate isolation, not the normal way to make a runner available to one component.
- Historical/frozen and public repositories must not consume persistent shared runners merely because they remain in the organization.
- Untrusted fork-PR code must not execute on a persistent self-hosted runner unless a stronger isolation model is deliberately introduced.
- Maintain one canonical runner service per intended runner identity and avoid stale duplicate repository-level registration/configuration.
- Docker access by the runner account is effectively root-equivalent on the VM and must be treated as privileged host access.
- Snapshot/revert is a persistence/recovery mechanism, not a live-job sandbox: it does not prevent a running job from attacking reachable network resources or exfiltrating credentials.
- Registration/removal tokens are ephemeral credentials and must never be committed or preserved in project documentation; exposed tokens must be replaced.

Public CI security requirements are recorded in `OceanMail/oceanmail-infrastructure/docs/CI-RUNNERS.md`.

## Deployment direction

Hosted Internet-side services will run on VPS infrastructure. The architecture deliberately separates Internet-mail conversion, account/identity/auth, encrypted telemetry/log analytics, Grid coordination/data publishing, software/update/config/data distribution, and internal admin concerns even when they initially share one host.

The initial permanent gateway is an owner-operated pilot; its specific location is private operational planning. Future institutional gateway candidates include yacht clubs, universities/maritime institutions, harbormasters, marinas, and similar maritime hosts. Permanent managed gateways use the same Station software as vessel Stations.

Outstanding public-mail deployment decisions include provider/hosting model, initial host count/geography, IP allocation/reverse DNS, reputation monitoring, failover/HA/recovery targets, and deployment of the authenticated Station/Server gateway service contract. These may evolve without changing the centralized public SMTP/MX authority defined by ADR-006.

## Constraints

- do not redefine product/application semantics to simplify deployment;
- do not commit live credentials/secrets/customer data;
- do not store GitHub runner registration/removal tokens or other ephemeral credentials in Git;
- avoid premature production-scale clustering;
- keep upstream communications dependencies explicit/pinned where deployment consumes them;
- hosted service and RF Station responsibilities remain separable;
- telemetry/log infrastructure must support encrypted ingestion, confirmed receipt before local purge, retention controls, and later separation to dedicated processing infrastructure if scale warrants it;
- permanent Station deployment must account for unattended operation, durable local storage, hard-power-loss recovery requirements, and bounded local queues/log/cache;
- keep CI runner network reachability least-privilege and document/verify the actual network isolation boundary before claiming it as an implemented security control;
- do not distribute public-SMTP relay credentials or public-MTA responsibilities to Stations as a deployment shortcut;
- central mail-boundary outages may delay Internet mail, but infrastructure design must not make native OMail dependent on central availability.
