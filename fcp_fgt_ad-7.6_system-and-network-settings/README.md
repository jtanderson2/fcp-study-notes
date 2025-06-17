# FortiGate 7.6 – System and Network Settings

## Initial Setup

- **Default Access**:
  - IP: `192.168.1.99/24`
  - Port: `port1` or `internal` on entry-level models
  - Default login: `admin` (blank password)
- **Initial Configuration**:
  - Change default password immediately
  - Set hostname, configure dashboard, register with FortiCare
- **Access Methods**:
  - GUI: https://192.168.1.99
  - CLI: Console port, USB, or terminal emulator (e.g., PuTTY)

## Network Interface Configuration

- **IP Assignment Methods**:
  - Manually assigned
  - DHCP
  - PPPoE
- **Interface Roles**:
  - LAN, WAN, DMZ, Undefined
  - Roles control GUI options visibility
- **Aliases**: Descriptive names for interfaces, used in policies

## VLANs

- Subdivide Layer 2 networks into broadcast domains
- Tagged Ethernet frames identify VLANs
- Native VLANs remain untagged
- Use 802.1Q (standard VLAN) or 802.1ad (QinQ stacking)

## Routing

- **Default Gateway**:
  - Set via DHCP/PPPoE or manually (static route)
- Required for:
  - Internet access
  - FortiGuard services
- Static route example: Destination `0.0.0.0/0` to next-hop router

## Virtual Domains (VDOMs)

- Create isolated virtual FortiGate instances
- Independent routing, policies, and admin access
- Up to 10 VDOMs by default, more on high-end models

## Basic Administration

### Access Methods

- GUI (HTTP/HTTPS)
- CLI (Console/SSH)
- FortiManager (FGFM protocol)
- REST API (Ansible, Terraform)

### Administrator Accounts

- Create separate accounts for each admin
- Authentication options:
  - Local password
  - Remote server (LDAP, RADIUS)
  - Certificate-based
- Use strong, complex passwords

### Admin Profiles

- Control permissions for each admin
- Default profiles:
  - `super_admin`: Full system access
  - `prof_admin`: Full VDOM access, no global access
- Custom profiles for specific roles (e.g., read-only)

### Trusted Hosts and Security

- Restrict admin login by source IP (trusted hosts)
- Default: `0.0.0.0/0` allows any IP
- Customize administrative protocol ports
- Use secure protocols (HTTPS, SSH)

### Management Protocols

- Enable/disable protocols per interface:
  - HTTPS, SSH, PING (default enabled)
  - HTTP not shown in GUI by default
- Consider exposure risks (e.g., disable PING on WAN)

## Fundamental Maintenance

### Configuration Backup and Restore

- Backup options:
  - Manual
  - On logout (not on all models)
- Encryption:
  - Encrypted backups need same model/firmware and password
  - Password-masked option for safer sharing
- Restore causes device reboot

### Firmware Upgrade

- Check version via dashboard or CLI (`get system status`)
- Use System > Firmware & Registration to upgrade
- Consult FortiOS Release Notes for proper upgrade paths

### FortiGuard Services

- Provides updates (AV, IPS, web filter, etc.)
- Internet connection and valid contract required
- Uses TCP (443) and optionally DNS over TLS (DoT)
- Uses anycast routing and OCSP stapling for server validation

### License and Updates Verification

- Check license status and installed versions in GUI
- Use CLI: `diagnose autoupdate versions`
- Lists engine versions, last update times, and expiry dates
