# FortiGate 7.6 – Section 02: Firewall Policy and NAT

## Firewall Policies

### Policy Basics

- Control traffic flow between interfaces based on source, destination, service, and schedule.
- Policies are unidirectional (e.g., LAN to WAN).
- Evaluated in top-down order; first match is applied.
- Policy actions: Accept, Deny, SSL Inspection, Logging.

### Key Components

- **Source/Destination**: IP addresses or address groups.
- **Service**: Defines allowed ports/protocols.
- **Schedule**: Always or custom timeframes.
- **Action**: Accept (allow), Deny (block), Learn (with FSSO).

### Logging Options

- Log allowed or denied traffic.
- Options:
  - All sessions
  - Security events
  - UTM features (IPS, AV, etc.)
- Logs stored locally or sent to FortiAnalyzer/Syslog.

### Policy Interfaces

- Each policy defines source and destination interfaces.
- Interface pairs must match traffic direction.

## NAT (Network Address Translation)

### Types of NAT

- **Source NAT (SNAT)**:
  - Hides internal IPs behind public IPs.
  - Use cases: Internet access from internal users.
  - Methods:
    - Use outgoing interface address
    - Use IP pool

- **Destination NAT (DNAT)**:
  - Redirects inbound traffic to internal servers.
  - Common for hosting services (e.g., web servers).

### IP Pools

- Define external IPs used in NAT.
- Types:
  - Overload (PAT): Many-to-one
  - One-to-one: Each internal IP has a fixed external IP
  - Fixed port: Preserve source port if possible

### Central NAT

- Centralized NAT management in one table.
- Enabled globally; overrides NAT settings in firewall policies.
- More scalable and consistent.

## Policy Matching and Inspection

- Traffic inspected only if it matches a policy.
- Policy match checks:
  - Source & destination interfaces
  - Source & destination addresses
  - Services and schedule
- Additional options:
  - Deep packet inspection
  - SSL/SSH inspection
  - Application control

## Best Practices

- Place more specific policies above general ones.
- Minimize use of “ALL” objects for better security.
- Enable logging for visibility and troubleshooting.
- Regularly review and clean up unused policies.

## Troubleshooting Tools

- **Policy Lookup**: GUI or CLI (`diagnose firewall iprope`)
- **Session List**: View active sessions (`diag sys session list`)
- **Packet Capture**: Use built-in sniffer (`diag sniffer packet`)
