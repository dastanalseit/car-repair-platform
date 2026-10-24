# Project Plan and Risks

**Project:** Development of a Platform for Finding Car Repair Specialists with a Rating System Based on Verified Customer Reviews  
**Author:** Dastan  
**Supervisor:** Botagoz Mirzagalikova  
**Status:** Proposed delivery plan for review. The first-stage deadline for CRP-1 through CRP-6 is 24 October 2026. Later implementation dates remain to be agreed.

## 1. Delivery approach

Dastan is responsible for research, design, implementation, evaluation and documentation. Significant scope decisions and deliverables will be presented to the supervisor for feedback. No supervisor approval is implied by this plan.

The deliverable is a responsive website. The production stack is React, TypeScript and Vite for the frontend; Python, Django and Django REST Framework for the backend; PostgreSQL for persistent storage; and Django Admin for staff operations. The existing standalone prototype supports interface discussion and does not establish that the production website is implemented.

Work will proceed through small, reviewable increments. Each increment should reference its requirements and YouTrack task, identify outstanding issues and state what was actually checked. A completed document draft is distinct from a reviewed document, and a planned feature is distinct from an implemented feature.

## 2. First-version scope

The first version will support the complete journey: find a specialist, submit a service request, follow its progress, confirm that service occurred, and leave one review for an eligible request.

### Required capabilities

- Customer and specialist registration, sign-in and sign-out; separately provisioned administrator access.
- Published specialist profiles, city/service filters, ratings and review counts.
- Customer and specialist dashboards with server-enforced ownership and role permissions.
- Request transitions, explicit customer confirmation and a completion-dispute path.
- One review per completed, customer-confirmed request, including negative feedback.
- Consistent published rating calculations and an unrated state.
- Complaints, administrator decisions and retained moderation history.
- Responsive core pages, keyboard operation, safe input handling and private-information protection.

The [requirements](requirements.md) define acceptance criteria. All Must requirements remain part of the initial acceptance baseline. Review editing (FR-14) and the performance target (NFR-06) are Should items; any unmet target must be disclosed. A scope reduction requires an explicit documented decision rather than silently removing a requirement.

Online payments, live chat, native mobile applications, automated recommendations and independent mechanical inspection remain outside the initial scope. Machine-learning fraud detection is not an initial implementation commitment.

## 3. Work stages and completion criteria

The sequence below expresses dependencies, not calendar deadlines. Interface preparation and documentation may proceed alongside backend work when they do not depend on unfinished behaviour.

| Stage | Main work | Completion evidence | Dependency |
|---|---|---|---|
| 1. Research and scope | Refine the problem, review literature and alternatives, conduct driver interviews, define the initial scope | Traceable sources, anonymised actual interview findings, explicit limitations and a scope statement ready for supervisor review | None; existing drafts provide a starting point |
| 2. Requirements and design | Reconcile requirements, request states, roles, architecture, database design, API contract and prototype | Consistent documents; unresolved decisions recorded; review feedback and resulting changes recorded when received | Stage 1 evidence informs decisions; provisional designs may be prepared earlier |
| 3. Backend foundation | Set up the Django project, custom user model, migrations, sessions, permissions and specialist catalogue | Reproducible local setup; registration, login and catalogue behaviour implemented; planned acceptance checks recorded when executed | Agreed initial roles and API conventions |
| 4. Request and review workflow | Implement request ownership and transitions, confirmation, disputes, one-review rule and aggregate calculation | A complete backend journey; rejected invalid actions; retained history; concurrency and rating evidence from planned checks | Backend foundation |
| 5. Complaints and staff operations | Implement complaint submission, administrator decisions and public visibility changes using shared business rules | Complaint and moderation flows implemented without bypassing confirmation, review uniqueness or history | Request and review workflow |
| 6. Website integration | Build React pages and connect authentication, search, requests, reviews and complaints to the backend | Main journey works through the browser; loading, empty, validation and error states are usable; responsive and keyboard checks recorded | Stable API increments; integration can start as each area becomes available |
| 7. Evaluation and revision | Execute the planned functional, usability, comparison, browser and performance work; resolve defects | Actual results linked to the evaluated commit; failures and limitations included; blocking defects resolved and affected cases rechecked | Integrated website; no blocking functional defects before participant sessions |
| 8. Submission preparation | Update setup guidance, diagrams and dissertation material; assemble evidence and supervisor feedback | Reproducible deliverable, consistent documentation, sanitised evidence and an assessment snapshot with outstanding limitations | Evaluated version and documented revisions |

Do not mark a stage complete solely because its document or task exists. The backend and integrated website stages are not complete until implementation evidence exists. If interviews or specialist feedback cannot be obtained, record the gap and review its impact rather than inventing results.

## 4. Incremental implementation order

1. Establish the backend project, account model and migrations before dependent models.
2. Implement authentication and permissions, then the public specialist catalogue.
3. Deliver a narrow end-to-end request journey with an owning customer and assigned specialist.
4. Add customer confirmation, completion disputes, review eligibility and published aggregates.
5. Add complaints and administrator moderation using the same rules across interfaces.
6. Complete frontend integration, accessibility and error handling for all required flows.
7. Execute the separate evaluation protocol and revise the implementation based on recorded evidence.

Keep optional enhancements behind the required workflow. Pin dependency versions when implementation starts, and update the setup instructions with the actual supported environment. Planned checks in this document are future work, not a claim that tests have been run.

## 5. Risk register

Likelihood and impact are qualitative planning judgements, not measured probabilities. Dastan owns implementation and follow-up for each risk; scope or assessment decisions may require supervisor input.

| ID | Risk | Likelihood / impact | Early signal | Prevention or mitigation | Response if it occurs |
|---|---|---|---|---|---|
| R-01 | The individual project exceeds available capacity | Medium / High | Core workflow remains unfinished while optional features expand | Work in small increments; prioritise Must requirements and the complete user journey | Defer optional work and document any proposed scope change for review |
| R-02 | Suitable interview or evaluation participants are difficult to recruit | Medium / Medium | Too few willing participants or repeated cancellations | Prepare short sessions; recruit adult drivers through available contacts; keep participation voluntary | Report the actual sample and missing evidence; adapt recruitment without fabricating responses |
| R-03 | Customers and specialists collude to create artificial eligible requests | Medium / High | Repeated suspicious request/review patterns or complaints | Enforce ownership, statuses and one-review constraints; retain relevant history; explain verification limits | Review complaints and document residual risk; do not claim fraud is eliminated |
| R-04 | Unresolved or disputed requests exclude dissatisfied users from published ratings | Medium / High | Requests remain unconfirmed; users confuse confirmation with satisfaction | Permit negative reviews after confirmation, provide disputes and complaints, prohibit automatic completion | Examine the affected paths and disclose selection bias; revise policy only through a recorded decision |
| R-05 | Unauthorised access exposes private requests or changes another user's records | Medium / High | Direct API calls bypass interface restrictions | Enforce permissions and ownership on the server; use separate role fixtures and negative acceptance cases | Block release, fix the access path and recheck related operations |
| R-06 | Concurrent submissions or moderation produce duplicates or incorrect aggregates | Medium / High | Duplicate reviews, mismatched counts or stale public scores | Use transaction boundaries, a unique request-to-review constraint and consistent aggregate rules | Investigate persistent state; correct the cause and affected records with a reviewed procedure; repeat relevant cases |
| R-07 | Frontend and backend implement different contracts | Medium / Medium | Field, state or error responses differ from the documented API | Reconcile the contract and implementation incrementally; document changes with both components | Correct the mismatch before expanding the affected flow and update documentation |
| R-08 | Users treat the verified label as a guarantee of repair quality | Medium / High | Participants endorse a mechanical-quality or honesty guarantee | Use precise explanatory wording and the planned comprehension comparison | Revise wording and retest understanding; report remaining misconceptions |
| R-09 | Literature access or weak contextual relevance limits the review | Medium / Medium | Claims rely on restricted abstracts or unrelated market settings | Record access boundaries; include automotive evidence and explicit transfer limitations | Seek lawful full-text access where possible; narrow unsupported claims |
| R-10 | Credentials or identifying interview material enter public documentation | Low / High | Real contacts, tokens or identifiable notes appear in proposed changes | Use fictional examples, environment configuration and anonymised research summaries; inspect changes before publication | Remove exposed material, revoke exposed credentials where relevant and assess further corrective steps |
| R-11 | Browser, deployment or performance problems appear late | Medium / Medium | Core flows fail on supported browsers or target layouts | Integrate early; record environment versions; apply the planned browser, layout and bounded load checks | Fix Must failures; disclose unmet Should targets and environment limitations |
| R-12 | Draft documents and separate branches diverge from the implemented system | Medium / Medium | Conflicting README links, stale diagrams or contradictory state rules | Review related documents in each change and reconcile open pull requests before submission | Resolve inconsistencies, preserve relevant edits and produce one coherent reviewed snapshot |

## 6. Tracking and review checkpoints

Use the [YouTrack project](https://dastan-car-repair.youtrack.cloud/projects/CRP) to track work. Current planning areas include proposal (CRP-1), interviews (CRP-2), literature review (CRP-3), requirements/design/prototype (CRP-4), evaluation (CRP-5) and supervisor submission (CRP-6). Create implementation tasks as the stages are broken down; do not treat these planning tasks as evidence that software has been delivered.

Each task should identify the owner, expected output, requirement references where applicable, acceptance criteria, priority, dependencies and a link to the relevant pull request or evidence. CRP-1 through CRP-6 have a first-stage deadline of 24 October 2026. Open review items remain visible after this checkpoint; the date does not imply completion.

Review checkpoints:

- **Research and scope:** inspect source quality, interview evidence, scope and unresolved assumptions.
- **Design:** reconcile roles, transitions, eligibility, API, storage and prototype behaviour.
- **Integrated core workflow:** demonstrate actual implementation and identify blocking defects.
- **Evaluation:** inspect measured outcomes, failures, interpretation and limitations.
- **Submission:** reconcile documentation, changes, evidence and assessment snapshot.

Record feedback and actions only after feedback is received. Keep pending reviews visible; do not label a draft as supervisor-approved.

## 7. Change and completion rules

Use task-linked branches and pull requests. Describe what changed, why it changed, what was checked and what remains unresolved. Keep the reviewed baseline separate from draft changes. Before combining documentation pull requests, preserve links and content from all relevant changes rather than replacing one draft with another.

For each implementation increment, completion requires the intended behaviour, updated documentation, evidence from the applicable planned checks and a clear statement of remaining defects. Test results must identify the evaluated commit. A blocked or unexecuted check is not a pass.

Before final implementation submission, confirm that all Must requirements have evidence, the main browser journey is reproducible, private material is excluded, assessment tags identify the intended version, and known limitations are stated. Later implementation milestones need their own agreed deadlines.

## 8. Related documents

- [Requirements and acceptance criteria](requirements.md)
- [API design](api-design.md)
- [Technology choices](technology-comparison.md)
- [Prototype guide](prototype/README.md)
- [Literature review](literature-review.md)
- [Evaluation plan](evaluation-plan.md)
- [User research plan](user-research.md)

The repository contains the first-stage analysis and design documents. User Research summarises six individual driver interviews conducted through Threads and WhatsApp. The author confirms that all participants agreed to anonymous use. Unspecified details are recorded as limitations. The supervisor’s literature-review comments and the changes made in response are recorded in Supervisor Feedback. Confirmation of those revisions is pending.
