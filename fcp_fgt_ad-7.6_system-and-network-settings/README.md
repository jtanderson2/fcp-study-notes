# Section 01: System and Network Settings

## System Settings

- **Hostname Configuration**  
  Set a meaningful device name for easy identification in logs and dashboards.

- **Time Settings**  
  Configure NTP servers to ensure accurate system time, critical for log integrity and certificate validity.

- **Administrator Accounts**  
  Create admin profiles with role-based access control (RBAC) to enforce least privilege.

- **Dashboard Overview**  
  Monitor system health via widgets showing uptime, CPU/memory utilization, and license status.

## Network Settings

- **Interfaces**  
  Use physical, VLAN, and loopback interfaces to organize traffic and apply appropriate policies.

- **Zones**  
  Group interfaces into zones to simplify policy creation and improve readability.

- **DNS Settings**  
  Configure the FortiGate to act as a DNS forwarder or server; supports DNS over TLS/HTTPS.

- **Routing**  
  - Static routes: Define manual paths for known destinations.
  - Dynamic routing: Support for RIP, OSPF, and BGP for scalable route learning.

- **DHCP Services**  
  Use built-in DHCP server or relay to assign IP addresses dynamically within subnets.

## Best Practices

- Backup configurations before making changes.
- Restrict administrative access using trusted host IPs.
- Use descriptive names for interfaces and zones.
- Enable logging on system events and interface status changes.

