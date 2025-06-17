# FortiGate 7.6 – Section 11: IPsec VPN

## Overview

IPsec (Internet Protocol Security) VPNs provide secure communication tunnels over public or private IP networks by encrypting and authenticating IP packets. FortiGate supports both **site-to-site** and **remote access** IPsec VPNs using IKEv1 and IKEv2 protocols.

## IPsec VPN Types

### Site-to-Site VPN
- Connects two or more geographically dispersed sites.
- Common between headquarters and branch offices.
- Supports static or dynamic IP addresses at each end.

### Remote Access VPN
- Used by individual users to access internal resources securely.
- Compatible with FortiClient, native IPsec clients (Windows/macOS), and third-party clients.

## IPsec Architecture

### Protocols
- **IKE (Internet Key Exchange)**:
  - Negotiates and sets up Security Associations (SAs).
  - FortiGate supports both IKEv1 (Main or Aggressive Mode) and IKEv2.
- **ESP (Encapsulating Security Payload)**:
  - Provides confidentiality, integrity, and authentication.
- **AH (Authentication Header)**:
  - Provides integrity and authentication, no encryption (rarely used).

### Security Associations (SAs)
- Defines cryptographic parameters for a VPN session.
- Two types: Phase 1 SA (control channel) and Phase 2 SA (data channel).
- Each SA is uni-directional; bidirectional communication needs a pair.

## IPsec VPN Configuration

### Phase 1 Configuration (IKE Phase 1)
- Establishes initial secure tunnel using:
  - Remote Gateway (Static IP, FQDN, or Dialup)
  - Authentication (Pre-shared Key or Certificate)
  - Encryption/Authentication algorithms (e.g., AES256/SHA256)
  - DH Group (e.g., 14 for 2048-bit)
  - IKE version (v1 or v2)
  - Lifetime (default: 28800 seconds)

### Phase 2 Configuration (IPsec SA)
- Negotiates parameters for encrypting data traffic:
  - Local and Remote Subnets
  - Protocols/Ports (default: any)
  - Encryption/Authentication (e.g., AES256/SHA1)
  - PFS (Perfect Forward Secrecy)
  - Lifetime (default: 3600 seconds)

### Interface vs. Policy-Based VPN

#### Interface-based (Route-based VPN)
- Creates a virtual IPsec interface (e.g., `vpn-to-branch`).
- Integrated with routing (static or dynamic).
- Enables granular control via firewall policies.
- Recommended for scalability and flexibility.

#### Policy-based VPN
- IPsec configuration embedded in firewall policies.
- Simpler setup, suitable for basic VPNs.
- Limited flexibility and deprecated for advanced setups.

## Advanced Features

- **Dead Peer Detection (DPD)**: Detects unresponsive VPN peers and triggers failover or re-negotiation.
- **NAT Traversal (NAT-T)**: Enables IPsec over NAT environments using UDP 4500.
- **Redundant VPNs**: Configure backup tunnels for high availability.
- **Dynamic DNS**: Useful for peers with non-static public IP addresses.
- **Replay Detection**: Protects against replay attacks.
- **Fragmentation Support**: Handles large packets over MTU-restricted links.

## Authentication Methods

- **Pre-Shared Key (PSK)**: Simple, but must be kept confidential.
- **Certificates**: Uses X.509 certificates and CA validation; more secure for scalable environments.
- **XAuth**: Supports user/password authentication on top of PSK.

## Monitoring and Troubleshooting

### CLI Tools
- List tunnel status:
  ```bash
  get vpn ipsec tunnel summary
  ```
- Show detailed Phase 1/2 status:
  ```bash
  diagnose vpn tunnel list
  ```
- Debug IKE negotiation:
  ```bash
  diagnose debug application ike -1
  diagnose debug enable
  ```
- Reset debug:
  ```bash
  diagnose debug reset
  ```

### GUI Tools
- VPN Monitor: See tunnel status, bytes sent/received, and SA details.
- Log & Report > Events: View VPN logs, connection attempts, and errors.

## Best Practices

- Use IKEv2 for better performance and NAT compatibility.
- Prefer route-based VPNs with proper firewall rules and routing.
- Use strong encryption (AES256), integrity (SHA256), and DH groups.
- Enable DPD and NAT-T for resilience.
- Monitor SAs and log events to track usage and detect issues.
- For large deployments, manage IPsec via FortiManager or scripts.

