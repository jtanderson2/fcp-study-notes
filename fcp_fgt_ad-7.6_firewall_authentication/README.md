# FortiGate 7.6 – Section 04: Firewall Authentication

## Overview

Firewall authentication allows FortiGate to control user access to network resources by requiring login credentials. This ensures that only authorized users can access specific network segments or services, providing granular user-based policy enforcement.

## Authentication Types

### 1. Policy-based Authentication
- Applied to specific traffic via firewall policies.
- Triggers when unauthenticated traffic matches a policy.
- Authentication prompt can be:
  - Web-based (Captive Portal)
  - Integrated (e.g., with browser-based SSO)

### 2. Identity-based Policies
- Enhances firewall rules with user or group criteria.
- Supports role-based access control (RBAC).
- Used for different access levels depending on group membership.

## Authentication Methods

### Local User Authentication
- User credentials stored on the FortiGate.
- Best for small environments or fallback accounts.

### Remote Authentication
- FortiGate integrates with external identity providers:
  - **LDAP**: Connects to Active Directory or other directory servers.
  - **RADIUS**: Centralized authentication with accounting.
  - **TACACS+**: Granular command authorization (common for admin auth).
  - **SAML**: Web-based single sign-on.
  - **FSSO (Fortinet Single Sign-On)**: Uses logon events from AD to map users to IPs without prompting for credentials.

### Certificate-based Authentication
- Uses client certificates to validate identity.
- Offers strong, phishing-resistant authentication.

## Authentication Flow

1. User initiates a connection matching a firewall policy requiring authentication.
2. FortiGate intercepts and presents a login challenge.
3. Upon successful login, a session is created for the user.
4. Traffic is allowed according to user-based policy settings.

## Captive Portal

- Web page prompting users to authenticate before allowing access.
- Can be:
  - Default FortiGate login page
  - Custom HTML/CSS portal
  - Redirected to external RADIUS or SAML IdP

## Session Management

- Authenticated sessions tracked in the firewall session table.
- Session timeout values:
  - Idle timeout (default: 5 minutes)
  - Can be customized per user/group or policy
- Sessions can be manually cleared via CLI:
  ```bash
  diagnose firewall auth list
  diagnose firewall auth clear
  ```

## Firewall Policy Configuration

- Authentication is enabled per policy:
  - Check "Enable Identity-based Policy"
  - Specify user groups and authentication method
- Policy actions can vary by user group (e.g., limited access for guests)

## Logging and Monitoring

- Active logins visible via:
  - **GUI**: Monitor > Firewall Users
  - **CLI**:
    ```bash
    diagnose firewall auth list
    get user identity-list
    ```
- Logs record login attempts, successes, and failures.

## Security Considerations

- Always use HTTPS for captive portals and credential transmission.
- Use trusted certificates to avoid browser warnings.
- Enforce strong password policies or integrate with MFA.
- Limit login attempts and lock out accounts on repeated failures.

## Best Practices

- Prefer remote authentication with AD integration for scalability.
- Use FSSO or SAML for seamless user experience.
- Apply minimal necessary access per group (principle of least privilege).
- Customize captive portal branding for usability.
- Log and audit authentication activity for compliance.
