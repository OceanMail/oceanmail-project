# Station Deployment, Power, and Networking Requirements

Status: CURRENT design requirements reconciled from accepted Station discussions.

## Deployment roles

OceanMail-operated permanent gateways use the same OceanMail Station software as vessel Stations. There is no separate gateway product. A permanent gateway is a Station provisioned for continuous gateway service with reliable power, Internet backhaul, radio, antenna, and managed configuration.

The initial permanent Station is an owner-operated pilot; its specific location is private operational planning. Later institutional sites may include a yacht club, university, harbormaster, marina, or similar maritime host. Wider deployment through yacht clubs/harbors is a candidate growth path after unattended operation is proven.

## Hardware profiles

The software must not require one hardware SKU. Two reference profiles are intended:

- **Marine / owner Station:** low-power, passively cooled ARM64 SBC class, with Ethernet, USB, Wi-Fi, and sufficient durable storage. Orange Pi-class hardware is a candidate, not a frozen vendor requirement.
- **Permanent / institutional gateway:** fanless x86-64 thin client or N100-class system with Ethernet, multiple USB ports, replaceable SSD storage, and simple Debian-class support. Used enterprise thin clients are acceptable where reliable.

Storage capacity is secondary to durability. Permanent Internet-connected gateways are primarily transit nodes, not long-term mailbox archives; local queue/log/cache storage should be bounded and cleared after authoritative synchronization/acknowledgement. 32–64 GB durable SSD-class storage is expected to be ample for normal gateway operation, subject to measured queue/outage requirements.

## Local service network

A Station may provide its own Wi-Fi access point for local OceanMail clients when the vessel LAN or Internet AP is unavailable.

This WLAN is an **OceanMail service network, not an Internet router**:

- no general-purpose NAT or Internet forwarding;
- intended services are OMail, OChat, Station management/status, and explicitly authorized Station APIs;
- it must not compete with or replace the vessel router.

Preferred topology when Ethernet exists:

```text
radio <-> USB <-> Station <-> Ethernet <-> vessel LAN / Internet
                         \
                          +-- Wi-Fi AP <-> OceanMail clients
```

When Wi-Fi is the only upstream path, Station networking must support configurable behavior:

- Wi-Fi AP mode for local OMail/OChat/management while disconnected;
- Wi-Fi client/STA mode for joining Starlink, marina Wi-Fi, or another upstream AP;
- concurrent AP+STA only where the selected radio/driver is proven reliable;
- otherwise role switching is an acceptable fallback;
- a second supported USB Wi-Fi adapter may be used to dedicate one radio to backhaul and one to the local OceanMail AP.

Do not assume a specific SBC's built-in radio supports simultaneous AP+STA. Hardware qualification must test the actual Linux driver/interface combination.

## Power-loss behavior

Routine hard power removal is a normal marine operating condition. Many installations will place the Station power supply behind a physical switch.

Therefore:

- users must not be required to perform an OS/software shutdown before switching power off;
- durable state and queues must survive abrupt power loss;
- writes must be transactional/crash-safe where applicable;
- critical state must not exist only in volatile memory;
- interrupted writes must recover automatically;
- ordinary switch-off must not be expected to require manual filesystem repair;
- after power restoration, the Station must boot and automatically resume service, queue recovery, and communications work.

Prefer eMMC/SSD or other robust storage over inexpensive microSD where practical. Filesystem/database choices and write patterns must be evaluated for repeated unclean shutdowns.

## Low-power behavior

The Station is fundamentally an always/frequently-on communications appliance. Deep suspend is not a baseline requirement if it prevents radio listening, local client access, queue work, or connectivity detection. Power optimization should focus on low idle draw, CPU frequency scaling, disabling unused peripherals, bounded logging/writes, and optional control of radio/peripheral power where useful.

## Open qualification work

- choose and qualify one low-cost ARM64 reference platform;
- choose and qualify one fanless x86-64 permanent-gateway reference platform;
- verify Wi-Fi AP behavior, client-mode failover, and any concurrent AP+STA behavior on real hardware;
- test repeated hard power removal/recovery under active queue/database writes;
- establish measured idle and active power budgets;
- validate RF/USB isolation and reliability with actual ICOM-class radio hardware.

