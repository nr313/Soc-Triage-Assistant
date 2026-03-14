# SOC Triage Assistant — AI-Powered Alert Triage

A browser-based SOC alert triage tool that uses Claude AI to analyze raw SIEM alerts and determine true positive vs false positive — giving analysts an attack timeline, extracted IOCs, and a prioritized action list in seconds.

## Features

- **True/False Positive classification** — AI determines verdict with confidence score
- **4 classifications** — True Positive, False Positive, Needs Investigation, Benign
- **Attack timeline** — Step-by-step reconstruction of the event sequence
- **IOC extraction** — Pulls IPs, users, ports, hashes directly from the alert
- **Prioritized actions** — Immediate / Soon / Standard priority action steps
- **5 alert sources** — Splunk, Microsoft Sentinel, CrowdStrike, Palo Alto, Generic
- **Split-panel UI** — Input on left, live results on right — mirrors real SOC tools
- **Zero dependencies** — Single HTML file, runs in any browser

## Alert Types Supported

- SSH/RDP Brute Force
- Malware Detection (EDR alerts)
- Phishing/BEC indicators
- Data exfiltration alerts
- Privilege escalation
- Lateral movement
- C2 communication
- Port scanning / reconnaissance
- Any raw SIEM alert format

## Getting Started

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/soc-triage-assistant.git
cd soc-triage-assistant
```

### 2. Get an Anthropic API key
Sign up at [console.anthropic.com](https://console.anthropic.com) and create a free API key.

### 3. Open in browser
```bash
open soc-triage.html
```
Or just double-click the file — no server required.

### 4. Triage an alert
1. Enter your API key
2. Select the alert source (Splunk, Sentinel, etc.)
3. Set environment and affected asset
4. Paste the raw alert or click **Load sample**
5. Click **Triage Alert**

## Example Output

For a high-volume SSH brute force alert with one successful login:

```
Classification:  TRUE POSITIVE — Active SSH Brute Force — Likely Compromised
Confidence:      96%

Summary: This alert represents a confirmed brute force attack from a known Tor
         exit node (185.220.101.47) that successfully authenticated as 'deploy'
         after 47 failed attempts. The successful login requires immediate
         investigation and containment.

Attack Timeline:
  02:14:22  Brute force begins        — 47 login attempts over 60 seconds
  02:14:22  Root targeted             — Failed password for root (×12)
  02:14:25  Admin targeted            — Failed password for admin (×8)
  02:14:30  Successful login          — Accepted password for deploy

Extracted IOCs:
  IP      185.220.101.47    HIGH
  User    deploy            HIGH
  Port    22 (SSH)          MEDIUM

Actions:
  [IMMEDIATE] Isolate affected server — Block 185.220.101.47 at firewall
  [IMMEDIATE] Lock deploy account    — Disable until investigation complete
  [SOON]      Review active sessions — Kill any live sessions from this IP
  [SOON]      Check auth logs        — Look for lateral movement post-login
  [STANDARD]  Enable MFA on SSH      — Prevent future credential attacks
```

## How It Works

1. Analyst pastes a raw SIEM alert into the input panel
2. Context is provided (source tool, environment, affected asset)
3. Claude AI analyzes the alert against known attack patterns
4. Results stream into the right panel — verdict, timeline, IOCs, and actions

## Why This Matters

Alert triage is the #1 daily task for SOC analysts. The average SOC receives hundreds of alerts per day — the majority are false positives. Being able to quickly classify, prioritize, and respond to alerts is the core skill this tool demonstrates.

## Technologies

- Vanilla HTML / CSS / JavaScript (zero dependencies)
- [Anthropic Claude API](https://docs.anthropic.com) — `claude-sonnet-4-20250514`
- Fira Code + Plus Jakarta Sans fonts (Google Fonts)

## Learning Concepts

This project demonstrates practical knowledge of:
- SOC analyst alert triage workflows
- True positive vs false positive classification
- SIEM alert analysis (Splunk, Sentinel, CrowdStrike)
- Attack timeline reconstruction
- IOC extraction and classification
- Incident prioritization and response steps
- MITRE ATT&CK technique identification
- Brute force, lateral movement, and credential attack patterns

## License

MIT
