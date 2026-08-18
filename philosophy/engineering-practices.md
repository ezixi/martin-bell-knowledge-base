---
type: capability
title: Engineering Practices
scope: career-wide
domain:
  - Data Engineering
  - Analytics Engineering
  - Data Architecture

summary: >
  I apply software engineering principles to data development, with an emphasis
  on maintainability, repeatability, testing, observability and safe delivery.
  My approach includes source control, code review, CI/CD, automated testing,
  coding standards, environment separation, documentation and explicit ownership
  of production data systems. I have introduced and developed these practices
  across multiple organisations and data platforms.

skills:
  - Software Engineering Practices
  - Data Engineering
  - Analytics Engineering
  - CI/CD
  - Git
  - Code Review
  - Automated Testing
  - Data Quality
  - Observability
  - SQL Standards
  - Documentation
  - Infrastructure as Code
  - Technical Leadership
  - Developer Experience

principles:
  - Treat data code as production software.
  - Keep code and platform definitions in source control.
  - Make changes reviewable before they reach production.
  - Automate repeatable quality checks.
  - Separate development from production.
  - Make failures visible through monitoring and alerting.
  - Prefer reproducible systems over manual intervention.
  - Establish standards without creating unnecessary bureaucracy.
  - Keep documentation close to the code.
  - Continuously improve the engineering process.

evidence:
  - company: Apollo
    examples:
      - Introduced Git-based development and pull-request workflows.
      - Established development and production separation.
      - Implemented CI/CD for the Azure data platform.
      - Introduced automated data-quality testing and reconciliation.
      - Maintained platform configuration and documentation in source control.

  - company: ESL FACEIT Group
    examples:
      - Introduced Analytics Engineering standards and working practices.
      - Established SQL coding standards and strict linting.
      - Introduced testing and documentation practices.
      - Improved data quality to eliminate recurring daily data-quality failures.
      - Built an Analytics Engineering function around disciplined engineering practices.

  - company: Newport Takkt
    examples:
      - Applied code-first data engineering practices using Python, SQL and dbt.
      - Used CI/CD to support reliable data-platform development.
      - Introduced testing and repeatable ELT processes.

related:
  - leadership.md
  - ../experience/EFG/analytics-engineering-function.md
  - ../experience/EFG/snowflake-migration.md
  - ../experience/Apollo/cloud-modernisation.md
  - ../experience/Apollo/architecture-review.md
---

# Engineering Practices

## Overview

I believe data systems should be treated as production software.

SQL transformations, data models, pipelines and analytical logic can be just as critical to a business as application code. Errors can affect financial reporting, operational decisions, customer-facing products and strategic decisions.

The engineering practices surrounding data development should reflect that responsibility.

My approach is based around a relatively small number of principles:

- Changes should be reproducible.
- Code should be reviewable.
- Quality should be tested automatically where possible.
- Production should be protected from development.
- Failures should be visible.
- Systems should be understandable by people other than their original author.
- Repetitive engineering processes should be automated.

I have introduced or developed these practices across Data Engineering and Analytics Engineering teams, adapting the level of process to the maturity and needs of each organisation.

## Source Control

Production data logic should live in source control.

This includes more than application-style code. Depending on the platform, I expect repositories to contain things such as:

- SQL transformations.
- dbt models.
- Pipeline definitions.
- Configuration.
- Tests.
- Infrastructure definitions.
- Seed and mapping data.
- Documentation.

The repository should represent, as closely as practical, the definition of the deployed data platform.

This provides history, accountability and reproducibility while removing dependency on knowledge held only by individual engineers or definitions that exist only inside production systems.

Directly editing production views, stored procedures or pipelines makes changes difficult to review, understand or reverse and should be avoided.

## Branching and Pull Requests

Changes should normally be developed on a branch and merged through a pull request.

A typical workflow is:
**Work item → branch → development → automated checks → pull request → peer review → deployment**

Pull requests provide more than a mechanism for approving code. They create an opportunity to:

- Identify bugs.
- Challenge assumptions.
- Discuss modelling decisions.
- Share knowledge.
- Maintain standards.
- Improve consistency across a team.

Review should not become a bureaucratic approval process. Its purpose is to improve the quality of the system and distribute understanding of how it works.

## Development and Production Separation

Engineers should be able to make and test changes without modifying production.

At minimum, I want a clear distinction between development and production data environments.

The exact implementation depends on the platform and organisation. It might involve separate cloud projects, databases, schemas, storage locations or accounts.

The principle is more important than the implementation:

> A developer should be able to make a mistake without immediately affecting an end user.

Environment separation also makes automated deployment possible because production becomes something that is **deployed to**, rather than somewhere engineers manually develop.

## CI/CD

I use CI/CD to turn engineering standards into repeatable processes.

Continuous Integration should automatically perform the checks that otherwise rely on engineers remembering to perform them.

Depending on the platform, this can include:

- SQL linting.
- Compilation.
- Unit tests.
- Data tests.
- Schema validation.
- Dependency validation.
- Configuration validation.

Continuous Deployment then provides a controlled mechanism for moving an approved change into an environment.

The objective is not CI/CD for its own sake. The objective is to make the safest path to production also the easiest and most repeatable path.

## Coding Standards

Consistency matters in a shared codebase.

I have introduced coding standards covering areas such as:

- SQL formatting.
- Naming conventions.
- Aliasing.
- Model naming.
- CTE structure.
- Directory structure.
- Documentation.
- Model grain.
- Testing expectations.

Where practical, these standards should be enforced automatically through tools such as linters rather than manually during code review.

At EFG, for example, I introduced strict SQL linting alongside Analytics Engineering standards.

The purpose of standards is not aesthetic uniformity. Consistent code is easier to review, debug and maintain, particularly as teams grow.

## Testing

I believe testing should happen at multiple levels.

### Code-level testing

Basic engineering checks should catch structural problems before deployment.

Examples include:

- Compilation.
- Syntax.
- Linting.
- Schema expectations.
- Unit tests where appropriate.

### Data testing

Data models should test the assumptions on which they depend.

Common tests include:

- Uniqueness.
- Non-null keys.
- Referential integrity.
- Accepted values.
- Valid ranges.
- Expected grain.
- Duplicate detection.

Tests should reflect actual business and modelling assumptions rather than simply maximising the number of tests.

For example, if a model claims to contain one row per athlete per day, that grain is an important contract and should be tested.

### Reconciliation

When replacing an existing data product, I also use reconciliation against the existing system.

At Apollo, migrated Gold models could be compared against both underlying source data and the legacy SQL Server reporting output before a Tableau report was redirected to the new platform.

This is particularly valuable during migrations because a technically correct new model is not sufficient; differences from the existing business output need to be understood.

## Data Quality

I treat data quality as an engineering responsibility rather than something that should primarily be discovered by analysts or end users.

A mature data system should detect problems as close as possible to where they are introduced.

This means combining:
**Prevention** — good modelling, explicit contracts, code review and testing.
**Detection** — automated data-quality tests and monitoring.
**Response** — clear ownership, alerting and processes for resolving failures.

At EFG, improving these practices helped move the platform from recurring daily data-quality problems to zero routine daily data-quality failures.

The broader objective is to move from:
**customer or analyst finds problem → engineer investigates**

to:
**system detects problem → team responds before downstream users are affected**

## Observability

Passing tests does not necessarily mean a production data platform is healthy.

I want visibility into areas such as:

- Pipeline failures.
- Data freshness.
- Processing duration.
- Unexpected row-count changes.
- Data-quality failures.
- Expensive queries.
- Infrastructure utilisation.
- Cloud costs.

Observability also provides the evidence needed for optimisation.

Without measurements, engineering teams can easily respond to performance problems by increasing resources without understanding the underlying cause.

Monitoring makes it possible to distinguish between genuine capacity requirements and inefficient pipelines, queries or infrastructure.

## Documentation

I consider documentation part of the engineering deliverable.

For data models, useful documentation includes:

- Purpose.
- Grain.
- Sources.
- Important transformations.
- Relationships.
- Business rules.
- Known limitations.
- Expected usage.

For platforms, documentation should also cover the operational processes engineers need to work safely, such as adding a source, deploying a change, creating a model, onboarding a client or responding to failures.

I prefer documentation to live as close as practical to the code and to be maintained through the same review process.

This reduces the likelihood of documentation becoming detached from the system it describes.

## Reproducibility

A recurring principle in my architecture and engineering work is that systems should be reproducible.

If an important dataset, pipeline or environment can only be recreated through undocumented manual actions, that represents operational risk.

Depending on the technology, reproducibility can come from:

- Version-controlled transformations.
- Declarative models.
- Configuration.
- Generated metadata.
- Infrastructure as Code.
- CI/CD.
- Deterministic rebuild processes.

This principle was particularly important in the Apollo platform, where analytical Silver and Gold datasets could be recreated from source data and version-controlled definitions rather than depending on manually maintained database state.

## Automation

I look for repetitive engineering work that can be standardised and automated.

That might include deployments, testing, linting, configuration generation, pipeline orchestration, environment provisioning, data-quality checks and monitoring.

Automation is not valuable simply because something *can* be automated.

The first question should be whether the underlying process is sensible and sufficiently understood. Automating a poor process simply makes the poor process run faster.

The objective is to remove routine work so engineers can spend more time solving problems that require judgement and technical expertise.

## Engineering Practices and Team Maturity

I don't believe every organisation needs the same level of engineering process.

A small team maintaining a relatively simple platform does not need the same controls as a large organisation operating hundreds of critical pipelines.

**Process should solve a problem.**

When introducing engineering practices, I consider:

- Team size.
- Technical maturity.
- Platform complexity.
- Business criticality.
- Frequency of change.
- Consequences of failure.

At Apollo, for example, my initial architecture recommendations deliberately favoured technologies and practices the existing team could realistically operate rather than immediately introducing the most sophisticated possible platform.

My goal is to establish a strong engineering foundation and increase sophistication when the organisation actually requires it.

## Developer Experience

I believe good engineering practices should make engineers more effective, not make their jobs harder.

Standards, tooling and automation should reduce cognitive load and make the expected way of working obvious.

An engineer joining a project should be able to understand:

- Where code belongs.
- How to run it.
- How to test it.
- How to make a change.
- How to submit that change.
- How it reaches production.
- How they know whether it worked.

If those things depend primarily on asking the person who built the platform, the engineering system is not mature enough.

## My Standard

The outcome I aim for is a data platform where:

- Production changes are traceable.
- Code is reviewed.
- Standards are largely automated.
- Development can happen safely.
- Important assumptions are tested.
- Failures are visible.
- Ownership is clear.
- Documentation is available.
- Deployments are repeatable.
- Infrastructure and data products can be reproduced.
- Engineers can work independently without relying on undocumented knowledge.

The specific tools will change.

The underlying objective does not:

**Make data systems reliable, understandable and safe to change.**

## Questions this experience answers

- How does Martin approach engineering practices in data teams?
- How does Martin apply software engineering principles to analytics engineering?
- What is Martin's approach to CI/CD?
- How does Martin approach data quality?
- How does Martin use automated testing?
- What is Martin's approach to code review and pull requests?
- How does Martin think about development and production environments?
- How does Martin approach observability?
- What is Martin's approach to documentation?
- How does Martin introduce engineering standards?
- How does Martin balance engineering rigour with team maturity?
- How does Martin approach developer experience?
- How does Martin make data platforms reproducible?
- What engineering practices has Martin introduced at EFG, Apollo and Newport?
