---
type: philosophy
title: Data Strategy
scope: career-wide

summary: >
  I approach data strategy by starting with business goals, decisions and user
  needs before selecting technologies or designing architecture. My approach
  combines data quality, shared business definitions, data literacy, appropriate
  architecture, engineering practices and pragmatic governance to create data
  capabilities that improve business outcomes. I favour simple architectures
  appropriate to organisational maturity, measurable outcomes, and iterative
  delivery over technology-led transformation.

subjects:
  - Data Strategy
  - Data Leadership
  - Data Architecture
  - Analytics Engineering
  - Data Governance
  - Data Quality
  - Data Literacy
  - Semantic Layers
  - Self-Service Analytics
  - AI Readiness

principles:
  - Business outcomes before technology.
  - People before platforms.
  - Meaning before metrics.
  - Quality before sophistication.
  - Simplicity before complexity.
  - Capability before novelty.
  - Enablement before control.
  - Outcomes before activity.
  - Evolution before perfection.

related:
  - engineering-practices.md
  - leadership.md
  - ../stories/creating-a-data-strategy.md
  - ../stories/data-literacy.md
  - ../stories/data-quality-is-everything.md
---

# Data Strategy

## Overview

I believe a data strategy should explain how data will help an organisation achieve its goals.

That sounds obvious, but data strategies can easily become technology strategies: lists of platforms to migrate to, tools to implement, teams to build or capabilities that an organisation believes it should have.

I prefer to start somewhere else:
**What is the organisation trying to achieve, what decisions and activities will help it get there, and how can data make those things more effective?**

Technology, architecture, organisation and governance follow from those questions.

A good data strategy should connect:
**Business goals → decisions and behaviours → data capabilities → technology and delivery**

The result should be practical enough to turn into priorities, ownership and a roadmap.

## Start With the Business

I don't start a data strategy by asking what the data platform should look like.

I start by understanding the organisation.

That means questions such as:

- What is the organisation trying to achieve?
- What are its most important business problems?
- How does it expect to grow or change?
- What decisions have the greatest impact on those outcomes?
- Who makes those decisions?
- What prevents those people from making better decisions today?
- Where could data materially improve the way the organisation operates?

This helps distinguish genuine data requirements from interesting technical opportunities.

There will always be new platforms, frameworks and architectural patterns worth exploring. I enjoy learning and experimenting with them, but novelty is not a strategy.
**A tool is useful because it solves a problem, not because it is new.**

## Understand the People

A data strategy needs to account for the people who produce, manage and consume data.

I want to understand:

- Who creates the data?
- Who owns its meaning?
- Who consumes it?
- What decisions are they making?
- How technically capable are they?
- How quickly do they need information?
- What level of detail do they need?
- How do they currently work?
- What do they trust or distrust about the existing data?

The same underlying data might need to serve a Data Scientist working in Python, an analyst writing SQL, a finance team working in spreadsheets, an executive looking at a dashboard, or an operational employee who simply needs a clear signal telling them what action to take.

A successful strategy needs to support those different needs rather than expecting everyone to interact with data in the same way.

## Understand the Data

Before deciding how data should be stored or processed, I want to understand where it comes from and what it represents.

That includes:

- Source systems.
- Ownership.
- Business entities.
- Important events.
- Data volumes.
- Data quality.
- Timeliness.
- Historical requirements.
- Security and access requirements.
- Dependencies on external systems.
- How likely source structures are to change.

I also want to understand the relationships behind the data.

What is a customer? What is an active user? What constitutes revenue? What is a session? What does availability mean?

These questions are often more important than the technology used to store the answers.

## Define the Important Business Concepts

One of the most valuable things a data strategy can establish is a shared understanding of the organisation.

Important entities, metrics and business rules should have clear definitions.

If Finance, Product and Marketing use different definitions of an active customer, the organisation has a semantic problem rather than a dashboard problem.

A good analytical architecture therefore needs somewhere for shared business meaning to live.

Depending on the organisation, that might include:

- Conformed dimensions and facts.
- Metric definitions.
- Semantic models.
- Data dictionaries.
- Business glossaries.
- Governed reporting models.

The implementation can vary.

The principle is that important business concepts should not need to be independently reconstructed every time somebody asks a question.

This becomes even more important when AI systems are consuming organisational data. An LLM cannot reliably reason about concepts the organisation itself has never clearly defined.

## Data Quality Comes First

I consider data quality foundational to data strategy.

A fast, elegant and sophisticated data platform has very little value if people cannot trust the information coming out of it.

Data quality therefore needs to be designed into the system through:

- Clear ownership.
- Good modelling.
- Testing.
- Monitoring.
- Observability.
- Reconciliation.
- Documentation.
- Engineering standards.

Trust is cumulative.

Consistently reliable data encourages people to use data in their work. Unreliable data pushes people back towards spreadsheets, private datasets, anecdotes and intuition.

Once trust has been lost, rebuilding it is much harder than maintaining it in the first place.

## Data Literacy Is Part of the Strategy

Making data available is not the same as making an organisation data-driven.

If people are expected to use metrics to understand their performance and make decisions, they need to understand what those metrics mean.

That does not mean everyone needs to know SQL.

It means people should understand:

- The metrics relevant to their work.
- How those metrics are defined.
- What they can and cannot conclude from them.
- How their actions affect them.
- Basic analytical and statistical concepts appropriate to their role.
- Where to go when they do not understand the data.

I see data as a common organisational language.

Shared definitions make conversations easier because people can discuss outcomes without first negotiating what every number means.

Data literacy and semantic consistency are therefore closely connected.

## Architecture Should Follow Requirements

Once the business, users and data are understood, architectural decisions become much easier.

I consider things such as:

- Data volume.
- Data velocity.
- Required freshness.
- Query patterns.
- Consumer skills.
- Security.
- Reliability requirements.
- Team capability.
- Operational overhead.
- Cost.
- Expected growth.

Not every organisation needs streaming infrastructure, a lakehouse, a semantic platform or the latest distributed processing framework.

Sometimes a relatively simple warehouse is exactly the right architecture.

Sometimes it is not.

The goal is to use the **simplest architecture that can reliably meet the organisation's requirements and reasonably expected growth**.

Complexity should be earned by a real requirement.

## Team Capability Matters

A technically excellent architecture that nobody can operate is not an excellent architecture.

Strategy therefore needs to account for the people who will build and maintain the platform.

When considering technologies and architectural patterns, I ask:

- Does the team understand this technology?
- Can they support it in production?
- How difficult will it be to hire for?
- What operational burden does it introduce?
- What new capabilities would the team need?
- Is the benefit worth that complexity?

This does not mean avoiding new technology.

It means introducing sophistication deliberately rather than assuming technical sophistication is inherently valuable.

The platform and the team should mature together.

## Engineering Practices Are Strategic

Data strategy is not only about architecture.

How the team develops and operates the platform has a direct impact on its ability to support the business.

I therefore consider engineering capabilities such as:

- Source control.
- Code review.
- Testing.
- CI/CD.
- Environment separation.
- Observability.
- Documentation.
- Reproducibility.
- Automation.

These practices reduce operational risk and make future change easier.

They also affect delivery speed. A platform that can be changed confidently is ultimately more adaptable than one where every change risks breaking production.

See `engineering-practices.md` for my detailed approach.

## Governance Should Enable, Not Obstruct

I believe governance is necessary, but I don't believe governance should mean creating an approval process around every use of data.

Good governance makes important things explicit:

- Who owns the data?
- Who owns its meaning?
- Who can access it?
- What does a metric mean?
- Where should business logic live?
- What quality standards are expected?
- How are changes made?

Where possible, I prefer these controls to be embedded into normal engineering and analytical workflows.

Tests, pull requests, semantic models, documentation, access controls and clearly defined ownership can provide governance without creating a separate bureaucracy around data.

The objective is **trusted self-service**, not centralised control for its own sake.

## Self-Service Needs Foundations

I support self-service analytics, but simply giving everyone access to a BI tool does not create self-service.

People need:

- Trusted data.
- Understandable models.
- Consistent metrics.
- Appropriate tools.
- Documentation.
- Sufficient data literacy.

Without those foundations, self-service can simply distribute inconsistent analysis more efficiently.

The role of a central data team should not be to answer every question.

It should increasingly be to build the data products, definitions, tools and capabilities that allow other people to answer appropriate questions themselves.

## Cost Is an Architectural Requirement

Cost should be considered when designing the platform rather than reviewed only after cloud bills become a problem.

I consider:

- Compute versus storage.
- Workload patterns.
- Incremental processing.
- Materialisation.
- Query efficiency.
- Infrastructure utilisation.
- Licensing.
- Operational support cost.
- Engineering time.

The cheapest individual technology is not necessarily the cheapest overall solution.

A technology that saves infrastructure spend but requires substantial specialist support may have a higher total cost than a simpler managed service.

Cost optimisation therefore needs to consider **money, time and people**.

## Build for Change

A data strategy should not assume that today's requirements will remain unchanged.

Businesses change.

Metrics change. Products change. Source systems change. Organisations acquire companies, enter markets and restructure teams.

I therefore favour architectures and operating models that make change safe:

- Modular models.
- Reusable business logic.
- Explicit interfaces.
- Source control.
- Automated testing.
- Clear ownership.
- Documentation.
- Configurable pipelines.
- Reproducible infrastructure.

The objective is not to predict every future requirement.

It is to avoid making future change unnecessarily expensive.

## Measure Outcomes

A data strategy should define how we will know whether it is working.

I prefer measures connected to business and user outcomes rather than simply technical activity.

Depending on the strategy, these might include:

- Time to insight.
- Data quality.
- Platform reliability.
- Adoption.
- User satisfaction.
- Self-service usage.
- Development velocity.
- Cost per workload or user.
- Time required to onboard new data.
- Time required to change a metric.
- Reduction in duplicated logic.
- Reduction in manual work.

Building more pipelines, dashboards or models is not inherently success.

The question is whether the organisation has become better at using data to achieve its goals.

## Turning Strategy Into Delivery

A strategy needs to become executable.

Once the direction is understood, I translate it into:

1. **Current state** — where are we now?
2. **Target capabilities** — what do we need to be able to do?
3. **Gaps** — what prevents us doing those things today?
4. **Priorities** — which gaps matter most?
5. **Roadmap** — what should happen and in what order?
6. **Ownership** — who is responsible?
7. **Measures** — how will we know it worked?

I prefer iterative roadmaps over large transformation programmes that assume everything can be designed correctly in advance.

Deliver useful improvements, measure the results, learn from them and adjust the strategy.

## My Data Strategy Principles

### Business outcomes before technology

Start with what the organisation is trying to achieve.

### People before platforms

Understand who produces and consumes the data and what they need from it.

### Meaning before metrics

Define important business concepts before building multiple representations of them.

### Quality before sophistication

Reliable basic analytics is more valuable than advanced analytics built on unreliable foundations.

### Simplicity before complexity

Use the simplest architecture that meets the requirements.

### Capability before novelty

Choose technologies the organisation can successfully operate and evolve.

### Enablement before control

Governance should make safe, trusted data use easier.

### Outcomes before activity

Measure whether data capabilities improve the organisation, not how much technical output the data team produces.

### Evolution before perfection

Build a strong foundation, deliver incrementally and allow the strategy to evolve as the organisation learns.

## Questions this experience answers

- What is Martin's approach to data strategy?
- How does Martin create a data strategy?
- How does Martin align data strategy with business strategy?
- How does Martin decide which data technologies to use?
- How does Martin approach data architecture decisions?
- How does Martin balance technical sophistication with pragmatism?
- How does Martin approach data governance?
- How does Martin think about self-service analytics?
- How does Martin approach data literacy?
- How does Martin build trust in data?
- How does Martin approach data quality strategically?
- How does Martin think about semantic layers and metric definitions?
- How does Martin approach AI readiness within a data strategy?
- How does Martin account for team capability when designing a data platform?
- How does Martin measure whether a data strategy is successful?
- How does Martin turn a data strategy into a roadmap?
