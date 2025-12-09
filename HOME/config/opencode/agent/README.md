# Armis Purple Sub-Agents Index

> **Complete listing of all Armis Purple sub-agents for the FedRAMP 2025 Red Team Exercise**

## Agent Overview

This directory contains all specialized sub-agents that support the Armis Purple primary agent in executing the FedRAMP Red Team Exercise Test Plan.

## Agent Inventory

### Primary Orchestration Agent

The primary orchestration agent is defined at:
- **File**: `/home/ap/.config/opencode/armis-purple.md`
- **Config**: Configured in `opencode.jsonc` as the primary agent

> **Note**: The primary agent (`armis-purple`) is an **orchestrator** that delegates all specialized tasks to the sub-agents listed below. It does NOT perform security testing directly.

### Phase 1: Reconnaissance and Establishing the Foothold

| Agent File | Description | Objective |
|------------|-------------|-----------|
| `recon-agent.md` | Deep System Reconnaissance (OSINT & Local) | (1) Gather critical details about collector and Debian OS |
| `vuln-analysis-agent.md` | Configuration & Vulnerability Analysis | (2) Identify security misconfigurations |
| `container-security-agent.md` | Container Escape & Security Testing | Test container security (TC-001 to TC-007) |
| `auth-bypass-agent.md` | Authentication Bypass & Account Mapping | (3) Identify unauthenticated access vectors |
| `dataflow-mapping-agent.md` | Critical Dataflow Mapping | (4) Document communication paths to backend |

### Phase 2: Exploitation and Lateral Movement

| Agent File | Description | Objective |
|------------|-------------|-----------|
| `exploitation-agent.md` | Vulnerability Exploitation & PoC Development | Develop and execute exploits |
| `cloud-pivot-agent.md` | Cloud Back-end Pivot via Collector | (5) Pivot to backend using collector access |
| `reverse-tunnel-agent.md` | Reverse Tunneling & Covert Channels | (6) Establish reverse tunnel to backend |
| `lateral-movement-agent.md` | Internal Lateral Movement | (7) Move between systems and collectors |
| `persistence-agent.md` | Persistence Mechanism Analysis | Analyze persistence vectors |

### Phase 3: Action on Objectives

| Agent File | Description | Objective |
|------------|-------------|-----------|
| `data-exfiltration-agent.md` | Data Exfiltration from Cloud Back-end | (8) Demonstrate data exfiltration capability |

### Continuous/Support Agents

| Agent File | Description | Purpose |
|------------|-------------|---------|
| `compliance-agent.md` | CIS & NIAP Compliance Assessment | CIS Debian 11 & NIAP PP-OS v4.3 compliance |
| `certificate-agent.md` | Certificate & Cryptographic Analysis | Certificate validity verification (TC-010) |
| `evidence-collection-agent.md` | Evidence Collection & Chain of Custody | Collect and preserve all evidence |
| `tools-arsenal-agent.md` | Security Tools Management | Manage and document all tools |
| `social-engineering-agent.md` | Social Engineering Assessment | Phishing/pretexting if authorized |
| `report-generation-agent.md` | Final Report Generation | Generate comprehensive final report |

## Test Case Coverage

| Test Case | Agent | Description |
|-----------|-------|-------------|
| TC-001 | container-security-agent | Container Escape Prevention |
| TC-002 | container-security-agent | Memory Residue Protection |
| TC-003 | container-security-agent | Resource Limit Enforcement (DoS Prevention) |
| TC-004 | container-security-agent | Container Isolation |
| TC-005 | container-security-agent | Privilege Minimization |
| TC-006 | container-security-agent | Credential Security (Container) |
| TC-007 | container-security-agent | Image Signing Verification |
| TC-008 | auth-bypass-agent | Low-Privilege Command Escalation |
| TC-009 | auth-bypass-agent | Authentication Lockout |
| TC-010 | certificate-agent | Certificate Validity Period (≤13 months) |

## Objective Coverage

| Objective | Agent(s) | Phase |
|-----------|----------|-------|
| (1) Deep System Reconnaissance | recon-agent | Phase 1 |
| (2) Configuration and Vulnerability Analysis | vuln-analysis-agent | Phase 1 |
| (3) Authentication Bypass and Account Mapping | auth-bypass-agent | Phase 1 |
| (4) Critical Dataflow Mapping | dataflow-mapping-agent | Phase 1 |
| (5) Cloud Back-end Pivot via Collector | cloud-pivot-agent | Phase 2 |
| (6) Reverse Tunneling Attempt | reverse-tunnel-agent | Phase 2 |
| (7) Internal Lateral Movement | lateral-movement-agent | Phase 2 |
| (8) Data Exfiltration from Cloud Back-end | data-exfiltration-agent | Phase 3 |

## Compliance Framework Coverage

| Framework | Agent | Scope |
|-----------|-------|-------|
| CIS Debian 11 Benchmark v2.0.0 | compliance-agent | Full benchmark assessment |
| NIAP PP-OS v4.3 | compliance-agent | Protection profile verification |
| NIST 800-53 | vuln-analysis-agent | Control correlation |
| NIST 800-115 | report-generation-agent | Methodology documentation |
| MITRE ATT&CK | All agents | Technique mapping |

## Agent Dependencies

```
armis-purple-primary
├── Phase 1 Agents
│   ├── recon-agent
│   │   └── feeds → vuln-analysis-agent, dataflow-mapping-agent
│   ├── vuln-analysis-agent
│   │   └── feeds → exploitation-agent, compliance-agent
│   ├── container-security-agent
│   │   └── feeds → exploitation-agent, lateral-movement-agent
│   ├── auth-bypass-agent
│   │   └── feeds → exploitation-agent, cloud-pivot-agent
│   └── dataflow-mapping-agent
│       └── feeds → cloud-pivot-agent, reverse-tunnel-agent
├── Phase 2 Agents
│   ├── exploitation-agent
│   │   └── feeds → lateral-movement-agent, persistence-agent
│   ├── cloud-pivot-agent
│   │   └── feeds → lateral-movement-agent, data-exfiltration-agent
│   ├── reverse-tunnel-agent
│   │   └── feeds → data-exfiltration-agent
│   ├── lateral-movement-agent
│   │   └── feeds → data-exfiltration-agent
│   └── persistence-agent
│       └── feeds → report-generation-agent
├── Phase 3 Agents
│   └── data-exfiltration-agent
│       └── feeds → report-generation-agent
└── Support Agents
    ├── compliance-agent → report-generation-agent
    ├── certificate-agent → compliance-agent, report-generation-agent
    ├── evidence-collection-agent → report-generation-agent
    ├── tools-arsenal-agent → All agents
    ├── social-engineering-agent → report-generation-agent
    └── report-generation-agent → Final deliverables
```

## Usage

### Invoking a Sub-Agent

There are two methods to invoke sub-agents:

**Method 1: @ Mention (Direct)**
```
@recon-agent Perform comprehensive reconnaissance on the target collector system
```

```
@container-security-agent Execute test case TC-001 for container escape prevention
```

```
@compliance-agent Run CIS Debian 11 Benchmark assessment on the collector
```

**Method 2: Task Tool (Programmatic)**
```python
Task(
    description="Reconnaissance scan",
    prompt="Perform comprehensive reconnaissance on the target collector system",
    subagent_type="recon-agent"
)
```

### Parallel Execution for Maximum Performance

Launch multiple independent agents simultaneously:
```python
# Phase 1 parallel execution
Task(description="Recon", prompt="...", subagent_type="recon-agent")
Task(description="Vuln scan", prompt="...", subagent_type="vuln-analysis-agent")
Task(description="Container tests", prompt="...", subagent_type="container-security-agent")
Task(description="Auth testing", prompt="...", subagent_type="auth-bypass-agent")
Task(description="Dataflow mapping", prompt="...", subagent_type="dataflow-mapping-agent")
Task(description="Cert analysis", prompt="...", subagent_type="certificate-agent")
Task(description="Compliance", prompt="...", subagent_type="compliance-agent")
```

### Agent Communication

Sub-agents communicate findings through structured output that feeds into:
1. Other dependent agents for continued assessment
2. Evidence collection agent for documentation
3. Report generation agent for final deliverables

## Agent Configuration

Each sub-agent is configured with:
- **temperature**: Controls response creativity (0.1-0.4 for security tasks)
- **maxSteps**: Maximum agentic iterations before forced response
- **tools**: Specific tool access (bash, read, write, etc.)
- **permission**: Permission levels for sensitive operations

See `opencode.jsonc` for full configuration details.

## File Locations

All agent definition files are located in:
```
/home/ap/.config/opencode/agent/
```

Primary agent configuration:
```
/home/ap/.config/opencode/armis-purple.md
/home/ap/.config/opencode/opencode.jsonc
```

## Version Information

- **Created**: December 2024
- **FedRAMP Test Plan Version**: 2025
- **Assessment Period**: November 2025 - January 2026
