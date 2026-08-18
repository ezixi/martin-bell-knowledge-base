---
type: project
title: "SEO and Organic Acquisition"
company: "Safari Books Online"
role: "Web Analytics Manager"

domain:
  - Web Analytics
  - SEO
  - Customer Acquisition
  - Product Analytics

summary: >
  I identified organic search as a major unrealised acquisition opportunity
  at Safari Books Online. Despite having a large catalogue of authoritative
  technical content, Safari received almost no organic search traffic because
  of architectural, accessibility and SEO problems. I diagnosed the issues,
  presented recommendations to senior leadership and implemented many of the
  technical changes myself. Organic search subsequently grew from almost zero
  to Safari's largest traffic source, attracting millions of users per month.

skills:
  - Web Analytics
  - SEO
  - Customer Acquisition
  - Technical SEO
  - Product Analytics
  - Data Analysis
  - Stakeholder Management
  - Technical Implementation

technologies:
  - Adobe Omniture
  - Google Search Tools
  - HTML
  - JavaScript
  - XML
  - cURL
  - SVN
  - Excel

outcomes:
  - "Organic search grew from almost zero to the number one source of traffic"
  - "Organic search attracted millions of users per month"
  - "Established organic search as a major customer acquisition channel"

questions:
  - "Does Martin have SEO experience?"
  - "Does Martin have web analytics experience?"
  - "Does Martin have customer acquisition experience?"
  - "Has Martin identified a major commercial opportunity through data?"
  - "Has Martin worked on products with millions of users?"
  - "How does Martin use data to influence product decisions?"
  - "How hands-on is Martin technically?"

related:
    - overview.md
    - conversion-optimisation.md
    - content-analytics-product-strategy.md
    - ../../philosophy/analytics.md
    - ../../philosophy/data-strategy.md

---

# SEO and Organic Acquisition

## Overview

I joined Safari Books Online in 2010 as Web Analytics Manager.

Safari was a joint venture between O'Reilly Media and Pearson, bringing their technical and educational publishing catalogues online through a subscription product.

I had been hired primarily to manage Safari's Adobe Omniture implementation and use it to provide insight into customer acquisition, behaviour and product usage.

While analysing acquisition performance, I noticed something that didn't make sense.

Safari had an enormous amount of authoritative technical content from publishers with strong reputations, particularly within the developer community.

Yet organic search traffic was almost nonexistent.

At a time when search was one of the dominant mechanisms for discovering information on the web, I believed organic search should have been one of Safari's strongest acquisition channels.

I investigated why it wasn't.

## The Existing Product

Safari was an early attempt to translate a business based around physical technical books into a web product.

The technology reflected that history.

Print publications were converted from PDFs into XML and then transformed into HTML for display on the web.

The resulting pages were complicated and relied heavily on JavaScript.

They contained large amounts of code relative to actual content.

There was also significant concern within the publishing industry about piracy, which had influenced how Safari exposed its content.

Much of the implementation was deliberately obfuscated and almost all meaningful book content was behind a paywall.

Anonymous users typically received only a small amount of content from each page, with some of that content injected through JavaScript.

From the perspective of protecting traditional publishing content, some of those decisions were understandable.

From the perspective of search engines trying to discover and understand useful web content, they created substantial problems.

## Finding the Opportunity

My initial responsibilities were primarily around Omniture.

The implementation itself had originally been done well, but it hadn't kept pace with changes to the product.

Reporting was also highly manual. The previous approach involved repeatedly extracting data from Omniture into Excel and creating reports from it.

I automated some of that work through the Omniture API, which gave me more time to investigate the underlying acquisition data.

Organic search stood out immediately.

Given the amount and quality of the material Safari had available, the absence of meaningful search traffic looked like an enormous missed opportunity.

I began analysing search performance using Google's search tools and inspecting the site directly at the HTTP and HTML level, including extensive use of cURL.

The problem wasn't a lack of useful content.

**Search engines were having difficulty discovering, accessing and understanding it.**

## Diagnosing the Problems

I found a range of issues, from very basic configuration problems through to deeper architectural ones.

At the simplest end, crawlers were being blocked through `robots.txt`.

More broadly, the architecture had not been designed around accessibility or search-engine discoverability.

Problems included:

* Restricted crawler access.
* Very little publicly accessible page content.
* Heavy reliance on JavaScript.
* Poor content-to-code ratios.
* Complicated XML-to-HTML rendering.
* Obfuscated page implementations.
* Limited semantic markup.
* A product architecture based around reproducing physical books rather than publishing web-native content.

Individually, some of these issues were relatively straightforward.

Together, they made a huge catalogue of valuable content effectively invisible to search engines.

## Making the Case

SEO wasn't what I had originally been hired to do.

But the analytics showed a clear commercial opportunity.

I put together an analysis and presented it to my boss, the CTO, and the VP of Product.

I explained why I thought organic acquisition was underperforming and proposed a range of changes based around accessibility and SEO best practices.

These ranged from relatively simple configuration changes, such as allowing appropriate crawler access, through to changes in page structure, content presentation and semantic markup.

The argument wasn't simply that the website needed "better SEO."

It was that Safari already owned an extremely valuable acquisition asset — its content — but its technology prevented potential customers from discovering it.

## Implementing the Changes

Safari didn't have a large internal technical team that I could simply hand the recommendations to.

Development was primarily performed by an external engineering company working through a fairly traditional waterfall process.

Rather than limiting my involvement to producing the analysis, I learned SVN and implemented many of the changes myself.

This required me to move outside the normal boundaries of a Web Analytics Manager role.

But I understood both the evidence behind the recommendations and enough of the underlying web technology to make many of the changes directly.

The objective was to remove the barriers preventing search engines from discovering and understanding Safari's content.

## Outcome

The impact was substantial.

Organic search went from almost nonexistent to becoming **Safari's number one traffic source**.

At its peak, organic search was bringing **millions of users per month** to the product.

The project changed Safari's acquisition funnel dramatically.

Instead of relying predominantly on paid and other established acquisition channels, Safari now had a large stream of potential customers discovering its content naturally through search.

That success also created the next analytical problem.

Traffic had increased enormously, but subscription conversion had not increased proportionally.

As a result, the anonymous-to-subscriber conversion rate fell.

That wasn't evidence that the SEO project had failed. The denominator had changed dramatically because we had introduced millions of additional prospective users into the top of the funnel.

The next question became:

**How do we convert more of those users into trials and paying subscribers?**

That led directly to the conversion optimisation and experimentation work I subsequently led.

## What I Learned

This project reinforced one of the principles that has remained central to how I approach analytics:

**Start with the business problem, not the reporting request.**

I had been hired to produce web analytics and acquisition reporting.

I could have continued producing those reports.

Instead, looking at the underlying data revealed that one of the largest potential acquisition channels was effectively absent.

The valuable analytical question wasn't:

> "How much organic traffic did we receive?"

It was:

> "Why do we have so little organic traffic when we own exactly the type of content people are searching for?"

Answering that question required moving beyond analytics into product architecture, accessibility, SEO and implementation.

It also reinforced my belief that analysts create more value when they are willing to follow evidence beyond the boundaries of the original request.

My job wasn't ultimately to produce an Omniture report.

It was to use the information available to help improve the business.

## Questions this experience answers

* What did Martin do at Safari Books Online?
* What experience does Martin have at O'Reilly?
* Does Martin have SEO experience?
* Does Martin have web analytics experience?
* Does Martin have customer acquisition experience?
* Has Martin worked with Adobe Omniture?
* Has Martin identified a major commercial opportunity through data?
* What is an example of Martin using analytics to create business value?
* Has Martin grown organic traffic?
* Has Martin worked on products with millions of users?
* How does Martin approach an analytical problem?
* Does Martin go beyond the initial stakeholder request?
* Has Martin influenced senior product and technology leaders?
* Has Martin presented recommendations to a CTO?
* How does Martin use data to influence product decisions?
* Has Martin implemented technical changes himself?
* How hands-on is Martin?
* Has Martin worked outside the formal boundaries of his role?
* Does Martin have technical SEO experience?
* Does Martin have experience with accessibility and semantic markup?
* Has Martin worked with third-party engineering teams?
* How does Martin balance analysis with implementation?
* What is an example of Martin discovering an opportunity nobody had asked him to investigate?
* How did Martin increase traffic at Safari Books Online?
