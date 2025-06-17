# FortiGate 7.6 – Section 08: Web Filtering

## Overview

Web filtering controls user access to websites based on content categories, URLs, domain names, and other criteria. It is essential for enforcing acceptable use policies, blocking malicious websites, and preventing data leaks.

## Web Filtering Modes

### 1. DNS Filter
- Checks domain names against FortiGuard category database before DNS resolution.
- Very fast; can block domains without inspecting full HTTP/S content.
- Effective for pre-emptively blocking access to malicious or unwanted sites.

### 2. Web Filter (Proxy-based or Flow-based)
- Inspects HTTP/HTTPS traffic to control access based on URL, category, or keywords.
- Requires SSL Inspection for HTTPS sites.

## FortiGuard Web Filtering

- Uses Fortinet’s cloud-based service to categorize URLs into 80+ categories.
- Categories include Adult/Mature, Social Media, News, Phishing, etc.
- Real-time updates and dynamic rating.
- Can be configured for:
  - Allow
  - Block
  - Warning
  - Monitor
  - Authenticate

## Static URL Filtering

- Manually defined list of URLs/domains:
  - Blocked
  - Allowed
  - Exempted from inspection
- Matches exact, wildcard, or regex patterns.

## Web Content Filtering

- Keyword and phrase filtering within web page content.
- Can block pages containing restricted words even if URL is allowed.

## Safe Search and YouTube Restriction

- **Safe Search**: Enforces search engine filtering for Google, Bing, YouTube, etc.
- **YouTube Restriction**: Applies Google Admin restrictions for video content.

## SSL Inspection Integration

- Required for full visibility into HTTPS traffic.
- Works with deep inspection profile to allow FortiGate to inspect URLs in encrypted sessions.

## Logging and Monitoring

- Web filtering logs show:
  - Visited URLs
  - Blocked attempts
  - Filter actions taken
- Logs forwarded to FortiAnalyzer, Syslog, or FortiCloud.

## Configuring Web Filtering

- Create or edit a Web Filter profile:
  - GUI: Security Profiles > Web Filter
  - CLI: `config webfilter profile`
- Assign profile to a firewall policy.

## Best Practices

- Enable DNS filter as a first layer of defense.
- Use category-based filtering with FortiGuard for broad coverage.
- Combine with SSL Inspection to inspect HTTPS traffic.
- Monitor logs for user behavior and policy violations.
- Apply stricter rules to guest or public networks.

## Troubleshooting

- Verify categorization using FortiGuard Web Rating Service.
- Use diagnostic commands:
  ```bash
  diagnose debug application urlfilter -1
  diagnose debug enable
  ```
- Inspect log messages for blocked access attempts and reasons.
