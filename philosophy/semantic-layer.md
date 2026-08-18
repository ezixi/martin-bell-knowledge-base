---
type: philosophy
title: "Semantic Layers"

domain:
  - Semantic Layers
  - Data Architecture
  - Data Modelling
  - Analytics Engineering
  - Metric Governance
  - Data Governance
  - Business Intelligence
  - AI
  - Conversational Analytics

summary: >
  I see a semantic layer as the contract through which an organisation turns
  data into agreed business meaning. It should provide consumers with a
  consistent representation of business entities, processes, metrics,
  dimensions and relationships without requiring them to understand the
  complexity of the underlying source systems. My approach starts with business
  concepts rather than tables, progressively moves data from source-conformed
  to business-conformed structures, centralises reusable logic, and makes
  semantics explicit through metadata and governance. I developed this approach
  while rebuilding the analytical model at EFG and have subsequently extended
  it to consider AI agents as first-class consumers of semantic information.

principles:
  - "A semantic layer represents business meaning, not just database structure"
  - "Start with business concepts and processes, not source tables"
  - "Define business meaning before implementing metrics"
  - "Every analytical model should have an explicit grain"
  - "Shared business logic should be defined once"
  - "Business definitions and technical implementations should be distinguishable"
  - "Metadata is part of the product, not documentation added afterwards"
  - "Semantic models should make downstream consumption simpler"
  - "Metrics require ownership, governance and a lifecycle"
  - "Semantic definitions should be understandable by humans and machines"
  - "AI should consume governed semantic interfaces rather than infer meaning from raw data"

skills:
  - Semantic Layer Design
  - Dimensional Modelling
  - Conceptual Data Modelling
  - Logical Data Modelling
  - Metric Governance
  - Data Governance
  - Analytics Engineering
  - Data Product Design
  - Metadata Design
  - AI Grounding
  - Stakeholder Management

technologies:
  - dbt
  - Snowflake
  - BigQuery
  - Looker
  - LookML
  - Tableau
  - Azure Synapse

questions:
  - "What is Martin's approach to semantic layers?"
  - "Has Martin designed a semantic layer?"
  - "What semantic layer experience does Martin have?"
  - "How does Martin define business metrics?"
  - "How does Martin create a single source of truth?"
  - "How does Martin approach metric governance?"
  - "How does Martin approach dimensional modelling?"
  - "What does Martin mean by business-conformed data?"
  - "How does Martin move business logic out of BI tools?"
  - "How does Martin approach data modelling for AI?"
  - "How should a semantic layer support an AI agent?"
  - "What semantic modelling work did Martin do at EFG?"
  - "How did Martin improve metric consistency at EFG?"
  - "How does Martin test semantic definitions?"
  - "How does Martin balance self-service analytics with governed metrics?"
---

# Semantic Layers

## My Approach

I see a semantic layer as the **contract through which an organisation turns
data into agreed business meaning**.

Source systems tell us how applications store data.

They don't necessarily tell us what the business means by a customer,
subscriber, active user, match, injury, revenue, retention or any of the other
concepts people actually use when making decisions.

Creating those definitions is the difficult part.

A semantic layer should allow consumers to work with those business concepts
without requiring them to understand all of the complexity underneath them.

Those consumers might be:

- Analysts.
- BI tools.
- Product teams.
- Applications.
- APIs.
- Data scientists.
- AI agents.

The technology used to expose those semantics can change.

The need for agreed business meaning does not.

## A Single Source of Truth Is Not a Database Problem

I learned this particularly clearly at EFG.

The organisation wanted a single source of truth, but the underlying data
landscape made that extremely difficult.

EFG had a highly distributed microservice architecture. Many services
represented overlapping versions of the same business concepts.

The canonical source for a user might be the Users service, but understanding
that user could require data from other services. Authentication data could
tell us when they last logged in, while a Verification service might determine
whether they had been verified.

Gameplay was even more fragmented.

Services including Matches, Games and Leaderboards contained overlapping and
sometimes conflicting representations of how users played.

The problem wasn't simply that there were many tables.

There were many **interpretations of reality**.

Product teams were also highly independent. Subscriptions, Growth, Customer
Safety, Advertising and other teams developed their own services and data
without necessarily understanding what neighbouring teams were doing.

The analytical platform inherited all of that ambiguity.

## Analytics Had Added Another Semantic Layer — Accidentally

When I joined EFG, analysts were primarily working with BigQuery and Looker.

The analysts were relatively junior and were working very reactively.

For a new request, the normal response was often to create another BigQuery
table and expose it through another piece of LookML.

Some calculations lived in BigQuery.

Others lived in LookML because they needed to support a hierarchy, dashboard
filter or some other reporting requirement.

Similar concepts could therefore be implemented several times across different
tables and Looker Explores.

Instead of resolving the ambiguity of the source systems, the analytical
platform was creating another layer of it.

## Event Data Had the Same Problem

Client-side behavioural data arrived through a separate events pipeline into
BigQuery.

That data had significant quality problems, including duplicate events and
events with future timestamps.

There was also little governance over event creation.

Product managers and developers could introduce events independently, and some
events accumulated thousands of attributes.

I initially tried introducing an event-definition approval process.

That exposed another problem.

If Data had to approve every event before Product could ship it, I became a
bottleneck. Governance was perceived as the Data team slowing down product
development.

That wasn't sustainable.

It helped shape an important part of my later approach to governance:

**the correct way of working needs to be built into the system and normal
development process wherever possible.**

Governance that depends on one person approving everything does not scale.

## Trying to Define the Truth

I also tried to address metric consistency directly.

I created a spreadsheet containing important metrics, their definitions and
business uses.

My intention was to make it collaborative: analysts and business stakeholders
could agree definitions and the spreadsheet could become the canonical
reference for important metrics.

That approach also ran into resistance.

When I tried to get senior Product leadership involved, the response was
essentially that Product wasn't going to write a huge document describing every
metric.

The spreadsheet wasn't the answer, but it helped expose the actual problem.

The organisation first needed to agree what its concepts meant.

## The 90-Minute Subscriber Count

One meeting made that particularly clear.

Using the metric catalogue as a starting point, I brought together the Product
Manager responsible for subscriptions and the Head of Monetisation.

We had around ten subscription metrics to define.

I deliberately started with what I thought would be the simplest possible
metric:
**How many subscribers do we have?**

My initial suggestion was essentially a point-in-time count of unique user IDs
whose subscription was currently flagged as active.

Ninety minutes later, the stakeholders were still debating what a subscriber
actually meant.

I had to leave the meeting before they had resolved it.

That experience changed how I thought about a "single source of truth".

You cannot create one merely by creating a single table, dashboard, catalogue
or metrics store.
**First, people have to agree what the truth means.**

Even apparently simple measures can encode assumptions about state, time,
eligibility and intended business use.

Resolving those assumptions is usually harder than writing the SQL.

## Moving From Source-Conformed to Business-Conformed Data

The migration from BigQuery to Snowflake gave me an opportunity to address the
problem more fundamentally.

Rather than reproducing the existing warehouse on a different technology, I
introduced a much stricter modelling approach.

I described the objective to the Analytics Engineering team as creating:
**a cohesive arc moving data from source-conformed to business-conformed.**

The basic progression was:
**Sources → Staging → Curated dimensional model → Business-facing marts → BI**

Each layer had a different responsibility.

### Source and staging

At the beginning of the pipeline, data still largely represented the systems
that created it.

Staging models cleaned and standardised that data while retaining the basic
meaning and grain of the source.

I wanted transformations at this level to remain predictable and relatively
simple.

Business meaning should not be scattered through hundreds of staging models.

### Business concepts

The curated layer was where we began deliberately modelling the business.

I taught the team to start by talking to users about the concepts and processes
they worked with rather than immediately looking at source tables.

Questions included:

- What is a user?
- What attributes describe one?
- What business processes are they part of?
- What is the grain of those processes?
- Which dimensions are needed to understand them?
- Which metrics describe them?

From those conversations we could create conceptual models and then translate
them into logical and physical analytical models.

## Facts, Dimensions and Grain

I used dimensional modelling because it gave us a relatively simple way of
representing the organisation.

Dimensions represented business entities and their attributes.

Facts represented business processes — effectively what those entities did.

Most importantly, every model needed an explicit **grain**.

Grain is fundamental to semantic modelling because a metric has little meaning
without understanding what one row represents.

A count, sum or average can produce perfectly valid SQL while answering the
wrong business question if the underlying grain is misunderstood.

Being explicit about grain made relationships and aggregation behaviour much
easier to reason about.

## Define Business Logic Once

Another core rule was:
**Define metrics, attributes and other reusable business logic once.**

If the same calculation appeared repeatedly, it should normally be abstracted
into an appropriate dbt model rather than copied into multiple downstream
models.

Intermediate models were particularly useful for isolating reusable pieces of
business logic that did not themselves represent final business entities.

The objective was not simply reducing lines of SQL.

Every duplicate implementation of business logic creates another opportunity
for the definitions to diverge.

Centralisation therefore became a governance mechanism.

This approach contributed to a substantial reduction in duplicated analytical
logic across the platform.

## Business-Facing Data Marts

Because we moved from Looker to Tableau, we no longer had LookML available as
the obvious semantic interface.

We solved the immediate consumption problem through domain-oriented data marts.

For important business processes, we created wide, denormalised reporting
models containing the measures and attributes users needed for analysis.

These were deliberately designed around **business terminology and business
questions**, rather than the structures of source applications.

When designing them, I wanted the team to ask:

- What question is the user trying to answer?
- Which metrics do they need?
- How should those metrics aggregate?
- Which dimensions will they use to segment them?
- What terminology does the business use?
- What downstream dashboards or analyses depend on this model?

The ideal consumption model should be relatively boring.

The hard work of understanding source systems, resolving relationships,
applying business logic and determining grain should already have happened
upstream.

Tableau should consume trusted business data rather than reconstruct the
organisation's semantics independently in every workbook.

## What We Had — and What We Didn't

I would not describe the EFG implementation as a complete formal semantic or
metrics layer in the way I would design one today.

We had built many of the foundations:

- Business-conformed dimensional models.
- Explicit facts and dimensions.
- Defined grains.
- Centralised reusable business logic.
- Domain-oriented marts.
- Testing.
- Documentation.
- Metadata.
- Lineage.
- Controlled engineering processes.

But we had not created a separate machine-readable metrics layer containing
every governed metric and its semantic definition.

Individual metric calculations were generally implemented as reusable
intermediate dbt models and exposed through the appropriate business-facing
models.

In retrospect, I would have taken the architecture one step further.

I would have explicitly represented metrics and their metadata in something
such as YAML or a dedicated semantic framework rather than relying entirely on
the physical dbt models and their documentation.

The architecture solved much of the immediate human consumption problem.

AI subsequently made the missing piece much more obvious.

## Metadata Is as Important as Data

One of the principles I taught the Analytics Engineering team was:
**metadata is as important as data.**

A table containing accurate numbers isn't sufficient if nobody knows what it
means, where it came from or how it should be used.

I expected models and columns to be documented in YAML and wanted lineage to
be understandable from source through facts and dimensions, into marts and
ultimately into dashboards.

Metadata served two purposes.

For engineers, it made systems easier to understand, maintain and change.

For consumers, it made data easier to discover and interpret.

That becomes even more important when the consumer is an AI system.

## AI Exposed the Missing Semantic Contract

Towards the end of my time at EFG, we began working with a conversational AI
vendor.

Our dimensional model gave them a much stronger foundation than the original
warehouse would have done.

Entities, business processes, relationships and reusable logic had already been
made substantially more explicit.

But the vendor still needed to create a semantic representation on top of that
model.

This exposed an important distinction.

A dimensional model describes the analytical structure of the organisation.

A semantic layer goes further by explicitly telling a consumer **what those
things mean and how they should be used**.

We worked with the vendor to define that model and had begun creating
**golden queries** to test whether natural-language questions produced the
correct analytical answers.

The project had reached the implementation and testing stage when the wider
Data team was made redundant, so I don't claim a production outcome from that
work.

It did, however, significantly influence how I subsequently thought about
semantic layers for AI.

## A Semantic Layer Is More Than a Metrics Store

My thinking has continued to develop since EFG.

I don't see a semantic layer as simply a dictionary containing:

`metric_name → SQL expression`

Metrics need context.

A useful semantic model can include:

- Business entities.
- Business processes.
- Metrics.
- Dimensions.
- Grain.
- Relationships.
- Hierarchies.
- Business filters.
- Ownership.
- Definitions.
- Source lineage.
- Valid aggregation behaviour.
- Usage constraints.

A metric such as `subscriber_count` is not useful merely because its SQL has
been centralised.

A consumer also needs to understand what a subscriber means, at what point in
time the metric applies, which dimensions can safely segment it, which
population is included and who owns the definition.

## Metric Governance

I now think of important metrics as managed data products with a lifecycle.

A typical process is:
**Draft → Business review → Design → Approval → Implementation → Testing →
Publication → Monitoring → Deprecation**

The exact process should be proportionate to the organisation, but several
principles matter.

### One clear owner

An important metric needs somebody accountable for its business meaning.

Analytics can facilitate definition and implement it, but Analytics should not
quietly decide what a business concept means when legitimate business
stakeholders disagree.

### Define before implementing

The business definition should exist before the SQL.

This separates questions such as:

> "What counts as a subscriber?"

from:

> "Which tables and conditions calculate subscriber count?"

Those are related questions, but they are not the same question.

### Treat genuinely different meanings as different metrics

If two teams legitimately need different versions of a measure because they
answer different business questions, forcing them into one definition does not
create a single source of truth.

It creates ambiguity.

The differences should instead be made explicit through separate, clearly
defined metrics.

### Version and test them

Important semantic definitions should be treated like other production
artefacts.

Changes should be controlled, tested and observable.

Consumers should be able to understand what changed and why.

## Semantic Layers and Self-Service

Governance and self-service are not opposites.

A good semantic layer should increase the amount of self-service an
organisation can safely support.

I want analysts and business users to be able to:

- Explore data.
- Combine metrics and dimensions.
- Create new analyses.
- Build visualisations.
- Ask questions we didn't anticipate.

What I don't want is every consumer independently deciding what core concepts
such as Revenue, Subscriber or Active User mean.

The semantic layer establishes the shared language.

People remain free to use that language creatively.

## Semantic Layers for AI

AI makes explicit semantics considerably more important.

An experienced analyst encountering an unfamiliar model can investigate it,
read SQL, inspect data and ask colleagues what unusual fields mean.

An AI agent can make a plausible assumption and confidently return the wrong
answer.

I therefore increasingly think of the semantic layer as an **approved query
surface for AI**.

Rather than exposing a complicated warehouse and expecting an LLM to infer the
organisation, I want to explicitly provide the information required to reason
about it.

In my later Apollo work, that included defining:

- Preferred reporting models.
- Table grain.
- Authoritative join paths.
- Temporal relationships.
- Business terminology.
- Metric identifiers.
- Season and calendar semantics.
- Current versus historical population rules.
- Unit conversions.
- Null behaviour.
- Query-cost guardrails.

For example, athlete squad membership changes over time.

Simply joining an athlete to a squad identifier can produce duplicated or
historically incorrect results.

The semantic information supplied to the AI therefore needs to explain the
temporal relationship and the correct bounded join.

Likewise, terms such as "two days before a game" have specific business
semantics that should map to an approved field rather than asking the model to
invent date logic.

The objective is straightforward:
**reduce the amount of business meaning the model has to infer.**

## Testing AI Semantics

Semantic testing also needs to go beyond traditional data-quality tests when
AI is involved.

The underlying model still needs normal engineering tests for things such as:

- Uniqueness.
- Referential integrity.
- Null behaviour.
- Accepted values.
- Freshness.
- Business rules.

But an AI-facing semantic layer also needs to test whether the consumer
interprets those semantics correctly.

Golden queries are useful for this.

For a known business question, I want a known correct answer or query pattern.

We can then evaluate whether changes to prompts, metadata, models or the
semantic layer alter the result.

That turns "the AI seems to understand our data" into something we can begin
to measure.

## How My Thinking Has Evolved

My approach to semantic layers has developed through several stages.

At EFG, I initially tried to solve semantic inconsistency through **process and
documentation**.

That taught me that governance based on manual approval can become a
bottleneck, and documentation alone cannot make stakeholders agree.

During the Snowflake migration, I moved much more of that governance into the
**architecture**: explicit business entities, dimensional models, defined
grain, reusable logic, testing, metadata and business-facing marts.

The conversational AI project exposed the need for a more explicit
**machine-readable semantic contract** above that analytical foundation.

In later architectural work, I have treated AI as a first-class consumer when
thinking about semantic design, governance and testing.

The technology has changed.

The underlying problem has remained remarkably consistent:

**How do we take fragmented technical representations of reality and turn them
into business concepts that everybody — human or machine — can understand and
use consistently?**

That is what I believe a semantic layer is for.

## Questions this experience answers

- What is Martin's approach to semantic layers?
- What does Martin mean by a semantic layer?
- Has Martin designed semantic architectures?
- Has Martin implemented the foundations of a semantic layer?
- What semantic-layer work did Martin do at EFG?
- How did Martin improve metric consistency at EFG?
- How did Martin move business logic out of Looker?
- What was wrong with the original BigQuery and Looker architecture at EFG?
- How did Martin approach the BigQuery to Snowflake migration?
- How does Martin approach dimensional modelling?
- How does Martin identify business entities and processes?
- Why does Martin consider grain important?
- How does Martin approach reusable business logic?
- How does Martin design business-facing data marts?
- What does Martin mean by source-conformed and business-conformed data?
- How does Martin create a single source of truth?
- Why does Martin believe a single source of truth is a governance problem?
- What is an example of stakeholders disagreeing over a metric definition?
- How does Martin define metrics?
- How does Martin govern metrics?
- Who should own business metric definitions?
- How does Martin handle teams that legitimately use different versions of a metric?
- How does Martin balance semantic governance with self-service analytics?
- How does Martin approach metadata and lineage?
- Why does Martin believe metadata is as important as data?
- Has Martin worked with LookML?
- Has Martin used dbt to centralise business logic?
- What would Martin change about the semantic architecture he built at EFG?
- Has Martin worked with conversational analytics?
- How has Martin designed data for AI consumption?
- What is an approved query surface for AI?
- How does Martin prevent an AI agent from misunderstanding business data?
- What are golden queries?
- How does Martin test an AI semantic layer?
- What semantic-layer work did Martin do at Apollo?
- How has Martin's approach to semantic layers evolved?
