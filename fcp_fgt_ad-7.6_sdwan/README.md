# FortiGate 7.6 – Section 12: SD-WAN

## Overview

Software-Defined WAN (SD-WAN) enables FortiGate to combine and intelligently manage multiple WAN links under a single virtual interface. It dynamically steers traffic based on link performance, application needs, and business intent policies, ensuring optimized bandwidth usage, improved application experience, and link redundancy.

## SD-WAN Architecture

FortiGate abstracts physical WAN links into logical SD-WAN members. Traffic is steered using SD-WAN rules based on criteria like source/destination, applications, SLA metrics, and cost.

## Key SD-WAN Components

### 1. SD-WAN Members
- Physical or virtual interfaces (e.g., `wan1`, `wan2`, IPsec).
- Must be added to the SD-WAN virtual interface.
- Each member is monitored for health and availability.

### 2. SD-WAN Zones
- Group SD-WAN members logically.
- Simplifies policy creation by referencing zones rather than interfaces.
- Enables inter-zone and intra-zone policies with clarity.

### 3. Performance SLAs
- Use synthetic probes to track link health:
  - Probe types: `ping`, `HTTP`, `DNS`, `TCP echo`
  - Measured metrics: latency (ms), jitter (ms), packet loss (%)
- SLAs are used by SD-WAN rules to select the best-performing link.

### 4. SD-WAN Rules
- Define traffic steering logic:
  - Matching criteria: source IP, destination IP, application, ports, user group
  - Link selection strategy: 
    - `Manual`: Always prefer specific interface
    - `Best Quality`: Uses SLA metrics
    - `Lowest Cost`: Uses configured link costs
    - `Maximum Bandwidth`: Based on interface capacity

### 5. Application Awareness
- FortiGate uses DPI (Deep Packet Inspection) to identify application-level traffic.
- Combined with SD-WAN rules to route critical applications over better-performing or lower-cost paths.

## Load Balancing and Failover

### Load-Balancing Algorithms
- **Volume-based**: Based on byte/packet volume.
- **Session-based**: Round-robin by sessions.
- **Quality-based**: Chooses link with best SLA compliance.

### Failover
- SD-WAN monitors links in real-time.
- If SLA thresholds are exceeded, traffic is rerouted to backup links.
- Ensures automatic failover with minimal disruption.

## Configuration Workflow

1. **Enable SD-WAN**: Create SD-WAN interface and add member interfaces.
2. **Define Performance SLAs**:
   - Set targets (e.g., `8.8.8.8`) and thresholds (e.g., 100ms latency).
3. **Create SD-WAN Rules**:
   - Use application- or IP-based matching.
   - Choose link preference strategy.
4. **Policy Creation**:
   - Use SD-WAN zones in firewall policies for granular control.

## Monitoring and Logging

### GUI Tools
- **Network > SD-WAN > Monitor**:
  - Displays real-time link performance metrics.
  - Shows SLA status and link usage.
- **FortiView Dashboards**:
  - Traffic by application, SLA compliance, rule hits.

### CLI Commands
- View link health:
  ```bash
  diagnose sys virtual-wan-link health-check
  ```
- Display rule matches:
  ```bash
  diagnose sys virtual-wan-link service
  ```
- Log performance issues:
  ```bash
  diagnose sys virtual-wan-link log
  ```

## Best Practices

- Always configure multiple heartbeat targets per SLA for accuracy.
- Use `Best Quality` for real-time applications like VoIP.
- Apply `Lowest Cost` or `Manual` for non-critical or high-bandwidth traffic.
- Use application-based rules for fine-grained control.
- Define SD-WAN zones to simplify policy references.

## Troubleshooting Tips

- Use `diag sys virtual-wan-link intf` to verify interface roles and status.
- Ensure SLAs are reachable and respond to probes.
- Monitor FortiView and logs for route flapping or policy misfires.
- Adjust thresholds based on link characteristics (e.g., higher jitter on cellular links).
