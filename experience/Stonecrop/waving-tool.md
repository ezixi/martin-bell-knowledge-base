---
type: project
title: "Operational Waving and Near-Real-Time Data"
company: "Stonecrop Technologies"
role: Senior Manager, Data

domain:
  - Data Engineering
  - Operational Analytics
  - Data Architecture
  - Observability
  - Incident Management
  - Data Operations

summary: >
  I helped turn an analyst-built dashboard for prioritising warehouse orders
  into a reliable operational data product after its rapid adoption exposed
  weaknesses in our batch-oriented data platform and contributed to a production
  outage. I stabilised the immediate system, introduced monitoring and alerting,
  moved critical pipelines to incremental ingestion with approximately seven-minute
  refresh cycles, improved database and Tableau performance, and used the incident
  to drive longer-term improvements in architecture, engineering practices and
  stakeholder governance. Order waiting times ultimately fell from weeks to minutes.

skills:
  - Data Engineering
  - Operational Analytics
  - Incident Response
  - Observability
  - Performance Optimisation
  - Incremental Data Processing
  - Data Modelling
  - Technical Leadership
  - Stakeholder Management
  - Engineering Management

technologies:
  - PostgreSQL
  - Oracle
  - Airflow
  - dbt
  - Tableau
  - AWS
  - Metabase
  - PagerDuty
  - Slack
  - Git
  - SQL

outcomes:
  - "Productionised a dashboard that had become part of a warehouse workflow handling approximately 2,000 orders per day"
  - "Reduced critical data refresh cycles from nightly batches to approximately seven minutes"
  - "Reduced order waiting times from weeks to minutes"
  - "Introduced monitoring, alerting and incident-management practices"
  - "Improved database performance through materialisation, indexing and query optimisation"
  - "Introduced post-mortems and tighter production access controls"
  - "Used operational demand to inform a longer-term streaming and data-platform roadmap"

questions:
  - "Has Martin built operational analytics systems?"
  - "Has Martin dealt with a major production data incident?"
  - "How does Martin respond when an analytics system becomes business critical?"
  - "Does Martin have Airflow experience?"
  - "Does Martin have PostgreSQL performance optimisation experience?"
  - "Has Martin implemented incremental data pipelines?"
  - "What observability experience does Martin have?"
  - "Has Martin used PagerDuty?"
  - "Has Martin worked with near-real-time data?"
  - "How does Martin approach architecture when resources are limited?"
  - "Has Martin introduced post-mortems?"
  - "How does Martin balance immediate fixes with longer-term architecture?"
---

# Operational Waving and Near-Real-Time Data

## Overview

At Stonecrop, the data team had originally been built to solve an operational crisis.

By this point we had made significant progress, but we were still a small and relatively junior team with limited resources. We had responsibilities for both
reporting and operational data processes, and much of the platform had been assembled quickly in response to immediate business problems.

One project demonstrated how quickly a seemingly simple analytical solution could become a critical production system.

An analyst created a dashboard to help the warehouse decide which orders should be picked and shipped next.

It worked extremely well.

So well, in fact, that it was rolled out to the outbound warehouse team and became part of the operational process for handling approximately *2,000 orders
per day*.

The problem was that neither the dashboard nor the underlying data platform had been designed for that.

Eventually, at around 3am one morning, the system contributed to an outage that
brought the production line down.

What began as a reporting request had become a production engineering problem.

## Starting Point

Our analytical platform was relatively simple.

Data from the web application was loaded nightly into PostgreSQL and transformed
using SQL scripts. Those processes had originally run through cron on AWS and
were being migrated to Airflow.

Staging data was transformed into a star schema which supported CSV outputs,
Tableau reporting and some data that was fed back into the application.

We had also begun experimenting with dbt as the longer-term approach to managing
our transformations.

The architecture had grown organically and under considerable pressure. We knew
where many of its weaknesses were and were gradually replacing the emergency
solutions with better-engineered ones.

The team itself was still developing.

I had introduced Agile working approximately six months earlier and was still
teaching people Git and other engineering practices. I manually deployed Airflow
DAGs following code review and testing in the development environment.

There was also no budget to bring in outside help.

## The Business Problem

Cell tower construction happened in phases.

The tower and ground infrastructure might be required first, followed later by
radios, antennas and other equipment.

If a site manager requested the wrong phase, warehouse material could be
allocated and shipped unnecessarily when it could have been used for a
higher-priority site.

There was another complication.

Warehouse process adherence wasn't always strong and material could be misplaced.
This meant partially picked but incomplete orders accumulated in the outbound
process, creating additional congestion.

A business analyst had been investigating the problem and developed SQL that
helped identify which orders should actually be prioritised.

The objective was to allow the warehouse to pick **complete, high-priority
orders first**.

Previously, answering this kind of question required exporting data from the
warehouse management system and application interfaces and combining it manually
using Excel and VLOOKUPs.

## From Analysis to Operational Tool

The analyst came to me because his logic was sitting in Tableau.

He wanted me to create a view in the reporting schema instead.

I was happy to do that.

Moving the logic out of Tableau meant we could version it, review it and manage
it as part of the data platform.

I tested the query against the development database, made some improvements to
the SQL and deployed it.

From an analytical perspective, everything worked.

A couple of weeks later I discovered that the dashboard had become much more
important than either of us realised.

The outbound warehouse team had adopted it as part of their daily workflow.

Instead of one analyst occasionally querying the view, people across outbound
operations were repeatedly using the dashboard to decide what should be processed
next.

It was now helping run approximately **2,000 orders each day**.

But Tableau was using a live database connection.

Every dashboard refresh therefore executed the underlying query.

## The Incident

At around 3am, my CTO woke me because the production line had gone down.

The Tableau workload was interacting badly with our nightly data processing.

The live dashboard connections prevented the ETL process from dropping and
rebuilding a PostgreSQL table. That caused the Airflow process to fail and
ultimately affected the warehouse management system database.

Using the Airflow logs, I was able to work through what was happening.

The immediate technical problem could be fixed, but the incident exposed several
larger weaknesses:

- We had an inexperienced team supporting increasingly important systems.
- The architecture had grown in an ad hoc fashion.
- Communication between Data and operational stakeholders wasn't good enough.
- Access and data governance controls were too weak.
- We didn't fully understand how extensively an analytical product was being used.
- We were trying to support transactional operational decisions from a
  batch-oriented analytical platform.

Most importantly, something we had treated as a dashboard was now a **production
system**.

## Stabilising the System

Replacing the entire architecture wasn't an option.

We needed to make small, controlled improvements that could stabilise production
quickly while keeping the warehouse operating.

### Materialising the data

I moved away from repeatedly executing the expensive view and materialised the
data instead.

The materialised objects could be recreated concurrently, reducing contention
with users of the data.

### Introducing monitoring and alerting

Airflow gave us useful visibility into pipeline execution, so I expanded that
into operational monitoring.

Scheduler failures generated alerts through PagerDuty so Production Services
could respond.

Successful runs generated messages into a dedicated Slack channel.

We also captured pipeline timings in Metabase so we could monitor whether
processing was becoming faster or slower over time rather than waiting for a
failure.

I joined the PagerDuty rotation myself.

### Optimising PostgreSQL

I reviewed and optimised indexes on the underlying source tables.

We monitored whether the PostgreSQL query planner actually used those indexes.
Where it continued to perform table scans, we changed or removed the indexes
rather than assuming that adding an index automatically improved performance.

We also built PostgreSQL-specific monitoring around:

- Running jobs.
- Query performance.
- Index usage.
- Database locks.

AWS monitoring provided additional infrastructure-level visibility.

### Removing Tableau from the live workload

I changed the Tableau dashboard from a live connection to an extract.

The data pipeline then called the Tableau API to refresh that extract **after**
the upstream processing had successfully completed.

This meant users still received current information without every interaction
with the dashboard generating a query against the database.

### Moving critical data to incremental ingestion

Nightly processing was no longer sufficient for an application being used to
make warehouse decisions throughout the day.

We identified the most important source tables and moved them to incremental
ingestion.

Through optimisation, we reduced the refresh interval to approximately **seven
minutes**.

We monitored runtime and alerted when a process took too long or when average
runtime began increasing.

We applied a similar approach to the Oracle warehouse-management-system data,
including improving connection handling so we could retrieve the required data
without destabilising the source system.

## Engineering and Process Changes

The incident wasn't just a database-performance problem.

It showed that our engineering and organisational practices needed to mature as
the importance of the data platform increased.

I introduced **post-mortems for production incidents** so failures became an
opportunity to understand and improve the system rather than simply repair it.

We tightened access to production systems.

I also brought key stakeholders into backlog-scrubbing and prioritisation
meetings. We needed better visibility into how people were actually using our
data and which requirements were becoming operationally important.

We continued moving transformations into **dbt**, where SQL could be better
modelled, tested and managed.

I subsequently hired more senior Data Engineering capability, including a
Senior Data Engineer who began improving automation around CI/CD and testing.

## Longer-Term Architecture

The experience made it clear that nightly batch reporting alone would not meet
the organisation's future operational requirements.

Once warehouse users had access to useful, timely information, demand for that
information was only going to increase.

I therefore added streaming to the architectural roadmap.

I had recently hired our first Data Engineer and asked him to investigate
streaming through **AWS Kinesis**. We spent time working through the system
design and scalability implications, and the work was eventually containerised
using Docker.

We also brought forward plans for an Oracle replica for the warehouse management
system so analytical workloads could be isolated from production.

Other longer-term work included:

- Continuing the migration of transformations to dbt.
- Improving SQL modelling and automated testing.
- Preparing for a potential move to Redshift, although budget constraints
  affected that work.
- Automating CI/CD and testing.
- Exploring scaling Airflow beyond the local scheduler using Celery and
  Kubernetes.

Not every element of that roadmap was implemented while I was there, but the
incident changed our understanding of what the data platform needed to become.

## Outcome

The dashboard itself gave us a useful measure of whether the overall operational
process was improving: **the age of orders waiting to be processed**.

Before the changes, some orders could sit in the process for weeks.

We reduced that wait to **minutes**.

The technical improvements were important, but the larger outcome was that a
manual and unreliable operational decision-making process had become a much more
timely and dependable data-driven workflow.

## What I Learned

The most important lesson from the project was simple:

**If we present data to users — in whatever form — we have a production system,
and we should treat it as such.**

A dashboard can be just as operationally critical as an application.

If people depend on it to do their jobs, it needs appropriate engineering:
monitoring, testing, performance management, controlled deployment, ownership
and incident response.

The project also reinforced the importance of understanding how a system is
actually being used.

Technically, the original implementation was reasonable for the requirement we
thought we had: one analyst wanted easier access to a useful piece of analysis.

The problem changed when hundreds of operational decisions began depending on
it.

Architecture has to respond to that reality.

It also demonstrated the value of incremental improvement.

We didn't have the resources to stop everything and build an ideal streaming
architecture from scratch. I stabilised the existing system first, measured its
behaviour, removed the most significant bottlenecks and progressively improved
it.

The longer-term architecture then followed from what we had learned in
production.

## Questions this experience answers

- Has Martin built operational data products?
- Has Martin worked with business-critical analytics?
- What is an example of Martin dealing with a production incident?
- How does Martin respond to a major data outage?
- Does Martin have incident-management experience?
- Has Martin participated in an on-call rotation?
- Has Martin used PagerDuty?
- What observability experience does Martin have?
- Has Martin implemented Airflow monitoring and alerting?
- Does Martin have Airflow experience?
- Does Martin have PostgreSQL experience?
- Has Martin optimised PostgreSQL queries and indexes?
- Does Martin understand database locking and contention?
- Has Martin worked with Oracle?
- Has Martin integrated Tableau with operational data pipelines?
- Has Martin used the Tableau API?
- Has Martin implemented incremental ingestion?
- Has Martin worked with near-real-time data?
- Has Martin worked with streaming architectures?
- Does Martin have AWS Kinesis experience?
- Has Martin used dbt?
- Has Martin introduced post-mortems?
- How does Martin approach production access and data governance?
- How does Martin work with operational stakeholders?
- How does Martin balance immediate operational needs with longer-term architecture?
- What does Martin do when there isn't budget to rebuild a system?
- How does Martin approach technical debt?
- How does Martin decide when batch processing is no longer sufficient?
- What does Martin mean when he says analytics should be treated as a production system?
- What is an example of Martin improving data latency?
- What is an example of Martin improving an operational business process?
- How did Martin reduce order waiting times at Stonecrop?
- What is an example of Martin learning from a production failure?
