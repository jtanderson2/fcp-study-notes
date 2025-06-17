# FortiGate 7.6 – Certificate Operations

## Overview

- Certificates are used to secure communications and validate identities.
- FortiGate uses certificates for:
  - HTTPS GUI access
  - SSL VPN
  - Deep SSL inspection
  - IPsec VPN
  - Authentication via client certificates

## Certificate Types

- **Local Certificates**: Issued to the FortiGate device.
- **CA Certificates**: Used to verify other certificates.
- **Self-Signed Certificates**: Created on FortiGate; not trusted by default.
- **Imported Certificates**: From external Certificate Authorities (CAs).

## Certificate Authorities (CA)

- FortiGate can act as an internal CA to issue certificates to clients.
- External CAs are trusted for public-facing services.
- CA certificates must be imported for validation.

## Generating and Importing Certificates

1. Generate a Certificate Signing Request (CSR) on FortiGate.
2. Submit CSR to a CA for signing.
3. Import the signed certificate and the CA certificate.

## Managing Certificates

- GUI: System > Certificates
- CLI: `config vpn certificate local`
- Use secure storage and encryption for private keys.

## Deep SSL Inspection

- Requires FortiGate to decrypt and inspect SSL/TLS traffic.
- Uses a certificate to impersonate HTTPS sites (man-in-the-middle).
- Requires installation of FortiGate CA certificate on client devices to avoid browser warnings.

## Certificate Constraints

- Certificate must match hostname (Common Name or SAN).
- Check validity dates and signature algorithm.
- FortiGate supports RSA and ECC keys.

## Automation and Renewal

- Certificates have expiry dates; must be renewed before expiration.
- Automate renewals when using ACME (e.g., Let's Encrypt).
- Monitor certificate expiry using FortiManager or alerts.

## Best Practices

- Use publicly signed certificates for user-facing services.
- Use internal CA for SSL inspection and internal authentication.
- Keep private keys secure and restrict access.
- Regularly audit certificates for expiration and trust chain issues.
