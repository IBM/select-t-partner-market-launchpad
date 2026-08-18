# Getting Started with Data Ingestion in watsonx.data

## Overview

This lab introduces data ingestion into IBM watsonx.data in a finance domain context. You will connect structured financial data sources — such as transaction records, account ledgers, and market feeds — to the watsonx.data lakehouse, making them available for querying, analytics, and downstream AI workloads.

## Benefits

- **Unified Data Layer:** Consolidates financial data from disparate sources into a single governed lakehouse platform.
- **Open Formats:** Stores data in open table formats (Apache Iceberg) that avoid vendor lock-in and support long-term auditability.
- **Performance at Scale:** Leverages Presto/Spark engines for fast, concurrent querying of large financial datasets.
- **Governance Ready:** Integrates with IBM Guardium and built-in metadata tagging to meet financial compliance requirements (SOX, GDPR, etc.).
- **Cost Efficiency:** Separates compute from storage, allowing teams to scale each independently.

## What you will do

In this lab you will use the watsonx.data **Data Manager** to ingest a CSV file into a managed Iceberg table using two different methods:

1. **Local system** — upload a CSV file directly from your machine.
2. **Cloud Object Storage (COS)** — load a CSV file from a registered COS bucket.

## Pre-requisites

- Access to an IBM watsonx.data web console.
- A sample CSV file containing financial records.
- A Cloud Object Storage bucket with the CSV file uploaded (for Part 2).

## Step by step hands-on instructions

Proceed to the Lab Guide to begin the hands-on data ingestion exercise.

[:material-check: Get started with the Lab](lab-guide.md){ .md-button .md-button--primary }
