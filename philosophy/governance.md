---
type: philosophy
title: "Data Governance"

domain:
  - Data Governance
  - Data Quality
  - Analytics Engineering
  - Data Architecture
  - Engineering Practices
  - Security
  - Semantic Layers

summary: >
  I see data governance as the combination of ownership, standards, controls
  and engineering practices that make data trustworthy and safe to use.
  Effective governance should be embedded into normal ways of working rather
  than imposed as a separate bureaucratic process. I favour version-controlled
  logic, clear ownership, governed metric definitions, automated testing,
  appropriate access controls, documented data models and observable production
  systems. The objective is not control for its own sake, but to allow people
  to use data confidently without creating unnecessary risk or inconsistency.

principles:
  - "Governance should enable people rather than create unnecessary gates"
  - "Business definitions need clear ownership"
  - "Important logic belongs in version control"
  - "Quality controls should be automated wherever possible"
  - "Production data systems require production engineering practices"
  - "Access should follow least-privilege principles"
  - "Governance should be proportionate to organisational maturity and risk"
  - "Good semantic design is a form of governance"

questions:
  - "What is Martin's approach to data governance?"
  - "How does Martin introduce governance without creating bureaucracy?"
  - "How does Martin improve trust in data?"
  - "How does Martin govern business metrics?"
  - "How does Martin approach data quality?"
  - "How does Martin approach access control?"
  - "What governance experience does Martin have?"
  - "How does Martin balance self-service with governance?"
  - "How does Martin introduce governance into an immature data organisation?"

related:
  - leadership.md
  - analytics.md
  - ../experience/EFG/analytics-engineering-function.md
  - ../experience/EFG/snowflake-migration.md
  - ../experience/Apollo/cloud-modernisation.md
  - ../experience/Apollo/architecture-review.md
---

# Data Governance

## My Approach

I don't see data governance primarily as a collection of committees, policies
and approval processes.

Governance is about creating enough structure around data that people can use
it confidently.

That includes knowing:

- What the data means.
- Where it came from.
- Whether it is trustworthy.
- Who owns important definitions.
- Who can access it.
- How changes are made.
- Whether those changes have been tested.
- What happens when something goes wrong.

A well-governed data platform should make the correct way of working the
**easiest way of working**.

Where possible, I prefer to enforce governance through architecture,
automation and normal engineering workflows rather than relying on people
remembering a policy document.

## Governance Should Match the Organisation

Governance needs to be proportionate.

A small organisation with a handful of engineers does not need the same
governance structure as a multinational company with hundreds of data
producers and consumers.

Trying to introduce an enterprise governance framework into an immature data
organisation can create process without solving the underlying problems.

I generally start with the controls that remove the greatest risks:
**version control → review → testing → ownership → access control → monitoring**

The sophistication of those controls can then increase as the organisation,
platform and risk grow.

This was particularly relevant at Stonecrop and Apollo, where the immediate
need was not to establish a large governance organisation. It was to replace
unsafe working practices with simple, repeatable ones.

## Business Logic Is Governed Data

One of the most important governance problems is often overlooked because it
doesn't look like traditional governance:
**What does a business metric actually mean?**

If Revenue, Active Customer, Availability or Training Load can mean different
things depending on which analyst, dashboard or SQL query calculates it, the
organisation has a governance problem.

I therefore treat modelling and semantic design as part of data governance.

Important business concepts should have:

- An agreed definition.
- A known grain.
- Clearly understood dimensions.
- A defined owner.
- Centralised calculation logic.
- Tests where appropriate.
- Documentation.
- A controlled process for changing the definition.

This is one of the reasons I favour semantic layers and well-designed
analytical models.

They turn business knowledge that might otherwise exist in people's heads,
dashboards and individual SQL queries into shared organisational infrastructure.

## Governance Through Engineering

A large part of governance can be implemented through good engineering
practice.

I want production logic in **Git**, with changes made through controlled
development workflows rather than edited directly in production.

Depending on the maturity of the organisation, that normally means some
combination of:

- Development and production environments.
- Branching and pull requests.
- Peer review.
- SQL and code standards.
- Automated linting.
- Automated data tests.
- CI/CD.
- Documentation.
- Monitoring and alerting.
- Incident management and post-mortems.

These mechanisms aren't just engineering preferences.

They are governance controls.

Version control provides an audit history. Peer review creates a control over
change. Automated testing protects data quality. CI/CD makes deployments
repeatable. Monitoring tells us whether the controls actually worked.

Good engineering therefore removes much of the need for governance to exist as
a separate manual activity.

## Data Quality

I don't think data quality can be solved by asking analysts to check dashboards
more carefully.

Quality needs to be designed into the system.

At different organisations I have introduced controls such as:

- Uniqueness and null testing.
- Referential-integrity checks.
- Business-rule validation.
- Pipeline monitoring.
- Runtime and freshness monitoring.
- Reconciliation against existing systems.
- Automated testing during deployment.
- Observability and alerting.

The exact implementation depends on the platform, but the principle remains the
same:
**detect problems as close as possible to where they are introduced.**

Finding a data problem during development is cheap.

Finding it after an executive has made a decision from a dashboard is not.

## Access and Security

Governance also means understanding who should be able to do what.

I favour **least-privilege access** rather than broad shared access to
production systems.

That distinction became particularly clear at Stonecrop.

An analytical workload unexpectedly became operationally critical and
contributed to a production outage. One of the resulting changes was to tighten
access to production systems and accelerate plans to isolate analytical
workloads from operational databases.

At Apollo, I found a more fundamental governance problem: shared credentials
and the absence of organised role-based access controls across the data
platform.

My architectural recommendations therefore included RBAC, environment
separation and client isolation alongside the data-platform changes.

Governance isn't useful if it exists only inside the warehouse while the
underlying production systems remain uncontrolled.

## Self-Service and Governance Are Not Opposites

I strongly favour making data accessible.

At Safari, for example, I ran open office hours to help people throughout the
organisation understand and use data rather than making Analytics the
gatekeeper for every question.

But self-service does not mean everyone independently recreating business
logic.

I want people to have considerable freedom to:

- Explore trusted data.
- Create analyses.
- Build visualisations.
- Ask new questions.
- Combine governed concepts in new ways.

I am much less comfortable with every analyst independently defining what
Revenue, Customer, Retention or another core business concept means.

The distinction I make is between **freedom to analyse** and **freedom to
redefine shared business concepts**.

Good governance enables the first by controlling the second.

## Governance in Practice: Stonecrop

Stonecrop started from a very immature position.

Operational processes relied heavily on manual work, the team was inexperienced
with software engineering practices, and important analytical systems had grown
quickly in response to business emergencies.

I progressively introduced:

- Git and version control.
- Development and review processes.
- More controlled deployments.
- Data modelling practices.
- Testing.
- Monitoring and alerting.
- Incident post-mortems.
- Better control of production access.
- Stakeholder involvement in prioritisation.

I also helped teams outside Data adopt GitHub and version-controlled working.

A former colleague specifically highlighted that this contributed to the
organisation's **SOC compliance testing**.

The objective wasn't to announce a governance programme.

It was to make the organisation safer and more predictable by improving how
people actually worked.

## Governance in Practice: EFG

At EFG, the governance challenge was different.

The organisation already had substantial analytics capability, but years of
organic development had created duplicated models and business logic.

Metrics could exist in the warehouse and in LookML, and similar metrics could
be defined differently across multiple Explores.

As I built the Analytics Engineering function, governance therefore focused
heavily on **standardisation and ownership of analytical logic**.

I introduced stronger modelling conventions, coding standards, linting,
testing and documentation.

I also acted as product owner for the wider analytical model, working with
analysts and business stakeholders to establish definitions and document
business rules.

The Snowflake migration gave us an opportunity to reduce the number of facts
and dimensions, isolate transformation logic more deliberately and move
important definitions towards a governed analytical layer.

This contributed to a substantial reduction in duplicated logic and much more
consistent data.

## Governance in Practice: Apollo

My architectural review of Apollo found many of the governance problems that
appear when a company grows faster than its engineering processes.

There was no meaningful separation between development and production for
data work. Analysts changed views and stored procedures directly in live
databases. Version control, peer review, automated testing, CI/CD and formal
observability were largely absent.

There were also access-control concerns, including shared credentials and no
organised RBAC model.

My recommendations therefore treated governance and architecture as the same
modernisation problem.

The target platform introduced:

- Development and production separation.
- Git-based development.
- Pull-request workflows.
- CI/CD.
- Coding and naming standards.
- Data quality testing.
- RBAC.
- Client isolation.
- Monitoring and alerting.
- Documented Bronze, Silver and Gold responsibilities.
- A governed semantic layer.

As implementation progressed, I also created standards including SQL style
guides, RBAC definitions, environment strategies, lifecycle rules and
deployment processes.

## Governance for AI

Governance becomes even more important when data is consumed by AI systems.

A human analyst can recognise that two tables contain similar concepts,
discover an unusual join and ask someone what a badly named field means.

An AI agent may confidently make the wrong assumption.

For Apollo's conversational analytics work, I therefore treated the semantic
layer as a **governed query surface** for AI.

The knowledge supplied to the agent included explicit information about:

- Table grain.
- Preferred Gold reporting models.
- Valid join paths.
- Temporal relationships.
- Metric identifiers.
- Date and season semantics.
- Unit conversions.
- Null handling.
- Query-cost constraints.
- Current versus historical roster logic.

The objective was to reduce the amount of business meaning the model had to
infer.

This is how I increasingly think about governance for AI:

**Don't give an AI system unrestricted access to complicated data and hope it
understands the organisation. Give it a controlled, documented and tested
representation of the organisation's data and semantics.**

## Governance as Enablement

Ultimately, I judge governance by whether it allows an organisation to move
with greater confidence.

Poor governance creates two extremes.

At one end, there is chaos: duplicated definitions, uncontrolled production
changes, unreliable data and unclear ownership.

At the other is excessive control: committees, approval processes and
gatekeepers that make people avoid the governed platform altogether.

The useful position sits between them.

Create clear ownership of the things that need consistency. Automate controls
where possible. Protect production systems. Make changes observable and
reversible. Give people trusted foundations.

Then give them room to work.

## Questions this experience answers

- What is Martin's approach to data governance?
- What data governance experience does Martin have?
- How does Martin introduce governance into an immature organisation?
- How does Martin avoid governance becoming bureaucratic?
- How does Martin balance governance and self-service analytics?
- How does Martin govern business metrics?
- How does Martin approach metric ownership?
- How does Martin improve trust in data?
- How does Martin approach data quality?
- How does Martin use engineering practices as governance controls?
- How does Martin approach production access?
- What is Martin's approach to RBAC and least privilege?
- Has Martin worked with compliance requirements?
- Has Martin introduced Git and version control as governance controls?
- Has Martin introduced development and production environments?
- Has Martin implemented code review and CI/CD?
- Has Martin introduced data quality testing?
- How does Martin approach observability?
- How does Martin govern semantic layers?
- What does governance mean for an AI data agent?
- How does Martin prevent an AI agent from misinterpreting data?
- What governance changes did Martin introduce at Stonecrop?
- What governance changes did Martin introduce at EFG?
- What governance changes did Martin recommend and implement at Apollo?
