# SecureOne Release Notes

## SecureGrep Initial SAST Scanning & AI Automatic Remediation Foundation

**Release: September 2026**

SecureOne continues to expand its application security capabilities with the introduction of **SecureGrep initial SAST scanning** and the foundation for **Continuous AI Automatic Remediation**.

This release integrates SecureGrep with SecureOne and the SecureOne Scan Agent, while also introducing the UI, backend routing, database models, and configuration management required for AI Automatic Remediation.

The next phase will introduce the actual continuous AI remediation engine, including automatic fix generation, security re-scanning, validation, Pull Request creation, configurable approval, and future automated merge capabilities.

---

# 🚀 What's New

## 1. SecureGrep Initial SAST Scanning

SecureOne now integrates **SecureGrep** as an initial Static Application Security Testing (SAST) capability.

SecureGrep enables SecureOne to analyze application source code and identify potential security vulnerabilities and coding issues.

### Key capabilities

* Initial SecureGrep SAST scanning
* Repository-based source-code scanning
* SecureGrep rule-pack integration
* Support for customized SecureGrep rules
* Container-based SecureGrep execution
* Integration with SecureOne Scan Agent
* SecureGrep scan result collection
* Integration of findings into the SecureOne security workflow

This provides an additional SAST scanning capability while leveraging the existing SecureOne scanning architecture.

---

# 2. SecureGrep Integration with SecureOne

SecureGrep is now integrated into the SecureOne platform and can participate in the existing SecureOne scanning workflow.

The integration allows SecureOne to manage the scanning process and process SecureGrep results as part of the broader application security workflow.

### SecureOne integration includes

* SAST scan configuration
* Repository scanning
* SecureGrep scanner execution
* Scan result collection
* Finding processing
* Security finding visibility
* Integration with existing scan execution infrastructure

The existing SecureOne scanning architecture remains the foundation for this integration.

---

# 3. SecureGrep Integration with SecureOne Scan Agent

SecureGrep is integrated with the **SecureOne Scan Agent** using the existing container-based scanning architecture.

The Scan Agent handles the SecureGrep workload in an isolated container and returns the results to SecureOne.

### Scan Flow

```text
Repository
     │
     ▼
SecureOne
     │
     │ Scan Request
     ▼
SecureOne Scan Agent
     │
     │ Start SecureGrep Container
     ▼
SecureGrep SAST Scan
     │
     ▼
Scan Results
     │
     ▼
SecureOne
     │
     ▼
Security Findings
```

### Benefits

* Container-isolated scanner execution
* Reuse of existing Scan Agent infrastructure
* Centralized scan management
* Consistent scan execution
* Scalable architecture
* Support for customized SecureGrep rules
* Foundation for future organization and campaign-level SAST scanning

---

# 🤖 4. AI Automatic Remediation Foundation

This release introduces the **AI Automatic Remediation configuration framework** within SecureOne.

The current implementation establishes the foundation required for continuous AI-powered remediation.

### Included in this release

* AI Automatic Remediation UI
* Remediation configuration workflow
* Backend router/API
* Database models
* Persistent database storage
* Configuration management
* Integration with the SecureOne application architecture

Administrators and security leads can configure AI Automatic Remediation settings through SecureOne.

---

# 🔧 Current AI Automatic Remediation Status

The current release provides the **configuration and management foundation**.

The actual automatic remediation engine is **not yet executing code fixes in this release**.

The current workflow is:

```text
Security Finding
       │
       ▼
AI Automatic Remediation Configuration
       │
       ▼
Configuration Stored in Database
```

The next phase will activate the continuous remediation workflow.

---

# 🔮 Coming Next — Continuous AI Automatic Remediation

The next phase of SecureOne AI Automatic Remediation will introduce a continuous, automated remediation process.

The system will be configuration-driven and will automatically begin remediation when the required configuration and scan data are available.

### Planned workflow

```text
Scan Repository
      │
      ▼
Security Findings Available
      │
      ▼
Check AI Remediation Configuration
      │
      ▼
AI Analyzes Finding + Code Context
      │
      ▼
Generate AI Fix
      │
      ▼
Apply AI-Generated Fix
      │
      ▼
Re-Scan Modified Code
      │
      ├───────────────┐
      │               │
      ▼               ▼
Existing Finding   New Finding
Still Present?     Introduced?
      │               │
      └───────┬───────┘
              │
              ▼
       Validation Result
              │
       ┌──────┴──────┐
       │             │
      Fail          Pass
       │             │
       ▼             ▼
 Require Review   Create PR
                     │
                     ▼
              Configured Workflow
                     │
              ┌──────┴──────┐
              ▼             ▼
          Manual Review   Automated QA
              │             │
              ▼             ▼
           Approval      QA Passed
              │             │
              └──────┬──────┘
                     ▼
                   Merge
```

---

# 🔄 AI Fix Validation Through Re-Scanning

A critical part of the planned automatic remediation workflow is **security validation through re-scanning**.

After AI generates a remediation, SecureOne will scan the modified code again.

The system will verify that:

* The original security finding has been resolved.
* The AI-generated change does not introduce new security findings.
* The remediation is consistent with the relevant security finding.
* The resulting code passes the configured security validation.

If the original finding remains or new security findings are introduced, the remediation will not automatically proceed to the next stage.

This creates a continuous security feedback loop:

**Find → Fix → Re-Scan → Validate → Proceed**

---

# 📋 AI Remediation Pull Requests

When an AI-generated fix successfully passes the configured security validation, SecureOne will be able to create a **Pull Request** containing the remediation.

The Pull Request behavior will be configurable by the organization.

Administrators or security leads will be able to determine how AI-generated changes move through the development workflow.

### Planned configuration options

#### PR Creation

Organizations can configure whether they want SecureOne to:

* Automatically create a Pull Request after successful validation.
* Require an approval step before creating a Pull Request.
* Keep the remediation available for manual review.

#### PR Approval and Merge

Organizations will also be able to configure how Pull Requests are approved and merged.

Possible workflows include:

```text
AI Fix
  │
  ▼
Security Re-Scan
  │
  ▼
Create PR
  │
  ├── Manual Review → Approve → Merge
  │
  ├── Configured Automated Approval → Merge
  │
  └── Automated QA → Pass → Configured Merge
```

The level of automation will remain under administrator/security-lead control.

---

# 🧪 Automated QA Integration

SecureOne will also explore integration with existing **automated QA and testing workflows**.

The goal is to allow AI-generated changes to pass through both security validation and automated QA before being merged.

### Planned workflow

```text
AI-Generated Fix
       │
       ▼
Security Re-Scan
       │
       ▼
No Existing/New Findings
       │
       ▼
Create Pull Request
       │
       ▼
Automated QA Testing
       │
       ├── Failed ──► Stop / Require Review
       │
       ▼
     Passed
       │
       ▼
Configured Approval
       │
       ▼
     Merge
```

This provides an additional validation layer before AI-generated changes are merged into the codebase.

---

# 🎛️ Configurable Automation Levels

SecureOne's long-term AI remediation workflow is designed to support different levels of automation.

Organizations will be able to determine how much human involvement is required.

| Mode              | Planned Behavior                                                              |
| ----------------- | ----------------------------------------------------------------------------- |
| Review Only       | AI generates a remediation for security-team review                           |
| PR Assisted       | AI generates the fix and creates a PR                                         |
| Approval Required | PR requires administrator/security-lead approval                              |
| QA Controlled     | Security scan and automated QA must pass                                      |
| Automated         | Validated changes can proceed through configured automated approval and merge |

This allows organizations to adopt AI remediation according to their own security and development policies.

---

# 🔐 Security and Governance

SecureOne is designing AI Automatic Remediation as a **controlled and configurable workflow**.

The system will not simply generate a code change and immediately merge it without validation.

The planned process includes:

**AI Generation → Security Re-Scan → Existing Finding Check → New Finding Check → PR → Optional QA → Configured Approval → Merge**

Organizations will be able to determine the appropriate level of automation.

---

# 🗺️ Product Roadmap

## September 2026 — Current Release

### SecureGrep SAST

* Initial SecureGrep SAST capability
* SecureGrep integration with SecureOne
* SecureGrep integration with SecureOne Scan Agent
* Container-based SecureGrep execution
* SecureGrep rule-pack support
* Customized rule support
* Security finding integration

### AI Automatic Remediation Foundation

* AI remediation UI
* Remediation configuration
* Backend router/API
* Database models
* Database persistence
* Configuration management

---

## End of September 2026 — Planned

### Continuous AI Automatic Remediation

* Automatic remediation workflow
* AI-generated security fixes
* Code-context analysis
* Automatic application of generated fixes
* Security re-scanning
* Existing-finding validation
* New-finding detection
* Remediation validation
* Pull Request generation
* Configurable PR workflow
* Configurable approval workflow

---

## Future Enhancements

### AI Remediation + Development Workflow

* Automated QA integration
* Additional code validation
* Configurable PR approval
* Configurable automatic merge
* Security + QA validation before merge
* Expanded AI remediation coverage
* Continuous remediation workflows

---

# 🔬 2027 Research & Innovation

SecureOne will continue researching the next generation of AI-driven application security capabilities.

Areas of research planned for **2027** include:

### Auto AI

* Autonomous security workflows
* Continuous AI-driven analysis
* Automated security decision workflows
* AI-driven remediation orchestration
* Greater automation across the application security lifecycle

### AI-Powered Penetration Testing

SecureOne will also research **AI-powered penetration testing** capabilities, including:

* AI-assisted penetration testing
* Automated security testing
* Intelligent attack-path analysis
* Continuous security validation
* AI-driven vulnerability discovery
* Integration of penetration testing with remediation workflows

These areas are part of the longer-term SecureOne research and development roadmap.

---

# 🎯 Long-Term SecureOne Vision

The long-term goal is to evolve SecureOne toward a **continuous AI-powered application security lifecycle**.

```text
              Repository
                   │
                   ▼
           Security Scanning
                   │
                   ▼
           Security Findings
                   │
                   ▼
              AI Analysis
                   │
                   ▼
           AI Remediation
                   │
                   ▼
             Re-Scanning
                   │
                   ▼
        Security Validation
                   │
                   ▼
             Pull Request
                   │
                   ▼
            Automated QA
                   │
                   ▼
        Approval / Automation
                   │
                   ▼
                Merge
                   │
                   └──────────────┐
                                  │
                                  ▼
                         Continuous Cycle
```

The objective is to evolve SecureOne from a platform that primarily **finds vulnerabilities** into a platform that can continuously:

**Detect → Understand → Remediate → Re-Scan → Validate → Deliver**

while keeping organizations in control of the level of automation.

---

# 📦 Release Summary

This release establishes two important foundations for SecureOne:

### SecureGrep

**Initial SAST scanning integrated with SecureOne and SecureOne Scan Agent.**

### AI Automatic Remediation

**Configuration, UI, API, and database foundation for the upcoming continuous AI remediation workflow.**

The next phase will bring the two capabilities closer together by enabling AI to act on security findings, generate remediation changes, re-scan the resulting code, validate that existing findings are resolved and no new findings are introduced, and then move the validated change through a configurable Pull Request and approval workflow.

### Current

**SecureGrep SAST: Available**

**AI Automatic Remediation Configuration: Available**

### Coming Next

**Continuous AI Automatic Remediation: Targeted for end of September 2026**

### 2027 Research

**Auto AI and AI-Powered Penetration Testing**

---

**SecureOne — Detect. Understand. Remediate. Validate.**
