# Lab Environment Setup — Track 02

Provision and validate all lab environments **at least 24 hours before** the session. Never leave this to the morning of.

---

## Track 02 Products

This track focuses on:

- watsonx.data
- Guardium
- Planning Analytics
- watsonx.data integration

!!! warning "Work in progress"
    This track is currently under development. Environment setup details will be finalized as the track content is completed.

---

## Environment Requirements

| Requirement | Detail |
|-------------|--------|
| **Platform** | IBM Cloud / watsonx SaaS / On-premises |
| **Accounts needed** | One per attendee (~20 total) |
| **Pre-provisioned resources** | watsonx.data instances<br>Guardium access<br>Planning Analytics workspace<br>Database connections<br>Sample datasets |
| **Network** | Stable internet, no restrictive firewall<br>Access to IBM Cloud domains<br>Database connectivity (if applicable) |
| **Attendee machine** | Any OS with a modern browser (Chrome/Firefox/Edge)<br>Terminal access for CLI operations<br>Database client tools (optional) |

---

## Setup Steps

### Step 1 — Provision watsonx.data Instances

```bash
# Provision watsonx.data instances for each attendee
# Replace with actual IBM Cloud CLI commands or provisioning script
ibmcloud login --apikey <API_KEY>
ibmcloud target -r <REGION>

# Create instances (example - adjust based on actual provisioning method)
for i in {1..20}; do
  echo "Provisioning watsonx.data instance for user$i"
  # Add actual provisioning command here
done
```

### Step 2 — Configure Guardium Access

Ensure each attendee account has appropriate access to Guardium:

```bash
# Grant Guardium access to each user
# Replace with actual access management commands
echo "Configure Guardium access for all users"
```

### Step 3 — Set Up Planning Analytics

Configure Planning Analytics workspaces:

```bash
# Set up Planning Analytics for each user
echo "Configure Planning Analytics workspaces"
```

### Step 4 — Load Sample Datasets

Pre-load sample datasets for lab exercises:

```bash
# Load sample data into watsonx.data
echo "Loading sample datasets for Track 02 labs"
```

### Step 5 — Validate Access

Run this check for each account before the session:

```bash
# Validation script for Track 02 environments
#!/bin/bash

for i in {1..20}; do
  echo "Validating environment for user$i"
  
  # Check watsonx.data access
  # Check Guardium access
  # Check Planning Analytics access
  # Verify database connectivity
  # Validate sample data availability
  
  echo "✓ user$i environment validated"
done
```

### Step 6 — Prepare Credentials Pack

Create a simple table with one row per attendee:

| Seat | Username | Password | watsonx.data URL | Guardium URL | Planning Analytics URL |
|------|----------|----------|------------------|--------------|------------------------|
| 1 | user01 | xxxxxxxx | https://... | https://... | https://... |
| 2 | user02 | xxxxxxxx | https://... | https://... | https://... |
| ... | ... | ... | ... | ... | ... |

!!! warning
    Distribute credentials on the day — not in advance — to avoid pre-session tinkering that breaks the environment state.

---

## Pre-Lab Checklist

Before each lab session, verify:

- [ ] All watsonx.data instances are running
- [ ] Guardium access is functional
- [ ] Planning Analytics workspaces are accessible
- [ ] Sample datasets are loaded
- [ ] Database connections are working
- [ ] Network connectivity is stable
- [ ] Credentials are prepared and secured

---

## Lab-Specific Requirements

### Lab 201 — Fundamentals
- Sample data catalogs configured
- Basic query access enabled

### Lab 301 — Intermediate
- Advanced data governance policies
- Integration endpoints configured

### Lab 401 — Advanced
- Production-like data environment
- Full governance and security framework

---

## Teardown

After the session, deprovision all environments within 48 hours to avoid unnecessary cost or license usage.

```bash
#!/bin/bash
# Teardown script for Track 02 environments

for i in {1..20}; do
  echo "Deprovisioning environment for user$i"
  
  # Delete watsonx.data instances
  # Revoke Guardium access
  # Clean up Planning Analytics workspaces
  # Remove sample datasets
  
  echo "✓ user$i environment deprovisioned"
done
```

---

## Troubleshooting

Common issues and solutions:

| Issue | Solution |
|-------|----------|
| Cannot access watsonx.data | Verify IBM Cloud authentication and region |
| Guardium policies not loading | Check IAM permissions and policy sync |
| Planning Analytics connection failing | Verify network access and workspace configuration |
| Sample data not visible | Check data catalog refresh and permissions |

For additional support, see the [Track 02 Troubleshooting Guide](troubleshooting.md).