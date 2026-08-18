---
type: project
title: Architectural Review
company: Apollo
project: Data Platform Modernisation
role: Data Architecture & Analytics Consultant
domain: Sports Performance Analytics
project_type:
  - Data Architecture
  - Strategic Consulting
  - Platform Modernisation

summary: >
  Conducted a comprehensive architectural review of Apollo's data platform and
  developed a detailed modernisation roadmap. Identified critical architectural
  issues stemming from coupled analytics and transactional workloads, and created
  a practical, phased approach to building a mature, scalable data platform on Azure.

technologies:
  - Microsoft Azure
  - SQL Server
  - Tableau
  - Azure Data Factory
  - Azure Data Lake
  - Synapse Serverless
  - Power BI
---

# Apollo — Architecture Review

## Overview

I worked with Apollo as a **Data Architecture & Analytics Consultant**, conducting an architectural review of the company's data platform and developing a roadmap for modernising its data and analytics architecture.

Apollo operates a sports performance platform for elite athletic organisations. Its application infrastructure was hosted on Azure, with SQL Server databases supporting transactional application workloads and Tableau providing much of the analytical and reporting capability.

The review focused on the data ecosystem: ingestion, storage, database architecture, analytics and reporting, Azure infrastructure costs, operational maturity, observability, and the organisation's ability to support future AI and machine-learning initiatives.

The central architectural problem was that **application and analytics workloads were tightly coupled**. Analytical queries, transformations and Tableau extracts were running directly against production SQL Server databases. This created performance contention, unnecessary compute and storage costs, operational risk, and limited opportunities to introduce consistent data modelling and business logic.

My work combined **data architecture, cloud architecture, analytics engineering and cost optimisation**, with a particular focus on creating a practical path from Apollo's existing architecture towards a more mature data platform.

---

## The Problem

Apollo had grown rapidly, and several architectural decisions that had been reasonable at smaller scale were becoming constraints as the platform expanded.

The principal issues identified were:

* Analytics workloads running directly against production transactional databases.
* Tableau extracts querying application databases and creating significant database load.
* Full Tableau extracts rather than incremental extraction.
* Analytics transformations implemented directly in production SQL Server databases.
* Heavy reliance on views and stored procedures for analytical processing.
* No clear separation between transactional and analytical data models.
* No dedicated development and production environments for data work.
* Limited version control and no mature CI/CD process for data transformations.
* No formal data quality testing.
* Limited observability and alerting across the data platform.
* Infrastructure sizing driven largely by reactive performance problems.
* Expensive premium SSD storage, particularly on Tableau servers.
* Limited documentation and operational processes.

This created a reactive operating model: problems were frequently discovered after they affected users or were reported by clients, and infrastructure was often scaled to address symptoms rather than underlying architectural problems.

---

## Architectural Assessment

A key conclusion of the review was that Apollo's data architecture needed to **decouple analytics from application workloads**.

The existing architecture effectively pushed analytical processing in two directions:

1. Down into the application database, where views, stored procedures and analytical queries consumed production compute.
2. Up into Tableau, where large, relatively unprocessed extracts required significant storage and processing.

Neither was an efficient long-term approach.

The recommended direction was to introduce a dedicated analytical platform in which data could be extracted from application databases, stored independently, transformed incrementally, and served to reporting tools from structures designed specifically for analytics.

This would allow the application databases to be optimised for transactional workloads while giving the analytics platform independent control over performance, modelling, storage and compute.

---

## Recommended Architecture

I proposed a staged modernisation rather than immediately moving Apollo to a highly sophisticated platform.

The initial target architecture consisted of:

* Azure Data Factory for orchestration and ELT.
* Azure Data Lake Storage for inexpensive, scalable storage.
* A dedicated **analytics SQL Server/database** for analytical workloads.
* A **medallion-style data architecture** consisting of Bronze, Silver and Gold layers.
* A dedicated **semantic layer** containing business definitions and analytical logic.
* Tableau extracts redirected away from production databases.
* Version-controlled data transformation code.
* Development and production environments.
* CI/CD and automated testing.
* Infrastructure monitoring and cost monitoring.

The architecture was deliberately designed around Apollo's current data maturity. The recommendation was to establish good architectural and engineering practices first rather than immediately introducing more complex technology.

A later-stage architecture could replace the ADF/SQL Server components with **Databricks** if Apollo's scale and requirements justified it.

---

## Data Architecture & Modelling

A core part of the recommendation was to introduce a structured data modelling architecture.

### Bronze

The Bronze layer would retain source data with minimal transformation.

Its purpose would be to provide an immutable source representation that could be reprocessed when data quality or transformation problems occurred.

### Silver

The Silver layer would create clean, conformed data.

Responsibilities would include:

* Data quality checks.
* Deduplication.
* Consistent data types.
* Standardised structures.
* Conformed entities.
* Centralised business logic where appropriate.

### Gold

The Gold layer would represent business-ready analytical data and act as the **semantic layer**.

This layer would:

* Define important business metrics.
* Organise data according to how users understand the business.
* Apply consistent business logic.
* Pre-aggregate data where appropriate.
* Provide efficient structures for Tableau.
* Create a foundation for future AI and machine-learning applications.

The underlying principle was to move from **source-organised data to analytics-organised and business-conformed data**.

---

## Semantic Layer & AI Readiness

One of the more strategic conclusions of the review was that Apollo's future AI ambitions depended on improving the underlying data architecture.

The existing system allowed business definitions to be recreated across SQL queries, Tableau dashboards and application logic. This created the risk of inconsistent definitions and made it difficult for an AI system to understand Apollo's business concepts reliably.

I identified the semantic layer as the mechanism for encapsulating concepts such as:

* Training load.
* Injury risk.
* Session intensity.
* Availability.
* Workload trends.
* Performance metrics.

The semantic layer would provide a consistent translation between underlying data and business concepts.

This was particularly relevant to Apollo's ambitions around conversational analytics. A future AI assistant could use the governed analytical layer rather than attempting to interpret raw application tables independently.

---

## Conversational Analytics / RAG-Relevant Work

As part of the Apollo work, I also designed the architecture and knowledge requirements for a **conversational analytics engine**.

The proposed system would allow non-technical sports science users such as physiotherapists, coaches and performance directors to ask questions in natural language and have those questions translated into T-SQL against an Azure Synapse Serverless SQL Pool backend.

The design included explicit AI guardrails covering:

* Date-range constraints to control serverless query costs.
* Current versus historical squad membership.
* Precision preservation for sports performance metrics.
* NULL versus zero handling.
* Approved table and join topology.
* Temporal joins for historical squad attribution.
* Wearable data relationships.
* Injury and availability calculations.
* Text-search conventions.
* Match-relative terminology such as `game_day_minus` and `game_day_plus`.
* Season and training-week definitions.
* Synapse Serverless SQL limitations.
* Approved data types and casting behaviour.
* Few-shot examples for common analytical questions.

The knowledge base therefore combined **business semantics, schema metadata, domain-specific rules, query patterns and execution guardrails** rather than relying on the LLM to infer everything from raw database structure.

This work is directly relevant to building reliable RAG and agentic data systems because it demonstrates an approach where the model is constrained by a curated body of domain knowledge and explicit execution rules.

---

## Cost Optimisation

Cost optimisation was a significant part of the architectural review.

Apollo's estimated Azure infrastructure cost was **over $100k annually** excluding Tableau licensing.

The review identified storage and SQL databases as significant cost drivers.

In particular:

* Premium SSD storage represented a substantial portion of infrastructure spend.
* Approximately 60% of the premium SSD cost was associated with Tableau servers.
* Tableau extracts were often large and unoptimised.
* SQL Server was handling both transactional and analytical workloads.
* Audit data represented significant database storage in some client environments.
* Infrastructure sizing was not consistently driven by observed utilisation.

The proposed architecture addressed these costs by:

* Moving analytical workloads away from transactional SQL Server.
* Moving long-term data to lower-cost object storage.
* Reducing unnecessary Tableau extract size.
* Introducing incremental data processing.
* Materialising analytical datasets where appropriate.
* Right-sizing SQL resources.
* Monitoring infrastructure utilisation.
* Introducing cost dashboards and alerting.

The initial estimate was a **20–30% short-term reduction** through rightsizing and optimisation, with potential for **40–60% analytical workload cost reduction** as the new architecture was implemented.

These were explicitly identified as preliminary estimates rather than guaranteed savings.

---

## Observability

I identified observability as an important architectural gap.

Apollo was largely learning about data problems after clients reported them. There was limited central visibility into:

* Pipeline health.
* Query performance.
* Storage growth.
* Infrastructure utilisation.
* Tableau extract failures.
* Data quality.
* Cloud costs.

The recommendation was to establish basic monitoring and alerting first, using Azure's existing capabilities, before introducing a dedicated data observability platform.

Potential future tooling included platforms such as Metaplane or Monte Carlo, combined with incident management tooling.

The broader objective was to move Apollo from **reactive firefighting to proactive, measurable operations**.

---

## Engineering Practices

The review also identified that architectural improvement would require changes to engineering practices, not simply new technology.

Recommended practices included:

* Version-controlled data code.
* Dedicated repositories.
* Development and production environments.
* Peer review.
* Linting and coding standards.
* CI/CD.
* Automated data quality tests.
* Infrastructure as Code using Terraform.
* Documented data models.
* Defined SLAs.
* Cost monitoring.
* Infrastructure monitoring.
* Automated alerting.

An important principle was that the technology change should be accompanied by a shift from **reactive problem solving to proactive engineering**.

---

## Roadmap

I proposed a staged implementation.

### Immediate / Quick Wins

* Add missing infrastructure monitoring and alerting.
* Create a central cost monitoring dashboard.
* Optimise or materialise expensive production views and stored procedures.
* Move data code into a dedicated repository.
* Analyse and optimise Tableau extract size and scheduling.
* Move database audit logs to lower-cost storage.
* Right-size SQL databases.

### Medium Term

* Build the dedicated analytics platform.
* Introduce Azure Data Lake Storage.
* Implement Azure Data Factory.
* Establish development and production environments.
* Introduce CI/CD.
* Build Bronze, Silver and Gold data layers.
* Implement data pipeline testing.
* Define the semantic layer.
* Redirect Tableau extracts to the analytical platform.
* Establish and measure SLAs.
* Monitor infrastructure performance and cost.

### Longer Term

* Reassess the architecture as Apollo grows.
* Consider Databricks where scale or workload requirements justify it.
* Introduce dedicated data observability.
* Develop AI-specific requirements.
* Automate wider platform provisioning.

---

## Key Lessons / Architectural Principles

The Apollo work reflects several principles that I apply to data architecture:

### Separate workloads by purpose

Transactional systems and analytical systems have different optimisation requirements. Combining them creates unnecessary contention and makes both harder to optimise.

### Introduce maturity incrementally

A modern architecture does not necessarily require the most sophisticated technology from day one. Establishing good modelling, testing, version control and operational practices can provide more value than immediately adopting a complex platform.

### Prefer cheap storage over repeated expensive compute

Where data can be processed incrementally and materialised appropriately, repeatedly recalculating large datasets at query time is often unnecessarily expensive.

### Treat semantics as an architectural concern

Business definitions should have an explicit home rather than being scattered across dashboards, SQL queries and application code.

### Design for AI from the data layer upward

Reliable AI analytics depends on reliable underlying semantics. A conversational interface does not remove the need for good data modelling; it makes it more important.

### Measure before optimising

Cost, performance and reliability improvements should be supported by monitoring and observable metrics rather than assumptions about where problems originate.

---

## Relevance to Martin's Experience

This project demonstrates experience across several areas:

* Data architecture: assessment and redesign of an existing data platform.
* Azure: Azure SQL, Azure Data Factory, Azure Data Lake Storage, Synapse Serverless and broader Azure infrastructure.
* Analytics engineering: medallion architecture, data modelling and semantic-layer design.
* Cloud cost optimisation: identifying infrastructure cost drivers and designing lower-cost alternatives.
* Data platform modernisation: separating transactional and analytical workloads.
* Observability: designing monitoring, alerting and data quality approaches.
* Engineering maturity: introducing version control, CI/CD, testing and infrastructure-as-code practices.
* AI / conversational analytics: designing a governed knowledge layer and execution guardrails for natural-language-to-SQL systems.
* Technical consulting: assessing an unfamiliar environment, identifying root causes, prioritising interventions and communicating a practical roadmap to stakeholders.

The project is particularly relevant to roles involving **data platform architecture, analytics engineering leadership, AI-ready data architecture, conversational analytics, RAG systems and cloud data modernisation**.
