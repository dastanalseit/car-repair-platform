# Project Proposal

## Project identity

**Title:** Development of a Platform for Finding Car Repair Specialists with a Rating System Based on Verified Customer Reviews

**Author:** Dastan  
**Supervisor:** Botagoz Mirzagalikova  
**Project type:** Individual diploma project  
**Deliverable:** Responsive website for desktop and smartphone browsers  
**Status:** Proposal prepared for supervisor review; approval has not yet been recorded.

Dastan is responsible for research, requirements, design, implementation, evaluation and documentation. The supervisor reviews significant deliverables at agreed checkpoints.

## Problem statement

Car owners need to find repair specialists whose services match their vehicle problem and location. They also need information that helps them compare specialists before submitting a request. A rating is more informative when a review can be connected to a recorded service relationship.

The author reported informal conversations with drivers who expressed concerns about repair quality and being misled. These are preliminary observations, not a documented interview study. The separate [user research](user-research.md) now contains six anonymised driver response summaries and preliminary findings. These records do not establish measured prevalence across repair services; collection metadata and clarifications remain incomplete.

This project addresses a specific information problem: helping customers find specialists and distinguish reviews linked to completed service requests from reviews with no recorded request relationship. It does not independently inspect repairs or guarantee that every review is truthful.

## Relevance and evidence plan

The initial rationale combines the author's observations with the [comparison of existing systems](existing-system-comparison.md). The comparison provides context for search, profiles, review counts and complaint handling; it does not establish that every competing system lacks review verification.

Before treating user needs as validated findings:

- Conduct and document 3–5 actual discussions with potential users, or document a substantive agreement with an actual client.
- Ask how drivers choose specialists, what difficulties they encounter, how they assess reviews, and whether they would confirm service completion.
- Where feasible, include a specialist perspective on request handling and completion disputes.
- Use anonymous participant identifiers, avoid unnecessary personal information and record participants' consent to use their responses.
- Keep observed findings, quotations, interpretations and design assumptions separate.
- Link each supported finding to the requirements it informs; report disagreements and limitations.

The literature review must meaningfully use at least 12 sources, including at least 8 scientific publications. It should examine online reputation, verified transactions, review manipulation, trust and marketplace usability. A [literature review draft](literature-review.md) with 18 scholarly sources and two contextual primary sources is available. The revised review adds Kazakhstan automotive evidence, dated official fleet statistics, review helpfulness and local-service manipulation incentives. Initial supervisor feedback is recorded; confirmation of these revisions remains pending.

## Target users

| User | Need | Planned capability |
|---|---|---|
| Visitor / prospective customer | Find relevant repair services and compare options | Browse published profiles, filter by city and service, inspect ratings and review counts |
| Customer | Request a service and record the outcome | Track own requests, confirm or dispute completion, review an eligible request and submit complaints |
| Repair specialist | Present services and manage incoming work | Maintain a profile, accept or decline requests and update permitted work statuses |
| Administrator | Handle complaints consistently | Review reports, record decisions and hide reviews that violate agreed rules |

The initial cities and service categories will be agreed during requirements review. Prototype entries are fictional and do not constitute real participating businesses.

## Aim

To develop and evaluate a responsive website that helps car owners find repair specialists and compare them through ratings based on reviews linked to completed, customer-confirmed service requests.

## Objectives

1. Investigate user needs through documented discussions and a critical review of relevant literature.
2. Compare existing systems against common, evidence-based criteria.
3. Define functional and non-functional requirements with priorities and acceptance criteria.
4. Compare technology alternatives and justify selections against the project requirements.
5. Design the architecture, database, interface and API with consistent roles and workflows.
6. Implement specialist discovery, service requests, customer confirmation and verified reviews.
7. Implement rating calculation and complaint moderation with traceable decisions.
8. Evaluate functional correctness, usability and selected performance targets under documented conditions.
9. Maintain a traceable repository and YouTrack workflow, including supervisor feedback and resulting revisions.

## Proposed solution

The website provides public specialist profiles, city/service filters and ratings with review counts. A signed-in customer selects a service and submits vehicle details, a problem description and a contact number. Price and timing may be agreed by telephone outside the platform.

The specialist accepts or declines the request. After work starts and finishes, the specialist submits it for customer confirmation. Only the customer can confirm completion or dispute it. A completed and confirmed request permits one text review with an integer score from 1 to 5.

The rating is the arithmetic mean of published eligible scores, displayed to one decimal place alongside the count. Specialists without published reviews are shown as “Not yet rated”. Administrators handle complaints with recorded reasons. A negative score alone does not justify removing a review.

### Meaning and limits of verification

Verified means that the review belongs to the customer associated with a recorded request that the customer confirmed as completed. Confirmation does not imply satisfaction.

The mechanism does not independently prove repair quality, physical attendance or the absence of collusion. Fake accounts and coordinated fake requests remain possible. Customer non-response does not automatically complete a request, and an administrator cannot confirm on the customer's behalf.

## Scope

### Included in the initial website

- Customer and specialist registration, sign-in and sign-out.
- Server-side role and object-access checks.
- Published specialist profiles, services and city information.
- Search by city and service and sorting by rating.
- Customer and specialist dashboards.
- Request creation, controlled status transitions and status history.
- Customer confirmation or dispute of completion.
- One review per eligible request, including protection against concurrent duplicates.
- Ratings derived from published reviews and visible review counts.
- Complaint submission, staff decisions and moderation history.
- Responsive layouts and keyboard-accessible primary flows.

### Outside the initial scope

- Online payments, escrow and refunds.
- Real-time chat or automatic appointment scheduling.
- Native mobile applications.
- Automated recommendations or machine-learning fraud detection.
- Independent inspection or certification of repairs.
- Third-party identity checks and guarantees against collusion.
- Review editing, appeals and reopening final complaint decisions in the initial implementation.

Optional review editing remains a Should requirement and may be reconsidered after the core workflow is complete. Handling abandoned requests and detailed moderation rules require supervisor review.

## Technical approach and engineering complexity

Selected technologies: React + TypeScript + Vite for the interface; Python + Django + Django REST Framework for the backend; PostgreSQL for persistent data; Django Admin for internal administration.

The application is planned as a modular monolith with separate modules for identity, specialist discovery, requests, reviews and complaints. The browser communicates with the backend through an HTTP API. The proposed authentication approach uses Django sessions and CSRF protection.

The engineering work includes:

- A request state machine with actor-specific transitions and an audit trail.
- Ownership and permission checks for private records.
- Transactional review eligibility and a database uniqueness constraint.
- Correct aggregate ratings after moderation changes.
- Privacy boundaries between public profiles/reviews and private request details.
- Consistent business rules shared by API operations and staff actions.

These elements provide engineering depth beyond a static catalogue. They remain design commitments, not completed implementation claims.

## Expected outcomes

| Deliverable | Evidence of completion |
|---|---|
| Research and relevance analysis | Documented real discussions, structured literature table and explicit assumptions |
| Requirements and design | Acceptance criteria, editable diagrams, database design and API contract |
| Working website | Demonstrable end-to-end customer and specialist workflows |
| Verified review mechanism | Ownership/completion checks and at-most-one-review enforcement |
| Evaluation report | Recorded method, environment, results, failures and limitations |
| Traceable project record | YouTrack tasks linked to branches, commits and pull requests |
| Supervision record | Actual supervisor comments and documented responses |

Current repository materials include comparisons, requirements, diagrams, a fictional-data interface prototype, database design and API design. Production backend and frontend implementation have not started.

## Evaluation approach

The [verification and evaluation plan](evaluation-plan.md) defines proposed procedures, metrics, measurement conditions and a comparison baseline. Confirm the protocol before evaluation begins.

Planned evidence includes:

- Functional checks against every Must acceptance criterion.
- Unauthorised access, invalid-transition and concurrent duplicate-review scenarios.
- Rating recalculation after a review is hidden.
- Representative user tasks with completion rate, time, errors and qualitative feedback.
- Search performance under the dataset and load conditions in the requirements.
- Responsive and keyboard-accessibility checks on the main flows.

The planned comprehension comparison uses the same specialist information and workflow in both variants: A displays the verified-review label alone; B displays the same label with an explanation of its meaning and limits. The evaluation plan specifies counterbalanced presentation and comprehension questions. This comparison has not been conducted; no success rates or performance results are claimed.

## Delivery plan and dependencies

| Stage | Main output | Dependency |
|---|---|---|
| Analysis and preparation | Proposal, user evidence, literature review, comparisons, requirements, prototype and evaluation plan | Actual user participation and supervisor input |
| Design review | Consistent architecture, database and API | Reviewed scope and requirements |
| Core implementation | Accounts, catalogue, requests and reviews | Agreed design and development environment |
| Moderation and integration | Complaint handling, staff actions and connected React flows | Reliable core workflow |
| Evaluation and refinement | Results, fixes and limitations | Runnable implementation and evaluation participants |
| Submission preparation | Reviewed repository version, tag and demonstration notes | Completed review and traceability checks |

Priorities, dependencies and acceptance criteria are tracked in the [YouTrack project](https://dastan-car-repair.youtrack.cloud/projects/CRP); the proposal is linked to [CRP-1](https://dastan-car-repair.youtrack.cloud/issue/CRP-1). The [project plan](project-plan.md) describes stages and responsibilities. Calendar dates remain unassigned; scheduling and approval require separate agreement.

## Initial risks

| Risk | Planned response |
|---|---|
| Too much scope for one developer | Implement the core journey first; defer optional features |
| Limited experience with the chosen stack | Build small vertical slices and document setup decisions |
| Fake requests or coordinated reviews | State verification limits; enforce request linkage and retain moderation history |
| Customer non-response or disputes | Preserve explicit states; do not assume completion |
| Leakage of private request details | Use separate public/private response fields and server-side checks |
| Insufficient research or supervisor feedback | Arrange real discussions and review checkpoints early |
| Missing task traceability | Create real YouTrack tasks and connect subsequent changes through pull requests |

## Review checkpoints

Ask the supervisor to review the problem and scope, evidence quality, requirements, architecture and evaluation method. Record the actual feedback and the resulting changes. This proposal has not yet received recorded supervisor approval.

## Related documentation

- [Requirements and acceptance criteria](requirements.md)
- [Existing system comparison](existing-system-comparison.md)
- [Technology comparison](technology-comparison.md)
- [Architecture diagrams](diagrams/README.md)
- [Database design](database-design.md)
- [API design](api-design.md)
- [Interface prototype](prototype/README.md)

- [User research plan, driver responses and preliminary findings](user-research.md)
- [Literature review](literature-review.md)
- [Evaluation plan](evaluation-plan.md)
- [Project plan and risks](project-plan.md)
- [Supervisor feedback — pending](supervisor-feedback.md)
