# Technology Comparison and Selection

Status: Selected for initial implementation; supervisor review pending.

## Context and criteria

This is an individual diploma project for a browser-based car repair specialist platform. The author selected Python for the backend. The main workflow is specialist search, a service request, customer confirmation and one verified review per completed request.

The choices below are design judgments based on official documentation and project scope, not benchmark results. Criteria are implementation effort for one developer, support for the required workflows, data integrity, maintainability, learning effort and deployment complexity. No claim is made about the author's existing proficiency.

## Selected stack

| Component | Choice | Responsibility |
|---|---|---|
| Frontend | React + TypeScript | Public pages, customer and specialist dashboards, forms and API interaction |
| Frontend tooling | Vite | Development server and production asset build |
| Backend | Python + Django + Django REST Framework (DRF) | Accounts, API endpoints, permissions and business rules |
| Database | PostgreSQL | Persistent relational data and integrity constraints |
| Internal administration | Django Admin | Staff management of records and complaint/moderation workflows, with custom actions |
| Communication | HTTP API with JSON over HTTPS in deployment | Communication between the React interface and Django backend |

TypeScript and Vite have different responsibilities and are used together. Vite supports a React TypeScript template; TypeScript types do not replace server validation. [React TypeScript guide](https://react.dev/learn/typescript), [Vite guide](https://vite.dev/guide/).

## 1. Frontend decision

| Option | Advantages for this project | Costs and limitations | Decision |
|---|---|---|---|
| React + TypeScript + Vite | Reusable components for profiles, requests and dashboards; typed interface models; separate API client | Requires routing, form handling and API error handling decisions; separate frontend build; learning TypeScript | Selected |
| Vue + TypeScript + Vite | Component-based interface with declarative templates; can implement the same workflows | Would require learning Vue conventions; no demonstrated project-specific advantage over the selected React approach | Valid alternative |
| Django Templates + JavaScript | Pages and backend can live in one application; fewer separate build/deployment concerns | Interactive dashboards require additional JavaScript; changes the chosen separation between React and the API | Simpler alternative, not selected |

React was selected to support the planned interactive interface and the author's preferred frontend direction. Django Templates would be a reasonable choice if reducing the number of technologies becomes the priority. Vue is also capable of this scope; the comparison does not establish a universal winner. [Vue introduction](https://vuejs.org/guide/introduction), [Django overview](https://www.djangoproject.com/start/overview/).

The current standalone HTML prototype remains a design reference. It has not yet been converted to React. Search-engine visibility for public specialist pages should be reviewed before public launch; server rendering is not a requirement of the initial prototype.

## 2. Backend decision

| Option | Advantages for this project | Costs and limitations | Decision |
|---|---|---|---|
| Python + Django + DRF | Django provides ORM, migrations, authentication tools and admin; DRF supports API implementation | Must learn Django/DRF conventions and implement request ownership, transitions and review eligibility explicitly | Selected |
| Java + Spring Boot | Suitable for a structured API backend and integration with the Spring ecosystem | Requires a Java backend learning path and additional choices for persistence, security and administration; no equivalent project admin is configured automatically | Valid alternative, not selected after choosing Python |
| Python + FastAPI | API-focused approach with validation and API documentation tools | Requires separate choices and integration for persistence, migrations, accounts and a staff administration interface | Valid alternative; more integration decisions for this scope |

Django + DRF was chosen because accounts, relational records and administration are central to the project. Reusing these tools is expected to reduce integration work for one developer; this is an estimate, not measured development time. [Django](https://www.djangoproject.com/start/), [DRF](https://www.django-rest-framework.org/), [Spring Boot](https://spring.io/projects/spring-boot), [FastAPI features](https://fastapi.tiangolo.com/features/).

Django Admin will be restricted to authorised staff. Customer and specialist interfaces will be built in React. Complaint decisions need recorded reasons and controlled actions; an unrestricted record-editing screen alone does not implement the moderation requirements.

## 3. Database decision

| Option | Advantages for this project | Costs and limitations | Decision |
|---|---|---|---|
| PostgreSQL | Relational links between accounts, requests and reviews; unique, foreign-key and check constraints; suitable for a shared server database | Requires a database service, credentials, backups and deployment configuration | Selected |
| SQLite | Simple file-based setup; useful for small applications and experiments; supports relational data | One writer at a time per database file; less suitable for the intended concurrent request/review workflow | Not selected as the deployment database |

PostgreSQL fits the project's relational model. Use it in development as well as deployment to reduce differences in database behaviour. SQLite is not inherently unsuitable for websites, but PostgreSQL is the chosen baseline here. [PostgreSQL constraints](https://www.postgresql.org/docs/16/ddl-constraints.html), [SQLite usage guidance](https://www.sqlite.org/whentouse.html).

## Business rules still requiring implementation

- Filter private request lists by the authenticated user and check ownership for individual operations.
- Permit only defined request-status transitions; a specialist's completion submission must not replace customer confirmation.
- Accept a review only from the request owner after confirmed completion.
- Enforce one review per request using a non-null unique request reference and use transactions for consistent writes.
- Validate scores from 1 to 5. Calculate ratings from published eligible reviews and show the review count.
- Record moderation reasons and preserve history. A negative score alone is not grounds for removal.

DRF requires deliberate object-permission checks and queryset filtering; installing it does not automatically enforce these rules. [DRF permissions](https://www.django-rest-framework.org/api-guide/permissions/). Database constraints complement backend logic: a normal check constraint cannot validate another table's completion status.

## Consequences and next steps

The selected stack is suitable for the planned scope, but requires learning Python/Django, React and TypeScript and maintaining separate frontend and backend builds. It does not by itself guarantee security, usability or performance.

The initial [database design and ER diagram](database-design.md) is documented. Next: define the API contract, choose compatible supported versions and pin dependencies when implementation starts. Authentication/session configuration, hosting and deployment remain to be documented. No production implementation, benchmark or acceptance testing is claimed by this decision record.

Related documents: [Requirements](requirements.md), [Architecture diagrams](diagrams/README.md), [Prototype](prototype/README.md).
