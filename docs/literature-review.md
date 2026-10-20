# Literature Review

**Project:** Development of a Platform for Finding Car Repair Specialists with a Rating System Based on Verified Customer Reviews  
**Author:** Dastan  
**Supervisor:** Botagoz Mirzagalikova  
**Related task:** [CRP-3](https://dastan-car-repair.youtrack.cloud/issue/CRP-3)  
**Status:** Draft for review.

## 1. Purpose and review questions

This review examines the evidence behind a website where customers find car repair specialists and publish reviews linked to completed service requests. It addresses four questions:

1. How do reputation systems support decisions in online marketplaces?
2. What does transaction verification establish, and what problems remain?
3. How do rating design, incentives and reviewer participation affect the information displayed?
4. Which findings can inform a feasible individual diploma project?

The central distinction is between a recorded service relationship, the honesty of a review and the technical quality of a repair. The proposed platform can enforce the first through its workflow. It cannot independently establish the other two.

## 2. Selection approach and evidence boundaries

This is a focused narrative review, not an exhaustive systematic review or meta-analysis. Sources were located through web searches directed at scholarly publishers, an author-hosted manuscript and research repositories, then checked against publisher or repository records. Search terms included “verified purchase reviews”, “fake review buyers”, “online reputation systems”, “rating system design”, “incentives to review”, “auto repair reputation” and “automotive after-sales service quality”. Searches also followed relevant references in the retrieved papers. No claim is made that Scopus or Web of Science was searched directly.

The selected set contains **15 scholarly sources: 14 journal publications and one explicitly identified NBER working paper**. Ten sources have publication years from 2022 to 2024. Five earlier works cover foundational reputation and rating mechanisms or directly relevant automotive service evidence. Three articles [13–15] specifically investigate auto repair or automotive after-sales service. Publication years below are bibliographic information, not project deadlines.

Inclusion required a clear connection to review credibility, manipulation, participation, rating design or automotive service quality and enough accessible evidence to identify the method and main finding. News articles, product marketing, duplicate manuscript versions and unrelated detection studies were excluded from the final set. Sources about retail, accommodation and online labour are used as adjacent evidence; they do not establish the prevalence of dishonest repairs in Kazakhstan.

Access varied. Full article text or an author manuscript was available for several works; other entries rely on publisher abstracts and accessible sections. The table records this distinction. Detailed methodological claims are limited accordingly, and full-text appraisal of restricted papers remains a review step before final submission. Limitations and proposed applications in the table are this project's critical assessment unless stated otherwise.

## 3. Critical synthesis

### 3.1 Reputation supports discovery but needs an interpretable basis

Tadelis [1] explains how feedback helps strangers trade while also documenting weaknesses in reputation mechanisms. For this project, a specialist profile should therefore expose the basis of its score: eligible review count, review text and an explanation of eligibility. A score alone cannot demonstrate repair competence.

The meaning of the scale also matters. Garg and Johari [2] study an online labour market and show that changing rating labels can improve informativeness. This supports reviewing how users interpret the proposed one-to-five scale. It does not demonstrate that their alternative scale is automatically suitable for car repair. The existing arithmetic mean remains a simple initial specification; its optimality is not established by this review.

### 3.2 A recorded purchase does not eliminate manipulation

He, Hollenbeck and Proserpio [3] connect observations of fake-review markets to Amazon outcomes and find evidence that manipulation affects sales. Their related network study [4] describes arrangements in which a purchase is reimbursed after a favourable review. This explains why a transaction record alone cannot establish independence.

For the proposed website, one review per confirmed request can block reviews without an eligible platform request and repeated reviews of the same request. Coordinated customers and specialists could still create artificial requests. The verification label must describe the actual check rather than promise that fraud has been eliminated.

Akesson et al. [5] provide experimental evidence that fake reviews can alter choices in a simulated retail setting. Their working paper strengthens the motivation for examining user decisions, but its estimated losses cannot be transferred to local repair services. Sahut, Laroche and Braune [6] frame deceptive reviews as a behavioural and organisational problem as well as a technical one. Together, these works support combining eligibility checks, understandable explanations and complaint handling.

### 3.3 Verification labels have conditional effects

Kakaria, Simonetti and Bigne [7] find that review valence dominates the other studied cues and that a verified-purchase badge has a negligible standalone effect on purchase intention in their experimental settings. Mardumyan and Siret [8] identify conditions in which verification badges are associated with stronger perceptions of manipulation and weaker credibility.

These findings challenge an assumption that adding a badge necessarily increases trust. They do not establish that every verification mechanism fails. The studies use different contexts and measures, and the proposed website adds an enforceable request workflow rather than only a visual label. Its interface should explain that customer confirmation records completion, including an unsatisfactory service. Evaluation should check whether users understand this distinction, rather than treating greater trust as the sole success criterion.

### 3.4 More reviews and higher scores are not sufficient outcomes

Fradkin and Holtz [9] find that an Airbnb review incentive increased participation but did not produce the intended market improvement. Park, Shin and Xie [10] show that disclosing incentives did not eliminate rating inflation in their Amazon setting. These results concern different incentive arrangements, so they should not be combined into a universal claim that all invitations or incentives have the same effect.

The initial repair website will not reward positive reviews. Customer non-response must remain distinguishable from successful completion. A further design concern is selection: people who finish and confirm requests may differ from those whose requests remain disputed. A technically valid rating can therefore still omit important negative experiences. Complaints provide an additional channel, but they do not make the published mean representative of every service attempt.

### 3.5 Perceived credibility and objective authenticity differ

Ko and Bowman [11] examine perceived suspiciousness and show that product and brand signals affect these judgements. Suspicion should therefore not be treated as proof that a review is false. Muchnik, Aral and Taylor [12] demonstrate social influence in a randomized online voting experiment; this is evidence about aggregate-feedback effects, not a direct estimate for five-star repair reviews.

For this project, these findings motivate separating a customer's account of the service from the existing specialist score and recording moderation reasons. A negative score, unfamiliar specialist or unusual writing style is insufficient grounds for removal. Any future automated suspicion score would require independent validation and a way to inspect errors.

### 3.6 Automotive repair: information gaps and customer satisfaction

Schneider [13] reports an undercover garage experiment comparing one-time and potential repeat customers. Both insufficient and unnecessary treatment occurred, while the repeat-business treatment did not significantly improve outcomes. This directly motivates caution about repair reputation, although it did not test online verified reviews. The website should explain that a confirmed request establishes a service relationship, not an independent inspection of repair quality.

Balinado et al. [14] surveyed 256 Toyota service customers in the Philippines. Their structural equation model associated reliability and empathy with satisfaction; the other three SERVQUAL dimensions were not significant. Fathulloh and Purnama [15], using 100 Honda customers in Yogyakarta, reported support for all five dimensions. These differing patterns suggest that service-quality priorities depend on context. Both studies analyse reported perceptions rather than independently inspected repairs, and neither establishes that the proposed website improves service outcomes.

For this project, the automotive evidence supports asking drivers about reliability, explanations and communication during real interviews, and inviting concrete descriptions in review text. These are proposed applications, not validated rating weights. The initial overall score should not be presented as a technical quality certificate; separate dimension scores would require further justification.

## 4. Structured source comparison

“Full text” means the article text was accessible for consultation, not that every statistical result has been independently reproduced. “Publisher sections” means the assessment is limited to the exposed abstract, introduction or other sections.

| ID | Source and evidence consulted | Method / setting | Main contribution | Limitation for this project | Design implication |
|---|---|---|---|---|---|
| [1] | Tadelis (2016); journal review; publisher abstract and author manuscript | Economic synthesis of online marketplace reputation | Explains trust formation and feedback bias | Foundational synthesis; no local repair evaluation | Explain score provenance and feedback rules |
| [2] | Garg & Johari (2021 issue; online 2020); publisher abstract | Randomized labour-market experiment and scale-design model | Rating labels can change information quality | Scale and market differ from repair services; full methods need closer appraisal | Evaluate interpretation of star labels; do not claim the mean is optimal |
| [3] | He, Hollenbeck & Proserpio (2022); publisher abstract | Fake-review market observations, product panel and policy variation | Manipulation can improve seller outcomes temporarily | Amazon context and observed review-buying channels | Treat collusion as a residual risk |
| [4] | He et al. (2022); full text | Product–reviewer networks and classifiers using observed review buyers | Network features outperform comparison feature sets in the study | Large platform data and labels are unavailable for a new repair website | Preserve request relationships; defer machine-learning detection |
| [5] | Akesson et al. (2023); NBER working-paper abstract | Incentive-compatible UK experiment, 10,000 participants | Fake reviews shift choices toward inferior products | Working paper; simulated retail choice, not repair outcomes | Assess choice comprehension; avoid transferring welfare estimates |
| [6] | Sahut, Laroche & Braune (2024); publisher abstract / sections | Multidisciplinary literature synthesis | Connects causes, credibility and consequences of fake reviews | Synthesis is not a benchmark of a particular software mechanism | Combine technical controls with clear moderation policy |
| [7] | Kakaria, Simonetti & Bigne (2024 issue; online 2023); full text | Experiment with 500 US participants; tablets and travel packages | Badge effects interact with other cues; valence is influential | Purchase intention and limited scenarios differ from actual repair selection | Evaluate explanation comprehension alongside perceived trust |
| [8] | Mardumyan & Siret (2023); publisher abstract / sections | 9,219 reviews and two survey-based designs | Badges may reduce credibility under perceived manipulation | Context-specific behavioural evidence; restricted full-text appraisal | Avoid broad authenticity promises |
| [9] | Fradkin & Holtz (2023); publisher article sections | Randomized Airbnb review-coupon experiment | Increased review production did not ensure improved market outcomes | Accommodation and a particular incentive mechanism | Track participation separately from usefulness |
| [10] | Park, Shin & Xie (2023); full text | Amazon review analysis and policy-change comparisons | Incentive disclosure did not remove inflation or its effects | Platform-specific setting; sales-rank proxy and identification assumptions | Do not reward favourable scores; treat disclosure as insufficient alone |
| [11] | Ko & Bowman (2023); publisher abstract / sections | Amazon review analysis with human judgements and machine learning | Brand and product signals affect perceived suspiciousness | Perceived deception is not definitive ground truth | Require evidence and a recorded reason for moderation |
| [12] | Muchnik, Aral & Taylor (2013); indexed journal abstract | Randomized manipulation of ratings on a social news website | Prior aggregate feedback affects later voting | Voting environment and metric differ from service reviews | Consider feedback influence when evaluating the review form |
| [13] | Schneider (2012); publisher abstract | Undercover auto-repair field experiment; matched one-time versus repeat-business treatment | Under- and overtreatment occurred; repeat-business treatment did not significantly improve outcomes | Older experiment; repeat-business reputation differs from online ratings | Distinguish request verification from technical inspection |
| [14] | Balinado et al. (2021); accessible publisher text | 256 Toyota service customers; Philippines; survey and SEM | Reliability and empathy were significantly associated with satisfaction | One dealer; voluntary respondents and reported perceptions | Explore reliability and communication in driver interviews |
| [15] | Fathulloh & Purnama (2024); publisher abstract | 100 Honda customers in Yogyakarta; online questionnaire and PLS-SEM | Reports support for all five SERVQUAL dimensions | Small local brand-specific sample; full methods await appraisal | Check local priorities instead of importing dimension weights |

## 5. Research gap and project contribution

The reviewed work establishes that review systems have multiple weaknesses: manipulation, selective participation, scale interpretation and contextual effects of credibility cues. The automotive studies add evidence on expert-service information gaps and satisfaction, but do not evaluate transaction-linked online reviews. The combined evidence does not demonstrate that the exact proposed request-confirmation workflow improves car repair outcomes in the intended local setting.

The project's contribution is an implementation and evaluation of a bounded mechanism: connect specialist discovery, request ownership, explicit customer confirmation, one-review eligibility, aggregate calculation and complaint history within one website. This is an engineering contribution to be demonstrated, not a claim to have invented transaction-linked reviews or solved review fraud.

The main open questions are whether the workflow is understandable, whether it enforces its eligibility rules and whether users correctly interpret the verification label. Actual driver discussions remain necessary to establish local needs. The literature cannot substitute for those discussions.

## 6. Traceability to requirements and planned evaluation

The following are proposed applications of the evidence, not findings reported by the cited authors. They are consistent with the current requirements; additions require review before becoming implementation commitments.

| Proposed decision | Evidence informing it | Related requirements | Evidence to collect later |
|---|---|---|---|
| Explain that verification means ownership of a completed, customer-confirmed request | [3], [4], [7], [8], [13] | FR-08, FR-09, FR-13 | Ask users what the label proves and what it does not; report correct and incorrect interpretations |
| Enforce one review per eligible request on the server | [1], [3], [4] | FR-09, NFR-02, NFR-04 | Planned cases for wrong owner, unfinished request and simultaneous duplicate submissions |
| Display published review count beside the mean and show an unrated state | [1], [2] | FR-04, FR-10 | Check calculation and user interpretation of small versus larger review counts |
| Allow negative reviews after completion confirmation; keep disputes separate | [8], [9], [10] | FR-08, FR-11, FR-12 | Check whether users confuse confirmation with satisfaction; examine disputed and abandoned paths |
| Record moderation decisions and update aggregates consistently | [6], [11] | FR-10, FR-12, FR-13 | Planned checks for hidden-review exclusion and retained decision history |
| Keep automated fraud classification outside the initial implementation | [4], [11] | Scope boundary | Document residual threats and the absence of a validated local labelled dataset |
| Compare interface understanding using equivalent specialist information | [5], [7], [12] | Evaluation-plan input | Keep task and information constant; vary the verification explanation; measure comprehension, task success and time |
| Use concrete repair-experience prompts in interviews and review-form evaluation | [13], [14], [15] | FR-09; interview and evaluation inputs | Check whether drivers distinguish service experience, satisfaction and technical repair quality |

The final evaluation plan must specify participants, conditions, baseline, metrics and analysis before collecting results. Functional enforcement and user understanding should be reported separately. An increase in perceived trust without correct understanding would not, by itself, demonstrate success. No tests or user study have been conducted as part of this literature review.

## 7. Limitations and review actions

- The selection is focused and non-exhaustive. Publisher accessibility may have affected which studies could be appraised in detail.
- The automotive studies concern garages or branded after-sales services, not the intended local specialist marketplace; their methods and contexts differ.
- Most review-system evidence comes from established international platforms. Language, market size and repair-service characteristics may affect transferability.
- Several works use related Amazon settings; they should not be treated as wholly independent evidence for every conclusion.
- A confirmed request may be fabricated through collusion, while an honest dissatisfied customer may never reach the confirmation step. Both risks need explicit treatment.
- Consult the complete restricted articles through lawful university access where available, and refine the methodological assessment before submission.
- Ask the supervisor to review the evidence selection and proposed evaluation questions. Supervisor approval has not been recorded.

## 8. References

Numbered references are used throughout. Publication years distinguish source versions; online-first and journal-issue years are stated where they differ.

1. Tadelis, S. (2016). Reputation and feedback systems in online platform markets. *Annual Review of Economics, 8*, 321–340. [Publisher / DOI](https://doi.org/10.1146/annurev-economics-080315-015325). [Author manuscript](https://faculty.haas.berkeley.edu/stadelis/Annual_Review_Tadelis.pdf).
2. Garg, N., & Johari, R. (2021; online 2020). Designing informative rating systems: Evidence from an online labor market. *Manufacturing & Service Operations Management, 23*(3), 589–605. [Publisher / DOI](https://doi.org/10.1287/msom.2020.0921).
3. He, S., Hollenbeck, B., & Proserpio, D. (2022). The market for fake reviews. *Marketing Science, 41*(5), 896–921. [Publisher / DOI](https://doi.org/10.1287/mksc.2022.1353).
4. He, S., Hollenbeck, B., Overgoor, G., Proserpio, D., & Tosyali, A. (2022). Detecting fake-review buyers using network structure: Direct evidence from Amazon. *Proceedings of the National Academy of Sciences, 119*(47), e2211932119. [DOI](https://doi.org/10.1073/pnas.2211932119). [Full text](https://pmc.ncbi.nlm.nih.gov/articles/PMC9704690/).
5. Akesson, J., Hahn, R. W., Metcalfe, R. D., & Monti-Nussbaum, M. (2023). *The impact of fake reviews on demand and welfare*. NBER Working Paper 31836. Working-paper version, not presented here as a peer-reviewed journal article. [Repository / DOI](https://www.nber.org/papers/w31836).
6. Sahut, J. M., Laroche, M., & Braune, E. (2024). Antecedents and consequences of fake reviews in a marketing approach: An overview and synthesis. *Journal of Business Research, 175*, 114572. [Publisher / DOI](https://doi.org/10.1016/j.jbusres.2024.114572).
7. Kakaria, S., Simonetti, A., & Bigne, E. (2024; online 2023). Interaction between extrinsic and intrinsic online review cues: Perspectives from cue utilization theory. *Electronic Commerce Research, 24*, 2469–2497. [Publisher / full text](https://link.springer.com/article/10.1007/s10660-022-09665-2).
8. Mardumyan, A., & Siret, I. (2023). When review verification does more harm than good: How certified reviews determine customer–brand relationship quality. *Journal of Business Research, 160*, 113756. [Publisher / DOI](https://doi.org/10.1016/j.jbusres.2023.113756).
9. Fradkin, A., & Holtz, D. (2023). Do incentives to review help the market? Evidence from a field experiment on Airbnb. *Marketing Science, 42*(5), 853–865. [Publisher / DOI](https://doi.org/10.1287/mksc.2023.1439).
10. Park, S., Shin, W., & Xie, J. (2023). Disclosure in incentivized reviews: Does it protect consumers? *Management Science, 69*(11), 7009–7021. [Publisher / full text](https://pubsonline.informs.org/doi/10.1287/mnsc.2023.00930).
11. Ko, E. E., & Bowman, D. (2023). Suspicious online product reviews: An empirical analysis of brand and product characteristics using Amazon data. *International Journal of Research in Marketing, 40*(4), 898–911. [Publisher / DOI](https://doi.org/10.1016/j.ijresmar.2023.06.006).
12. Muchnik, L., Aral, S., & Taylor, S. J. (2013). Social influence bias: A randomized experiment. *Science, 341*(6146), 647–651. [DOI](https://doi.org/10.1126/science.1240466). [Indexed abstract](https://pubmed.ncbi.nlm.nih.gov/23929980/).
13. Schneider, H. S. (2012). Agency problems and reputation in expert services: Evidence from auto repair. *The Journal of Industrial Economics, 60*(3), 406–433. [Publisher / DOI](https://doi.org/10.1111/j.1467-6451.2012.00485.x).
14. Balinado, J. R., Prasetyo, Y. T., Young, M. N., Persada, S. F., Miraja, B. A., & Perwira Redi, A. A. N. (2021). The effect of service quality on customer satisfaction in an automotive after-sales service. *Journal of Open Innovation: Technology, Market, and Complexity, 7*(2), 116. [DOI](https://doi.org/10.3390/joitmc7020116). [Publisher text](https://www.mdpi.com/2199-8531/7/2/116).
15. Fathulloh, M. A., & Purnama, N. (2024). Assessing customer satisfaction in automotive after-sales service: A SERVQUAL analysis. *Asian Journal of Economics, Business and Accounting, 24*(9), 98–110. [DOI](https://doi.org/10.9734/ajeba/2024/v24i91479). [Publisher abstract and PDF access](https://journalajeba.com/index.php/AJEBA/article/view/1479).
