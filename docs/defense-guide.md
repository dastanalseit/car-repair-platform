# First pre-defense guide

## Prepare the demonstration

Open the [tagged repository](https://github.com/dastanalseit/car-repair-platform/tree/pre-defense-1), [submission summary](submission-summary.md), [YouTrack project](https://dastan-car-repair.youtrack.cloud/projects/CRP) and the local prototype before presenting. Download the repository ZIP and keep the prototype HTML files and theme.css together. Open `docs/prototype/ru.html` or `docs/prototype/kk.html` in a browser.

Ask the supervisor or a committee member to open the repository and YouTrack links from their own account before the session. The hosted preview may require owner access, so use the repository copy for the demonstration.

## Suggested presentation order

1. Explain the problem: drivers need to compare suitable repair specialists, while a high rating alone gives limited evidence about the repair experience.
2. State the scope: a website for specialist search, service requests, completion confirmation and reviews. Contracts, payments and a native mobile app are outside the first version.
3. Show the six driver summaries. Explain that interviews were individual conversations through Threads and WhatsApp and that participants agreed to anonymous use. Include P3’s view that personal recommendations make the website less useful to them.
4. Show the literature table and local-market section. Explain why technical repair quality can remain difficult for a customer to assess. Identify the changes made after supervisor feedback.
5. Show the system comparison and explain one technology choice, such as Django for accounts, relational records and administration.
6. Open the context, use case and component diagrams. Follow one customer request through the planned components.
7. Demonstrate search, a request, specialist completion, customer confirmation and a review using the prototype guide. Explain the role switch and fictional data before using them.
8. Open CRP-3, follow its PR 10 link, and show the supervisor’s comment, resulting document change and merge history.
9. Explain the evaluation baseline and metrics. Finish with the implementation work that remains.

## Short answers to likely questions

**What is verified?** A published review must belong to the customer who owns the completed, customer-confirmed request. This is evidence of a recorded interaction. It does not certify the mechanical work.

**How do you handle negative experiences?** Customers can leave low scores after confirmation. Disputes and complaints cover disagreements about completion. The design must account for dissatisfied customers whose requests never reach confirmation.

**Why this project if other platforms have reviews?** The project studies a specific request-to-review workflow for car repair. Its value must be evaluated locally; verified reviews themselves are already used by existing systems.

**What did the interviews establish?** They describe six drivers’ experiences and preferences. They inform the requirements but cannot estimate what all drivers want or how common dishonest repairs are.

**Is the website finished?** The interface prototype and analysis documents are available. The production backend, persistent data and integrated website still need implementation and evaluation.

**What is your contribution?** This is an individual project. Be ready to explain the research decisions, scope, diagrams, requirements and each demonstrated interaction using your own understanding.
