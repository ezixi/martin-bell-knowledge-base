---
type: experience-documentation-framework
purpose: Reusable role and project documentation template
---

# Experience Documentation Framework

Use this framework to document a new role as work happens. Create an employer directory (for example, `experience/Zego/`), begin with `overview.md`, then add one kebab-case Markdown file for each substantial project, decision or body of work.

Record evidence as it becomes available. Keep facts, estimates, proposals and lessons clearly distinct; remove prompts that are not relevant rather than filling them with assumptions.

## Role overview

Start each employer directory with `overview.md`.

```markdown
---
type: experience
company: [Company]
role: [Role]
start: [YYYY-MM]
end: [YYYY-MM or present]

industries:
  - [Industry]

technologies:
  - [Technology]

skills:
  - [Skill]

related:
  - [project-file.md]
---

# [Company]

## Summary

[What the role exists to achieve, the scope, and the context.]

## Responsibilities

- [Ongoing responsibility or area of ownership.]

## Major achievements

- [Delivered outcome, with evidence or a link to the project case study.]

## Leadership and collaboration

[How you led, influenced, partnered or developed others.]

## Technologies

- [Technology, platform or practice used in the role.]

## Questions this experience answers

- [Recruiter, CV or interview question this role evidences.]
```

## Project or decision case study

Create a separate document when a project, problem, technical decision or change is substantial enough to reuse as evidence.

```markdown
---
type: project
title: [Project or decision title]
company: [Company]
role: [Role]
domain:
  - [Domain]

summary: >
  [One or two sentences covering the problem, your contribution and the result.]

technologies:
  - [Technology]

skills:
  - [Skill]

outcomes:
  - [Measured result, observed result, or clearly labelled in-progress result]

related:
  - overview.md
---

# [Project or decision title]

## Overview

[Why this work mattered and what changed.]

## Starting point and problem

[Context, constraints, users affected, and evidence of the problem.]

## Objectives and success measures

- [Desired outcome or measure.]

## My role and contribution

[What you personally owned, influenced or supported.]

## Decisions and trade-offs

### [Decision]

- **Options considered:** [Options and relevant constraints.]
- **Choice:** [What was chosen and why.]
- **Trade-off:** [What was accepted, deferred or deliberately avoided.]

## Technical implementation

[Architecture, data, delivery approach, quality controls, rollout and operational considerations.]

## Outcomes and evidence

- **Measured:** [Metric, baseline, result and time period.]
- **Observed:** [Stakeholder feedback or operational change, with source where possible.]
- **In progress / not measured:** [State this plainly; do not imply a result.]

## Lessons learned

- [What you would repeat, change or investigate next time.]

## Reusable interview and CV story

- **Situation:** [Concise context.]
- **Task:** [Your responsibility or goal.]
- **Action:** [The decisions and actions you took.]
- **Result:** [Evidence-backed outcome or current status.]
- **CV version:** [One outcome-led bullet, including a number only when supported.]

## Questions this project answers

- [Interview or recruiter question this case study supports.]
```

## Maintenance

- Update the role overview when responsibilities or evidenced achievements materially change.
- Add project case studies incrementally; link them from the relevant `overview.md` through `related`.
- Prefer a small number of complete, evidence-backed stories to a long list of incomplete notes.
