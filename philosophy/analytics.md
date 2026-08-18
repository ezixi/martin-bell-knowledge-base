---
type: philosophy
title: Analytics
scope: career-wide

summary: >
  I see analytics as a decision-making capability rather than a reporting
  function. The purpose of analytics is to help people understand what is
  happening, why it is happening, what they should do about it, and whether
  their actions worked. My approach emphasises business context, clearly
  defined metrics, actionable insight, appropriate self-service, experimentation
  and close relationships between analysts and the people making decisions.

subjects:
  - Analytics
  - Business Intelligence
  - Decision Making
  - Data Analysis
  - Product Analytics
  - Marketing Analytics
  - Self-Service Analytics
  - Metrics
  - KPI Design
  - Experimentation
  - Data Literacy
  - Stakeholder Management

principles:
  - Start with the decision, not the dashboard.
  - Analytics should lead to action.
  - Understand the business before analysing the data.
  - Define metrics around outcomes and behaviours.
  - Explain why something happened, not only what happened.
  - Build reusable capabilities instead of repeatedly answering the same questions.
  - Enable appropriate self-service.
  - Make analysis understandable to the people who need to act on it.
  - Measure whether interventions actually worked.
  - Challenge the question when necessary.

related:
  - data-strategy.md
  - leadership.md
  - engineering-practices.md
  - ../stories/data-literacy.md
---

# Analytics

## Overview

I believe the purpose of analytics is to help people make better decisions, and take action.

Dashboards, reports, models and analyses are ways of achieving that. They are not the outcome themselves.

The questions I ultimately want analytics to help answer are:

1. What is happening?
2. Why is it happening?
3. What should we do about it?
4. Did what we did actually work?

An analytics function that produces large numbers of dashboards and reports but rarely changes decisions or behaviour may be productive in terms of output, but it is not necessarily effective.

My preference is therefore to start with the decision or problem and work backwards to the data and analytical capability required to support it.

## Start With the Decision

When somebody asks for a dashboard, metric or analysis, I want to understand what they are going to do with it.

Questions I commonly want answered include:

- What are you trying to understand?
- What decision are you trying to make?
- What action would you do differently depending on the answer?
- How frequently does that decision need to be made?
- Who needs the information?
- How quickly do they need it?
- What level of detail is useful?
- How will we know whether the resulting action worked?

Sometimes the answer genuinely is a dashboard.

Sometimes it is an alert, a dataset, an experiment, a one-off analysis, a metric added to an existing report, or simply an answer to a question.

Starting with the decision helps avoid building analytical products simply because somebody requested a particular implementation.

## Understand the Business

I think strong analysts need to understand the business they are analysing.

Technical analytical ability is important, but without context it is easy to produce technically correct analysis that is commercially irrelevant or misleading.

I want analysts to understand things such as:

- How the organisation makes money.
- How customers use its products.
- What different teams are trying to achieve.
- Which behaviours drive important outcomes.
- How the organisation measures success.
- What constraints decision-makers operate under.

That knowledge changes the relationship between an analyst and a stakeholder.

Instead of simply receiving a question and returning an answer, the analyst can challenge assumptions, suggest better questions and identify things the stakeholder may not have considered.

I don't see analysts as human query interfaces.

Their judgement is part of the value they provide.

## Ask the Right Question

The question initially asked is not always the question that needs answering.

For example, someone might ask:

> "Can you show me which marketing channel has the highest conversion rate?"

But perhaps the real question is:

> "Where should we invest our next £100,000 of acquisition budget?"

Those questions are related, but they are not equivalent.

Conversion rate alone may ignore acquisition cost, customer value, incrementality, volume, retention or the ability to scale a channel.

Part of good analytics is identifying the underlying decision and making sure the analysis actually supports it.

That sometimes means pushing back on the original request.

## From Reporting to Insight to Action

Reporting is useful. Organisations need reliable ways of understanding what has happened.

But analytics should be capable of moving beyond reporting.

I think of this as a progression:

### What happened?

Reporting and descriptive analytics.

### Why did it happen?

Investigation, segmentation, comparison and diagnosis.

### What action should we take?

Recommendations based on evidence and business context.

### Did it work?

Measurement, experimentation and iteration.

Not every analytical question needs to travel through every stage, but an analytics function should be capable of doing more than describing the past.

## Metrics Should Have a Purpose

A metric should represent something the organisation cares about.

I want to understand:

- What does the metric measure?
- Why does it matter?
- Who owns it?
- What behaviour influences it?
- What action should somebody take when it changes?
- What other metrics provide necessary context?
- Can people unintentionally optimise it at the expense of the real objective?

A KPI is particularly useful when people can influence it.

Showing somebody a number they cannot affect may provide information, but it does not necessarily help them perform their job better.

Metrics should help connect individual and team activity to organisational outcomes.

## Shared Definitions Matter

Analytics becomes much harder when different parts of an organisation use different definitions for the same concept.

If Product, Marketing and Finance all mean something different by "active customer", discussions quickly become arguments about numbers rather than decisions about the business.

Important metrics therefore need clear definitions and ownership.

Those definitions should be represented consistently in the data platform rather than independently recreated in dashboards, spreadsheets and individual SQL queries.

This is one reason I see dimensional modelling, metric governance and semantic layers as analytical capabilities rather than purely technical concerns.

They allow the organisation to have a shared language.

## Analysis Should Be Actionable

An insight is most useful when somebody can do something with it.

I want analytical work to make the implication clear:

**We observed X.**
**The evidence suggests Y is contributing to it.**
**Therefore we recommend Z.**

That does not mean pretending the data provides certainty where it does not.

Analysts should communicate assumptions, limitations and uncertainty.

But simply presenting information and expecting the audience to determine its significance leaves much of the analytical work unfinished.

The analyst should help connect evidence to action.

## Communicate for the Audience

Good analysis that nobody understands has limited value.

The appropriate presentation depends on the audience.

An analyst may need detailed statistical evidence and methodology.

An operational team may need a simple list of customers requiring attention.

An executive may need three numbers, the reason they changed and the decision that needs to be made.

I don't believe simplifying an analysis for a non-technical audience means making it less rigorous.

The complexity can remain behind the result.

Part of the analyst's job is translating that complexity into something the audience can use.

## Self-Service Analytics

I support self-service analytics, but I don't define self-service as giving everyone access to a BI tool and expecting them to become analysts.

Different users need different levels of analytical capability.

Some people may need:

- Governed dashboards.
- Clearly defined KPIs.
- Alerts.
- Curated datasets.
- Spreadsheet access.
- Exploratory BI.
- SQL access.
- Direct warehouse access.

The objective is to give people the **appropriate level of access and capability for the decisions they need to make**.

For self-service to work, people also need trusted data, understandable models, consistent metrics, documentation and sufficient data literacy.

Without those foundations, self-service can simply allow inconsistent analysis to spread more quickly.

## Build Capabilities, Not Dependencies

A central analytics team should not aim to answer every data question in an organisation forever.

If the same question is repeatedly being asked, I want to understand whether we can turn the answer into a reusable capability.

That might mean:

- Defining a metric.
- Adding a field to a model.
- Creating a reusable dataset.
- Improving a dashboard.
- Providing an alert.
- Documenting a concept.
- Training users.
- Improving an existing self-service tool.

The analytics team can then spend less time repeatedly answering predictable questions and more time working on new, higher-value problems.

A successful analytics function should gradually make the organisation more capable of using data without creating unnecessary dependence on analysts.

## Data Literacy

Self-service and analytics depend on people understanding the information they are using.

I don't expect everyone in an organisation to become a data specialist.

I do think people should understand the metrics relevant to their work and enough basic analytical concepts to interpret them responsibly.

That includes understanding things such as:

- What a metric actually measures.
- Difference between totals, averages and percentages.
- Trends and variability.
- Correlation versus causation.
- Sample size.
- How filters and segmentation affect conclusions.
- When a result may require further investigation.

I see data literacy as part of building a shared organisational language around performance.

## Experimentation

Where possible, I want analytics to close the loop between observation and action.

A useful pattern is:
**Measure → understand → intervene → measure again**

Sometimes this can be done through a formal A/B or multivariate experiment.

Sometimes the business environment does not allow a clean controlled experiment and the analysis needs to use observational evidence instead.

The important principle is that decisions should create opportunities to learn.

If analytics recommends changing something, we should think about how we will determine whether the change produced the intended outcome.

Otherwise organisations can accumulate large numbers of initiatives without knowing which ones actually worked.

## Analytics and Causality

One of the dangers in analytics is confusing relationships in data with explanations.

Two things moving together does not necessarily mean one caused the other.

I want analysts to be careful about the strength of the claims they make.

Depending on the problem, establishing causality might require:

- Controlled experiments.
- Appropriate control groups.
- Cohort analysis.
- Pre/post comparisons.
- Statistical modelling.
- Additional qualitative evidence.

Sometimes the available data cannot establish causality.

In those situations, saying **"the evidence suggests"** is better than manufacturing certainty.

Good analytics should reduce uncertainty, not hide it.

## Prioritising Analytics Work

Not every analytical request has equal value.

When prioritising work, I consider factors such as:

- Business impact.
- Number of people affected.
- Frequency of the decision.
- Urgency.
- Cost of making the wrong decision.
- Effort required.
- Reusability.
- Strategic importance.

A complicated analysis requested by one person once may be less valuable than a small improvement to a metric used by hundreds of people every day.

This is another reason I prefer thinking in terms of outcomes rather than analytical output.

## Analysts and Stakeholders

I prefer analysts to work closely with the people they support.

The relationship should not be:
**stakeholder → ticket → analyst → output**

I want analysts involved early enough to understand the problem, contribute their expertise and influence the approach.

That also means analysts need to build trust.

They should be comfortable saying:

- "I don't think the data supports that conclusion."
- "I think we should measure this differently."
- "There is a better way to answer that question."
- "We don't currently have enough evidence to know."
- "I don't think building this dashboard will solve the problem."

Constructive challenge is part of the job.

## Analytics and AI

AI changes how people may interact with analytics, but I don't think it changes the underlying principles.

A conversational analytics agent may allow somebody to ask a question in natural language instead of navigating a dashboard or writing SQL.

But the system still needs:

- Reliable data.
- Clearly defined metrics.
- Business context.
- Semantic consistency.
- Appropriate access controls.
- Guardrails.
- Ways of communicating uncertainty.

If those foundations do not exist, an AI interface can make incorrect or inconsistent analytics easier to produce.

I therefore see AI as another consumption mechanism built on top of good analytical foundations rather than a replacement for them.

## Measuring an Analytics Function

I don't think the success of an analytics team should primarily be measured by the number of dashboards, reports, tickets or analyses it produces.

Those are measures of activity.

I am more interested in outcomes such as:

- Are people making decisions faster?
- Do they trust the data?
- Are important metrics consistently understood?
- Has repeated manual analysis decreased?
- Can users answer appropriate questions themselves?
- Are analyses changing decisions?
- Can we demonstrate that interventions improved outcomes?
- Is the organisation becoming more capable of using data?

The purpose of an analytics team is not to produce analytics.
**It is to help the organisation perform better through the use of data.**

## My Analytics Principles

### Decisions before dashboards

Start with what somebody needs to decide, not what they have asked us to build.

### Business understanding before analysis

Context is necessary to interpret data properly and ask better questions.

### Questions before queries

Make sure we are answering the problem behind the request.

### Insight before output

Producing something is not the same as creating value.

### Action before information overload

Show people what matters and help them understand what to do about it.

### Shared meaning before self-service

People cannot independently use data effectively if the organisation has not agreed what the data means.

### Enablement before dependency

Build reusable analytical capabilities rather than making the analytics team the permanent gateway to information.

### Evidence before certainty

Be clear about what the data supports and what remains uncertain.

### Measurement before assumption

When we change something, determine whether it actually worked.

### Outcomes before activity

Judge analytics by the decisions and improvements it enables, not the volume of analytical output.

## Questions this experience answers

- What is Martin's philosophy on analytics?
- What does Martin believe the purpose of an analytics team is?
- How does Martin approach an analytics problem?
- How does Martin work with stakeholders?
- How does Martin challenge stakeholder requests?
- How does Martin decide whether to build a dashboard?
- What is Martin's approach to KPI and metric design?
- How does Martin approach metric governance?
- How does Martin think about self-service analytics?
- What is Martin's approach to data literacy?
- How does Martin make analytics actionable?
- How does Martin communicate analysis to non-technical audiences?
- How does Martin approach experimentation and A/B testing?
- How does Martin think about correlation and causation?
- How does Martin prioritise analytics work?
- How does Martin measure the effectiveness of an analytics function?
- What does Martin think makes a good analyst?
- How does Martin think AI will affect analytics?
