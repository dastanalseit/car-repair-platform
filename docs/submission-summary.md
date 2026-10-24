# First pre-defense submission

Author: Dastan Alseit

Supervisor: Botagoz Mirzagalikova

Submission tag: `pre-defense-1`

First-stage deadline: 24 October 2026

[Repository snapshot](https://github.com/dastanalseit/car-repair-platform/tree/pre-defense-1) · [YouTrack](https://dastan-car-repair.youtrack.cloud/projects/CRP) · [Defense guide](defense-guide.md)

## Work included

The project proposes a website where drivers can find repair specialists, send requests and review completed work. A review belongs to one customer-confirmed request. This records the service relationship; it cannot certify mechanical quality or prevent every form of collusion.

| Assessment component | Evidence in this version |
|---|---|
| Proposal and scope | [Project proposal](project-proposal.md), including users, objectives, scope and expected outcomes |
| Relevance | [User research](user-research.md): six individual interviews through Threads and WhatsApp, anonymous response summaries and findings; the author confirms permission for anonymous use |
| Literature | [Review and analysis table](literature-review.md): 18 scholarly sources and two official contextual sources; Kazakhstan evidence and the supervisor’s requested themes are included |
| Existing systems | [Comparison](existing-system-comparison.md): three systems assessed against eight criteria |
| Technologies | [Comparison](technology-comparison.md): frontend, backend and database alternatives with reasons for the selected stack |
| Requirements | [Functional and non-functional requirements](requirements.md), priorities and acceptance criteria |
| Architecture | [Context, use case and component diagrams](diagrams/README.md), with editable PlantUML sources and SVG exports; database and API designs are also included |
| Prototype | [Russian and Kazakh interface files](prototype/README.md), with local opening instructions |
| Evaluation | [Plan](evaluation-plan.md) with functional cases, metrics, conditions and a comparison baseline |
| Management | [Plan and risks](project-plan.md), task ownership and [YouTrack](https://dastan-car-repair.youtrack.cloud/projects/CRP) |
| Supervision | [Feedback and responses](supervisor-feedback.md); the literature changes are recorded in [PR 10](https://github.com/dastanalseit/car-repair-platform/pull/10) |

## Task traceability

Dastan owns all six first-stage tasks through the YouTrack account `admin`. Their deadline is 24 October 2026. Review stages remain open until the corresponding acceptance criteria are met.

| Task | Main deliverable | Development evidence |
|---|---|---|
| [CRP-1](https://dastan-car-repair.youtrack.cloud/issue/CRP-1) | Proposal | [PR 1](https://github.com/dastanalseit/car-repair-platform/pull/1), [PR 10](https://github.com/dastanalseit/car-repair-platform/pull/10) |
| [CRP-2](https://dastan-car-repair.youtrack.cloud/issue/CRP-2) | Driver interviews | [PR 9](https://github.com/dastanalseit/car-repair-platform/pull/9), [PR 12](https://github.com/dastanalseit/car-repair-platform/pull/12) |
| [CRP-3](https://dastan-car-repair.youtrack.cloud/issue/CRP-3) | Literature analysis | [PR 10](https://github.com/dastanalseit/car-repair-platform/pull/10) |
| [CRP-4](https://dastan-car-repair.youtrack.cloud/issue/CRP-4) | Design and prototype | [Prototype guide revision](https://github.com/dastanalseit/car-repair-platform/commit/5571e8a), [PR 8](https://github.com/dastanalseit/car-repair-platform/pull/8) |
| [CRP-5](https://dastan-car-repair.youtrack.cloud/issue/CRP-5) | Evaluation plan | [Evaluation plan commit](https://github.com/dastanalseit/car-repair-platform/commit/ca1e0dd) |
| [CRP-6](https://dastan-car-repair.youtrack.cloud/issue/CRP-6) | Feedback and submission package | [PR 10](https://github.com/dastanalseit/car-repair-platform/pull/10), this tagged package |

## Limits and remaining work

The production backend and integrated React website are not implemented. The prototype uses fictional records and keeps changes in browser memory. No completed usability study, load test or production acceptance result is claimed.

The interview sample is small. Responses are translated summaries, and some session details were not recorded. P1 did not explicitly state whether an online review was posted; P2 did not explicitly assess the repair outcome. These gaps remain visible in the response records. The participants’ permission is recorded from the author’s confirmation; private messages are not included in the repository.

The supervisor has commented on the literature review. Confirmation of the revisions and review of the other deliverables remain pending. Specialist-side assumptions still need evidence. The additional review-text comparison proposed in the literature review must be agreed before it becomes part of the evaluation protocol.

The GitHub repository returned an HTTP 200 response without a signed-in session during submission preparation. The hosted Sites preview was documented as private. Reviewers should use the prototype included in the repository ZIP. YouTrack access must be checked with the intended reviewers; access from the author’s account alone does not establish committee access.

## Next development work

Set up Django and the database, implement accounts and specialist search, then build the request and review workflow. Connect the React interface to the API and run the evaluation plan against the integrated website. Keep later results tied to the version that was evaluated.
