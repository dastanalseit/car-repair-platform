# Car Repair Platform

**Diploma project:** Development of a Platform for Finding Car Repair Specialists with a Rating System Based on Verified Customer Reviews.

## Overview

The project will be delivered as a responsive website accessible through a web browser on computers and smartphones. Users will not need to install a separate application. Registration, specialist search, personal accounts, service requests, reviews, and ratings will be available through the website.

Car Repair Platform is a planned website that will help car owners find repair specialists, request services, and compare specialists using ratings based on verified customer reviews.

A verified review will be linked to a service request that has been completed and confirmed by the customer. This confirms the review’s connection to a recorded service request; it does not guarantee the quality of the service or eliminate all fraudulent activity.

## Problem Statement

Initial informal discussions with drivers raised concerns about repair quality and the risk of being misled when choosing repair specialists.

These discussions provide preliminary observations rather than formal research findings. Further user interviews and analysis of existing systems will be used to refine the problem statement and requirements.

## Aim

To develop a web platform for finding car repair specialists, requesting repair services, and evaluating specialists through a rating system based on reviews linked to completed and customer-confirmed service requests.

## Objectives

1. Investigate how car owners find and evaluate repair specialists.
2. Review relevant literature and compare existing platforms.
3. Define functional and non-functional requirements with acceptance criteria.
4. Compare technology alternatives and justify the selected technologies.
5. Design the system architecture, database, and user interface.
6. Implement specialist search, service requests, and verified customer reviews.
7. Evaluate the platform’s functionality and usability.

## Target Users

- **Car owners:** search for specialists, submit service requests, confirm service completion, and leave reviews.
- **Car repair specialists:** manage profiles and service listings, accept requests, and update service statuses.
- **Platform administrators:** review complaints and manage content that violates platform rules.

## Planned Features

- User registration and login
- Role-based access for customers, specialists, and administrators
- Specialist profiles with services, location, and descriptions
- Search and filtering by city and service type
- Sorting specialists by rating
- Service request submission and status tracking
- Customer confirmation of service completion
- One review and a score from 1 to 5 per eligible service request
- Specialist ratings displayed alongside the number of verified reviews
- Basic complaint management

## Proposed Review Verification Workflow

1. A customer submits a service request to a specialist.
2. The specialist accepts the request.
3. After performing the service, the specialist marks it as awaiting customer confirmation.
4. The customer confirms that the service has been completed.
5. The customer can submit one review and a rating for that request.

Only the customer associated with the eligible service request can review it. Reviews cannot be submitted for incomplete requests or for requests belonging to another customer.

The initial rating calculation will use the arithmetic mean of published verified review scores. Specialists without reviews will be shown as “Not yet rated.”

This workflow is an initial design proposal and may be refined during requirements analysis.

## Project Scope

The initial version will focus on the main workflow:

**Find a specialist → Submit a service request → Confirm completion → Leave a verified review**

The project will deliver a website with customer, specialist, and basic administrator functionality.

The following features are outside the initial scope:

- Online payments
- Real-time chat
- Native mobile applications
- Automated specialist recommendations
- Independent verification of repair quality

## Expected Outcomes

- A working website covering the main user scenarios
- A documented review verification mechanism
- Architecture diagrams and database design
- An interface prototype
- Verification and evaluation results
- A traceable development history linked to project tasks

## Author and Supervisor

- **Author:** Dastan
- **Supervisor:** Botagoz Mirzagalikova

This is an individual diploma project. Dastan is responsible for research, requirements analysis, design, implementation, testing, and documentation.

Significant deliverables and design decisions will be reviewed with the supervisor at agreed checkpoints.

## Current Development Status

**Stage:** Requirements and initial interface/system design.

The proposal, literature review, comparisons, requirements, diagrams, database/API designs, evaluation plan and project plan are available as drafts. A clickable Russian/Kazakh interface prototype is available.

**Intentionally pending:** interview records, interview findings and supervisor feedback remain blank. No supervisor approval or completed user study is claimed. The production website and backend have not been implemented; evaluation results are not yet available.

## Technologies

Selected technology stack:

| Component | Technology |
|---|---|
| Frontend | React + TypeScript + Vite |
| Backend | Python + Django + Django REST Framework |
| Database | PostgreSQL |
| Internal administration | Django Admin |
| Communication | HTTP API with JSON; HTTPS in deployment |

See the [technology comparison and selection](docs/technology-comparison.md) for alternatives, reasons and limitations. Exact versions will be pinned when implementation starts. The existing prototype is still standalone HTML; the selected production stack has not yet been implemented.

## Project Documentation

| Document | Current status |
|---|---|
| [Project proposal](docs/project-proposal.md) | Draft for supervisor review |
| [User research](docs/user-research.md) | Questions and procedure prepared; interview records and findings intentionally blank |
| [Literature review and source comparison](docs/literature-review.md) | Draft with 15 sources; full-text appraisal of restricted sources remains pending |
| [Existing system comparison](docs/existing-system-comparison.md) | Draft comparison |
| [Requirements and acceptance criteria](docs/requirements.md) | Initial requirements |
| [Technology comparison and selection](docs/technology-comparison.md) | Proposed production stack and alternatives |
| [Use case, context and component diagrams](docs/diagrams/README.md) | Initial design; editable sources and exports |
| [Database design and ER diagram](docs/database-design.md) | Initial design |
| [API design and permissions](docs/api-design.md) | Initial contract |
| [Prototype guide](docs/prototype/README.md) | Russian/Kazakh demonstration interface |
| [Prototype review notes](docs/prototype/verification-notes.md) | Historical notes; the latest visual revision has not been scenario-tested |
| [Evaluation plan](docs/evaluation-plan.md) | Protocol prepared; results pending |
| [Project plan and risks](docs/project-plan.md) | Stages, responsibilities and risk register; calendar dates not assigned |
| [Supervisor feedback](docs/supervisor-feedback.md) | Intentionally blank until actual feedback is received |

## Remaining Evidence

- Conduct actual driver discussions and complete anonymised interview records and findings.
- Record actual supervisor feedback and resulting revisions.
- Complete outstanding source appraisal and reconcile requirements with research findings.
- Before submission, confirm the required deliverables, reviewer access and scheduling with the supervisor. Create the assessment tag only for the version actually submitted.
- Implement and evaluate the production website during the subsequent development stages.

Document availability does not imply supervisor approval or completion of the full diploma.

## Task Management

**YouTrack project:** [Car Repair Platform (CRP)](https://dastan-car-repair.youtrack.cloud/projects/CRP).

Planning areas: CRP-1 proposal, CRP-2 interviews, CRP-3 literature, CRP-4 design/prototype, CRP-5 evaluation and CRP-6 supervisor submission.

Each meaningful task will include:

- Responsible person
- Expected outcome
- Acceptance criteria
- Priority
- Deadline when scheduling is agreed; dates are currently unassigned

Task IDs will be referenced in branch names and commit or pull request descriptions. Relevant commits or pull requests will also be linked from YouTrack.

## Development Workflow

- Maintain the same repository throughout the diploma project.
- Record meaningful changes progressively with descriptive commit messages.
- Develop changes in separate task or feature branches.
- Submit changes through pull requests, describing the task and how the work was checked.
- Keep `main` as the consolidated project baseline; supervisor review is recorded separately.
- Arrange supervisor review of selected significant changes at agreed checkpoints.
- Record documentation and design changes alongside code changes.

## Verification and Evaluation Plan

See the [evaluation plan](docs/evaluation-plan.md) for requirement-linked cases, participant tasks, the comparison baseline, metrics and proposed acceptance targets. Related task: [CRP-5](https://dastan-car-repair.youtrack.cloud/issue/CRP-5). The plan is a draft; evaluation has not been conducted.

Planned checks include:

- Search results match the selected filters.
- Users can perform only actions permitted for their role.
- Service requests follow the defined status transitions.
- Reviews are allowed only after customer-confirmed service completion.
- Users cannot review another customer’s request.
- Duplicate reviews for the same request are prevented.
- Specialist ratings are calculated correctly.
- Representative users can complete the main platform workflows.

The detailed plan proposes metrics, measurement conditions and a baseline for comparison. Confirm the protocol before evaluation begins.

## Setup, Execution, and Testing

Download the repository ZIP or clone the repository, then open `docs/prototype/ru.html` (Russian) or `docs/prototype/kk.html` (Kazakh). Keep the HTML files and `theme.css` together. The prototype uses fictional data held in memory and requires no installation. See the [prototype guide](docs/prototype/README.md) for the walkthrough and local-server option.

[Hosted preview](https://autosenim-dastan-prototype.magic-coin-2293.chatgpt.site/ru) — currently private and owner-only; use the repository copy for a reviewer who cannot access Sites.

Production application code is not yet available.

Installation, configuration, execution, and testing instructions will be added when implementation begins. Configuration examples will use placeholder values. Passwords, API keys, and other confidential data must not be committed.

## Submission Milestones

The following Git tags are planned for versions submitted for assessment. They are not created by this documentation cleanup:

- `pre-defense-1`
- `pre-defense-2`
- `final-pre-defense`

Each submission will include the repository link, submission tag, completed work summary, known limitations, and outstanding tasks.

