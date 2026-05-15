# AI Governance use case

## Overview

Consider an enterprise procurement team, where a Compliance Analyst (Sarah) must evaluate third-party vendors before any contract is signed or system access is granted. Typically, Sarah must manually pull security profiles, cross-check policy frameworks like GDPR and ISO 27001, calculate a risk score, and create an audit record — a process that takes several hours per vendor. With the **AI Governance Risk Agent**, she can trigger a full vendor risk assessment by asking something like "Run a risk assessment for Gamma Tech" and the agent will fetch the vendor's security profile, calculate a risk score, check policy compliance, and generate a tamper-evident audit log automatically within minutes. Additionally, she can ask targeted compliance questions like "Is Beta Solutions GDPR compliant?" and the agent will check the relevant policy framework and return a clear compliance verdict. Post-assessment, Sarah can also verify that every evaluation was recorded correctly by asking something like "Show me the audit log for the Acme Corp assessment" — the agent maintains an immutable trail of every decision made. The **AI Governance Risk Agent** also supports red-teaming and adversarial testing, allowing teams to probe the agent with attack patterns like instruction overrides, role-playing exploits, and jailbreak injections — and validate that the agent consistently refuses to deviate from its guardrails.

## Benefits

- **Automated vendor risk assessment:** The AI Governance Risk Agent fetches vendor security profiles, calculates risk scores, checks policy compliance (GDPR, ISO 27001, SOC 2), and generates a tamper-evident audit log — all in a single conversational request.
- **Immutable audit trail:** Every assessment is recorded with a tamper-evident audit log, giving compliance teams the proof they need that due diligence was performed.
- **Adversarial robustness testing:** The agent can be evaluated against real-world attack patterns — instruction overrides, role-playing exploits, and jailbreak injections — to validate that guardrails hold under pressure before production deployment.

## Step by step hands-on instructions

Proceed to the Lab Guide to begin building your AI Agents.

[:material-check: Get started with the Lab](lab-guide.md){ .md-button .md-button--primary }