# FortiGate 7.6 – Section 14: High Availability (HA)

## Overview

High Availability (HA) allows two or more FortiGate units to operate as a single logical unit. This ensures continuous availability of network services by providing automatic failover and configuration synchronization.

## HA Cluster Fundamentals

- HA clusters consist of one **primary unit** and one or more **secondary units**.
- The primary handles all management and traffic processing.
- Secondary units monitor the primary and assume control if it fails.
- HA operates as an **active-passive** or **active-active** configuration.

## HA Modes Explained

### Active-Passive (A-P)
- One unit is active; the other is standby.
- All traffic is processed by the primary.
- On failure, the secondary becomes the new primary using the same IPs and configuration.
- Provides stateful failover with minimal service disruption.

### Active-Active (A-A)
- All units process traffic concurrently.
- Requires UTM (Unified Threat Management) load balancing.
- Sessions are distributed based on a hash algorithm (e.g., source IP or destination port).
- More complex and resource-intensive, but scalable.

## Pre-requisites and Setup

- Same model and hardware version for all units.
- Identical firmware and VDOM configuration.
- Configured HA mode, group name, group ID, priorities, and heartbeat links.
- Optional—but recommended—use of a dedicated switch for HA heartbeat traffic.

## Cluster Role Selection

- Determined by the **device priority** (default 128, configurable).
- Tiebreaker: Uptime (longest uptime wins).
- Override mode allows manual control over master selection.
  - If override is enabled, the higher-priority unit always becomes primary after recovery.

## HA Interface Roles

- **Heartbeat Interfaces**: Synchronize state and monitor peer status.
- **Monitored Interfaces**: Interfaces watched for link failure.
  - Their failure can trigger HA failover.
- **Management Interface Reservation**: Assign management traffic to a dedicated port.

## Synchronization Details

- Config sync: Admin settings, firewall policies, objects, routes.
- State sync: Session tables, NAT mappings, UTM data.
- Sync is encrypted and uses the heartbeat link.
- Initial sync is a full push; subsequent syncs are delta-based.

## Split Brain and Loop Prevention

- Occurs when HA units lose communication but both assume the primary role.
- Avoid using:
  - Multiple isolated heartbeat links.
  - Redundant HA links with proper fail detection mechanisms.
- FortiGate uses heartbeat message counts and frequency for cluster decision logic.

## Monitoring and Failover Logic

- Devices send heartbeat messages every 200 ms (by default).
- Failure detection is triggered by:
  - Missed heartbeat threshold
  - Monitored interface down
  - Critical failure in routing/management daemon

## Upgrade and Maintenance

- FortiGate supports **rolling upgrades**:
  - Upgrade one unit while the other remains active.
  - Requires firmware versions to be compatible.
- Use **CLI or FortiManager** to coordinate firmware upgrades in HA mode.

## Management and Logging

### GUI
- Navigate to **System > HA** to:
  - View cluster members and roles.
  - Monitor synchronization status and uptime.
  - Force failover or shutdown secondary units.

### CLI Commands
- View HA status:
  ```bash
  get system ha status
  ```
- Force a failover:
  ```bash
  execute ha failover set 1
  ```
- Monitor heartbeat:
  ```bash
  diagnose sys ha status
  diagnose sys ha dump-by vcluster
  ```

## Best Practices

- Use two or more heartbeat interfaces on separate switches/VLANs.
- Configure interface monitoring for all critical links.
- Avoid configuring override unless deterministic master control is required.
- Perform regular failover testing in controlled maintenance windows.
- Monitor logs (`event.log`, `ha.log`) for state transitions and sync errors.

## Known Limitations

- Not all objects (e.g., some local certificates, FortiToken) are synced automatically.
- Some features (e.g., FortiExtender, dial-up IPsec) may have limitations in HA.
- HA is not supported in transparent mode without careful planning.
