# 🛡️ Sentinel

**Local AI-Powered Penetration Testing Platform**

Sentinel is a self-hosted pentesting co-pilot that orchestrates seven industry-standard security tools and uses a local LLM to analyze their output, identify real exploitable vulnerabilities, and generate professional pentest reports — all on your own infrastructure, with zero per-scan cost and no external API dependencies.

A free, local alternative to commercial AI pentesting tools that charge $50+ per scan.

---

## ✨ Features

- **7-Tool Security Pipeline** — Nmap, Nikto, SQLMap, WhatWeb, Dirb, Subfinder, and Nuclei orchestrated through a unified web interface
- **Local AI Analysis** — Ollama + Nemotron-3-Nano 30B (1M context window) reads raw tool output and extracts exploitable findings
- **White-Box Code Review** — Point Sentinel at a source directory and the LLM performs OWASP-focused static analysis
- **Live Dashboard** — Real-time scan progress, streaming logs, finding counters, and tool status
- **Professional Reports** — Markdown pentest reports with executive summary, risk breakdown, detailed findings, PoCs, and remediation
- **Scheduled Scans** *(optional)* — Cron-driven recurring scans with overlap prevention
- **Self-Hosted** — Runs entirely on your infrastructure. No API keys, no telemetry, no recurring costs

---

## 🧱 Stack

| Layer | Technology |
|-------|------------|
| OS | Ubuntu 22.04 |
| Web | Apache 2.4 |
| Backend | PHP 8.2 |
| Database | MariaDB |
| AI | Ollama + Nemotron-3-Nano 30B (cloud variant) |
| Recon | Nmap, WhatWeb, Dirb, Subfinder |
| Vuln Scanning | Nikto, Nuclei, SQLMap |
| SSL *(optional)* | Cloudflare Tunnel |

---

## 🚀 Quick Start

```bash
# Clone the repo
git clone https://github.com/advanced-data-intelligence/sentinel.git
cd sentinel

# Copy and configure
cp config.example.php config.php
nano config.php   # set your DB password
```

Then follow the full walkthrough in **[INSTALL.md](INSTALL.md)** — system packages, MariaDB schema, Ollama + Nemotron setup, Apache vhost, and sudoers configuration.

---

## 📊 How It Works

A scan runs through five phases:

1. **Recon** — Nmap, WhatWeb, Dirb, Subfinder, HTTP header analysis
2. **Vulnerability Scanning** — Nikto, Nuclei, SQLMap
3. **AI Analysis** — Nemotron reads each tool's raw output and extracts real exploitable findings (not noise)
4. **Code Review** *(optional)* — When a source path is provided, the LLM audits the codebase for OWASP Top 10 issues
5. **Report Generation** — Nemotron compiles all findings into a professional Markdown pentest report

Typical quick scan: **~8 minutes end-to-end.**

---

## 📁 Project Structure

```
sentinel/
├── index.php              # Dashboard
├── config.example.php     # Configuration template
├── new_scan.php           # Launch new scan
├── scans.php              # Scan history
├── scan_detail.php        # Live progress + logs
├── report_view.php        # Rendered pentest report
├── reports.php            # Report list
├── settings.php           # Tool paths + Ollama config
├── run_scan.php           # Background scan runner
├── api/                   # Live progress / log polling endpoints
├── includes/              # DB, Ollama client, scanner orchestration
├── templates/             # Header, sidebar, footer partials
├── assets/                # Dark dashboard theme (CSS + JS)
├── reports/               # Generated reports (gitignored)
├── uploads/               # Source code uploads (gitignored)
└── tools/                 # Tool wrappers (gitignored)
```

---

## ⚙️ Requirements

- Ubuntu 22.04 (or compatible Debian-based distro)
- 4GB+ RAM (more for local LLM inference)
- Apache 2.4, PHP 8.2+, MariaDB 10.5+
- Ollama with cloud account (for Nemotron cloud variant) **or** local GPU for self-hosted inference
- Sudo access (one-time setup for tool permissions)

---

## 🔒 Security & Authorized Use

> ⚠️ **Sentinel is intended for authorized security testing only.**
>
> Use Sentinel against systems you own or have explicit written permission to test. Unauthorized scanning of third-party systems is illegal in most jurisdictions. The authors accept no liability for misuse.

The default scan type is `recon` (passive, gentle) precisely because aggressive scans against production systems can:
- Trip WAFs, fail2ban, and IDS/IPS systems
- Submit junk data via SQLMap form testing
- Generate thousands of log entries that look like an attack
- Consume target server resources

Always scope your scans tightly and start with **Recon Only** against any live target.

---

## 🗺️ Roadmap

- [ ] Diff reports (compare two scans — "what's new since last week?")
- [ ] Email notifications on scan completion / critical findings
- [ ] Multi-target campaigns
- [ ] Authenticated scanning (login flows)
- [ ] Custom Nuclei template library
- [ ] Slack / Discord webhook integrations
- [ ] Export to PDF / HTML report formats

---

## 🤝 Contributing

PRs welcome. Areas where help is especially valued:
- Additional tool integrations (Wapiti, ZAP, Gobuster, etc.)
- Improved AI prompts for specific vulnerability classes
- UI / dashboard improvements
- Documentation and example scan configurations

---

## 📜 License

MIT — see [LICENSE](LICENSE) for details.

---

## 🙏 Credits

Built on the shoulders of giants:

- **[Ollama](https://ollama.com)** — local LLM runtime
- **[NVIDIA Nemotron](https://huggingface.co/nvidia)** — the brain
- **[ProjectDiscovery](https://projectdiscovery.io)** — Subfinder & Nuclei
- **[Nmap](https://nmap.org), [Nikto](https://github.com/sullo/nikto), [SQLMap](https://sqlmap.org), [WhatWeb](https://github.com/urbanadventurer/WhatWeb), [Dirb](http://dirb.sourceforge.net)** — the classic recon and vuln tooling that makes this all possible

---

*Sentinel — your local AI pentester. No subscriptions. No API keys. No data leaves your network.*
