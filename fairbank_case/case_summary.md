# FairBank Case Summary

## Business objective

Scale small-loan approvals while improving repayment prediction and controlling staffing cost.

## Model decision

Approve applicants whose loan-worthiness score exceeds a common threshold.

## Protected attribute

Race is not used by the approval model, but is available from third-party data for fairness analysis.

## Central question

Can a model be unfair even when it is race-blind and has the same overall error rate across racial groups?

## Executive summary

FairBank introduced an automated small-loan approval model to improve repayment prediction, expand lending volume, and free experienced loan officers for larger accounts. The model uses a loan-worthiness metric and applies the same approval threshold to every applicant. Race and gender are not model inputs.

The fairness review shows why that design is not sufficient on its own. White applicants are approved at a higher rate than Black applicants, yet the overall classification error rate is 16% for both groups. The disparity becomes visible only after separating the two error types: among applicants who would have repaid, 18% of White applicants are denied compared with 30% of Black applicants. The case therefore shifts the question from “Does the model use race?” to “Who experiences the model’s mistakes?”

## Business context

FairBank’s automation project has a clear commercial rationale. More accurate repayment estimates can improve the economics of small loans, while automation lets the bank grow the portfolio without increasing staffing at the same rate. The same system, however, controls access to credit. That makes the distribution of errors a customer, compliance, and reputation issue rather than a modeling detail.

The model uses applicant information such as debt, monthly income, loan-to-discretionary-income ratio, and repayment history to create a loan-worthiness score. Applicants above the chosen threshold are approved; applicants below it are denied.

## Fairness audit findings

| Metric | All applicants | White applicants | Black applicants |
|---|---|---|---|
|Approval rate	| 43% |	54%	| 32% |
|Overall error rate |	16% |	16% |	16% |
|Would repay but denied |	23% |	18% |	30% |
|Would default but approved |	10% |	13% |	8% |

The headline accuracy result is misleading by itself. White and Black applicants have the same total error rate, but the errors are distributed differently. The largest customer-impact gap is the false-negative side of the decision: repay-capable Black applicants are denied more often than repay-capable White applicants.

## Why a race-blind model can still produce disparity

•	A single threshold interacts with different loan-worthiness score distributions across groups. Equal treatment of scores does not automatically produce equal error rates.

•	Historical and socioeconomic conditions can affect the variables used to build the score, so a protected attribute can matter indirectly even when it is absent from the model.

•	Proxy variables or legacy training patterns can preserve past disparities without an explicit race field.

•	Overall accuracy can hide which group bears each type of mistake. Fairness analysis has to separate false negatives from false positives.

## The decision trade-offs

The case does not offer a cost-free mitigation. Lowering the threshold for one group could improve opportunity parity but may increase defaults, reduce profitability, and raise questions about individual fairness. Using race directly in a threshold policy also creates legal and regulatory concerns. Keeping one threshold avoids those concerns but leaves the observed opportunity gap in place.

This is the core management problem: the bank has to define which harms it is trying to reduce, understand the trade-offs between them, and choose a policy that is defensible technically, legally, and commercially.

## Recommended action plan

•	Commission an independent algorithmic audit to validate the internal findings and establish a defensible baseline.

•	Review any threshold changes with legal counsel before implementation, especially when a protected attribute could influence the decision rule.

•	Evaluate equal-opportunity interventions alongside manual review for borderline cases, rather than treating threshold adjustment as the only mitigation.

•	Audit current features for proxy effects and investigate alternative credit signals that may measure repayment capacity more directly.

•	Continue outreach to underserved communities to broaden the applicant pool, while recognizing that this is a long-term intervention rather than an immediate fix.

•	Track fairness metrics on a recurring basis, including approval rates and group-specific opportunity/error measures, so progress is visible to management and the board.

## Key takeaway

The FairBank case shows that “not using race” and “being fair” are different claims. A model can be race-blind, equally accurate in aggregate, and still deny qualified applicants from one group more often. Responsible lending ML therefore requires subgroup evaluation, careful threshold design, feature and proxy review, legal oversight, and ongoing monitoring after deployment.

> **Note:** The material is educational fairness analysis, not legal advice.
