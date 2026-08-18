---
type: project
title: Analytics Engineering Operating Model
company: ESL FACEIT Group
role: Manager of Analytics Engineering & Insights
parent:
    - analytics-engineering-function.md

technologies:
    - dbt
    - SQL
    - Git
    - CI/CD
    - Looker
    - Snowflake
    - BigQuery

skills:
    - Operating Model Design
    - Analytics Engineering
    - Data Architecture
    - Data Governance
    - Agile Delivery
    - Team Leadership
    - Stakeholder Management
    - Data Modelling
    - Software Development Lifecycle

themes:
    - Data Products
    - Governance
    - Business Conformance
    - Self-Service Analytics
    - Engineering Standards
    - Continuous Improvement

related:
    - overview.md
    - analytics-engineering-function.md
    - core-data-model.md
    - snowflake-migration.md
    - ../../philosophy/leadership.md
    - ../../philosophy/engineering-practices.md
---

# Analytics Engineering Operating Model

## Overview

When I established the Analytics Engineering function at ESL FACEIT Group, I wanted to avoid creating a team that simply became another queue for analysts to submit data requests.

The objective was to establish a repeatable operating model for turning business requirements into reliable, governed and reusable data products.

The model combined:

* Business discovery.
* Data modelling.
* Engineering standards.
* Agile delivery.
* Code review and version control.
* Testing and quality assurance.
* Documentation and metadata.
* Data observability.
* Stakeholder communication.
* Continuous improvement.

The underlying principle was that **analytics engineering should operate as a product and engineering discipline**, rather than as ad-hoc SQL development.

## The Role of Analytics Engineering

The function existed between Data Engineering and Analytics.

Data Engineering was primarily concerned with acquiring, moving and reliably delivering data.

Analytics and Insights teams were primarily concerned with understanding business questions, analysing data and communicating insight.

Analytics Engineering was responsible for transforming source-conformed data into **business-conformed data**: data structured around the concepts, definitions and processes that the organisation actually uses.

This created a clear progression:

```text
Source Systems
      ↓
Source-Conformed Data
      ↓
Staging
      ↓
Curated Business Models
      ↓
Business-Conformed Data
      ↓
Domain Data Marts
      ↓
BI / Analytics / Data Products
```

The purpose was not simply to move data through technical layers. Each layer added structure, quality, abstraction or business meaning.

The team's dbt guidance explicitly described this as creating a cohesive arc from source-conformed to business-conformed data.

## Data Product Lifecycle

The team used a recurring production cycle:

1. Research
2. Planning
3. Design
4. Build
5. Communication

The purpose was to ensure that development started with understanding the business problem rather than immediately writing SQL.

### 1. Research

The team reviewed:

* Insights from previous releases.
* Tactical requests.
* KPI performance.
* Product usage.
* Strategic initiatives.
* Stakeholder feedback.
* Existing work.

This allowed the team to identify opportunities proactively rather than operating entirely from an incoming request queue.

### 2. Planning

The team then:

* Prioritised work.
* Assessed feasibility.
* Considered available capacity.
* Allocated resources.
* Obtained stakeholder alignment.

The goal was to ensure that work being taken into a development cycle had a clear reason for existing.

### 3. Design

The first development stage focused on understanding and designing the solution.

Typical artefacts included:

* Conceptual data model.
* Logical data model.
* Entity Relationship Diagram.
* Bus matrix.
* Source-to-target mapping.
* Metric definitions.
* Data requirements.
* Test requirements.

This separation between design and implementation was deliberate.

We wanted business and data modelling decisions to be made before implementation details constrained the solution.

### 4. Build

Once the design had been agreed, the team implemented the models.

This included:

* dbt development.
* SQL development.
* Testing.
* Code review.
* Deployment.
* Documentation.
* Data quality validation.
* Performance optimisation.

### 5. Communication

After release, the team communicated the resulting data product and captured longer-term documentation.

The objective was to ensure that deployment was not the end of the process. Consumers needed to understand what had changed, how the data should be used and where the resulting data product fitted into the wider architecture.

## Data Modelling Lifecycle

A central part of the operating model was the separation of conceptual, logical and physical modelling.

### Conceptual Model

The conceptual model captured the business view of the data.

It focused on:

* What entities exist?
* What business processes matter?
* How are those entities related?
* What does the business need to measure?

The conceptual stage was deliberately collaborative and could produce artefacts such as:

* Bus matrix.
* Source-to-target mapping.
* Metric definitions.

The objective was to establish shared understanding before technical implementation.

### Logical Model

The logical model translated the business understanding into a more detailed representation.

It defined:

* Entities.
* Attributes.
* Relationships.
* Keys.
* Grain.

This created the bridge between business requirements and the eventual physical implementation.

### Physical Model

The physical model translated the logical model into the target database implementation.

In the modern analytics engineering approach, dbt provided the mechanism for implementing these models as version-controlled code rather than relying on manually maintained DDL.

## Modelling Approach

The team adopted a **Kimball / dimensional modelling** approach for the analytical layer.

The model separated:

* Facts — representations of business processes, actions or measurable events.
* Dimensions — attributes describing the people, objects and entities associated with those processes.

A simple question helped guide modelling decisions:

*Is this something we want to measure, or something we want to describe or filter by?*

This helped keep models understandable to analysts and optimised for analytical workloads.

The approach was chosen because dimensional models provide high query performance, support incremental development and work naturally with BI tools and analytical workloads.

## Layered dbt Architecture

The dbt project followed a deliberate progression from source representation to business meaning.

### Staging

Staging represented the physical source data as code.

Key principles included:

* Organise models by source.
* Maintain an approximately 1:1 relationship with source tables.
* Use clear source-based naming.
* Avoid materialising unnecessarily.
* Apply basic standardisation.
* Fix data types.
* Improve naming.
* Apply simple transformations consistently.

Staging was intended to be the last point at which models closely reflected the source-system structure.

From this point onward, downstream models were designed around business concepts rather than source schemas.

### Curated

The curated layer was where the organisation's business concepts were introduced.

This included:

* Facts.
* Dimensions.
* Intermediate models.
* Business logic.
* Entity-level abstractions.

Models were designed around the unique grain of the business entity or process they represented.

A key principle was to **refactor and abstract rather than continually create new models**.

If logic was repeated, it was a signal that the abstraction belonged in an intermediate model or shared business model.

This was intended to prevent the warehouse from developing hundreds of duplicated fact and dimension tables again.

### Analytics / Data Marts

The analytics layer provided domain-focused data products for business users.

The preferred pattern was a data mart representing the business process or domain required by the consumer.

These marts were designed to:

* Be easy for business users to query.
* Provide a stable source for Looker Explores.
* Reduce unnecessary joins.
* Improve performance.
* Allow Looker to query a simpler structure.
* Provide a controlled boundary between the analytical model and the BI tool.

Where appropriate, marts were materialised as tables according to user requirements.

This also allowed upstream models to be changed without immediately disrupting the availability of the consumer-facing data product.

## One Source of Truth

A central architectural principle was:

```text
staging
   ↓
fact / dimension
   ↓
data mart
   ↓
dashboard
```

The objective was to avoid multiple implementations of the same business logic.

If a metric, attribute or transformation was needed in multiple places, the preferred solution was to identify the appropriate shared abstraction and implement the logic there.

The operating model therefore encouraged:

* Reuse.
* DRY principles.
* Refactoring.
* Shared dimensions.
* Shared business logic.
* Consistent metric definitions.

Creating a new model was not automatically considered the right solution.

## Engineering Standards

Analytics Engineering was treated as software development.

I introduced standards covering:

* SQL style.
* dbt conventions.
* Naming.
* Linting.
* Code review.
* Merge requests.
* Testing.
* Documentation.
* Version control.
* CI/CD.

The intention was to make quality the default rather than relying on individual engineers remembering a collection of unwritten rules.

Strict SQL linting was introduced to enforce the agreed development standards.

## Test-Driven Development

Testing was treated as part of model development rather than an activity performed after implementation.

The team's guidance was:

_Write your tests first._

Models were expected to pass their tests before deployment.

Testing was combined with documentation and metadata so that the team could understand not only whether a model worked, but also what it represented and how it connected to other data products.

## Metadata and Lineage

Metadata was treated as an essential part of the data product.

The team aimed to document:

* Tables.
* Columns.
* Business definitions.
* Changes.
* Lineage.
* Model relationships.
* BI dependencies.

The goal was to make it possible to understand the path from source data through analytical models to dashboards.

Lineage also provided practical operational benefits: it helped engineers troubleshoot changes and understand which downstream products would be affected by an upstream modification.

## Development Principles

Several principles were deliberately reinforced across the team.

### Start simple

Models should start as simple as possible.

Views were preferred during development and materialisation was introduced where performance or user requirements justified it.

### Keep the model small

The team actively resisted unnecessary proliferation of facts, dimensions and intermediate models.

The existence of fewer fundamental business processes and entities than initially assumed was an important modelling insight.

### Refactor rather than duplicate

If a new requirement could be satisfied by extending an existing model, the preferred solution was to update the existing model rather than create another competing representation.

### Abstract repeated logic

Repeated SQL or repeated business logic was treated as a signal that an abstraction was missing.

Intermediate models were introduced when they provided a meaningful reusable abstraction rather than as a mandatory layer for every transformation.

### Design for consumers

Models were designed with their eventual consumers in mind.

For analytical marts, this included considering:

* How metrics would be aggregated.
* How they would be segmented.
* Which dimensions users would filter by.
* How the BI tool would query the data.
* What performance users expected.

## Agile Delivery

The team operated using Agile principles, with work organised into planned development cycles.

This allowed the team to:

* Prioritise work regularly.
* Make capacity visible.
* Break larger data products into deliverable stages.
* Review progress.
* Adapt based on stakeholder feedback.
* Improve the development process over time.

Agile was not treated as a rigid methodology. The objective was to create a predictable delivery mechanism without allowing process to become an impediment to producing useful data products.

## Stakeholder Engagement

Analytics Engineering required close collaboration with both technical and business stakeholders.

The team worked with:

* Data Engineering.
* Analysts.
* Product teams.
* Business stakeholders.
* Data consumers.

Stakeholder engagement was particularly important during the modelling stage.

Business users were interviewed to understand:

* The concepts they used.
* The processes they followed.
* What they needed to measure.
* How metrics were currently calculated.
* Where the existing data failed to represent their understanding.

This information was then translated into ERDs, metric definitions and logical models before implementation.

## Team Development

The operating model was also a mechanism for developing the team's capability.

The initial team included analysts and BI engineers who had strong business and reporting knowledge but less experience with formal data modelling and software engineering practices.

Rather than expecting them to learn these disciplines independently, I established explicit processes, standards and architectural guidance.

I acted as a Principal Analytics Engineer / Data Architect, providing guidance on:

* Data modelling.
* Grain.
* Entity relationships.
* Architecture.
* Business logic.
* dbt patterns.
* Engineering practices.

I also hired a Senior Analytics Engineer to strengthen the technical capability of the team.

The aim was to create a team capable of making good architectural decisions independently rather than creating a permanent dependency on a single technical expert.

## Continuous Improvement

The operating model itself was treated as a version-controlled product.

We did not assume that the initial process was perfect.

The intention was to:

1. Establish a process.
2. Measure how it worked.
3. Identify bottlenecks.
4. Gather feedback.
5. Change the process.
6. Measure the result.

This was consistent with the broader principle that governance should add value rather than simply add bureaucracy.

## Success Measures

The function was measured against outcomes rather than simply technical delivery.

Key measures included:

### Business Enablement

* Time to insight.
* Data landscape coverage.
* Proactive delivery.

### Service Quality

* Consumer satisfaction.
* Documentation coverage.
* Test coverage.

### Efficiency

* Analytics products delivered.
* Development velocity.
* Cost efficiency.

### Reliability

* Data availability.
* Mean Time to Identify.
* Mean Time to Recover.
* Test coverage.

The intention was to ensure that engineering quality remained connected to the experience and productivity of the people consuming the data.

## What This Operating Model Was Designed to Solve

The operating model addressed several recurring problems in the previous environment:

| Problem                               | Operating Model Response                      |
| ------------------------------------- | --------------------------------------------- |
| Analysts repeatedly cleaning data     | Reusable curated models                       |
| Inconsistent metric definitions       | Governed business models                      |
| Duplicated SQL                        | DRY principles and abstraction                |
| Poor modelling                        | Conceptual → logical → physical modelling     |
| Unclear ownership                     | Explicit Analytics Engineering responsibility |
| Poor data quality                     | Testing and observability                     |
| Slow development                      | Reusable models and standard patterns         |
| Slow BI queries                       | Consumer-focused data marts                   |
| Difficult troubleshooting             | Metadata and lineage                          |
| Ad-hoc development                    | Defined production lifecycle                  |
| Knowledge concentrated in individuals | Documentation and standards                   |

## What This Experience Demonstrates

This experience is evidence of my ability to:

* Design an operating model for an Analytics Engineering function.
* Translate software engineering practices into an analytics environment.
* Establish a structured data product lifecycle.
* Define responsibilities across Data Engineering, Analytics Engineering and Analytics.
* Introduce conceptual, logical and physical modelling practices.
* Establish dimensional modelling standards.
* Create governed paths from source data to business-facing data products.
* Introduce testing, linting, version control and CI/CD.
* Build stakeholder engagement into technical delivery.
* Develop inexperienced engineers through explicit standards and mentoring.
* Measure a data team's effectiveness through business and technical outcomes.
* Treat governance and operating processes as products that can be continuously improved.

## Questions This Experience Answers

* How does Martin structure an Analytics Engineering team?
* What should an Analytics Engineering operating model look like?
* How does Martin take data from source-conformed to business-conformed?
* How does Martin approach data modelling?
* Why does Martin use conceptual, logical and physical models?
* Why did Martin choose dimensional modelling?
* How does Martin structure dbt projects?
* How does Martin prevent duplication in a data warehouse?
* How does Martin approach testing and data quality?
* How does Martin approach data lineage and metadata?
* How does Martin balance governance with delivery speed?
* How does Martin develop Analytics Engineers?
* How does Martin measure the effectiveness of a data team?
* How does Martin ensure that technical data products remain useful to business users?
