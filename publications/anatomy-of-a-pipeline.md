---
title: "Anatomy of a Pipeline: CI/CD for a dbt Data Warehouse on Google BigQuery Using Azure Pipelines"
publication: "Backhand Media"
type: "technical article"
external_url: "https://www.backhandmedia.com/s/stories/anatomy-of-a-pipeline-cicd-for-a-dbt-data-warehouse-on-google-big-query-using-azure-pipelines"
topics:
- analytics engineering
- data engineering
- dbt
- BigQuery
- Azure Pipelines
- CI/CD
- automated testing
- Git
skills:
- Analytics Engineering
- Data Engineering
- CI/CD
- dbt
- BigQuery
- Azure DevOps
- Git
- Automated Testing
related_docs:
- ../experience/newport-takkt/overview.md
- ../experience/newport-takkt/projects/data-warehouse.md
- ../philosophy/engineering-practices.md
---

# Anatomy of a Pipeline

[**Anatomy of A Pipeline: CI/CD For a dbt Data Warehouse on Google Big Query Using Azure Pipelines**](https://www.backhandmedia.com/s/stories/anatomy-of-a-pipeline-cicd-for-a-dbt-data-warehouse-on-google-big-query-using-azure-pipelines) is a technical article I wrote while working at Newport Takkt.

The article documents how I implemented automated deployment and testing for the dbt and BigQuery data warehouse I was building there.

It is both a technical walkthrough and a record of the engineering practices I was introducing into an analytics environment that had previously relied heavily on locally executed Alteryx workflows and manual development processes.

## Context

At Newport, I was replacing a loosely structured analytics environment with a more conventional data warehouse built using BigQuery and dbt.

One important part of that change was treating analytical transformations as software.

Development took place against a separate BigQuery development project, while production changes were version controlled and deployed through Azure Pipelines.

The article documents the CI/CD implementation I created to support that workflow.

## What the article covers

The pipeline was defined as YAML stored alongside the dbt project and automatically executed following changes to the production branch.

The article walks through the implementation step by step, including:

- configuring branch-based deployment triggers;
- running the pipeline inside a Python container;
- checking out the dbt repository and its dependencies;
- managing BigQuery service-account credentials using Azure Secure Files;
- securely configuring the dbt profile at runtime;
- caching Python dependencies to reduce pipeline execution time and cost;
- installing dbt within the deployment environment;
- executing dbt models automatically;
- running dbt tests as part of the deployment process.

I also describe combining the pipeline with protected Git branches and pull-request rules so that production changes could only be introduced through an approved development process.

## Engineering approach

The implementation was relatively simple, but the more important change was the development model behind it.

Previously, much of the analytical transformation work depended on graphical Alteryx workflows stored and executed on analysts' machines. Changes were difficult to review, reproduce or safely deploy.

Moving transformations into dbt made them code. Git then provided version control and collaboration, while CI/CD made deployment repeatable.

The resulting workflow was:
**develop → review → merge → deploy → test**

rather than relying on an individual analyst to manually modify and execute a production workflow.

The pipeline also kept credentials outside the repository. BigQuery service-account credentials and dbt configuration were stored using Azure Secure Files, made available only for the duration of the pipeline execution, and removed afterwards.

## Testing

Automated testing was part of the production deployment rather than a separate manual activity.

This meant data tests were executed consistently whenever the production models were deployed and failures could be surfaced automatically.

The article also notes that this was only the beginning of the CI/CD capability. Further improvements I identified included running only changed models and automatically generating and publishing dbt documentation.

## Why it is relevant

The article provides a concrete example of a principle that has remained consistent throughout my later work:
Data and analytics development should follow the same engineering disciplines as other production software.

Version control, peer review, environment separation, automated deployment and testing are not additional bureaucracy around analytics. They make change safer, faster and more repeatable.

The Newport implementation was an early practical example of those principles in my work. I subsequently applied and expanded the same approach when building Analytics Engineering capabilities and modernising data platforms in later roles.

## Questions this experience answers

- Has Martin implemented CI/CD for a data platform?
- Has Martin used dbt in a production environment?
- Has Martin implemented automated data testing?
- Has Martin worked with BigQuery?
- Has Martin used Azure Pipelines / Azure DevOps?
- Has Martin introduced software engineering practices into an analytics team?
- Does Martin understand secure credential handling in automated data pipelines?
- Can Martin communicate technical engineering concepts through long-form writing?
- Has Martin implemented development and production separation for analytics workloads?
