---
type: project
title: Cloud Modernisation
company: Apollo
project: Data Platform
role: Data Architecture & Analytics Consultant
domain: Sports Performance Analytics
project_type:
  - Data Platform Modernisation
  - Cloud Architecture
  - Data Engineering

summary: >
  Designed and implemented a cloud-native Azure analytical platform to
  decouple analytics from Apollo's operational SQL Server infrastructure.
  Built a reusable multi-client architecture using Azure Data Lake Storage,
  Parquet, Azure Synapse Serverless, and Bronze/Silver/Gold data modelling,
  with metadata-driven pipelines, CI/CD, automated testing, and
  report-ready Gold datasets.

technologies:
  - Microsoft Azure
  - Azure Data Lake Storage Gen2
  - Azure Synapse Serverless SQL
  - Azure Data Factory
  - Parquet
  - T-SQL
  - SQL Server
  - Tableau
  - Git
  - CI/CD

skills:
  - Data Architecture
  - Data Engineering
  - Cloud Architecture
  - Azure
  - Data Platform Modernisation
  - Dimensional Modelling
  - Medallion Architecture
  - Data Modelling
  - Analytics Engineering
  - Metadata-Driven Pipelines
  - Multi-Client Architecture
  - Data Quality
  - CI/CD
  - Technical Leadership

key_contributions:
  - Designed and implemented a new Azure analytical data platform.
  - Decoupled analytical processing from operational SQL Server workloads.
  - Introduced a Bronze, Silver, and Gold modelling architecture.
  - Designed conformed dimensional models with explicit model grain.
  - Built reusable metadata-driven ingestion and transformation pipelines.
  - Designed the platform to support multiple clients from a shared codebase.
  - Introduced Git-based development, pull requests, testing, and CI/CD.
  - Migrated reporting workloads from legacy SQL Server views to Gold models.
  - Established reproducible Serverless SQL models over Parquet data.
  - Created a platform suitable for both BI and future AI consumption.

architecture:
  source:
    - SQL Server
  ingestion:
    - Azure Data Factory
  storage:
    - Azure Data Lake Storage Gen2
    - Parquet
  query_engine:
    - Azure Synapse Serverless SQL
  layers:
    - Bronze
    - Staging
    - Intermediate
    - Silver
    - Gold
  consumers:
    - Tableau
    - Analytics
    - AI

design_principles:
  - Separate analytical workloads from operational systems.
  - Prefer shared models over client-specific implementations.
  - Use configuration rather than pipeline duplication.
  - Define explicit grain for analytical models.
  - Centralise reusable business logic upstream of reporting.
  - Treat analytical datasets as reproducible outputs.
  - Keep platform definitions in source control.
  - Build data quality into the development lifecycle.

outcomes:
  - Established a reusable Azure analytical platform.
  - Separated analytics from operational SQL Server workloads.
  - Created a shared analytical architecture supporting multiple clients.
  - Reduced duplication through parameterised pipelines and shared models.
  - Established consistent dimensional modelling across client implementations.
  - Introduced repeatable client onboarding.
  - Introduced CI/CD-controlled deployment and automated data-quality testing.
  - Enabled migration of Tableau reporting away from legacy SQL Server views.
  - Created a governed analytical foundation for future AI use cases.

related:
  - architecture-review.md
  - overview.md
---

# Cloud Modernisation

## Summary

Modernised Apollo's legacy data platform into a cloud-native Azure architecture supporting multiple sports organisations from a shared, configurable codebase.

The platform moved analytical workloads away from direct dependency on operational SQL Server databases and established a layered architecture using Azure Data Lake Storage, Parquet and Azure Synapse Serverless.

The resulting platform provides repeatable ingestion, conformed dimensional modelling, report-ready datasets, automated deployment and a standard onboarding process for new clients.

## Problem

The existing analytical architecture relied heavily on operational SQL Server infrastructure and client-specific reporting logic.

This created several problems:

- analytical workloads competed with operational workloads
- transformations and stored procedures were difficult to maintain
- reporting logic was duplicated across clients
- infrastructure and storage costs were higher than necessary
- onboarding new clients required significant manual configuration
- downstream reporting was tightly coupled to the source application schema

The platform needed to support multiple clients while allowing genuine client-specific differences without creating separate implementations for every organisation.

## Architecture

Designed and implemented a medallion-style Azure data platform:
**Source systems → Bronze → Staging / Intermediate → Silver → Gold → Tableau / downstream consumers**

### Bronze

Operational SQL data is ingested into Azure Data Lake Storage and stored as Parquet, providing a reproducible source layer without requiring analytical workloads to query operational databases directly.

### Staging and Intermediate

Staging provides the boundary between source-conformed data and analytical transformations, handling schema alignment, datatype conversion, null handling and basic cleansing.

Reusable or more complex transformations are moved into intermediate models, while static mappings and reference data are maintained as version-controlled seeds.

### Silver

Silver provides the conformed analytical model.

Source data is transformed into reusable dimensions and facts with:

- explicit grain
- consistent naming
- deduplication
- standardised datatypes
- reusable business logic
- dimensional relationships

Shared models are used across clients by default, with client-specific overrides available where source behaviour genuinely differs.

### Gold

Gold provides flattened, report-ready datasets built from Silver dimensions and facts.

Business logic and dimensional joins are resolved upstream so Tableau and other consumers do not need to recreate metric logic independently.

This allowed existing reports to be migrated away from legacy SQL Server views onto the new data platform.

## Serverless Architecture

The platform uses Azure Synapse Serverless SQL with analytical data stored as Parquet in ADLS and exposed through external tables.

Silver and Gold datasets can be recreated deterministically from source data and version-controlled SQL.

Rather than maintaining complex schema migration chains, model changes can be deployed and the affected analytical datasets rebuilt from their definitions.

## Metadata-Driven Pipelines

Built generic ingestion and transformation pipelines rather than separate pipelines for each client or dataset.

Runtime behaviour is controlled through generated configuration including:

- ingestion metadata
- table dependencies
- client configuration
- pipeline parameters

Dependency metadata determines which upstream Bronze and Silver models must be refreshed for requested Gold outputs.

## Multi-Client Design

The platform was designed so new clients could reuse the same core implementation.

Client identity and behaviour are supplied through configuration and pipeline parameters rather than hardcoded pipeline definitions.

Core pipelines and shared Silver models remain common, while controlled extension points support client-specific requirements.

This reduces onboarding effort and prevents the platform becoming a collection of client-specific forks.

## Software Development Lifecycle

Introduced a Git-based engineering workflow:
**Jira → feature branch → models → tests → documentation → pull request → peer review → deployment → production QA**

SQL models, pipeline definitions, configuration generation and documentation are maintained in source control and deployed through CI/CD.

## Data Quality

Testing was incorporated into the development process, including:

- model grain and uniqueness
- null-key detection
- referential integrity
- valid value checks
- source-to-target reconciliation
- downstream report validation

Migrated Gold datasets can also be reconciled against legacy SQL Server reporting views before reports are repointed.

## Key Design Decisions

### Shared models by default

Core pipelines and Silver models are shared across clients. Client-specific implementations are introduced only where the underlying source behaviour genuinely differs.

### Configuration over duplication

Client behaviour is parameterised rather than implemented by copying pipelines or datasets.

### Rebuild rather than migrate

Silver and Gold are reproducible analytical outputs. Where practical, datasets are rebuilt from version-controlled definitions rather than maintaining complex schema migration history.

### Business logic upstream of reporting

Reusable transformations and metric logic belong in the analytical model rather than individual Tableau workbooks.

### Explicit model grain

Fact, dimension and Gold models have a defined grain, preventing incompatible analytical levels from being mixed.

### Source control as the platform definition

SQL models, pipelines, configuration, tests and documentation are maintained in Git and deployed through an engineering workflow rather than managed manually in Azure.

## Outcome

The modernisation established a reusable Azure analytical platform rather than a collection of client-specific reporting pipelines.

It provided:

- separation of analytics from operational SQL workloads
- lake-based Parquet storage and serverless analytical compute
- a reusable Bronze / Silver / Gold architecture
- consistent dimensional modelling
- parameterised multi-client ingestion
- repeatable client onboarding
- CI/CD-controlled deployment
- automated data-quality testing
- report-level reconciliation
- a foundation for BI and AI-driven data consumption
