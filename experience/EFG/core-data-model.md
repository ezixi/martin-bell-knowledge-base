---
type: project
title: Core Data Model
company: ESL FACEIT Group
role: Manager of Analytics Engineering & Insights
parent:
    - analytics-engineering-function.md

technologies:
    - dbt
    - SQL
    - BigQuery
    - Snowflake
    - Looker

skills:
    - Data Modelling
    - Data Architecture
    - Analytics Engineering
    - Metric Governance
    - Data Strategy
    - Stakeholder Management
    - Data Quality

themes:
    - Enterprise Data Model
    - Business Conformance
    - Metric Governance
    - Data Reuse
    - Self-Service Analytics
    - Data Quality

related:
    - snowflake-migration.md
    - analytics-engineering-function.md
    - overview.md
---

# Core Data Model

## Overview

As part of establishing the Analytics Engineering function at ESL FACEIT Group, I led the development of a Core Data Model (CDM) to provide a consistent business representation of the organisation's data.

The existing analytics environment had developed organically, with different teams creating their own models and definitions to answer specific questions. This made it difficult to establish a common understanding of important business concepts and resulted in duplicated logic, inconsistent metrics and limited reuse.

The Core Data Model was intended to provide a stable, reusable foundation for analytics across the organisation.

It was not intended to reproduce the structure of individual source systems. Instead, it represented the business concepts that analysts and other consumers needed to work with consistently.

## Why We Needed a Core Data Model

The organisation had multiple business areas, data sources and analytical use cases.

Different teams often approached the same underlying business concepts from different perspectives. This was particularly problematic for concepts such as users, products, events, transactions and engagement.

Without a shared model:

* Analysts repeatedly solved the same modelling problems.
* Business logic was duplicated across datasets and dashboards.
* Metric definitions could differ between teams.
* New analytical work required understanding multiple underlying schemas.
* It was difficult to build a comprehensive view of customers and their behaviour.
* Improvements to shared business logic were difficult to propagate.

The CDM was intended to establish a common vocabulary and reusable data structures across these use cases.

## Design Principles

The model was designed around several principles.

### Model the business, not the source systems

The CDM represented business concepts rather than simply exposing the schemas of operational systems.

Source systems remained responsible for capturing operational events. The Core Data Model was responsible for representing those events in a form that could be consistently understood and analysed by the business.

### Establish reusable business concepts

Common entities such as users, products, events and campaigns should be modelled once and reused rather than recreated independently for each analytical use case.

### Separate business logic from presentation

Business definitions should live in the governed analytical model rather than being repeatedly implemented in dashboards or other presentation tools.

This was particularly important given the previous environment, where logic had been distributed between the warehouse and Looker.

### Keep the model manageable

The objective was not to create a model containing every possible table.

A core model should provide a relatively small set of stable, well-understood entities and facts from which a wide range of analytical use cases can be supported.

### Build around business questions

The model was driven by how the organisation needed to understand its customers, products, activities, revenue and costs rather than by what happened to be easiest to extract from source systems.

## Core Business Concepts

The initial model was organised around four major categories of business activity.

### User Activity — Take Part

This represented interactions with EFG platforms where users actively participated.

Examples included:

* Playing a match.
* Joining a queue.
* Participating in an event or competition.

The purpose was to establish a consistent representation of participation and engagement.

### User Transactions — Buy

This represented commercial transactions involving users.

Examples included:

* Purchasing tickets.
* Purchasing products.
* Other relevant commercial transactions.

This provided a common foundation for understanding customer value and commercial behaviour.

### User Interactions — Consume

This represented interactions where users consumed EFG content or engaged with social and broadcast channels.

Examples included:

* Watching streams.
* Following content.
* Liking content.
* Other forms of content engagement.

This allowed engagement to be analysed alongside participation and commercial activity.

### Cost and Revenue

This represented the financial dimensions of EFG activities and projects.

The intention was to enable analytical models that connected activity and engagement with the financial outcomes and costs associated with the organisation.

## Core Dimensions

The initial CDM included a set of shared dimensions used across the business model.

### Users

Represented the organisation's users and customers and provided a common entity against which participation, transactions and consumption could be analysed.

### Products

Represented products and commercially relevant offerings.

### Events

Represented events and activities in which users could participate or engage.

### Competitions

Represented competitions and related esports activity.

### EFG Entities

Represented the organisation's relevant business entities and structures.

### Marketing Campaigns

Represented campaigns used to understand acquisition, engagement and commercial activity.

## Model Structure

The CDM was designed around a relatively small number of core facts and shared dimensions rather than allowing each analytical team to create independent models.

At a conceptual level:

```text
                         ┌──────────────┐
                         │    Users     │
                         └──────┬───────┘
                                │
              ┌─────────────────┼─────────────────┐
              │                 │                 │
              ▼                 ▼                 ▼
       ┌──────────────┐  ┌──────────────┐  ┌──────────────┐
       │ User Activity│  │ Transactions │  │ Interactions │
       │  Take Part   │  │     Buy      │  │   Consume    │
       └──────┬───────┘  └──────┬───────┘  └──────┬───────┘
              │                 │                 │
              └─────────────────┼─────────────────┘
                                │
                       ┌────────▼────────┐
                       │ Shared Business │
                       │   Dimensions    │
                       └─────────────────┘

       Events | Competitions | Products | Campaigns | EFG Entities
```

The exact physical implementation could evolve independently of the conceptual model. The important objective was to establish stable business concepts and relationships that could be implemented consistently in the analytical platform.

## Metric Development

The Core Data Model was also used as the foundation for improving metric governance.

As part of the initial programme, approximately 150 Digital Product metrics and 150 Esports metrics were reverse-engineered.

Rather than attempting to model every metric immediately, the team identified the highest-priority metrics and focused on establishing governed definitions and the underlying data structures required to support them.

The process involved:

1. Identifying existing metrics.
2. Understanding how they were currently calculated.
3. Identifying duplication and inconsistencies.
4. Agreeing business definitions.
5. Designing the logical model required to support those definitions.
6. Creating curated-layer precursors.
7. Onboarding required source data.
8. Implementing the models.
9. Testing and deploying them.
10. Documenting the resulting data structures.

This connected metric governance to actual data architecture rather than treating metric definitions as documentation alone.

## Business Conformance

A key concept behind the CDM was the distinction between **source-conformed data** and **business-conformed data**.

Source-conformed data represents the information as supplied by operational systems.

Business-conformed data adds the organisation's understanding of what those data represent.

For example, an operational system might record an event, transaction or user interaction. The CDM establishes how those concepts should be understood consistently across the organisation and how they relate to other business entities.

This creates a layer of business meaning between the technical source systems and the tools used by analysts and decision makers.

## Ownership

Analytics Engineering owned the development and governance of the Core Data Model.

The team worked with analysts and business stakeholders to understand how data was being used and to establish shared definitions.

This created a clear boundary:

* Data Engineering was responsible for reliably acquiring and delivering source data.
* Analytics Engineering was responsible for transforming that data into governed, reusable business models.
* Analytics / Insights consumed those models to answer business questions and create insight.

This ownership model was important because it prevented the analytical model from becoming either an extension of the source systems or a collection of bespoke analyst datasets.

## Relationship to the Analytics Engineering Function

The CDM was the first major product of the Analytics Engineering function.

It provided a concrete mechanism through which the new team could demonstrate its value:

* Analysts received reusable data structures.
* Business definitions became more consistent.
* Data modelling became a shared discipline.
* Metric logic could be centralised.
* Data quality could be tested systematically.
* New analytical products could build on existing foundations rather than starting from scratch.

The CDM therefore became both a **data product** and an expression of the operating model I was establishing for Analytics Engineering.

## Challenges

The biggest challenge was that the model had to reconcile several different perspectives.

Analysts were accustomed to solving individual questions quickly and could naturally favour models optimised for their immediate use case.

Data Engineering was primarily focused on reliable data acquisition and platform concerns.

Business stakeholders often cared about the outcome of a metric rather than the underlying model.

The Analytics Engineering function had to bridge these perspectives and establish a model that was technically sound while remaining useful to consumers.

Another challenge was scope.

A Core Data Model can easily become an attempt to model the entire organisation. I therefore focused on identifying the core entities and business processes that would provide the greatest reuse and value rather than attempting to solve every analytical requirement in the first iteration.

## Outcomes

The Core Data Model provided:

* A common business vocabulary for important analytical concepts.
* A reusable foundation for analytical models and metrics.
* Greater consistency between different analytical use cases.
* A mechanism for reducing duplicated business logic.
* Clearer ownership of the analytical data model.
* A foundation for governed metrics.
* A scalable structure for future data products.

It also established the conceptual foundation for the subsequent Snowflake migration and the broader move towards a governed analytics engineering architecture.

## Lessons Learned

### A data model is an organisational product

The hardest part of creating a shared data model is rarely the SQL.

The difficult work is agreeing what the organisation's business concepts actually mean and getting different groups to use those concepts consistently.

### Governance works best when embedded in delivery

Metric definitions and modelling standards are more effective when they are part of the process for creating data products rather than maintained as separate documentation.

### The model should be smaller than the data estate

A good core model does not need to represent every source table or every possible analytical question.

Its value comes from establishing a relatively small set of stable concepts that can be reused across many use cases.

### Business understanding is part of data engineering

Reliable pipelines are necessary but insufficient.

Someone needs to understand what the data means to the business and translate that understanding into reusable analytical structures.

That was the gap the Analytics Engineering function was designed to fill.

## What This Experience Demonstrates

This experience is evidence of my ability to:

* Design enterprise analytical data models.
* Translate business concepts into technical data structures.
* Establish shared definitions across business units.
* Create reusable fact and dimension models.
* Connect data modelling with metric governance.
* Define ownership between Data Engineering and Analytics.
* Lead modelling decisions across technical and business stakeholders.
* Build a data model as an organisational product rather than simply a collection of tables.

## Questions This Experience Answers

* Has Martin designed a Core Data Model?
* How does Martin approach enterprise data modelling?
* How does Martin distinguish source-conformed and business-conformed data?
* How does Martin approach metric governance?
* How does Martin decide what belongs in a core data model?
* How does Martin prevent analytical models from becoming overly complex?
* How does Martin work with Data Engineering and Analytics teams?
* How does Martin translate business concepts into data architecture?
* How does Martin build reusable data foundations for self-service analytics?
* What role does Analytics Engineering play in data architecture?
