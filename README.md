# Prodapt Autonomous NOC Console

> **Interactive AI-driven Network Operations Center automation demo** — built for SageNet's NOC Outsourcing RFP (NOC-01-022026), demonstrating Prodapt's Autonomous NOC approach powered by Agent Hub, Nucleus, and ServiceNow Autonomous Workforce.

---

## Overview

This is a fully self-contained, single-file interactive console that demonstrates how Prodapt's Autonomous NOC platform operates in real time. It simulates live alarm ingestion, multi-agent AI processing, workflow automation, and persona-driven dashboards — all running in the browser with zero dependencies and no backend.

The console is designed to be shown to SageNet stakeholders as a live walkthrough of the autonomous NOC value proposition: how AI agents replace manual L1/L2 toil, reduce alarm noise, correlate cascading failures, and operate across Fortinet, Cisco Meraki, Starlink, Cradlepoint, and IoT platforms.

---

## Live Demo

Deploy to Vercel in under 60 seconds — see [Deployment](#deployment) below.

---

## Architecture

The console visualises Prodapt's four-layer Autonomous NOC stack:

```
┌─────────────────────────────────────────────────────────────────┐
│          SINGLE PANE OF GLASS  (Persona-Driven SPoG)            │
│   L1 Triage · L2 Diagnostics · L3 Config · L4/SDM · Supervisor  │
└────────────────────────┬────────────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────────────┐
│                    AGENT HUB  (Multi-Agent AI)                   │
│  Alert Triage · Diagnostic · Resolution · Escalation · Analytics │
│  + Platform RCA Agents: Fortinet · Meraki · Starlink · CP · IoT  │
│  + Remediation Agents:  Fortinet · Meraki · Starlink · CP · IoT  │
└───────────────┬────────────────────────┬────────────────────────┘
                │                        │
┌───────────────▼──────────┐  ┌──────────▼──────────────────────┐
│  NUCLEUS  (Network Asset  │  │  SERVICENOW AUTONOMOUS WORKFORCE │
│  Gateway + Orchestration) │  │  CMDB · ITSM · AIOps · SNaaS    │
│  Runbooks · Workflows     │  │  Enrichment · SLA · Escalation   │
└───────────────┬──────────┘  └──────────┬────────────────────────┘
                └────────────┬───────────┘
┌───────────────────────────▼────────────────────────────────────┐
│               NETWORK INFRASTRUCTURE                            │
│   Fortinet · Cisco Meraki · Starlink/VSAT · Cradlepoint/Digi   │
│   Navori · BrightSign · ServiceNow SNaaS                       │
└────────────────────────────────────────────────────────────────┘
```

---

## Features

### Workflow Automation (3 Live Demos)

| Workflow | What It Shows |
|---|---|
| **Alarm Deduplication** | 5 identical LinkDown alarms arrive → fingerprint hashing → dedup window → collapsed to 1 enriched ServiceNow ticket instead of 5 |
| **Alarm Suppression** | Maintenance window activated for FW-DAL-02 → 4 alarms suppressed, 0 tickets raised → 2 non-suppressed alarms forwarded normally |
| **Ticket Mediation** | BGP session drop on FW-NYC-03 → Diagnostic Agent maps 3 downstream impacts → CMDB enrichment via Nucleus → 1 parent P1 ticket + 3 linked child tickets in ServiceNow |

Each demo animates step-by-step through the workflow, activates the relevant AI agents with progress indicators, and logs every action to the Agent Log panel.

### AI Agent Hub (16 Agents)

#### Core Intelligence Agents (6)
| Agent | Role |
|---|---|
| 🔍 Alert Triage Agent | Ingests all incoming events, classifies severity (P1–P4), routes to downstream agents |
| 🧠 Diagnostic Agent | Deep topology analysis, BGP peer inspection, root cause mapping, impact radius identification |
| 📋 Resolution Playbook | Selects and executes the appropriate Nucleus runbook for each alarm type and platform |
| ⚡ Escalation Agent | Monitors SLA timers, triggers VP notifications at T+25 min, manages escalation chains |
| 📊 Analytics Agent | Pattern learning, suppression rule optimisation, KPI tracking, trend detection |
| 🔄 Self-Healing Agent | Autonomous remediation execution, config restore, auto-reboot, zero-touch fix recording |

#### Platform RCA Agents (5)
| Agent | Platform | Diagnostic Capability |
|---|---|---|
| 🔥 Fortinet RCA | FortiGate / FortiManager | BGP neighbour table, routing RIB/FIB, firewall policy conflict, CMDB circuit correlation |
| 🔵 Meraki RCA | Cisco Meraki MX/MR | Dashboard API, SD-WAN uplink health, path scores, VPN tunnel state |
| 🛰️ Starlink RCA | Starlink LEO / VSAT | Beam handoff events, obstruction data, orbital/weather correlation, latency root cause |
| 📡 Cradlepoint RCA | Cradlepoint / Digi LTE | NCM API telemetry, RSRP/RSRQ signal levels, APN/SIM config validation, failover logs |
| 📺 IoT/Display RCA | Navori / BrightSign | Endpoint ping, content server reachability, player crash logs, DNS/DHCP inspection |

#### Remediation Agents (5)
| Agent | Platform | Automated Actions |
|---|---|---|
| 🛠️ Fortinet Remediation | Fortinet | BGP session clear/restart, config rollback, ACL update via FortiManager, firmware scheduling |
| 🔧 Meraki Remediation | Cisco Meraki | Interface bounce via API, uplink priority change, SSID template push, warm spare failover |
| 📶 Starlink Remediation | Starlink | Dish reboot, beam steer request, LTE backup activation, satellite reconnect |
| 📲 Cradlepoint Remediation | Cradlepoint | Modem restart via NCM, APN profile reset, SIM slot failover, carrier band lock |
| ♻️ IoT Remediation | Navori / BrightSign | Remote display reboot, content cache flush, player service restart, firmware push |

### Invoke Agent Hub — Command Palette

Click **⬡ Invoke Agent Hub** (top right of tab bar) to open the command palette:
- Select any of the 16 agents from the picker grid
- Choose a target device from the full SageNet device inventory
- Add optional context/parameters (BGP peer IP, circuit ID, etc.)
- Click **Invoke Agent** — watch the agent card animate, step through platform-specific actions, and return a detailed outcome logged to the Agent Log

### Agent Observability Dashboard

Switch to the **Agent Observability** tab to see live performance metrics for all 16 agents:
- Total invocations, average success rate, active queue depth
- Per-agent table: invocations, success %, average resolution time (seconds), current queue
- Animated activity sparklines showing recent invocation history
- Status dot: green = idle, amber = queued
- Stats refresh every 3 seconds

### Nucleus Workflow Engine

Switch to the **Nucleus Engine** tab to explore the orchestration layer:
- **Runbook Library**: 10 platform-specific runbooks (RB-01 through RB-10) with status, step count, and average execution time. Click **Execute** on any runbook to trigger a simulated run
- **Platform Integrations**: Live connection status and latency for all 9 integrated platforms (FortiManager, Meraki Dashboard, Starlink API, Cradlepoint NetCloud, Digi Remote Manager, Navori QL, BrightSign Network, ServiceNow SNaaS, Nucleus CMDB Gateway)
- **Active Pipelines**: Current workflow pipeline flow diagrams showing step-by-step progression
- **Execution History**: Recent runbook executions with timestamp, result, and duration

### Single Pane of Glass — 6 Persona Views

The SPoG bar below the workflow tabs switches between role-specific dashboards. Each persona sees relevant KPIs, live queue data, platform health, and AI agent guidance:

| Persona | Badge | Focus | KPIs |
|---|---|---|---|
| L1 Remote Operations | `L1` | Event triage, auto-resolution monitoring | Event queue, auto-resolved, escalated to L2, automate rate |
| L2 Network Diagnostics | `L2` | SD-WAN health, P2 investigation | Diag queue, active RCAs, auto-remediated, MTTR avg |
| L3 Config & Firmware | `L3` | Config drift, firmware compliance, BGP policy | Config drift count, FW compliance %, change queue, policy violations |
| L4 / SDM | `L4/SDM` | SLA adherence, escalation management | SLA compliance, P1 active, escalations, P1 MTTR |
| NOC Supervisor | `NOC SUP` | Team throughput, shift performance | Automate rate, total events, open tickets, SLA health |
| Select L2 / IoT / Dispatch | `IoT/DSP` | IoT fleet, field dispatch | IoT fleet health, displays offline, dispatch queue, auto-healed |

All KPI values are live — they update in real time as alarms arrive and scenarios run.

### Severity & Coloring

All alarm severity uses strict **RAG coloring**. Prodapt brand red (`#EB262A`) appears only on the logo mark.

| Severity | Color | Hex |
|---|---|---|
| P1 Critical | Red | `#EF4444` |
| P2 High | Amber/Orange | `#F97316` |
| P3 Medium | Yellow | `#EAB308` |
| P4 Low | Green | `#22C55E` |
| Suppressed | Gray | `#6B7280` |
| Deduplicated | Purple | `#8B5CF6` |

---

## Platform Coverage

| Platform | Vendor | Use Case at SageNet |
|---|---|---|
| FortiGate / FortiManager | Fortinet | SD-WAN, firewall, BGP routing, VPN |
| Meraki MX / MR | Cisco | SD-WAN, switching, wireless, hospitality & retail |
| Starlink | SpaceX | LEO satellite — remote/mobile sites |
| VSAT | Various | Maritime and remote fixed sites |
| Cradlepoint / NetCloud | Ericsson | LTE/5G cellular routers, mobile |
| Digi Remote Manager | Digi International | Cellular IoT gateway |
| Navori QL | Navori | Digital signage player management |
| BrightSign Network | BrightSign | Kiosk and display player management |
| ServiceNow | ServiceNow | ITSM, CMDB, AIOps, SNaaS |

---

## SageNet RFP Context

This console was built as part of Prodapt's response to **SageNet NOC Outsourcing RFP (NOC-01-022026)**.

**Current SageNet NOC:**
- ~136 FTEs across L1 (58), L2 (25+37 CallTek), L3 (21), Supervisory/SDM/Dispatch (30+)
- Estimated current spend: ~$8.25M per year
- Four business lines: Terrestrial, WiFi/IoT, Digital Signage, Satellite

**Prodapt's Autonomous NOC Target:**
- 30–40% cost reduction → targeting ~$5.0M (vs $8.25M baseline)
- 90%+ autonomous handling of P3/P4 events (L1 tier)
- Agent-led P2 investigation and remediation (L2 tier)
- AI-augmented L3 config/firmware engineering
- Zero-touch runbook execution via Nucleus for routine fixes

---

## Technology

| Attribute | Detail |
|---|---|
| Stack | Pure HTML5 / CSS3 / Vanilla JavaScript (ES2020+) |
| Dependencies | None — zero npm, zero frameworks, zero build step |
| File count | 1 (`index.html`) |
| File size | ~140 KB |
| Browser support | All modern browsers (Chrome, Firefox, Safari, Edge) |
| Deployment | Any static host — Vercel, Netlify, GitHub Pages, S3 |

---

## File Structure

```
prodapt-noc-console/
├── index.html      # Complete application — all HTML, CSS, and JS in one file
├── vercel.json     # Vercel static deployment config with cache headers
├── .gitignore      # Standard gitignore for Node/OS artifacts
└── README.md       # This file
```

---

## Deployment

### Option A — GitHub + Vercel (Recommended)

Gives you auto-deploy on every `git push`:

```bash
# 1. Create a new empty repo on github.com (no README, no .gitignore)

# 2. Add the remote and push
git remote add origin https://github.com/YOUR_USERNAME/prodapt-noc-console.git
git push -u origin main

# 3. Go to vercel.com → New Project → Import Git Repository
#    Select prodapt-noc-console → Deploy
#    Vercel auto-detects static HTML — no config required
```

### Option B — Vercel CLI

```bash
# Install Vercel CLI (one-time)
npm install -g vercel

# Deploy from the project folder
vercel

# Follow the prompts — live URL returned in ~30 seconds
# To promote to production:
vercel --prod
```

### Option C — Vercel Drag and Drop

Go to [vercel.com/new](https://vercel.com/new), drag the entire `prodapt-noc-console` folder into the browser window. Deployed instantly.

### Option D — GitHub Pages

```bash
# Push to GitHub, then enable GitHub Pages in repo Settings
# Set source: Deploy from branch → main → / (root)
# Your URL: https://YOUR_USERNAME.github.io/prodapt-noc-console/
```

### Option E — Netlify

Drag the folder to [app.netlify.com/drop](https://app.netlify.com/drop) — live in seconds.

---

## Local Development

No build tools required. Open `index.html` directly in any browser:

```bash
# macOS / Linux
open index.html

# Or serve locally with Python
python3 -m http.server 8080
# Then open http://localhost:8080
```

---

## Walkthrough Guide

Use this sequence when demoing to SageNet stakeholders:

1. **Start on L1 persona** — show the live alarm feed auto-populating, point out auto-resolved counter climbing, explain the autonomous triage rate
2. **Run Deduplication scenario** — click "▶ Trigger: 5× Same Alarm Burst" on the Dedup tab, walk through the 5-step workflow animation, show how 5 alarms collapse to 1 ticket
3. **Switch to L2 persona** — show the Diagnostic Agent recommendations and SD-WAN health view
4. **Enable Maintenance Window, run Suppression** — demonstrate how planned downtime generates zero tickets for FW-DAL-02
5. **Switch to Ticket Mediation** — run the BGP Cascade scenario, show the 1 parent + 3 child ticket hierarchy, point out CMDB enrichment ("Hotels-East region, 22 properties")
6. **Switch to L4/SDM persona** — show SLA compliance dashboard and escalation queue
7. **Open Invoke Agent Hub** — select "Fortinet RCA Agent", target "FW-NYC-03", invoke — walk through the live BGP diagnostic output
8. **Switch to Agent Observability tab** — show invocation counts, success rates across all 16 agents
9. **Switch to Nucleus Engine tab** — execute runbook RB-01 (BGP Session Recovery), watch it run and land in execution history
10. **Switch to NOC Supervisor persona** — show team throughput and automation rate as the headline close

---

## Contributing

This is a proposal/demo asset. To update or extend:

- All logic is in `index.html` — search for `// ═══` section headers to navigate
- Key sections: `PERSONAS`, `AGENTS`, `RUNBOOKS`, `PLATFORM_INTEGRATIONS`, `ALARM_TEMPLATES`
- To add a new platform agent: add an entry to `AGENTS` with `cat:'rca'` or `cat:'rem'`, add its HTML card in the platform agent rows, add its `rcaSteps` or `remActions` array
- To add a new persona: add an entry to `PERSONAS` with `kpis` and `renderDash()` function

---

## Contact

**Rajiv Papneja** — rajiv.papneja@prodapt.com
Prodapt Solutions · Intelligent Transformation

---

*Built with Prodapt Agent Hub · Nucleus Workflow Engine · ServiceNow Autonomous Workforce*
