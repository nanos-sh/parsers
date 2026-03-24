# nano Community Parsers

A collection of VRL parsers for nano log source ingestion.

## Available Parsers

### Endpoint

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [CrowdStrike Falcon](parsers/crowdstrike_falcon) | CrowdStrike | JSON (FDR + Streaming API) | 25+ event types: ProcessRollup2, NetworkConnect, DnsRequest, FileWrite, UserLogon, DetectionSummary, and more |
| [Microsoft Defender EDR](parsers/defender_edr) | Microsoft | JSON | Process creation, network connections, file events, logon activities |
| [Microsoft Sysmon (JSON)](parsers/sysmon) | Microsoft | JSON (Winlogbeat/NXLog) | Process, network, file, registry, DNS events from Sysmon |
| [Microsoft Sysmon (XML)](parsers/sysmon_xml) | Microsoft | Native XML | All 29 Sysmon event IDs with hash splitting and MITRE extraction |
| [Windows Event Log (JSON)](parsers/windows_event) | Microsoft | Winlogbeat/NXLog JSON | 24+ EventIDs: logon, process, service, Kerberos, account mgmt |
| [Windows Event Log (XML)](parsers/windows_event_xml) | Microsoft | Native XML | 30+ EventIDs parsed from raw Windows Event XML |
| [Windows Event Log (Text)](parsers/windows_event_text) | Microsoft | Rendered text | Splunk UF / wevtutil format with section-aware body parsing |

### Network & Firewall

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [Palo Alto PAN-OS](parsers/palo_alto) | Palo Alto Networks | CSV syslog | TRAFFIC, THREAT, SYSTEM, CONFIG, USERID, GlobalProtect, HIP, AUTH |
| [Fortinet FortiGate](parsers/fortinet) | Fortinet | key=value syslog | Traffic, UTM (webfilter, app-ctrl, DNS, IPS, virus), event |
| [Cisco ASA](parsers/cisco_asa) | Cisco | Syslog message codes | 30+ message IDs: connections, ACL, NAT, VPN, IPS, auth |
| [Check Point](parsers/checkpoint) | Check Point | RFC 5424 + LEA | Firewall rules, NAT, VPN, threat prevention, system |
| [Sophos Firewall](parsers/sophos) | Sophos | key=value syslog | Firewall, content filtering, AV, ATP, IDP, anti-spam, WAF |
| [Zscaler ZIA](parsers/zscaler_zia) | Zscaler | JSON envelope | Web, firewall, DNS, tunnel, DLP, audit log types |
| [Broadcom ProxySG](parsers/broadcom_proxy) | Broadcom | ELFF space-delimited | Web proxy access logs with URL reconstruction |
| [Cloudflare](parsers/cloudflare) | Cloudflare | JSON (Logpush) | HTTP requests, firewall events, DNS logs with WAF/bot scoring |
| [Infoblox DHCP](parsers/infoblox_dhcp) | Infoblox | Syslog | DISCOVER, OFFER, REQUEST, ACK, RELEASE, NAK, INFORM |

### Network Security Monitoring

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [Zeek](parsers/zeek) | Zeek Project | JSON | 24 log types: conn, dns, http, ssl, files, notice, smtp, ssh, rdp, intel, weird, and more |
| [Suricata](parsers/suricata) | OISF | EVE JSON | 24 event types: alert, flow, dns, http, tls, fileinfo, smtp, ssh, anomaly, and more |

### Cloud

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [AWS CloudTrail](parsers/aws_cloudtrail) | Amazon | JSON | API calls, user identity, resources, error tracking |
| [AWS VPC Flow Logs](parsers/aws_vpc_flow) | Amazon | Space-delimited / JSON | VPC network flow logs v2-v5 with protocol mapping |
| [AWS GuardDuty](parsers/aws_guardduty) | Amazon | JSON | Threat findings: network, IAM, S3, malware detections |
| [Azure Activity Log](parsers/azure_activity) | Microsoft | JSON | Operations, status, caller identity, resources |
| [Azure Sign-in Logs](parsers/azure_signin) | Microsoft | JSON | Entra ID sign-ins: interactive, non-interactive, service principal |
| [GCP Audit Log](parsers/gcp_audit) | Google | JSON | IAM changes, API calls, resource operations, authorization |

### Security & IAM

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [Okta](parsers/okta) | Okta | JSON | System Log API: auth, MFA, user lifecycle, group, policy events |
| [Duo Security](parsers/duo) | Cisco | JSON | Authentication, admin actions, MFA with device/geo context |
| [Auth0](parsers/auth0) | Okta | JSON | 20+ event types: login, signup, MFA, token exchange, management API |
| [F5 BIG-IP ASM](parsers/f5_waf) | F5 | JSON | Web application firewall: attacks, violations, security events |

### Application

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [Apache HTTP Server](parsers/apache) | Apache | Combined/common log | Client IP, method, status, bytes, user agent, referrer |
| [Nginx](parsers/nginx) | Nginx | Combined / JSON / error | Access and error logs with upstream and proxy support |
| [Squid Proxy](parsers/squid_proxy) | Squid Project | Access log | Cache hit/miss, URL extraction, HTTP metadata |

### Generic

| Parser | Vendor | Format | Description |
|--------|--------|--------|-------------|
| [Generic JSON](parsers/json_generic) | — | JSON | Auto-detects common field names for timestamps, IPs, users, actions |

## Structure

Each parser lives in its own directory under `parsers/` with a `parser.yaml` file containing:

- **name**: Machine-readable identifier (snake_case)
- **display_name**: Human-friendly name
- **version**: Semantic version
- **description**: What this parser does
- **match_values**: Source type aliases that route to this parser
- **category**: Log category (endpoint, network, cloud, security, application, generic)
- **vendor**: Vendor/organization name
- **product**: Product name
- **parser_vrl**: The VRL transformation code

## Usage

Import these parsers into nano via **Log Sources > Repositories**. Parsers are imported as draft log sources ready for review and deployment.

## Contributing

1. Create a new directory under `parsers/` with your parser name
2. Add a `parser.yaml` following the format above
3. Test your VRL with `vector vrl --program your_parser.vrl --input test.json --print-object`
4. Ensure all fields map to [UDM](https://docs.nanosiem.com/udm) or overflow to `.ext.*`

