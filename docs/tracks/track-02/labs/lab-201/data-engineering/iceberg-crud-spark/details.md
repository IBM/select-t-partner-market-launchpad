# Build CRUD-Capable Apache Iceberg Tables with Spark

## Overview

Organizations store raw analytical data — CSVs, logs, exports — directly in object storage because it is cheap and scalable. The problem is that object storage is fundamentally read-only: once a file lands in a bucket, there is no way to update a single row or delete a record without rewriting the entire file.

This lab tackles that challenge by combining **watsonx.data**, **Apache Spark**, and **Apache Iceberg** to turn a flat, read-only `cars.csv` sitting in IBM Cloud Object Storage into a fully CRUD-capable SQL table — without moving the data out of object storage. Using the built-in Spark engine (v3.5) in watsonx.data, you will ingest the CSV into an Iceberg table and run standard SQL `SELECT`, `UPDATE`, `INSERT`, and `DELETE` statements directly against it.

## Benefits

- **Row-level CRUD on object storage:** Update or delete exact records instead of rewriting entire files — enabled by Apache Iceberg's ACID transaction support.
- **Schema evolution & time travel:** Evolve the table schema without downtime and query any previous snapshot of the data.
- **Decoupled compute and storage:** Spark compute scales independently of COS storage, keeping costs low and workloads elastic.

## Step by step hands-on instructions

Proceed to the Lab Guide to begin building CRUD-capable Apache Iceberg tables with Spark.

[:material-check: Get started with the Lab](lab-guide.md){ .md-button .md-button--primary }
