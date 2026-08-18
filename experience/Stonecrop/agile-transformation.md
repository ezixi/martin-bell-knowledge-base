---
type: project
title: Agile and Data Operations Transformation
company: Stonecrop Technologies
role: Senior Manager, Data
domain:
  - Data Operations
  - Data Engineering
  - Analytics
  - Operational Transformation

summary: >
  I inherited a data team that was manually performing business-critical
  operational processes that the company's core application was intended to
  automate. Thousands of outstanding requests, locally executed Excel macros
  and insufficient processing capacity had created a major operational backlog
  and put the company's relationship with its only customer at risk. I
  stabilised the operation, introduced measurable workflows and direct customer
  communication, automated manual processes, introduced Agile delivery, trained
  the existing team in SQL and Python, and subsequently rebuilt the function
  into a Data Operations team with an associated analytics capability.

skills:
  - Crisis Management
  - Data Operations
  - Data Engineering
  - Agile Transformation
  - Process Automation
  - Team Leadership
  - People Development
  - Stakeholder Management
  - Customer Management
  - Operational Analytics
  - SQL
  - Python
  - Bash
  - Jira
  - Zendesk
  - Scrum

key_contributions:
  - Quantified and made visible a business-critical operational backlog.
  - Introduced a structured escalation process between Customer Service and Data Operations.
  - Established direct communication and progress reporting with the customer.
  - Reverse engineered business logic implemented through hundreds of Excel macros.
  - Began replacing manual Excel processing with automated scripts.
  - Introduced SQL and Python to the existing team.
  - Created space for team members to learn while operating under significant pressure.
  - Introduced Jira, Scrum, sprints and demonstrations.
  - Recruited Scrum expertise from elsewhere in the organisation.
  - Reduced the operational backlog sufficiently to retire Zendesk as the team's work-management mechanism.
  - Restructured the function into a dedicated Data Operations team.
  - Hired Data Engineers to strengthen the technical capability of the function.
  - Established an associated insight capability around analysts outside my formal reporting line.

challenges:
  - The company's core application did not perform critical allocation processes as intended.
  - Business-critical processing depended on hundreds of Excel macros running on individual PCs.
  - The team could not process work as quickly as it arrived.
  - Employees were working extended hours and weekends without reducing the backlog.
  - Customer Service had thousands of outstanding requests and escalating SLAs.
  - The company's only customer was considering moving elsewhere.
  - The existing team had limited software and data engineering experience.
  - Introducing new processes required influencing senior leadership and other teams.

approach:
  - Measure the problem before attempting to solve it.
  - Stabilise communication and workflow first.
  - Give the customer visibility rather than hiding operational problems.
  - Understand existing business logic before replacing it.
  - Automate the highest-value manual processes.
  - Develop existing people rather than assuming the team needed replacing.
  - Introduce delivery structure through Scrum and visible prioritisation.
  - Reshape the team once the immediate crisis was under control.

outcomes:
  - Brought a severe operational backlog under control.
  - Reduced Zendesk escalations until the team no longer needed Zendesk for operational work.
  - Replaced significant manual processing with automated tooling.
  - Moved work management into structured Jira sprints.
  - Developed existing team members in SQL, Python and more technical ways of working.
  - Established a dedicated Data Operations capability.
  - Added Data Engineering capability to the team.
  - Established a more structured analytics capability alongside Data Operations.
  - Restored visibility and predictability for Customer Service and the customer.

related:
  - overview.md
  - ../philosophy/leadership.md
  - ../philosophy/engineering-practices.md
  - ../philosophy/analytics.md
---

# Agile and Data Operations Transformation

## Overview

When I joined Stonecrop Technologies, I thought I had been hired by the CTO to manage a relatively conventional data team.

Instead, I walked into an operational crisis that represented an existential risk to the company.

Stonecrop managed telecoms equipment and logistics for a major telecommunications provider. Its purpose was to make sure the equipment required to build or upgrade individual cell tower sites was correctly allocated, assembled and available when engineers needed it.

By the time I joined, Stonecrop was managing a warehouse containing transmission equipment worth tens of billions of dollars, alongside significant kitting and manufacturing operations.

The entire process depended on Stonecrop's proprietary application, Capstan.

There was one major problem:
**Capstan didn't perform some of the critical operational processes the business depended upon.**

The team I had been hired to manage wasn't really a reporting or analytics team.

It was effectively the manual processing engine keeping the company's core product running.

## The Problem

Capstan took site designs from the customer's engineers, converted them into Bills of Materials and passed those requirements into warehouse processes so equipment could be allocated and physically kitted for individual tower sites.

It was also supposed to prioritise work based on factors such as material availability and site priority.

Much of the business logic required to make this happen wasn't actually being executed successfully within the application.

Instead, three people in the "data team" were extracting data from Capstan, running hundreds of Excel macros locally on their PCs to perform material allocation, and uploading the resulting data back into Capstan so it could continue through the warehouse operation.

They had extremely powerful desktop machines because Excel processing capacity had effectively become part of the company's production infrastructure.

It still wasn't enough.

The team was processing work as quickly as it could, but incoming demand was greater than its ability to complete it.

They arrived first in the morning, left last at night and worked weekends.

The backlog continued to grow.

That backlog propagated through the rest of the organisation:
**data processing backlog → delayed allocation → delayed kitting/manufacturing → late equipment → delayed customer projects**

Customer Service was inundated with calls from site managers asking where their equipment was.

Zendesk KPIs and SLAs deteriorated and thousands of tickets accumulated.

Customer Service's main escalation mechanism was effectively:

> Email the data team.

Most seriously, Stonecrop's only customer was threatening to take its business elsewhere.

## Making the Problem Visible

My first priority was not to introduce a new technology.

It was to understand and quantify the problem.

I mapped the existing processes and introduced the data team as a formal escalation layer within Zendesk.

That gave us two things we hadn't previously had:
**Visibility for Customer Service.**

They could see that work had reached us and understand its progress rather than sending emails into an effectively invisible queue.
**Measurement for us.**

Zendesk gave me a way to quantify backlog size, incoming demand, resolution rates and progress.

Once the problem was measurable, I could start prioritising improvements and demonstrate whether the changes we made were actually working.

## Communicating Directly With the Customer

I also changed how we communicated with the customer.

Rather than allowing information about the operational problem to pass through multiple internal layers, I spoke directly to them.

I was clear about the scale of the problem, what I believed was causing it, what we were doing to fix it and how the backlog was changing.

They weren't happy about the situation.

But they now had visibility.

Regular progress updates were considerably better than allowing a critical customer to experience repeated failures without understanding whether anything was being done about them.

That transparency also created accountability for me and the team: I was telling the customer what we were going to improve and then showing them whether we had done it.

## Understanding the Existing Business Logic

The Excel macros were ugly from an engineering perspective, but they contained critical business knowledge.

I couldn't simply replace them without understanding what they did.

I therefore worked through the existing macros and processes to understand the allocation rules and operational logic they represented.

Once I understood those processes, I could start extracting them from the manual Excel environment and implementing them in more reliable forms.

My earliest replacements were simple Bash tools.

I then worked with a Rails developer to create scripts that could execute more of the business logic automatically.

The immediate objective wasn't architectural elegance.

It was throughput.

Every piece of work we could automate removed manual processing from a team that was already operating beyond its capacity.

## Developing the Existing Team

I inherited people who had been placed in an extremely difficult position.

They weren't software engineers, but they had developed complicated Excel processes because the organisation needed somebody to solve the problem.

They were smart, curious and had accumulated substantial knowledge about how the business actually worked.

Rather than replacing them because their existing tools were inappropriate, I wanted to increase what they were capable of doing.

I introduced them to SQL and Python and gave them opportunities to automate parts of their own work.

That involved accepting that they would make mistakes while learning.

Given the pressure they had been under, they were enthusiastic about anything that could remove repetitive manual work.

The objective wasn't simply to teach them programming languages. It was to move the team from:
**people executing processes**

towards:
**people improving and automating processes.**

## Introducing Agile Delivery

As the immediate situation became more manageable, I wanted a better mechanism for organising and prioritising the work.

After some disagreement with the CTO, I secured Jira licences for the team and introduced Scrum, sprints and demonstrations.

I also recruited an experienced Scrum Master internally who had become disenchanted with the product team.

She was instrumental in helping me establish a successful sprint process.

The structure gave us:

- A visible backlog.
- Explicit prioritisation.
- Clear ownership.
- Regular delivery cycles.
- Opportunities to demonstrate improvements.
- A mechanism for discussing and improving how we worked.

There were disagreements across the team as we changed established ways of working, but I was consistent about the direction.

The processes weren't the objective themselves.

They gave a team that had previously been overwhelmed by an uncontrolled stream of urgent work a way to regain control of its workload.

## From Firefighting to Improvement

Gradually, the situation changed.

Zendesk tickets fell.

The backlog became manageable.

Eventually we no longer needed Zendesk as the team's operational work queue at all.

We moved fully onto Jira and could increasingly spend our time building improvements to tools and processes rather than responding to escalations.

That represented an important change in the team's role.

We had moved from:
**trying to keep up with operational failures**

to:
**systematically improving the systems responsible for those operations.**

## Building the Data Operations Function

Once the immediate crisis was under control, I could start thinking about what the company actually needed from the function longer term.

I reshaped the team into a Data Operations capability responsible for managing the flow of data through the organisation.

I hired Data Engineers to strengthen the engineering side of the team and made changes where existing team members were not successful in the new structure.

There were also a couple of capable analysts elsewhere in the organisation who repeatedly came to my team for data and technical assistance.

They did not formally report to me, but their existing management structure wasn't giving them sufficient direction.

I began organising their work into the same sprint process and effectively provided the day-to-day leadership for their analytical work.

That created a useful operating model:
**Data Operations / Engineering → trusted operational data → Insights / Analysis**

It allowed the operational data capability we had built to begin supporting the wider reporting and analytical needs of the company.

## Leadership Under Pressure

One of the most important aspects of this project was that the technical problem couldn't be separated from the people problem.

The team I inherited was working extremely hard.

Telling them simply to work harder would have achieved nothing.

The problem was systemic.

They needed:

- Better visibility of incoming work.
- Clear priorities.
- Automation.
- Better tools.
- Technical development.
- Protection from uncontrolled escalation.
- A way to demonstrate progress.
- A believable route out of the situation.

At the same time, senior management and the customer needed evidence that the situation was improving.

My role was therefore a combination of technical problem solving, process design, people development, stakeholder management and customer communication.

## What I Learned

This experience reinforced my belief that before trying to solve a large operational problem, I need to make it visible and measurable.

When I arrived, everybody knew things were bad, but there was no shared mechanism for understanding the size of the problem or whether it was improving.

Establishing that visibility changed the conversation.

It also reinforced the importance of understanding why apparently bad technical decisions exist.

Hundreds of Excel macros running on desktop PCs were clearly not an appropriate production architecture.

But the people who created them weren't the problem.

They had created solutions to business problems that the company's application had failed to solve.

Those macros contained valuable operational knowledge that needed to be understood before it could be automated.

Finally, it demonstrated the importance of developing people during transformation.

Some of the strongest assets I inherited were the people who understood those processes. Giving them better tools and the opportunity to learn was far more valuable than treating the existing team as part of the legacy system that needed replacing.

## Questions this experience answers

- What did Martin do at Stonecrop Technologies?
- Has Martin led a business-critical transformation?
- How does Martin operate during a crisis?
- Has Martin inherited a team that was struggling?
- How does Martin turn around an underperforming operation?
- Has Martin dealt directly with a major customer during a crisis?
- How does Martin communicate bad news to customers?
- How does Martin approach customer trust when things have gone wrong?
- Has Martin worked in a start-up or operationally immature environment?
- How does Martin prioritise when everything appears urgent?
- How does Martin approach process improvement?
- Has Martin automated manual business processes?
- How does Martin approach legacy Excel processes?
- Does Martin have experience with operational data systems?
- Has Martin introduced Agile or Scrum into a team?
- How does Martin approach Agile transformation?
- Has Martin introduced Jira into an organisation?
- How does Martin deal with resistance to organisational change?
- How does Martin influence senior leadership?
- How does Martin develop non-technical or less technical team members?
- Has Martin trained people in SQL and Python?
- How does Martin balance delivery pressure with developing people?
- Has Martin built or restructured a data team?
- Has Martin hired Data Engineers?
- Has Martin managed people outside his formal reporting line?
- How does Martin influence without authority?
- Has Martin created a Data Operations function?
- How hands-on is Martin when solving operational problems?
- Can Martin combine technical leadership with people leadership?
