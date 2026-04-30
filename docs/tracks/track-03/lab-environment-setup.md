# Lab Environment Setup — Track 03

Provision and validate all lab environments **at least 24 hours before** the session. Never leave this to the morning of.

---

## Track 03 Products

This track focuses on:

- Terraform
- Cloudability
- Kubecost
- Instana
- Concert
- Vault
- Verify
- NS1
- Maximo
- WebMethods Hybrid Integration

!!! warning "Work in progress"
    This track is currently under development. Environment setup details will be finalized as the track content is completed.

---

## Environment Requirements

| Requirement | Detail |
|-------------|--------|
| **Platform** | IBM Cloud / Multi-cloud / On-premises |
| **Accounts needed** | One per attendee (~20 total) |
| **Pre-provisioned resources** | Terraform workspaces<br>Cloudability/Kubecost access<br>Instana monitoring instances<br>Concert access<br>Vault instances<br>Verify access<br>NS1 DNS zones<br>Maximo instances<br>WebMethods integration platform |
| **Network** | Stable internet, no restrictive firewall<br>Access to multiple cloud providers (if applicable)<br>Kubernetes cluster access |
| **Attendee machine** | Any OS with a modern browser (Chrome/Firefox/Edge)<br>Terminal access for CLI operations<br>kubectl, terraform CLI installed<br>SSH client |

---

## Setup Steps

### Step 1 — Provision Terraform Workspaces

```bash
# Set up Terraform workspaces for each attendee
# Replace with actual provisioning commands
terraform login

for i in {1..20}; do
  echo "Creating Terraform workspace for user$i"
  # Add actual workspace creation commands
done
```

### Step 2 — Configure Monitoring Tools

Set up Cloudability, Kubecost, and Instana access:

```bash
# Configure monitoring tool access
echo "Setting up Cloudability access"
echo "Setting up Kubecost access"
echo "Setting up Instana monitoring"
```

### Step 3 — Set Up Concert and Vault

Configure Concert and Vault instances:

```bash
# Set up Concert access
echo "Configuring Concert for all users"

# Set up Vault instances
echo "Provisioning Vault instances"
```

### Step 4 — Configure NS1 and Maximo

Set up DNS and asset management:

```bash
# Configure NS1 DNS zones
echo "Setting up NS1 DNS zones"

# Set up Maximo instances
echo "Provisioning Maximo instances"
```

### Step 5 — Set Up WebMethods Integration

Configure WebMethods Hybrid Integration platform:

```bash
# Set up WebMethods integration
echo "Configuring WebMethods Hybrid Integration"
```

### Step 6 — Validate Access

Run this check for each account before the session:

```bash
# Validation script for Track 03 environments
#!/bin/bash

for i in {1..20}; do
  echo "Validating environment for user$i"
  
  # Check Terraform workspace access
  # Check Cloudability/Kubecost access
  # Check Instana monitoring
  # Check Concert access
  # Check Vault connectivity
  # Check Verify access
  # Check NS1 DNS zones
  # Check Maximo access
  # Check WebMethods integration
  
  echo "✓ user$i environment validated"
done
```

### Step 7 — Prepare Credentials Pack

Create a comprehensive credentials table:

| Seat | Username | Password | Terraform | Cloudability | Instana | Concert | Vault | NS1 | Maximo | WebMethods |
|------|----------|----------|-----------|--------------|---------|---------|-------|-----|--------|------------|
| 1 | user01 | xxxxxxxx | https://... | https://... | https://... | https://... | https://... | https://... | https://... | https://... |
| 2 | user02 | xxxxxxxx | https://... | https://... | https://... | https://... | https://... | https://... | https://... | https://... |

!!! warning
    Distribute credentials on the day — not in advance — to avoid pre-session tinkering that breaks the environment state.

---

## Pre-Lab Checklist

Before each lab session, verify:

- [ ] All Terraform workspaces are accessible
- [ ] Monitoring tools (Cloudability, Kubecost, Instana) are functional
- [ ] Concert access is working
- [ ] Vault instances are running
- [ ] Verify access is configured
- [ ] NS1 DNS zones are set up
- [ ] Maximo instances are accessible
- [ ] WebMethods integration platform is ready
- [ ] Kubernetes clusters are available (if required)
- [ ] Network connectivity is stable
- [ ] Credentials are prepared and secured

---

## Lab-Specific Requirements

### Lab 101 — Basics
- Basic Terraform configurations
- Read-only monitoring access

### Lab 201 — Fundamentals
- Terraform state management
- Cost optimization tools configured

### Lab 301 — Intermediate
- Advanced automation workflows
- Integration endpoints ready

### Lab 401 — Advanced
- Production-like multi-cloud environment
- Full observability and automation stack

---

## Teardown

After the session, deprovision all environments within 48 hours to avoid unnecessary cost or license usage.

```bash
#!/bin/bash
# Teardown script for Track 03 environments

for i in {1..20}; do
  echo "Deprovisioning environment for user$i"
  
  # Delete Terraform workspaces
  # Revoke monitoring tool access
  # Clean up Concert/Vault instances
  # Remove NS1 DNS zones
  # Deprovision Maximo instances
  # Clean up WebMethods configurations
  
  echo "✓ user$i environment deprovisioned"
done
```

---

## Troubleshooting

Common issues and solutions:

| Issue | Solution |
|-------|----------|
| Terraform workspace not accessible | Verify authentication tokens and organization access |
| Monitoring data not appearing | Check agent installation and network connectivity |
| Vault sealed/unavailable | Unseal Vault and verify cluster health |
| NS1 DNS propagation delays | Allow time for DNS propagation (up to 5 minutes) |
| Maximo connection timeout | Verify network access and instance status |
| WebMethods integration failing | Check endpoint configuration and credentials |

For additional support, see the [Track 03 Troubleshooting Guide](troubleshooting.md).