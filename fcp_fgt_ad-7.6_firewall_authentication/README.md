# FortiGate 7.6 – Firewall Authentication

## Overview

- Firewall authentication verifies users before granting network access.
- Supports multiple methods to suit different deployment needs.
- Can control access through policies, captive portals, or authentication rules.

## Authentication Methods

- **Local User Accounts**:
  - Stored directly on the FortiGate
  - Used for small networks or fallback

- **Remote Authentication Servers**:
  - LDAP, RADIUS, TACACS+, SAML
  - Integrates with existing directory services

- **Single Sign-On (SSO)**:
  - Fortinet SSO (FSSO)
  - Captures Windows logon events
  - Transparent authentication for users

- **Captive Portal**:
  - Web-based login prompt
  - Triggered when users access the network
  - Can apply different authentication rules by interface or policy

## Authentication Rules

- Used to specify:
  - Source interface
  - User group
  - Authentication method
- Applies when traffic matches a policy with authentication enabled

## Policy-Based Authentication

- Enable authentication in a specific firewall policy.
- Traffic triggers authentication before being allowed.
- Session persists after authentication.

## Authentication Timeout and Re-authentication

- Timeout: Defines session duration (default: 5 minutes)
- Can be adjusted per user or globally
- Re-authentication can be enforced for higher security

## Security Measures

- Limit failed login attempts to prevent brute force
- Use HTTPS for secure credential transmission
- Use group-based policies to minimize exposure

## Monitoring and Troubleshooting

- View active authenticated users:
  - GUI: Monitor > Firewall Users
  - CLI: `diagnose firewall auth list`
- Debug authentication:
  - `diagnose debug application fnbamd -1`
  - `diagnose debug enable`

## Best Practices

- Use SSO for seamless experience in enterprise environments
- Deploy captive portals in guest networks or BYOD scenarios
- Segment internal users via user groups and roles
- Regularly audit authentication logs and configurations
