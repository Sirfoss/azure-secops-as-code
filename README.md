# Azure SecOps as Code

A security engineering lab built entirely from code: Azure infrastructure in
Terraform, Microsoft Sentinel detections mapped to MITRE ATT&CK, automated
response with human approval, and cloud and AI security posture. Every module
ships with evidence that it works.

> **Status:** in progress (Dec 2026 – Mar 2027). Modules are marked below as they land.
> Everything here runs in my own lab, built for a fictional company. See
> [Evidence rules](EVIDENCE_RULES.md).

## Modules

| # | Module | What it shows | Status |
|---|---|---|---|
| 1 | **Platform baseline** | Log Analytics, Sentinel and Key Vault from Terraform with remote state; GitHub Actions with OIDC (no stored secrets); teardown and rebuild with no portal clicks | Planned · Dec |
| 2 | **Detections as code** | 10 KQL rules mapped to ATT&CK, each with a test that fires it, an alert screenshot and false-positive notes | Planned · Dec – Feb |
| 3 | **Identity and Conditional Access** | Break-glass accounts and an MFA / Conditional Access policy set in Terraform, run in report-only and then enforced | Planned · Jan |
| 4 | **Automated response** | Enrichment, risky-user and device-isolation playbooks deployed from Git; isolation waits for human approval | Planned · Jan – Feb |
| 5 | **Cloud posture** | Defender for Cloud and Azure Policy baseline, storage and Key Vault behind private endpoints, managed identity and least-privilege RBAC, with secure score before and after | Planned · Jan – Feb |
| 6 | **AI security** | A model-backed app behind an API Management AI gateway, with Defender for AI Services; a prompt-injection test traced from alert to response | Planned · Mar |

**Supporting work**

| Item | What it shows | Status |
|---|---|---|
| `scripts/graph-mfa-report/` | Python and Microsoft Graph: MFA registration and sign-in reporting, lab-tenant version | Planned · Jan |
| `docs/threat-model.md` | The fictional company, its assets and the threats the modules address | Planned · Dec |
| Repo skeleton and evidence rules | Structure, `.gitignore`, PR checklist and [evidence rules](EVIDENCE_RULES.md) | Done |

## Repo layout

```
docs/           threat model, architecture diagram, case studies
infra/          Terraform: baseline, identity, posture, ai-gateway
detections/     rules/ (KQL + ATT&CK) and tests/ (how each rule is fired)
playbooks/      response automation (Logic Apps)
scripts/        Python and PowerShell automation
evidence/       screenshots and before/after results
.github/        CI workflows and the PR checklist
```

## How evidence works

Nothing is marked done without proof. Each detection has a test, an alert
screenshot, tuning notes and the date it was last tested. Posture work shows
before-and-after results. Artifacts are labeled **Lab**, **Simulated** or
**Case Study**. Full rules are in [EVIDENCE_RULES.md](EVIDENCE_RULES.md).

## License

MIT
