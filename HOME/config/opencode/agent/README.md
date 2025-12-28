# Armis Purple Sub-Agents Index

> **Complete listing of all Armis Purple sub-agents for the FedRAMP 2025 Red Team Exercise**

---

## oh-my-opencode Design Patterns Integration

All agents in this framework have been updated to follow the **oh-my-opencode design patterns** for optimal performance and consistency:

### Core Design Patterns

| Pattern | Description | Applied To |
|---------|-------------|------------|
| **EXECUTION DISCIPLINE** | Mandatory execution protocols with numbered rules | All sub-agents |
| **NO PREAMBLE** | Start with action, not explanation | All agents |
| **PARALLEL FIRST** | Launch independent operations simultaneously | Orchestrator + sub-agents |
| **EVIDENCE ALWAYS** | No finding without proof | All security agents |
| **STRUCTURED OUTPUT** | Defined response formats | All agents |
| **FAIL FAST** | 3-strike escalation protocol | All agents |

### Response Format Standard

All sub-agents use structured response formats:
```
[AGENT-TAG] {brief_action_description}

{execution_details}

[FINDINGS]
{structured_findings}

[EVIDENCE]
{evidence_references}

[NEXT]
{recommended_next_steps}
```

### Failure Protocol (3-Strike Rule)

All agents implement the standardized failure handling:
- **Strike 1**: Retry with modified parameters
- **Strike 2**: Try alternative tool/technique  
- **Strike 3**: Report blocker to orchestrator with options

### Prime Directives (Orchestrator)

The primary orchestrator (`armis-purple-latest.md`) implements these mandatory protocols:

1. **Long-Term Memory Protocol**: AGENTS.md file for session persistence
2. **Context Window Management**: 150k token threshold with CONTEXT.md handoff
3. **Intent Classification System**: Pre-action analysis for optimal routing
4. **Communication Discipline**: Direct, action-oriented responses
5. **7-Section Delegation Protocol**: Structured prompts for sub-agents

---

## Agent Overview

This directory contains all specialized sub-agents that support the Armis Purple primary agent in executing the FedRAMP Red Team Exercise Test Plan.

## Agent Inventory

### Primary Orchestration Agent

The primary orchestration agent is defined at:
- **File**: `/home/ap/.config/opencode/armis-purple-latest.md`
- **Config**: Configured in `opencode.jsonc` as the primary agent

> **Note**: The primary agent (`armis-purple`) is an **orchestrator** that delegates all specialized tasks to the sub-agents listed below. It does NOT perform security testing directly.

### Phase 1: Reconnaissance and Establishing the Foothold

| Agent File | Description | Objective |
|------------|-------------|-----------|
| `recon-agent.md` | Deep System Reconnaissance (OSINT & Local) | (1) Gather critical details about collector and Debian OS |
| `vuln-analysis-agent.md` | Configuration & Vulnerability Analysis | (2) Identify security misconfigurations |
| `webapp-vuln-agent.md` | Web Application Vulnerability Analysis | Analyze web app auth, authz, injection, XSS, SSRF vulnerabilities |
| `container-security-agent.md` | Container Escape & Security Testing | Test container security (TC-001 to TC-007) |
| `auth-bypass-agent.md` | Authentication Bypass & Account Mapping | (3) Identify unauthenticated access vectors |
| `dataflow-mapping-agent.md` | Critical Dataflow Mapping | (4) Document communication paths to backend |
| `certificate-agent.md` | Certificate & Cryptographic Analysis | Certificate validity verification (TC-010) |
| `compliance-agent.md` | CIS & NIAP Compliance Assessment | CIS Debian 11 & NIAP PP-OS v4.3 compliance |

### Phase 2: Exploitation and Lateral Movement

| Agent File | Description | Objective |
|------------|-------------|-----------|
| `exploitation-agent.md` | Vulnerability Exploitation & PoC Development | Develop and execute exploits |
| `webapp-exploit-agent.md` | Web Application Exploitation | Weaponize web vulnerabilities (SQLi, XSS, SSRF, auth bypass) |
| `cloud-pivot-agent.md` | Cloud Back-end Pivot via Collector | (5) Pivot to backend using collector access |
| `reverse-tunnel-agent.md` | Reverse Tunneling & Covert Channels | (6) Establish reverse tunnel to backend |
| `lateral-movement-agent.md` | Internal Lateral Movement | (7) Move between systems and collectors |
| `persistence-agent.md` | Persistence Mechanism Analysis | Analyze persistence vectors |

### Phase 3: Action on Objectives

| Agent File | Description | Objective |
|------------|-------------|-----------|
| `data-exfiltration-agent.md` | Data Exfiltration from Cloud Back-end | (8) Demonstrate data exfiltration capability |

### Support Agents

| Agent File | Description | Purpose |
|------------|-------------|---------|
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
| TC-010 | certificate-agent | Certificate Validity Period (<=13 months) |

## Objective Coverage

| Objective | Agent(s) | Phase |
|-----------|----------|-------|
| (1) Deep System Reconnaissance | recon-agent | Phase 1 |
| (2) Configuration and Vulnerability Analysis | vuln-analysis-agent, webapp-vuln-agent | Phase 1 |
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
| OWASP Top 10 | webapp-vuln-agent, webapp-exploit-agent | Web application security |
| MITRE ATT&CK | All agents | Technique mapping |

## Agent Dependencies

```
armis-purple-primary (Orchestrator)
├── Phase 1 Agents (Parallel Execution)
│   ├── recon-agent
│   │   └── feeds → vuln-analysis-agent, webapp-vuln-agent, dataflow-mapping-agent
│   ├── vuln-analysis-agent
│   │   └── feeds → exploitation-agent, compliance-agent
│   ├── webapp-vuln-agent
│   │   └── feeds → webapp-exploit-agent, exploitation-agent
│   ├── container-security-agent
│   │   └── feeds → exploitation-agent, lateral-movement-agent
│   ├── auth-bypass-agent
│   │   └── feeds → exploitation-agent, webapp-exploit-agent, cloud-pivot-agent
│   ├── dataflow-mapping-agent
│   │   └── feeds → cloud-pivot-agent, reverse-tunnel-agent
│   ├── certificate-agent
│   │   └── feeds → compliance-agent, report-generation-agent
│   └── compliance-agent
│       └── feeds → report-generation-agent
├── Phase 2 Agents (After Phase 1 Completes)
│   ├── exploitation-agent
│   │   └── feeds → lateral-movement-agent, persistence-agent
│   ├── webapp-exploit-agent
│   │   └── feeds → lateral-movement-agent, cloud-pivot-agent, data-exfiltration-agent
│   ├── cloud-pivot-agent
│   │   └── feeds → lateral-movement-agent, data-exfiltration-agent
│   ├── reverse-tunnel-agent
│   │   └── feeds → data-exfiltration-agent
│   ├── lateral-movement-agent
│   │   └── feeds → data-exfiltration-agent
│   └── persistence-agent
│       └── feeds → report-generation-agent
├── Phase 3 Agents (After Successful Exploitation)
│   └── data-exfiltration-agent
│       └── feeds → report-generation-agent
└── Support Agents (Continuous)
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
@webapp-vuln-agent Analyze the web application for authentication and injection vulnerabilities
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

```python
Task(
    description="Web app vulnerability analysis",
    prompt="Analyze the web application for OWASP Top 10 vulnerabilities including auth, injection, and SSRF",
    subagent_type="webapp-vuln-agent"
)
```

### Parallel Execution for Maximum Performance

Launch multiple independent agents simultaneously:

**Phase 1 Parallel Execution:**
```python
# Launch ALL Phase 1 agents simultaneously
Task(description="Deep reconnaissance", prompt="...", subagent_type="recon-agent")
Task(description="Vulnerability analysis", prompt="...", subagent_type="vuln-analysis-agent")
Task(description="Web app vulnerability analysis", prompt="...", subagent_type="webapp-vuln-agent")
Task(description="Container security tests", prompt="...", subagent_type="container-security-agent")
Task(description="Authentication testing", prompt="...", subagent_type="auth-bypass-agent")
Task(description="Dataflow mapping", prompt="...", subagent_type="dataflow-mapping-agent")
Task(description="Certificate analysis", prompt="...", subagent_type="certificate-agent")
Task(description="Compliance assessment", prompt="...", subagent_type="compliance-agent")
```

**Phase 2 Parallel Execution:**
```python
# Launch Phase 2 agents after Phase 1 completes
Task(description="Exploitation attempts", prompt="...", subagent_type="exploitation-agent")
Task(description="Web app exploitation", prompt="...", subagent_type="webapp-exploit-agent")
Task(description="Cloud pivot testing", prompt="...", subagent_type="cloud-pivot-agent")
Task(description="Reverse tunnel tests", prompt="...", subagent_type="reverse-tunnel-agent")
Task(description="Lateral movement", prompt="...", subagent_type="lateral-movement-agent")
Task(description="Persistence analysis", prompt="...", subagent_type="persistence-agent")
```

**Phase 3 Execution:**
```python
# Launch Phase 3 after successful exploitation
Task(description="Data exfiltration test", prompt="...", subagent_type="data-exfiltration-agent")
Task(description="Evidence collection", prompt="...", subagent_type="evidence-collection-agent")
```

### Orchestration Patterns

**Pattern 1: Full FedRAMP Assessment**
1. Launch all Phase 1 agents in parallel
2. Wait for results, synthesize findings
3. Launch Phase 2 agents based on Phase 1 discoveries
4. Wait for results, identify successful exploitation paths
5. Launch Phase 3 agents for impact demonstration
6. Launch report-generation-agent with all findings

**Pattern 2: Targeted Vulnerability Assessment**
1. Launch recon-agent for target enumeration
2. Launch vuln-analysis-agent with recon results
3. Launch exploitation-agent for verified vulnerabilities
4. Launch evidence-collection-agent throughout

**Pattern 3: Compliance-Focused Assessment**
1. Launch compliance-agent for CIS/NIAP benchmarks
2. Launch certificate-agent for crypto analysis
3. Launch container-security-agent for TC-001 to TC-007
4. Launch auth-bypass-agent for TC-008, TC-009
5. Launch report-generation-agent with compliance focus

**Pattern 4: Web Application Security Assessment**
1. Launch recon-agent for web app enumeration (endpoints, parameters, technologies)
2. Launch webapp-vuln-agent for comprehensive vulnerability analysis:
   - Authentication flaws (session management, credential handling, MFA bypass)
   - Authorization flaws (IDOR, privilege escalation, access control)
   - Injection vulnerabilities (SQLi, command injection, SSTI, XSS)
   - SSRF and request forgery issues
3. Wait for vulnerability analysis report and exploitation queue
4. Launch webapp-exploit-agent with the exploitation queue:
   - Weaponize identified vulnerabilities
   - Demonstrate proof-of-impact for each finding
   - Document reproducible exploitation steps
5. Launch evidence-collection-agent for artifact preservation
6. Launch report-generation-agent with web app focus

### Agent Communication

Sub-agents communicate findings through structured output that feeds into:
1. Other dependent agents for continued assessment
2. Evidence collection agent for documentation
3. Report generation agent for final deliverables

## Mandatory Delegation Table

When ANY of these tasks are requested, the orchestrator **MUST** invoke the corresponding sub-agent:

| Task Category | Sub-Agent | subagent_type Value |
|---------------|-----------|---------------------|
| Reconnaissance, OSINT, enumeration | `recon-agent` | `"recon-agent"` |
| Vulnerability scanning, CVE analysis | `vuln-analysis-agent` | `"vuln-analysis-agent"` |
| Web app vulnerability analysis (auth, authz, injection, XSS, SSRF) | `webapp-vuln-agent` | `"webapp-vuln-agent"` |
| Container security, Docker, escape testing | `container-security-agent` | `"container-security-agent"` |
| Authentication testing, credentials | `auth-bypass-agent` | `"auth-bypass-agent"` |
| Network traffic, dataflow analysis | `dataflow-mapping-agent` | `"dataflow-mapping-agent"` |
| Exploit development, privilege escalation | `exploitation-agent` | `"exploitation-agent"` |
| Web app exploitation (auth bypass, injection, XSS, SSRF attacks) | `webapp-exploit-agent` | `"webapp-exploit-agent"` |
| Cloud backend access, AWS/Azure/GCP | `cloud-pivot-agent` | `"cloud-pivot-agent"` |
| Tunneling, covert channels, C2 | `reverse-tunnel-agent` | `"reverse-tunnel-agent"` |
| Lateral movement, pivoting | `lateral-movement-agent` | `"lateral-movement-agent"` |
| Data exfiltration | `data-exfiltration-agent` | `"data-exfiltration-agent"` |
| CIS/NIAP compliance | `compliance-agent` | `"compliance-agent"` |
| Certificate/TLS analysis | `certificate-agent` | `"certificate-agent"` |
| Persistence mechanisms | `persistence-agent` | `"persistence-agent"` |
| Social engineering | `social-engineering-agent` | `"social-engineering-agent"` |
| Evidence collection | `evidence-collection-agent` | `"evidence-collection-agent"` |
| Tool management | `tools-arsenal-agent` | `"tools-arsenal-agent"` |
| Report generation | `report-generation-agent` | `"report-generation-agent"` |

## Agent Configuration

Each sub-agent is configured with:
- **temperature**: Controls response creativity (0.1-0.4 for security tasks)
- **maxSteps**: Maximum agentic iterations before forced response
- **tools**: Specific tool access (bash, read, write, etc.)
- **permission**: Permission levels for sensitive operations

All agents implement:
- **EXECUTION DISCIPLINE**: Mandatory execution protocol block
- **RESPONSE FORMAT**: Standardized output structure
- **FAILURE PROTOCOL**: 3-strike escalation pattern
- **STRUCTURED OUTPUT**: JSON/Markdown templates for findings

See `opencode.jsonc` for full configuration details.

## File Locations

All agent definition files are located in:
```
/home/ap/.config/opencode/agent/
```

Primary agent configuration:
```
/home/ap/.config/opencode/armis-purple-latest.md
/home/ap/.config/opencode/opencode.jsonc
```

## Complete Agent File Listing

| Agent File | Type | Phase |
|------------|------|-------|
| `recon-agent.md` | Reconnaissance | Phase 1 |
| `vuln-analysis-agent.md` | Vulnerability Analysis | Phase 1 |
| `webapp-vuln-agent.md` | Web App Vulnerability Analysis | Phase 1 |
| `container-security-agent.md` | Container Security | Phase 1 |
| `auth-bypass-agent.md` | Authentication Testing | Phase 1 |
| `dataflow-mapping-agent.md` | Dataflow Mapping | Phase 1 |
| `certificate-agent.md` | Certificate Analysis | Phase 1 |
| `compliance-agent.md` | Compliance Assessment | Phase 1 |
| `exploitation-agent.md` | Exploitation | Phase 2 |
| `webapp-exploit-agent.md` | Web App Exploitation | Phase 2 |
| `cloud-pivot-agent.md` | Cloud Pivot | Phase 2 |
| `reverse-tunnel-agent.md` | Reverse Tunneling | Phase 2 |
| `lateral-movement-agent.md` | Lateral Movement | Phase 2 |
| `persistence-agent.md` | Persistence Analysis | Phase 2 |
| `data-exfiltration-agent.md` | Data Exfiltration | Phase 3 |
| `evidence-collection-agent.md` | Evidence Collection | Support |
| `tools-arsenal-agent.md` | Tools Management | Support |
| `social-engineering-agent.md` | Social Engineering | Support |
| `report-generation-agent.md` | Report Generation | Support |

## Advanced Orchestration Features

The primary orchestrator includes these advanced capabilities:

### Smart Routing Engine
Automatically routes requests to optimal sub-agents based on keyword patterns and context analysis.

### Prompt Templates Library
Pre-built optimized prompts for each sub-agent type:
- `RECON-FULL`, `RECON-WEB`, `RECON-NETWORK`
- `VULN-COMPREHENSIVE`, `VULN-CVE-SPECIFIC`
- `WEBAPP-FULL-AUDIT`, `WEBAPP-AUTH-FOCUS`
- `EXPLOIT-VERIFIED-VULNS`, `EXPLOIT-PRIVESC`
- `CONTAINER-FULL-ASSESSMENT`
- `COMPLIANCE-CIS`
- `REPORT-EXECUTIVE`, `REPORT-TECHNICAL`

### Workflow Automation
Predefined workflow chains for common assessment patterns:
- `FULL-PENTEST-CHAIN`: Complete penetration test workflow
- `WEB-APP-ASSESSMENT`: Focused web application security assessment
- `QUICK-VULN-SCAN`: Rapid vulnerability identification
- `CONTAINER-SECURITY`: Container and Kubernetes security assessment

### Result Synthesis Templates
Structured formats for combining multi-agent outputs:
- Phase Completion Summary
- Vulnerability Consolidation
- Attack Path Analysis
- Final Assessment Summary

### Fallback Logic
Alternative agent selection when primary choice is unavailable, with graceful degradation modes.

---

## 7-Section Delegation Protocol

When the orchestrator delegates to sub-agents, prompts MUST include:

| Section | Purpose |
|---------|---------|
| **CONTEXT** | Background and current state |
| **OBJECTIVE** | Clear, specific goal |
| **TARGET** | What to test/analyze |
| **SCOPE** | Boundaries and constraints |
| **METHOD** | Approach and techniques to use |
| **OUTPUT** | Required deliverables format |
| **EVIDENCE** | What proof to capture |

---

## Version Information

- **Created**: December 2024
- **Last Updated**: December 2024
- **FedRAMP Test Plan Version**: 2025
- **Assessment Period**: November 2025 - January 2026
- **Total Agents**: 19 specialized sub-agents + 1 orchestrator
- **Design Pattern**: oh-my-opencode integrated
