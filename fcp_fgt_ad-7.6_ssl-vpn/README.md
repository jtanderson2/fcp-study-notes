# FortiGate 7.6 – Section 10: SSL VPN

## Overview

SSL VPN allows secure remote access to internal network resources using a web browser or client application. It uses TLS/SSL encryption to protect data over the internet.

## SSL VPN Modes

### 1. Web Mode
- Access internal web applications via browser.
- Limited to HTTP/HTTPS, FTP, SMB, RDP via web proxy.
- No need to install VPN client.

### 2. Tunnel Mode
- Uses FortiClient software.
- Provides full network access as if the user were on the LAN.
- Supports all TCP/UDP traffic.

## Authentication and Access

- Supports local users, LDAP, RADIUS, and multifactor authentication (MFA).
- User groups mapped to different portals and access policies.
- Client certificate-based authentication is also supported.

## SSL VPN Portal

- Customizable web portal interface.
- Define bookmarks for web access, file shares, RDP, SSH.
- Configure split tunneling to limit traffic to internal subnets.

## Configuration Steps

1. **Enable SSL VPN** on a WAN interface.
2. **Create user accounts/groups** for remote access.
3. **Configure portal settings** (web/tunnel, bookmarks, themes).
4. **Create SSL VPN firewall policies**:
   - SSL VPN → LAN
   - LAN → SSL VPN (if needed)

## Routing and DNS

- Assign IP pool for tunnel users.
- Configure DNS and routing for name resolution and resource access.

## SSL VPN Security

- Enforce password policies and MFA.
- Use client certificates for stronger identity verification.
- Limit access by user group or device type.
- Apply security profiles (AV, IPS, Web Filter) to VPN policies.

## Monitoring and Logs

- View active sessions via:
  - GUI: VPN > Monitor > SSL-VPN Monitor
  - CLI: `diagnose vpn ssl monitor`
- Logs show login attempts, session info, and traffic logs.

## Troubleshooting

- Common commands:
  ```bash
  diagnose debug application sslvpn -1
  diagnose debug enable
  diagnose debug reset
  ```
- Review logs for authentication errors, tunnel failures, and policy mismatches.

## Best Practices

- Use tunnel mode for full access and security profiles.
- Apply role-based access via different user groups and portals.
- Enable MFA and strong password enforcement.
- Regularly monitor usage and update FortiClient.
