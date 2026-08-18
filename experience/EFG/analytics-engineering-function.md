---

type: project
title: Building the Analytics Engineering Function
company: ESL FACEIT Group
role: Manager of Analytics Engineering & Insights
status: completed

technologies:
    - dbt
    - SQL
    - BigQuery
    - Snowflake
    - Looker
    - Git
    - CI/CD

skills:
    - Analytics Engineering
    - Data Architecture
    - Team Building
    - Data Modelling
    - Data Governance
    - Metric Governance
    - Operating Model Design
    - Technical Leadership
    - Stakeholder Management
    - Data Strategy

themes:
    - Organisational Design
    - Data Quality
    - Governance
    - Self Service Analytics
    - Time to Insight
    - Team Development

related:
    - overview.md
    - snowflake-migration.md
    - ../../philosophy/leadership.md
    - ../../philosophy/engineering-practices.md
    - core-data-model.md
    - operating-model.md
---

# Building the Analytics Engineering Function

## Overview

At ESL FACEIT Group, I created and developed a dedicated Analytics Engineering function to address a gap between Data Engineering and Analytics.

The existing data organisation had strong capabilities in data analysis, dashboard development and data engineering, but lacked a dedicated function responsible for turning technically available data into well-modelled, governed and reusable business data.

My objective was not simply to add another engineering team. I wanted to establish an operating model that gave analysts better access to trusted data, improved the quality and consistency of the organisation's metrics, accelerated time to insight, and created clear ownership of the enterprise data model.

The function was designed around four outcomes:

* **Business Enablement** — enable analysts and reduce time to insight.
* **Efficiency** — increase development velocity and the number of useful analytics products.
* **Service Quality** — provide reliable, well-documented data services to consumers.
* **Data Reliability** — improve availability, testing, observability and recovery.

## Why the Function Was Needed

The wider data organisation was divided broadly between Data Analysts and Data Engineers.

Data Analysts were strong at producing dashboards and answering business questions, but generally did not have the deeper data modelling expertise required to build a sustainable analytical data layer.

Data Engineers were primarily focused on ingestion and platform engineering. There was also a deliberate organisational tendency to keep Data Engineering separated from business logic and the interpretation of how data should be used.

This created a gap between the technical data platform and the business-facing analytical layer.

### Poorly governed metric logic

The existing BigQuery warehouse had developed organically without a consistent modelling approach.

Looker was the primary visualisation layer, but business logic was distributed between LookML and the warehouse. The same metric could be defined differently in different Looker Explores, meaning that different dashboards could return different values for what users believed was the same business metric.

Changing a metric could therefore require identifying and updating logic in multiple locations.

This made it difficult to establish trusted, reusable definitions of business concepts.

### Inconsistent data modelling

The organisation had previously attempted to introduce dbt and more structured modelling practices.

However, the analytics engineering capability was still immature. The team did not yet have the conceptual modelling experience needed to apply these practices consistently.

The result was a large collection of fact and dimension tables, duplicated transformation logic and unclear boundaries between models.

The new Analytics Engineering function was intended to address this gap by establishing ownership of the analytical model and developing the capabilities required to maintain it properly.

## Vision

The vision for the function was to:

*Empower analysts, improve data quality, accelerate time to insights and improve data governance.*

The team would achieve this through well-documented and standardised processes, industry best practices, ownership of the enterprise data model, proactive data acquisition and enrichment, and closer alignment with the needs of Insight Analysts, Research Analysts and other data consumers.

A key principle was that Analytics Engineering should act as a **gatekeeper of the enterprise data model**, ensuring that data remained consistent and usable rather than allowing each analytical use case to create its own interpretation of the underlying data.

## Operating Model

I designed the function around a defined production cycle rather than treating Analytics Engineering as a reactive ticket-taking service.

The team used a recurring cycle of:

1. Research
2. Planning
3. Design
4. Build
5. Communication

### Research

Before a release cycle, the team would review:

* Insights from previous releases.
* Recurring tactical requests.
* KPI performance and product usage.
* Strategic initiatives.
* Feedback from data consumers.
* The existing book of work.

The intention was to identify opportunities proactively rather than simply responding to the next request in the queue.

### Planning

Before the release started, the team would:

* Prioritise projects.
* Assess feasibility.
* Align capacity and resources.
* Secure stakeholder buy-in.

### Design

The first sprint was deliberately focused on understanding the problem before writing production code.

Activities included:

* Designing the Entity Relationship Diagram (ERD).
* Cataloguing relevant data sources.
* Mapping source data.
* Defining requirements.
* Establishing tests.

### Build

The second sprint focused on implementation:

* Writing code.
* Deploying changes.
* Validating outputs.
* Reviewing and improving engineering practices.
* Communicating successes.

### Communication

Post-release work included capturing longer-term documentation and producing educational or external communication where appropriate.

This structure was intended to make Analytics Engineering a repeatable product-development process rather than an ad-hoc development function.

## Analytics Architecture

I established a layered analytical architecture to create clearer boundaries between source data, governed models and consumer-facing products.

### Staging

The staging layer was:

* Selective rather than a complete copy of every source.
* Organised by source system.
* Queryable.
* Monitored for availability.

### Curated

The curated layer was responsible for:

* Data validation.
* Testing.
* Governance.
* Consistent transformation.
* Preparing data for the business layer.

The emphasis was on creating a reliable, governed representation of source data before introducing business-specific interpretations.

### Business Layer / Data Marts

The business layer consolidated data into meaningful structures that could answer business questions.

The intention was to provide comprehensive subject coverage rather than creating a new bespoke model for every individual analytical request.

### Analytics / Presentation / Semantic layer

The presentation layer was tailored for specific stakeholders and use cases.

It could apply stakeholder-specific logic and terminology while consuming a consistent underlying business model.

The architecture and responsibilities of these layers were explicitly documented in the team's workshop materials.

## First Product: Core Data Model

The first major product for the new function was a **Core Data Model (CDM)**.

The purpose was to create a coherent model of the organisation's data landscape across business units, reduce data silos and establish a more comprehensive view of the customer journey and customer value.

The initial model was organised around a set of core business facts:

* **User Activity — Take Part**: interactions with EFG platforms, such as playing a match or joining a queue.
* **User Transactions — Buy**: transactions such as purchasing tickets or products.
* **User Interactions — Consume**: interactions with social and broadcast channels, such as watching streams or following and liking content.
* **Cost and Revenue**: costs and revenue associated with EFG projects.

Core dimensions included:

* Events
* EFG Entities
* Marketing Campaigns
* Users
* Products
* Competitions

The CDM therefore provided a business-oriented structure for understanding the organisation rather than simply reproducing source-system schemas.

## Metric Governance

A major responsibility of the function was bringing greater consistency to the organisation's metrics.

The initial CDM programme included reverse-engineering approximately 150 Digital Product metrics and 150 Esports metrics, identifying the highest-priority 50 metrics, documenting their definitions and creating tests around them.

The process then moved into:

1. Designing the logical model.
2. Creating curated-layer precursors.
3. Onboarding the required data.
4. Implementing the models.
5. Deploying and monitoring them.
6. Documenting the resulting layers.

This established a foundation for moving metric definitions away from scattered dashboard logic and towards governed, reusable data models.

## Team Development

Creating the function also required developing the people within it.

I built the initial Analytics Engineering team from existing analysts and BI engineers and hired a Senior Analytics Engineer.

A significant part of my role was raising the team's modelling and engineering capability.

Rather than simply giving the team new tooling, I introduced the conceptual practices required to use the tooling effectively:

* Data modelling principles.
* Entity and relationship modelling.
* Separation of transformation layers.
* Reusable business logic.
* Testing.
* Documentation.
* Coding standards.
* Development and review processes.

I acted as a Principal Analytics Engineer / Data Architect for the team, designing high-level conceptual and logical models and providing architectural guidance when engineers encountered difficult modelling decisions.

This allowed the team to progressively take greater ownership rather than relying on me for every design decision.

## Governance and Engineering Standards

The function introduced a set of standardised practices intended to make analytical development more predictable and maintainable.

These included:

* Version-controlled analytical artefacts.
* Consistent modelling conventions.
* Coding standards.
* Linting.
* Testing.
* Documentation requirements.
* Source-to-target mapping.
* ERDs.
* Data cataloguing.
* Cross-team agreements.
* CI/CD practices.
* Production monitoring.

The underlying principle was that analytical data development should follow appropriate software engineering practices rather than treating dashboards and analytical models as disposable outputs.

## Measuring the Function

I established measurable objectives for the team rather than defining success simply as "delivering data."

The charter identified four main areas of measurement.

### Service Quality

Measures included:

* Customer satisfaction.
* Documentation coverage.
* Test coverage.

The original objectives included a target of 90%+ CSAT and 100% documentation and test coverage for relevant models and new data products.

### Business Enablement

Measures included:

* Time to insight.
* Proactiveness.
* Data landscape coverage.

The initial objectives included reducing time to insight by 50% and achieving comprehensive coverage of at least two major business units.

### Efficiency

Measures included:

* Number of analytics products created.
* Development velocity.
* Cost savings.

### Data Reliability

Measures included:

* Data availability.
* Mean Time to Identify (MTTI).
* Mean Time to Recover (MTTR).
* Test coverage.

These measures were intended to connect the team's engineering work to outcomes experienced by its consumers rather than measuring only technical activity.

## What This Changed

The creation of the Analytics Engineering function established a dedicated capability between data platform engineering and business analytics.

It provided:

* Clearer ownership of the analytical data model.
* A structured approach to data modelling.
* Better separation between source, curated, business and presentation concerns.
* A formal production lifecycle for analytics products.
* Stronger engineering standards.
* A mechanism for developing analysts and BI engineers into Analytics Engineers.
* A more proactive approach to identifying and delivering data products.
* A framework for improving data quality, documentation and governance.

The function also created a foundation for the subsequent Snowflake migration and broader analytics platform modernisation.

## Lessons Learned

### A new function needs a clear value proposition

Analytics Engineering can easily be perceived as another technical layer unless its purpose is expressed in terms that matter to consumers.

For this reason, the function was explicitly measured against outcomes such as time to insight, service quality, data reliability and business coverage.

### Tooling cannot substitute for conceptual understanding

Introducing dbt or another analytics engineering tool does not automatically create an Analytics Engineering capability.

The team needed to understand modelling, grain, business logic, testing and architecture before the tooling could deliver its intended benefits.

### Ownership needs to cross technical and business boundaries

The function was deliberately positioned between Data Engineering and Analytics.

Data Engineering could provide reliable source data without necessarily owning the meaning of that data, while analysts understood business questions without necessarily having the modelling expertise to create sustainable shared models.

Analytics Engineering existed to bridge that gap.

### Data products need consumers

The team was designed around the needs of analysts, researchers, data scientists and other business users.

The production lifecycle therefore included research, stakeholder alignment, communication and post-release education rather than treating deployment as the end of the process.

## What This Experience Demonstrates

This experience is evidence of my ability to:

* Create a new Analytics Engineering function.
* Define an operating model for a data team.
* Establish data architecture and modelling standards.
* Build capability from existing analysts and BI engineers.
* Hire and develop senior technical talent.
* Bridge Data Engineering and Analytics.
* Establish metric and data governance practices.
* Introduce software engineering discipline into analytics.
* Define measurable objectives for a data function.
* Connect engineering activity to business outcomes.
* Lead organisational change rather than simply implement technology.

## Questions This Experience Answers

* Why did Martin create an Analytics Engineering function?
* What does Martin believe Analytics Engineering should own?
* How does Martin distinguish Analytics Engineering from Data Engineering?
* How does Martin distinguish Analytics Engineering from Data Analytics?
* How does Martin build an Analytics Engineering team?
* How does Martin develop junior or inexperienced Analytics Engineers?
* How does Martin approach data modelling?
* How does Martin approach metric governance?
* How does Martin design a data team's operating model?
* How does Martin measure the success of an Analytics Engineering function?
* How does Martin balance engineering quality with time to insight?
* Has Martin designed an enterprise data model?
* Has Martin created a Core Data Model?
