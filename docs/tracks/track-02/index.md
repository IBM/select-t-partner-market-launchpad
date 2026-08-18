# Track 02 — Build intelligent applications

![track2-hero](../../assets/images/track02-hero.png)
*AI Generated image*

## Track Overview

| Fields | Details |
|-------|--------|
| **Products** | :material-numeric-1-box: [watsonx.data](https://www.ibm.com/products/watsonx-data)<br> :material-numeric-2-box: [watsonx.data Intelligence](https://www.ibm.com/products/watsonx-data-intelligence)<br> :material-numeric-3-box: [watsonx.data Integration](https://www.ibm.com/products/watsonx-data-integration)<br> |
| **Target Persona** | Select-t growth partners, Application Developers/Technical Leaders and Select-t clients|
| **Overview sessions** | 2 |
| **Lab sessions** | 4 |
| **Estimated Duration** | ~6–7 hrs (excluding breaks) |

---

## Learning Journey

```mermaid
flowchart LR
    theory["<strong>Overview</strong><br/>What & Why"] --> lab101["<strong>Lab 101</strong><br/>Basics"]
    lab101 --> lab201["<strong>Lab 201</strong><br/>Fundamentals"]
    lab201 --> lab301["<strong>Lab 301</strong><br/>Intermediate"]
    lab301 --> lab401["<strong>Lab 401</strong><br/>Advanced"]
```

<!-- !!! warning "Before You Begin"

    - Complete the [Program Overview](../../program/overview.md) if you haven't already.
    - Create an IBMid by referring to the [instructions here](../../facilitator/create-ibm-id.md).
    - Ensure your lab environment is set up per the [Track 02 Lab Environment Setup Guide](lab-environment-setup.md).

---

## Overview

<div class="grid cards" markdown>

- :material-lightbulb-on: **[Market Landscape of Intelligent Applications](theory/what-and-why.md)**
  Introduction to the market landscape and IBM's vision and offerings in that market.

- :material-package-variant: **[Product Overview](theory/product-overview.md)**<br>
  Introduction to the select-t focused products

</div>

---

## Hands-on Labs

### Lab 101 - Basics lab

!!! tip "Goal"
    In this basic lab, you'll learn core concepts, explore the architecture overview, and complete the foundational setup. You'll understand what watsonx.data does and why it exists through hands-on experience in your chosen domain.

<div class="grid cards" markdown>

-   :material-placeholder: **Lab 101 Use Case 1**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

-   :material-placeholder: **Lab 101 Use Case 2**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

</div>

!!! note "Learning Objectives"
    By the end of this lab, you will be able to:

    - TBD
    - TBD
    - TBD

---

### Lab 201 - Foundational lab

!!! tip "Goal"
    In this foundational lab, you'll build upon the basics and dive deeper into fundamental concepts. You'll work with more advanced features and learn how to implement practical solutions in your chosen domain.

<div class="grid cards" markdown>

-   :material-placeholder: **Lab 201 Use Case 1**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

-   :material-placeholder: **Lab 201 Use Case 2**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

</div>

!!! note "Learning Objectives"
    By the end of this lab, you will be able to:

    - TBD
    - TBD
    - TBD

---

### Lab 301 - Intermediate lab

!!! tip "Goal"
    In this intermediate lab, you'll tackle more complex scenarios and integrate multiple components. You'll learn advanced techniques and best practices for building production-ready intelligent applications in your domain.

<div class="grid cards" markdown>

-   :material-placeholder: **Lab 301 Use Case 1**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

-   :material-placeholder: **Lab 301 Use Case 2**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

</div>

!!! note "Learning Objectives"
    By the end of this lab, you will be able to:

    - TBD
    - TBD
    - TBD

---

### Lab 401 - Advanced lab

!!! tip "Goal"
    In this advanced lab, you'll learn about data governance, security, analytics integration, and implementing production-grade intelligent applications. You'll learn advanced techniques and best practices for building production-ready solutions in your domain.

<div class="grid cards" markdown>

-   :material-placeholder: **Lab 401 Use Case 1**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

-   :material-placeholder: **Lab 401 Use Case 2**

    ---

    Description coming soon.
    
    [:octicons-arrow-right-24: Start Lab](#){ .md-button .md-button--primary }

</div>

!!! note "Learning Objectives"
    By the end of this lab, you will be able to:

    - TBD
    - TBD
    - TBD

---

## Support

<div class="grid cards" markdown>

- :material-wrench: **[Troubleshooting](troubleshooting.md)**
  Common issues and solutions

</div> -->

## Hands-on Labs

!!! tip "Before you begin"
    Make sure your lab environment is set up: [Lab Environment Setup](lab-environment-setup.md)

### Lab 101 - Basics lab

!!! tip "Goal"
    In this basic lab, you'll learn core concepts, explore the architecture overview, and complete the foundational setup. You'll understand the key products and why they exist through hands-on experience in your chosen domain.

<div class="grid cards" markdown>

-   :material-database-arrow-up: **Getting Started with Data Ingestion**

    **Domain: Finance**

    ---

    Ingest financial CSV data into watsonx.data using local file upload and Cloud Object Storage.

    [:octicons-arrow-right-24: Start Lab](labs/lab-101/finance/data-ingestion/details.md){ .md-button .md-button--primary }

</div>

!!! note "Learning Objectives"
    By the end of this lab, you will be able to:

    - Ingest structured data into watsonx.data using the Data Manager
    - Load data from both local file system and Cloud Object Storage
    - Register ingested data as a managed table in the watsonx.data catalog

---

### Lab 201 - Fundamentals lab

!!! tip "Goal"
    In this foundational lab, you'll build upon the basics and dive deeper into core platform capabilities. You'll work with more advanced features and learn how to implement practical intelligent application solutions in your chosen domain.

<div class="grid cards" markdown>

-   :material-database: **Build CRUD-Capable Apache Iceberg Tables with Spark**

    **Domain: Data Engineering**

    ---

    Turn flat CSV files in object storage into fully CRUD-capable SQL tables using Apache Spark and Apache Iceberg on watsonx.data.

    [:octicons-arrow-right-24: Start Lab](labs/lab-201/data-engineering/iceberg-crud-spark/details.md){ .md-button .md-button--primary }

-   :material-store: **Unified Data Access Through Federation in watsonx.data**

    **Domain: Retail**

    ---

    Use watsonx.data's federation capabilities to create a unified query layer across siloed retail data sources — without moving data.

    [:octicons-arrow-right-24: Start Lab](labs/lab-201/retail/data-federation/details.md){ .md-button .md-button--primary }

</div>

!!! note "Learning Objectives"
    By the end of this lab, you will be able to:

    - Build CRUD-capable Apache Iceberg tables using Spark on watsonx.data
    - Run row-level INSERT, UPDATE, and DELETE operations on object storage data
    - Federate queries across multiple data sources without data movement

---

Lab related support: TBD