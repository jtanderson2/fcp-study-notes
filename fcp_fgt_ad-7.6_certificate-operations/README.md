# FortiGate 7.6 – Section 06: Certificate Operations

## Overview

FortiGate uses digital certificates to secure communications and authenticate identities. Certificate operations are essential for features such as:

- HTTPS administrative access
- SSL inspection (deep packet inspection)
- SSL VPN and IPsec VPN
- Client certificate authentication
- Secure web filtering

FortiGate supports X.509 certificates in PEM and DER formats, using RSA and ECC keys.

## Certificate Types

### 1. Local Certificates
- Assigned to FortiGate for server identity in SSL/TLS connections.
- Methods of obtaining:
  - Generate self-signed certificates.
  - Create a Certificate Signing Request (CSR) and import the signed certificate.
  - Import a certificate with a private key from another source.

### 2. CA Certificates
- Used to validate certificates from clients or external servers.
- Includes root and intermediate certificates.
- Required for validating SSL VPN clients, HTTPS inspection targets, etc.

### 3. Self-Signed Certificates
- Created and signed by FortiGate itself.
- Useful for internal testing or trusted internal environments.
- Not trusted by browsers or operating systems by default.

### 4. Imported Certificates
- Certificates and private keys obtained from external CAs.
- Supported formats: PEM (.crt/.key), PKCS#12 (.pfx/.p12)

## Managing Certificates

### GUI Navigation
- **System > Certificates**: Manage local, CA, and self-signed certificates.

### CLI Commands
- Manage local certificates:
  ```bash
  config vpn certificate local
  ```
- Manage CA certificates:
  ```bash
  config vpn certificate ca
  ```

## Certificate Generation and Import

### Steps:
1. **Create CSR**:
   - Include details like Common Name (CN), Subject Alternative Name (SAN), key size (2048/4096), and algorithm (SHA-256).
2. **Submit to CA**:
   - Use internal enterprise CA (e.g., Microsoft CA) or public CA (e.g., DigiCert, Let's Encrypt).
3. **Import Certificate**:
   - Upload signed certificate and matching CA certificate.
   - If importing a .pfx file, include password for private key.

## SSL Inspection

- FortiGate decrypts SSL traffic for inspection (man-in-the-middle).
- Requires installation of FortiGate-generated CA certificate on all client devices.
- Configurations:
  - Create CA cert (or import one).
  - Distribute and trust the CA cert on client systems.
  - Enable deep inspection in firewall policies.

## Certificate Validation

FortiGate checks:
- **Hostname match**: CN or SAN must match server name.
- **Validity**: Must be within date range.
- **Signature algorithm**: Must be strong (e.g., SHA-256).
- **Revocation**: Supports OCSP and CRL.

## Automation and Renewal

- **ACME support**: Automatically obtain and renew certificates (e.g., Let's Encrypt).
- **Manual renewal**: Reissue new certs before expiry.
- **Monitoring**: GUI alerts or FortiManager notifications for expiring certs.

## Security Considerations

- Always use strong passphrases for private keys.
- Restrict access to certificate management.
- Replace default FortiGate certificates with CA-signed versions in production.
- Backup certificate and key material securely.

## Troubleshooting

### Commands
- Show certificate list:
  ```bash
  diagnose vpn certificate list
  ```
- Test SSL connections:
  ```bash
  diagnose debug application ssl
  ```

### External Tools
- Use `openssl s_client -connect <host>:443` to test cert chains and trust.
- Inspect certificates in browsers for SSL inspection-related issues.

## Best Practices

- Use CA-signed certificates for public-facing services (GUI, SSL VPN).
- Use internal CA for internal services and SSL inspection.
- Regularly audit certificate expiration and trust chain integrity.
- Enable certificate expiration alerts.
- Avoid using self-signed certs in production unless internally trusted.
