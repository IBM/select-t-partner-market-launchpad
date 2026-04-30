# Lab Environment Setup — Track 04

Provision and validate all lab environments **at least 24 hours before** the session. Never leave this to the morning of.

---

## Track 04 Products

This track focuses on:

- PowerVS
- Fusion
- Flush

!!! warning "Work in progress"
    This track is currently under development. Environment setup details will be finalized as the track content is completed.

---

## Environment Requirements

| Requirement | Detail |
|-------------|--------|
| **Platform** | IBM Cloud / Hybrid Cloud / On-premises |
| **Accounts needed** | One per attendee (~20 total) |
| **Pre-provisioned resources** | PowerVS instances<br>Fusion access<br>Flush configuration<br>Hybrid cloud connectivity |
| **Network** | Stable internet, no restrictive firewall<br>VPN access (if required)<br>Direct Link or Transit Gateway (for hybrid scenarios) |
| **Attendee machine** | Any OS with a modern browser (Chrome/Firefox/Edge)<br>Terminal access for CLI operations<br>SSH client<br>VPN client (if required) |

---

## Setup Steps

### Step 1 — Provision PowerVS Instances

```bash
# Provision PowerVS instances for each attendee
# Replace with actual IBM Cloud CLI commands or provisioning script
ibmcloud login --apikey <API_KEY>
ibmcloud target -r <REGION>

# Create PowerVS instances
for i in {1..20}; do
  echo "Provisioning PowerVS instance for user$i"
  # Add actual provisioning command here
done
```

### Step 2 — Configure Fusion Access

Set up Fusion platform access:

```bash
# Configure Fusion access for each user
echo "Setting up Fusion access for all users"
```

### Step 3 — Set Up Flush Configuration

Configure Flush for hybrid cloud scenarios:

```bash
# Set up Flush configuration
echo "Configuring Flush for hybrid cloud connectivity"
```

### Step 4 — Configure Hybrid Cloud Connectivity

Set up network connectivity for hybrid scenarios:

```bash
# Configure Direct Link or Transit Gateway
echo "Setting up hybrid cloud connectivity"

# Configure VPN access if needed
echo "Setting up VPN access"
```

### Step 5 — Validate Access

Run this check for each account before the session:

```bash
# Validation script for Track 04 environments
#!/bin/bash

for i in {1..20}; do
  echo "Validating environment for user$i"
  
  # Check PowerVS instance access
  # Check Fusion access
  # Check Flush configuration
  # Verify hybrid cloud connectivity
  # Test network latency
  
  echo "✓ user$i environment validated"
done
```

### Step 6 — Prepare Credentials Pack

Create a simple table with one row per attendee:

| Seat | Username | Password | PowerVS URL | Fusion URL | VPN Config | SSH Key |
|------|----------|----------|-------------|------------|------------|---------|
| 1 | user01 | xxxxxxxx | https://... | https://... | vpn-config-01 | ssh-key-01 |
| 2 | user02 | xxxxxxxx | https://... | https://... | vpn-config-02 | ssh-key-02 |
| ... | ... | ... | ... | ... | ... | ... |

!!! warning
    Distribute credentials on the day — not in advance — to avoid pre-session tinkering that breaks the environment state.

---

## Pre-Lab Checklist

Before each lab session, verify:

- [ ] All PowerVS instances are running
- [ ] Fusion access is functional
- [ ] Flush configuration is correct
- [ ] Hybrid cloud connectivity is working
- [ ] VPN access is configured (if required)
- [ ] SSH keys are distributed
- [ ] Network latency is acceptable
- [ ] Credentials are prepared and secured

---

## Lab-Specific Requirements

### Lab 201 — Fundamentals
- Basic PowerVS configurations
- Fusion platform access

### Lab 301 — Intermediate
- Advanced hybrid cloud scenarios
- Multi-cloud connectivity

### Lab 401 — Advanced
- Production-like hybrid environment
- Full disaster recovery setup

---

## Teardown

After the session, deprovision all environments within 48 hours to avoid unnecessary cost or license usage.

```bash
#!/bin/bash
# Teardown script for Track 04 environments

for i in {1..20}; do
  echo "Deprovisioning environment for user$i"
  
  # Delete PowerVS instances
  # Revoke Fusion access
  # Clean up Flush configurations
  # Remove VPN access
  # Revoke SSH keys
  
  echo "✓ user$i environment deprovisioned"
done
```

---

## Troubleshooting

Common issues and solutions:

| Issue | Solution |
|-------|----------|
| Cannot access PowerVS | Verify IBM Cloud authentication and region |
| Fusion connection failing | Check network access and authentication |
| Hybrid connectivity issues | Verify Direct Link/Transit Gateway status |
| VPN connection timeout | Check VPN configuration and firewall rules |
| High network latency | Verify network path and consider region proximity |

For additional support, see the [Track 04 Troubleshooting Guide](troubleshooting.md).