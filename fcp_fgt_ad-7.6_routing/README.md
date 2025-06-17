# FortiGate 7.6 – Section 3: Routing

## Routing Overview

- Determines best path for traffic to reach destination.
- FortiGate uses a routing table to evaluate possible routes.
- Types of routing:
  - Static Routing
  - Policy-Based Routing (PBR)
  - Dynamic Routing (RIP, OSPF, BGP)

## Static Routing

- Manually define routes for fixed destinations.
- Command line: `config router static`
- Requires:
  - Destination subnet
  - Next-hop IP or interface
- Administrative distance defaults to 10.

### Default Route

- Route for all unmatched traffic: `0.0.0.0/0`
- Typically used to forward to the internet gateway.

### Black Hole Routes

- Used to silently drop traffic to specific destinations.
- Prevent routing loops and DoS attacks.

## Policy-Based Routing (PBR)

- Overrides routing table decisions based on policy.
- Criteria can include:
  - Source address
  - Destination address
  - Service/port
  - Interface
- Often used to control routing for specific applications or users.

## Dynamic Routing Protocols

### RIP (Routing Information Protocol)

- Distance vector protocol
- Max hop count: 15
- Suitable for small networks

### OSPF (Open Shortest Path First)

- Link-state protocol
- Fast convergence and hierarchical areas
- Suitable for medium to large networks

### BGP (Border Gateway Protocol)

- Path-vector protocol
- Used for inter-AS routing
- Supports policies and prefix filtering

## Route Selection

- Route decision process:
  1. Longest prefix match (most specific route)
  2. Lowest administrative distance
  3. Lowest metric (cost)
- Equal-cost routes can be load balanced.

## Route Monitoring and Failover

- Detect link failures and trigger route changes.
- Methods:
  - Link status monitoring
  - Dead gateway detection
  - SLA-based route health check (e.g., ping tests)

## Routing Table Inspection

- View routing table:
  - GUI: Network > Static Routes
  - CLI: `get router info routing-table all`
- Dynamic routes: Use `get router info` with protocol filter

## Best Practices

- Use static routes for predictable paths and simple networks.
- Use dynamic routing for scalability and automatic updates.
- Regularly review routing table for outdated or conflicting entries.
- Combine PBR carefully with dynamic/static routes to avoid conflicts.

## Troubleshooting Tools

- `diagnose ip route list`: Display current routing table
- `traceroute`: Path analysis to a destination
- `ping`: Test reachability of a host
- `get router info bgp/ospf/rip`: Protocol-specific diagnostics
