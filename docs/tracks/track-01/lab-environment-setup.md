# Lab Environment Setup — Track 01

Provision and validate all lab environments **at least 24 hours before** the session. Never leave this to the morning of.

---

## Track 01 Products

This track focuses on:

- [watsonx Orchestrate](https://www.ibm.com/products/watsonx-orchestrate)
- [watsonx.governance](https://www.ibm.com/products/watsonx-governance)
- [IBM Bob](https://bob.ibm.com/)

---

## Environment Requirements

| Requirement | Detail |
|-------------|--------|
| **Platform** | IBM Cloud / watsonx SaaS |
| **Accounts needed** | One per attendee (~20 total) |
| **Pre-provisioned resources** | watsonx Orchestrate instances<br>watsonx.governance access<br>IBM Bob access<br>API keys for integrations |
| **Network** | Stable internet, no restrictive firewall<br>Access to IBM Cloud domains<br>Access to watsonx endpoints |
| **Attendee machine** | Any OS with a modern browser (Chrome/Firefox/Edge)<br>Terminal access for CLI operations |

---

## Setup Steps

### Step 1 — Provision watsonx Orchestrate Instances

```bash
# Provision watsonx Orchestrate instances for each attendee
# Replace with actual IBM Cloud CLI commands or provisioning script
ibmcloud login --apikey <API_KEY>
ibmcloud target -r <REGION>

# Create instances (example - adjust based on actual provisioning method)
for i in {1..20}; do
  echo "Provisioning watsonx Orchestrate instance for user$i"
  # Add actual provisioning command here
done
```

### Step 2 — Configure watsonx.governance Access

Ensure each attendee account has appropriate access to watsonx.governance:

```bash
# Grant governance access to each user
# Replace with actual access management commands
echo "Configure watsonx.governance access for all users"
```

### Step 3 — Set Up IBM Bob Access

Verify IBM Bob access for all attendee accounts:

1. Navigate to [IBM Bob](https://bob.ibm.com/)
2. Verify each user can authenticate
3. Confirm access to required Bob features for the labs

### Step 4 — Validate Access

Run this check for each account before the session:

```bash
# Validation script for Track 01 environments
#!/bin/bash

for i in {1..20}; do
  echo "Validating environment for user$i"
  
  # Check watsonx Orchestrate access
  # Check watsonx.governance access
  # Check IBM Bob access
  # Verify API connectivity
  
  echo "✓ user$i environment validated"
done
```

### Step 5 — Prepare Credentials Pack

Create a simple table with one row per attendee:

| Seat | Username | Password | watsonx Orchestrate URL | watsonx.governance URL | IBM Bob URL |
|------|----------|----------|-------------------------|------------------------|-------------|
| 1 | user01 | xxxxxxxx | https://... | https://... | https://bob.ibm.com |
| 2 | user02 | xxxxxxxx | https://... | https://... | https://bob.ibm.com |
| ... | ... | ... | ... | ... | ... |

!!! warning
    Distribute credentials on the day — not in advance — to avoid pre-session tinkering that breaks the environment state.

---

## Pre-Lab Checklist

Before each lab session, verify:

- [ ] All watsonx Orchestrate instances are running
- [ ] watsonx.governance access is functional
- [ ] IBM Bob is accessible
- [ ] Sample data/agents are pre-loaded (if required)
- [ ] Network connectivity is stable
- [ ] Credentials are prepared and secured

---

## Lab-Specific Requirements

### Lab 101 — Basics
- Pre-configured sample agents (optional)
- Access to skill catalog

### Lab 201 — Fundamentals
- API keys for external integrations
- Sample workflows/templates

### Lab 301 — Intermediate
- Advanced governance policies configured
- Integration endpoints ready

### Lab 401 — Advanced
- Production-like environment setup
- Full governance framework enabled

---

## Teardown

After the session, deprovision all environments within 48 hours to avoid unnecessary cost or license usage.

```bash
#!/bin/bash
# Teardown script for Track 01 environments

for i in {1..20}; do
  echo "Deprovisioning environment for user$i"
  
  # Delete watsonx Orchestrate instances
  # Revoke watsonx.governance access
  # Clean up API keys
  
  echo "✓ user$i environment deprovisioned"
done
```

---

## Troubleshooting

Common issues and solutions:

| Issue | Solution |
|-------|----------|
| Cannot access watsonx Orchestrate | Verify IBM Cloud authentication and region |
| Governance policies not loading | Check IAM permissions and policy sync |
| Bob integration failing | Verify network access and authentication tokens |
| API rate limits hit | Implement request throttling or increase limits |

For additional support, see the [Track 01 Troubleshooting Guide](troubleshooting.md).