# Existing System Comparison

Project: Car Repair Platform  
Author: Dastan  
Research date: 18 October 2026  
Status: Initial comparison based on public sources

## Purpose and Method

This document compares three existing services against eight criteria relevant to finding car repair specialists and evaluating customer reviews. It uses public product pages and official help articles. No repair was booked and no authenticated customer workflow was tested.

“Documented” means that an official source describes the feature or displays it. “Not established” means the reviewed sources do not provide sufficient evidence; it does not mean the feature is absent. Proposed platform features are plans, not implemented capabilities.

## Selected Systems

- **Profi.kz:** a specialist marketplace with car repair listings for Astana. It is relevant to individual specialist discovery and customer requests. The city label does not independently establish the location of every displayed specialist or review. [P1, P2]
- **2GIS:** a business directory and map service relevant to finding local workshops and comparing their reputations. Its review guidance describes mechanisms for confirming customer experience. [G1, G2, G3]
- **ClickMechanic:** an automotive booking platform used here as an international reference. Its UK location pages and booking-linked reviews provide a relevant comparison; availability in Kazakhstan is not claimed. [C1, C2, C3]

Remontista was considered, but its official website could not be retrieved during this review. ClickMechanic was selected because its official documentation provides inspectable evidence about booking and review eligibility.

## Comparison Matrix

| Criterion | Profi.kz | 2GIS | ClickMechanic | Proposed platform |
|---|---|---|---|---|
| 1. Location-based discovery | Documented: Astana-specific car repair listings. [P1] | Documented: searches can specify a street or location; Kazakhstan search results are available. [G1, G6] | Documented: location pages and postcode-based booking. [C2, C3] | Planned: city filter. |
| 2. Discovery by repair service | Documented: repair categories and task descriptions. [P1, P2] | Documented: searches by service or business category. Dedicated filter coverage varies and was not tested. [G1] | Documented: selection of repair, servicing, diagnostics and other work. [C2] | Planned: service-type filter. |
| 3. Specialist or workshop profiles | Documented: specialist listings with contact options, ratings and reviews. [P1] | Documented: company cards contain business reviews. [G2] | Documented: mechanic profile includes experience, qualifications and booking history. [C4] | Planned: profile with services, location and description. |
| 4. Service request or booking | Documented: customers create requests and specialists respond. [P2] | A complete car-repair booking workflow was not established from the reviewed sources; availability may depend on the business or integration. | Documented: online booking, date and location selection, and mechanic acceptance. [C2, C5] | Planned: request submission, acceptance and status tracking. |
| 5. Customer reviews | Documented: published customer feedback. [P1] | Documented: authorised users can submit reviews and scores. [G2] | Documented: reviews include service information and quality, punctuality and communication scores. [C1] | Planned: text review and score from 1 to 5. |
| 6. Verification of service experience | A mandatory customer-confirmed completion gate was not established from the reviewed Kazakhstan pages. This is not evidence that verification is absent. | Documented: visit or purchase confirmation can be requested; unconfirmed reviews can be separated. Not equivalent to requiring every review to follow an in-platform repair request. [G3] | Documented: the site states that reviews are from paying customers who booked through the platform. The exact two-party confirmation rule proposed here was not established. [C1, C2] | Planned: only the request owner may review after customer confirmation of completion; one review per request. |
| 7. Rating and review volume | Documented: specialist scores and review counts are displayed; the calculation formula was not established. [P1] | Documented: rating uses factors including recency, quantity and confirmation; it is not a simple arithmetic mean. [G4] | Documented: mechanic profile displays a score and rating count; the aggregate formula was not established. [C4] | Planned: arithmetic mean of published verified scores, count displayed, and “Not yet rated” for zero reviews. |
| 8. Complaints or dispute handling | A specific complaint process was not established from the reviewed pages. | Documented: users can report reviews for moderation. [G5] | Documented: support can help customers raise concerns with the mechanic for work booked and paid through the platform. [C2] | Planned: complaint submission and administrator review with recorded decisions. |

## Findings and Design Implications

Existing systems already support specialist discovery and customer feedback. Verification is also an established approach: 2GIS documents confirmation mechanisms, while ClickMechanic explicitly links review eligibility to platform bookings and paying customers. Therefore, verified reviews alone cannot be claimed as a new invention. [G3, G4, C1]

The proposed project will explore a focused workflow for car repair: search, request, acceptance, completion confirmation and review. Its intended engineering contribution is an explicit, testable relationship between a customer, a completed request and a single review. The usefulness of this workflow for the intended users remains a question for interviews and evaluation.

The comparison supports the following initial design decisions:

1. Provide location and service filters because discovery by both is relevant across the compared systems.
2. Show review count beside the rating so users can distinguish scores based on different amounts of feedback.
3. Store the request reference with each review and check ownership and completion status before publication.
4. Document the rating calculation and the treatment of removed reviews.
5. Provide a complaint process because a verified request does not guarantee an honest review or satisfactory repair.

Customer confirmation is evidence of a recorded interaction, not independent proof of repair quality. Collusion, fake requests and disputed completion remain risks. These should be addressed in the requirements and evaluation plan rather than described as solved.

## Limitations and Follow-up

This is a public-source comparison, not a transaction test or a market-wide survey. Product descriptions are provider claims. Features can vary by region, account, device and participating business.

Before the final submission, clarify Profi.kz review eligibility and complaint handling through its official help or support, and check whether selected local 2GIS workshop cards support booking. Record any later findings with their source and date. Unknown entries must not be converted to “No” without evidence.

## Sources

All sources below were reviewed on 18 October 2026.

- **P1:** [Profi.kz — Car repair in Astana](https://profi.kz/remont/avtoremont/).
- **P2:** [Profi.kz — Car repair specialist registration and request workflow](https://profi.kz/registration/remont/avtoremont/).
- **G1:** [2GIS — How to find an organisation or place](https://help.2gis.ru/question/kak-nayti-dom-organizaciyu-ili-mesto).
- **G2:** [2GIS — How to leave a company review](https://help.2gis.ru/question/kak-ostavit-svoy-otzyv-k-kompanii).
- **G3:** [2GIS — Unconfirmed reviews and confirmation of a visit or purchase](https://help.2gis.ru/question/kuda-propal-otzyv).
- **G4:** [2GIS — How company ratings are calculated](https://help.2gis.ru/question/otkuda-beryotsya-reyting-kompaniy).
- **G5:** [2GIS — Writing and reporting reviews](https://help.2gis.ru/question/kak-napisat-horoshiy-otzyv).
- **G6:** [2GIS Kazakhstan — Car service search in Astana](https://2gis.kz/kk/astana/search/%D0%90%D0%B2%D1%82%D0%BE%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D1%8B-%D1%8D%D1%81%D1%82%D0%B0%D0%BA%D0%B0%D0%B4%D1%8B).
- **C1:** [ClickMechanic — Customer reviews and review eligibility](https://www.clickmechanic.com/reviews).
- **C2:** [ClickMechanic — How it works](https://www.clickmechanic.com/how-it-works).
- **C3:** [ClickMechanic — Stanmore location page](https://www.clickmechanic.com/locations/stanmore).
- **C4:** [ClickMechanic — Example mechanic profile](https://www.clickmechanic.com/mechanics/525/rj-mobile-auto-services).
- **C5:** [ClickMechanic — Booking acceptance and confirmation](https://www.clickmechanic.com/help/articles/56/how-long-does-it-take-before-my-booking-is-confirmed).
