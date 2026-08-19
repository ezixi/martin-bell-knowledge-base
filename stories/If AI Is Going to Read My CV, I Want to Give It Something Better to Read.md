# **If an AI Agent Is Going to Judge Me on My CV, I Want to Give It Something Better to Read**

Looking for a new job usually starts roughly the same way;  digging out the old CV from last time I was searching, blowing the dust off it, thinking about what I could add and tweaking it slightly as I look over the paragraphs with smarter, more experienced eyes.

After chuckling to myself about how stupid old me was, I’ll make some attempt to compress years of work into two pages, create a few versions to match the general role types I’m looking for and write a standard cover letter that I can edit to match any particular job.

Then I’ll trawl LinkedIn, upload my new babies off to an application system and wait. And wait. And wait.

It must be better than this.

*We are using the wrong interface for modern recruitment.*

Like most of modern life, it’s no surprise that recruitment is becoming increasingly influenced by AI. No human is the first to look at a newly submitted CV. Applications are screened, ranked, summarised and matched against job descriptions well before any meaningful, human conversation takes place.

If an AI agent is going to form an opinion about my career, I don't want its primary source to be two pages of carefully compressed bullet points that I’m hoping I might be able to expand on in a theoretical face-to-face chat.

So I've built something else.

## **A career is bigger than a CV**

One of the hardest things I’ve found about writing a CV is deciding what *not* to include.

*A CV necessarily throws information away. It lacks context.*

It’s like valuing the quality of a meal by only reading the menu.

In [my CV](https://www.backhandmedia.com/cv) I have a bullet point that in one role I, *"Built an analytics engineering function"*. I did too. I think we did a great job, delivered useful work and really bonded as a team.

It might sound impressive (or not). But what it doesn't explain is **why** the function was needed, what was broken beforehand, how and why I structured the team, the resistance I encountered, the technical decisions we made, what worked, what didn't, or what I learned from it.

"*Migrated BigQuery to Snowflake"* is even worse.

It sounds like a technology migration. And, yes it was. But the interesting parts weren't really about either technology. They were about modelling, organisational ownership, metric governance, engineering standards, stakeholder adoption and… some decisions that I would definitely make differently if I did it again.

Those details matter when a hiring manager is trying to understand whether somebody has actually dealt with a problem before.

They don't fit particularly well on a CV. In the past, those contextual details would be filled in with a chat and some tough questions. But that chat will never happen if the AI classifying the CV doesn’t pass it through to the next stage of the process.

## **It’s an absence of context, Bob**

I've worked across analytics, analytics engineering, data engineering, architecture and leadership. The boundaries between those disciplines aren't particularly clean, yet a human assessing a candidate from their CV or LinkedIn profile is often also recruiting simultaneously for roles across dozens of technical disciplines.

It’s not reasonable to expect a recruiter to understand the difference between building a dbt project and designing a dimensional model, or between implementing a dashboard and defining the semantic layer underneath it.

They shouldn't need fifteen years of data experience to decide whether I have fifteen years of data experience.

But that creates a lossy translation layer.

I describe what I've done in my CV. A recruiter interprets that against their understanding of the role. A hiring manager eventually tries to reconstruct the reality from both.

Now we're adding AI into that chain.

Rather than fight that change, I started wondering whether I could adapt my job search to this new reality. To make the source material better.

## **This is a data problem**

Perhaps unsurprisingly, I've ended up approaching my own career in much the same way I approach data systems.

A CV is effectively a presentation layer.  It’s a product derived from the underlying model I’ve been building throughout my career: the entities, relationships, evidence, definitions and context that describe what I've actually done.

From that, I might create a CV. But it could also be the basis for a LinkedIn profile, a response to an application question, interview preparation or, eventually, a conversation.

The document becomes an output rather than the database.

That is a much more interesting idea to me than simply using an LLM to write better CV bullets.

## **Talking to the machines**

If there is one thing I’ve learned working with AI is that for it to be successful in its assigned task, we have to provide enough context and the correct semantics. As we might have done in the past, we can't rely on a human to, for example,  ask questions, look up a tutorial or run something past a colleague. We have to front load the context when we create the prompt.

**So I've created a [public, structured knowledge base describing my career.](https://github.com/ezixi/martin-bell-knowledge-base)**

It contains the obvious things: companies, roles, skills and technologies, but it also contains individual projects, architectural decisions, leadership examples, failures, lessons learned, ways of working, recommendations from people I've worked with, and my thinking about areas such as data strategy, governance and semantic layers.

[My CV is still there](https://github.com/ezixi/martin-bell-knowledge-base/blob/main/profile/career-timeline.md), but it’s backed up with context, evidence and examples. I don't have to reduce everything to a bullet point.

If somebody wants to know whether I've used dbt, the answer is there. If they want to know whether I've introduced dbt into an organisation that wasn't using modern engineering practices, that answer is there too. If they want an example of dealing with resistance while doing it, there is considerably more context available.

And if the "somebody" asking is an agent, that's fine.

In fact, that's the point.

I can send it to a recruiter. A hiring manager can search it. Search engines can discover it.

And, increasingly importantly, agents can use it to make informed decisions about my skills and career.

The repository becomes another representation of my professional identity on the web.

## **What comes next**

If recruitment is moving towards a world where machines increasingly evaluate people, perhaps we shouldn't spend all our time optimising documents designed for humans to skim in thirty seconds.

Perhaps we should give the machines better information.

I've started with mine. [Take a look](https://github.com/ezixi/martin-bell-knowledge-base).
