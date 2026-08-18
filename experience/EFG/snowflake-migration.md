---
type: project
title: Snowflake Migration
company: ESL FACEIT Group
role: Manager of Analytics Engineering & Insights
status: completed

technologies:
    - Snowflake
    - BigQuery
    - dbt
    - Looker
    - Metaplane
    - SQL

skills:
    - Data Architecture
    - Analytics Engineering
    - Data Modelling
    - Data Governance
    - Team Leadership
    - Product Ownership
    - Stakeholder Management
    - Data Migration
    - BI Modernisation

themes:
    - Data Quality
    - Platform Modernisation
    - Analytics Engineering
    - Technical Leadership
    - Organisational Change

related:
    - overview.md
    - analytics-engineering-function.md
    - ../../philosophy/leadership.md
    - ../../philosophy/engineering-practices.md
---

# Snowflake Migration

## Overview

At ESL FACEIT Group, I was involved in the migration of the company's legacy BigQuery analytics warehouse to Snowflake.

The migration was not simply a technology change. The existing warehouse had evolved in an ad-hoc way, with significant duplication of logic, inconsistent metric definitions and poor modelling practices. The migration provided an opportunity to establish a much stronger analytics engineering architecture and operating model alongside the move to a new platform.

My role combined people leadership, data architecture, analytics engineering, product ownership and programme delivery.

## Why We Migrated

The existing BigQuery warehouse had developed organically without a consistent data modelling approach. Over time this created significant technical and operational problems.

### Poorly governed metric logic

Looker was the primary visualisation layer, but business logic was split between LookML and the warehouse. The same metrics could be defined differently in different Looker Explores, making it difficult to establish a single definition of a business metric.

This created a situation where changing a metric could require finding and updating logic in multiple places, and different values for the same metric appearing in different dashboards.

### Inconsistent data modelling

The team had previously attempted to introduce dbt and more structured modelling practices. However, the analytics engineering capability was still relatively immature, and the team did not yet have the conceptual modelling experience required to apply those practices effectively.

The result was a large and difficult-to-maintain collection of fact and dimension tables, significant duplication of logic, and unclear separation of responsibilities between models.

### Performance and cost

The volume of data made the existing architecture expensive to operate. There was limited use of incremental ingestion and caching, while Looker dashboards frequently performed poorly.

Some dashboards took a very long time to load, making the analytics platform frustrating for end users and limiting its usefulness for day-to-day decision making.

## Options Considered

The Head of Data Engineering led the decision on the target warehouse platform.

One option was to remain on BigQuery and establish a new instance with a cleaner architecture. Snowflake was ultimately selected, influenced in part by the team's existing expertise and previous experience with the platform.

From my perspective, moving to a new platform also created an important architectural opportunity: rather than attempting to incrementally repair a heavily compromised warehouse, we could establish a cleaner foundation and introduce better modelling and engineering practices from the beginning.

## My Role

My role extended well beyond the technical migration itself.

### Building the Analytics Engineering capability

I created an Analytics Engineering team from existing analysts and BI engineers and subsequently hired a Senior Analytics Engineer.

A major part of my responsibility was developing the team's technical capability. I introduced stronger data modelling concepts and engineering processes and helped the team develop the conceptual understanding required to apply them effectively.

### Architecture and modelling

I acted as a Principal Analytics Engineer / Data Architect for the programme.

I designed high-level conceptual and logical data models that provided a foundation for the team to build from. I also acted as an architectural resource for the Analytics Engineering team, helping engineers work through difficult modelling and architecture decisions and guiding them towards more sustainable solutions.

A key architectural principle was to avoid recreating the complexity of the previous warehouse. We deliberately kept the number of fact and dimension models manageable and isolated complex transformation logic into intermediate models.

### Product ownership

I acted as the primary product owner for the broader data model.

This involved working with end users and analysts to understand how data was actually being used, aligning stakeholders on metric definitions and documenting the business rules behind those metrics.

This was important because the migration was not just about moving tables from one warehouse to another. We were attempting to establish a more reliable business representation of the organisation's data.

### Delivery and team management

I ran project sprints and coordinated resources across the work.

Alongside the migration, I was the people manager for the Analytics Engineering team and an Insights team of analysts. This meant balancing delivery responsibilities with hiring, mentoring, team development and day-to-day management.

## Technical Decisions

### Engineering standards

I introduced coding standards, development conventions and style guides for the Analytics Engineering team.

I also introduced strict linting rules to make the expected standard explicit and catch issues before code was merged.

### Data modelling

I was deliberately strict about model design.

Rather than allowing the warehouse to grow into hundreds of loosely defined fact and dimension tables, I aimed to keep the core dimensional model relatively small and understandable.

Complex transformation logic was isolated into intermediate models rather than being repeatedly implemented in downstream fact and dimension models.

This created clearer boundaries between transformation stages and reduced duplication of code by 70%.

### Incremental processing

Because of the volume of data, I introduced incremental ingestion and transformation across the platform rather than repeatedly processing complete datasets.

This was important both for performance and for controlling warehouse consumption.

### Materialisation and BI performance

I materialised the Gold-layer models as tables where appropriate.

One of the reasons for this was to provide a performant and stable endpoint for the BI layer and take advantage of caching behaviour rather than forcing Looker to repeatedly execute expensive transformations.

### Observability

We introduced Metaplane for data observability.

Initially, the obvious use case was identifying data quality errors. However, I also used observability information to identify slow-loading tables and pipelines that required optimisation.

This helped shift the team's approach from reacting to user-reported problems towards proactively identifying areas of the platform that needed improvement.

## Challenges

### The migration strategy

One of the biggest challenges was not technical.

Rather than rebuilding the new platform on Snowflake and switching users over once it was ready, there was pressure from Data Engineering leadership to reduce costs during the migration.

We therefore attempted a staged migration from BigQuery to Snowflake.

In practice, this created a difficult transition state. Other analysts continued to build against BigQuery, while end users continued to request and consume data from the existing platform.

This meant we effectively had two versions of the analytics environment operating simultaneously, incurring the cost and complexity of maintaining both.

### User adoption and trust

The technical quality of the Snowflake environment was significantly better, but getting users to move to it was difficult.

There was considerable inertia around the existing BigQuery environment. Users were familiar with the old data and processes and were understandably reluctant to change.

This created an important distinction between **data quality** and **data trust**.

Even when we could demonstrate that the new platform was more accurate and better reflected the underlying business reality, users did not automatically trust it. Familiarity with the old system had created its own form of trust.

## Outcomes

The Snowflake platform was substantially cleaner and more reliable than the legacy environment.

Key outcomes included:

* Data quality improved significantly, with the new platform producing error-free data compared with multiple data quality issues per day in the previous environment.
* Pipelines ran in a fraction of the time required by the previous platform.
* Business metrics were consolidated into a more consistent modelling layer rather than being duplicated across multiple Looker definitions.
* Changes to metric definitions could be made much more quickly because the business logic had a clearer single location.
* Incremental processing and improved materialisation reduced unnecessary processing of large datasets.
* Observability provided greater visibility into both data quality and platform performance.
* The Analytics Engineering team developed stronger modelling and engineering practices as part of the migration.

## What Didn't Work

The migration demonstrated that technical success does not necessarily translate into organisational adoption.

The staged migration approach was intended to reduce costs and minimise disruption, but in practice it prolonged the transition and resulted in two competing analytics environments.

The project also remained too engineering-focused for too long. While significant effort went into building a technically superior platform, end-user migration and change management were not treated as strongly enough as first-class workstreams.

As a result, the team was frequently playing catch-up when users needed new data or functionality on the old platform.

## Lessons Learned

### Platform migrations are change-management projects

A successful warehouse migration is not simply a technical exercise. The people using the data need a clear reason to change, confidence in the new platform, and a supported path away from the old one.

### Don't underestimate the cost of running two systems

A staged migration can look attractive from a cost and risk perspective, but maintaining two competing platforms can create its own costs and organisational complexity.

### Technical quality does not create trust automatically

Users can be resistant to a new data source even when it is demonstrably more accurate.

Trust comes from a combination of data quality, transparency, communication, familiarity and successful experiences using the new system.

### Architecture and capability need to develop together

The migration exposed that better tooling alone would not solve the underlying modelling problems. The team also needed stronger conceptual understanding of data modelling and analytics engineering.

Part of my role was therefore to develop the people and practices required to make the new architecture successful.

## What This Experience Demonstrates

This project is evidence of my ability to:

* Lead a major data platform migration.
* Design analytics architecture and data models.
* Build and develop an Analytics Engineering capability.
* Establish engineering standards and governance.
* Translate business requirements into governed data models.
* Own data products and metric definitions.
* Balance technical architecture with business requirements.
* Manage the organisational challenges associated with technology change.
* Recognise and learn from unsuccessful approaches rather than treating technical delivery as the sole measure of success.

## Questions This Experience Answers

* Has Martin led a Snowflake migration?
* Why did Martin choose Snowflake over BigQuery?
* Has Martin worked with both Snowflake and BigQuery?
* Can Martin design a dimensional data model?
* Has Martin built an Analytics Engineering team?
* Has Martin introduced dbt and analytics engineering practices?
* How does Martin approach data quality?
* How does Martin approach metric governance?
* Has Martin dealt with resistance to data platform change?
* What has Martin learned from a project that did not go entirely to plan?
* How does Martin balance technical architecture with stakeholder needs?
* Can Martin lead both people and technical architecture?
