---
type: project
title: Data Warehouse Modernisation
company: Newport Takkt
role: Lead Data Engineer
domain:
  - Data Engineering
  - Analytics Engineering
  - Data Architecture

summary: >
  I modernised Newport's analytics platform from an ad-hoc Alteryx and
  Tableau-based workflow into an engineered BigQuery data warehouse using dbt.
  I first stabilised the existing Alteryx estate with source control,
  standardisation and scheduling so analysts could continue delivering, then
  introduced dimensional modelling, development and production separation,
  automated testing, pull-request workflows and CI/CD through Azure Pipelines.
  Because multiple ecommerce businesses shared the same source-system structure,
  I was able to create reusable models for individual businesses and consolidated
  group-level reporting.

technologies:
  - BigQuery
  - dbt
  - SQL
  - Python
  - Alteryx
  - Tableau
  - Azure DevOps
  - Azure Pipelines
  - Git
  - GitHub
  - SQL Server

skills:
  - Data Engineering
  - Analytics Engineering
  - Data Architecture
  - Data Warehousing
  - Data Modelling
  - dbt
  - BigQuery
  - CI/CD
  - Data Quality
  - Technical Leadership
  - Platform Modernisation
  - Stakeholder Management

key_contributions:
  - Stabilised an existing Alteryx-based analytics workflow before replacing it.
  - Introduced source control and engineering conventions to existing Alteryx transformations.
  - Introduced dbt as the transformation and modelling layer on BigQuery.
  - Established separate development and production BigQuery environments.
  - Built automated dbt deployment and testing using Azure Pipelines.
  - Introduced pull-request-based changes to production.
  - Created reusable data models across multiple ecommerce businesses.
  - Created consolidated group-level reporting from common business models.
  - Moved transformation logic out of Tableau and into a governed data warehouse.
  - Drove adoption of engineering practices despite organisational resistance.

challenges:
  - Existing transformations were graphical Alteryx workflows stored and run locally.
  - There was no source control or consistent engineering process.
  - Significant business logic existed in Tableau.
  - Data quality was poor and dashboards frequently broke.
  - Development was slow and heavily dependent on manual processes.
  - Faced resistance to replacing Alteryx with a code-based transformation framework.

design_decisions:
  - Stabilise the existing platform before replacing it.
  - Keep BigQuery rather than introduce an unnecessary warehouse migration.
  - Use dbt to separate transformation and modelling from ingestion and visualisation.
  - Use views extensively because data volumes were low.
  - Reuse models across businesses sharing the same source-system schema.
  - Use Azure Pipelines for deployment while retaining BigQuery as the analytical warehouse.
  - Store credentials outside source control using Azure Secure Files.

related:
  - overview.md
  - ../philosophy/engineering-practices.md
  - ../philosophy/data-strategy.md
  - ../philosophy/analytics.md
---

# Data Warehouse Modernisation

## Overview

When I joined Newport, the analytics platform was heavily based on lightly transformed source-system data.

Alteryx was used to extract data, primarily from SQL Server, and load it into BigQuery. BigQuery was being used largely as a staging point from which Tableau could consume the data rather than as a properly modelled analytical warehouse.

A significant amount of transformation and business logic consequently existed either in Alteryx or directly in Tableau.

The overall process had developed organically and had very few software engineering practices around it.

My objective was to move the organisation towards an engineered analytical warehouse while allowing the analysts and existing reporting to continue operating during the transition.

## Existing Architecture

The basic flow was:
**SQL Server → Alteryx → BigQuery → Tableau**

Alteryx workflows performed extraction and lightweight transformation before loading tables into BigQuery.

The workflows were graphical rather than code-based and were generally stored and run locally from analysts' machines.

This created several problems:

- There was no reliable source control.
- Finding the correct version of a transformation could be difficult.
- Changes required analysts to locate and modify individual Alteryx files.
- There were no common engineering conventions.
- Pipeline execution was heavily dependent on individual analysts.
- Significant transformation logic existed in Tableau.
- Data quality was poor.
- Dashboards frequently broke.
- Development was slow.

BigQuery was present, but we weren't taking advantage of it as a central analytical modelling platform.

## Stabilising the Existing Platform

I didn't want to stop the analysts delivering while I built a replacement.

My first step was therefore to make the existing Alteryx estate safer and more manageable.

Alteryx transformations are represented internally as XML, which meant they could be version controlled even though development itself happened through a graphical interface.

I created a GitHub repository to hold the workflows and introduced version control around them.

I also used Python within the Alteryx environment to introduce greater standardisation and configured scheduling so pipeline execution was less dependent on analysts manually running processes.

This wasn't where I wanted the architecture to end up, but it reduced immediate operational risk and allowed analysts to continue working while I developed the new warehouse.

That sequencing was deliberate:
**stabilise the system we have → build the replacement → migrate incrementally**

rather than attempting a disruptive rewrite.

## Introducing dbt

In parallel, I began implementing dbt on top of BigQuery.

The important architectural change was that BigQuery would no longer simply be somewhere to put source data before Tableau consumed it.

It would become the analytical warehouse.

Transformation, modelling and reusable business logic could move into dbt, allowing Tableau to consume cleaner, governed analytical models rather than being responsible for significant parts of the transformation layer itself.

This gave us a much clearer separation of responsibilities:
**Source systems → ingestion → BigQuery → dbt modelling → Tableau**

It also allowed us to apply normal software engineering practices to analytical transformations.

## Development and Production

I introduced separation between development and production.

I developed dbt locally against a dedicated development project in BigQuery rather than making changes directly against production data models.

Approved changes could then be deployed automatically to the production environment.

This meant development could happen safely without immediately affecting reporting used by the business.

It also changed the nature of production: instead of being somewhere analysts manually edited analytical logic, it became an environment that we deployed tested code into.

## CI/CD

I built the dbt deployment process using Azure Pipelines.

Although the analytical warehouse was on Google BigQuery, Newport's wider infrastructure used Azure, so using Azure Pipelines allowed the warehouse development process to fit into the organisation's existing infrastructure.

The pipeline definition lived as YAML alongside the dbt project in source control.

Changes to the production branch triggered an automated deployment. Combined with repository rules requiring an approved pull request before merging, this provided a controlled route into production:
**development → pull request → review → merge → automated deployment → dbt run → dbt test**

The pipeline:

- Checked out the dbt repository.
- Loaded required credentials securely.
- Cached Python dependencies to reduce pipeline execution time and cost.
- Installed dbt and its dependencies.
- Connected securely to BigQuery.
- Built the production models.
- Executed dbt tests.

BigQuery service-account credentials and the dbt profile were stored using Azure Secure Files rather than committed to the repository. They were downloaded into the temporary pipeline environment when required and removed after execution.

A failed dbt test caused the pipeline to fail and surface the problem rather than allowing failures to remain unnoticed.

This gave us a reproducible mechanism for deploying and testing analytical code rather than relying on manual changes.

## Modelling Across Multiple Businesses

One of the most valuable opportunities came from Newport's organisational structure.

There were multiple ecommerce businesses within the group, but they operated on the same underlying commerce platform.

That meant their source SQL Server databases had effectively the same structure.

Rather than independently building analytical logic for every business, I could model the common structures once in dbt and apply the same modelling approach across them.

Individual businesses could have consistent analytical models while the same data could then be rolled up into group-level models.

Conceptually:
**Business A source → common models ┐**
**Business B source → common models ├→ group-level models**
**Business C source → common models ┘**

This was much more powerful than simply improving pipeline technology.

It allowed the organisation to analyse individual businesses consistently while also creating a consolidated view across the wider group.

Common definitions and modelling logic could be implemented once rather than independently recreated for every business.

## Materialisation Strategy

Data volumes were relatively small.

I therefore didn't introduce more complex materialisation strategies simply because dbt supported them.

Views were practical across much of the warehouse and avoided unnecessary storage and pipeline complexity.

This was a deliberate decision based on the characteristics of the platform rather than an attempt to implement the most sophisticated possible architecture.

If volumes or performance requirements increased, models could be materialised differently later without changing the logical modelling approach.

## Organisational Resistance

Introducing dbt was not purely a technical problem.

I faced significant resistance from the Head of Data, who wanted the organisation to continue using Alteryx.

They had introduced Alteryx and, without a technical engineering background, saw the accessibility of its graphical interface as an advantage rather than seeing the operational problems that had emerged as the analytics estate grew.

I had to make the case that the problem wasn't simply which transformation tool we preferred.

The existing approach made it difficult to:

- Version changes reliably.
- Review code.
- Test transformations automatically.
- Separate development from production.
- Reuse business logic.
- Understand dependencies.
- Deploy consistently.
- Build a maintainable analytical model.

I didn't try to solve that disagreement by immediately removing Alteryx.

Instead, I improved the existing environment while demonstrating a better development model through dbt.

That allowed the new approach to prove its value through working software rather than relying solely on an architectural argument.

## Outcomes

The project changed BigQuery from primarily being a staging location for Tableau into a structured analytical warehouse.

It introduced:

- Version-controlled analytical code.
- dbt-based transformation and modelling.
- Development and production separation.
- Pull-request-based development.
- Automated deployment.
- Automated dbt testing.
- More consistent analytical models.
- Reusable logic across multiple businesses.
- Consolidated group-level reporting.
- Reduced dependence on Tableau for business logic.
- A more maintainable route for future analytical development.

Just as importantly, it established many of the engineering practices that the existing analytics environment had been missing.

The modernisation wasn't a single platform replacement. It was an incremental transition from analyst-owned files and manually operated workflows towards a reproducible, testable and maintainable data platform.

## What I Learned

This project reinforced the importance of improving systems incrementally when people still depend on them.

The technically cleanest option would have been to replace the existing Alteryx workflows as quickly as possible. In practice, analysts needed to continue delivering while the new platform was being built.

Stabilising Alteryx first bought the time required to introduce dbt properly.

It also reinforced that technology decisions cannot be separated from organisational change.

Introducing a technically stronger tool does not automatically result in adoption. When people are invested in an existing approach, demonstrating the benefits through a working alternative can be more effective than arguing about the technology itself.

Finally, the project demonstrated the value of looking for structural similarities across an organisation. Because Newport's businesses shared a common source platform, modelling them independently would have created unnecessary duplication. Designing around that commonality created both engineering efficiencies and a new consolidated analytical capability.

## Questions this experience answers

- What data engineering work did Martin do at Newport Takkt?
- What was the Newport data warehouse modernisation project?
- Has Martin built a data warehouse?
- Does Martin have hands-on BigQuery experience?
- Does Martin have hands-on dbt experience?
- Has Martin introduced dbt into an organisation?
- Has Martin migrated from Alteryx to dbt?
- Does Martin have Alteryx experience?
- Has Martin built CI/CD for dbt?
- Does Martin have Azure Pipelines experience?
- Has Martin worked across Azure and GCP?
- How does Martin approach development and production separation?
- How does Martin approach source control for legacy systems?
- Has Martin introduced software engineering practices into an analytics team?
- How does Martin approach modernising a legacy data platform?
- How does Martin balance platform modernisation with ongoing business delivery?
- Has Martin dealt with resistance to technical change?
- How does Martin influence stakeholders who disagree with a technical direction?
- Has Martin worked with multiple businesses or brands sharing a data platform?
- How does Martin approach reusable data modelling?
- How does Martin decide between views and materialised tables?
- How does Martin approach data warehouse architecture?
- How hands-on is Martin technically?
