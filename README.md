# Fairness and Bias in AI

## Introduction

This repository brings together a set of applied fairness studies that look at AI risk from different angles: model evaluation, lending decisions, facial recognition, protected attributes, and data bias. The common thread is that a model can be technically accurate and still create uneven or harmful outcomes.

The work here treats fairness as a system-level engineering problem. That means looking beyond model architecture and asking who is represented in the data, what the labels really measure, how errors are distributed across groups, how thresholds affect decisions, and what governance is needed when a model operates in a high-stakes setting.

The repository is organized around five use cases. Together they show how fairness issues can enter before training, during model development, at decision time, and through the human processes built around an AI system.

## Repository Map

| Use case | What it examines | Core takeaway |
|---|---|---|
| **[FairBank lending case](https://github.com/saels/fairness-and-bias/tree/53a9f95ac2f1e5cfaec12d6806497a123a631e4c/fairbank_case)** | Fairness in automated small-loan approval, including demographic parity, opportunity parity, thresholds, and governance | A race-blind model can still produce unequal outcomes. Equal overall error rates can hide meaningful differences in who is denied credit incorrectly. |
| **[Repayment model fairness audit](https://github.com/saels/fairness-and-bias/blob/d03e1147d2507e8f158d6ddf4b61da6f54d06637/Repayment_model_fairness_audit/Repayment_model_fairness_audit.ipynb)** | Logistic regression for repayment prediction, subgroup error analysis, and threshold-based fairness mitigation | Removing a protected attribute from training does not guarantee equal treatment. Fairness must be checked in the model's outcomes, and improving one fairness metric can worsen another. |
| **[The Robert Williams case](https://github.com/saels/fairness-and-bias/blob/937dbbc82efd7767c77b86a35002f77ffe64ff34/The_Robert_Williams_case.md)** | A wrongful arrest following a facial-recognition candidate match, poor input quality, and weak human corroboration | Model uncertainty becomes dangerous when it is treated as ground truth. Fairness failures can come from both data imbalance and the decision process around the model. |
| **[Protected attributes and law](https://github.com/saels/fairness-and-bias/blob/871a1e19a9efe6dfacb0442e03a6c1c73d910d04/Protected_attributes_and_law.md)** | Sensitive and protected information, proxy variables, and differences across Peru, the EU, and the US | Fairness engineering has a legal context. Protected attributes can also be reconstructed indirectly from proxies, so simply removing a field may not remove the risk. |
| **[Representation vs. measurement bias](https://github.com/saels/fairness-and-bias/blob/82a8ae8db9e99b212b4871c7eba2794ef4243619/Representation_vs_Measurement_bias.md)** | The difference between who is represented in a dataset and what the dataset is actually measuring | Representation bias and measurement bias require different fixes. More data does not solve a bad proxy, and a better label does not solve an unrepresentative population. |

## FairBank Lending Case

The FairBank case asks a deceptively simple question: if a lending model does not use race, can its decisions still be unfair?

FairBank's small-loan model uses a common approval threshold and does not include race or gender as model inputs. At first glance, that looks neutral. The audit tells a more complicated story. Approval rates differ materially between White and Black applicants, while the model's **overall error rate is 16% for both groups**. Looking only at aggregate error would therefore suggest parity.

The disparity becomes visible when the errors are separated by type. Among applicants who would have repaid their loans, **18% of White applicants are denied compared with 30% of Black applicants**. The case demonstrates why subgroup error analysis matters: a single accuracy number can conceal who bears the cost of model mistakes.

The accompanying memorandum moves the discussion from diagnosis to governance. It recommends an independent audit, legal review before changing decision thresholds, investigation of alternative credit signals and proxy variables, a manual-review path for borderline decisions, outreach to underserved applicant pools, and recurring fairness monitoring.

## Repayment Model Fairness Audit

The notebook turns fairness concepts into a model-evaluation workflow. A logistic regression predicts repayment probability while **Gender is excluded from the training formula** and retained only for the fairness audit.

The initial decision threshold is selected to achieve an overall true-positive rate of at least 60%. At that threshold, the notebook records an overall TPR of **0.603** and accuracy of **0.67**. The group-level audit then reveals a gap: female applicants have a TPR of **0.57**, while male applicants have a TPR of **0.68**.

A second step explores group-specific thresholds to bring opportunity rates closer together. The resulting TPRs move to **0.65 for female applicants and 0.63 for male applicants**, but the false-positive rates move apart. This is an important engineering lesson: fairness is not a single scalar objective. Equalizing opportunity can change risk, accuracy, and other error rates, so the choice of fairness metric has to be tied to the real harm and reviewed with legal and business stakeholders.

## The Robert Williams Case

The Robert Williams case focuses on a different type of high-stakes AI failure. A low-quality surveillance image was submitted to a facial-recognition system, which returned Williams as a candidate match. The subsequent human process did not provide an effective safeguard: the model output shaped the photo lineup, independent corroboration was weak, and Williams was arrested before the case was dropped.

The case highlights two layers of risk. The first is technical: performance can vary across demographic groups when training data is unbalanced, and poor-quality inputs can further reduce reliability. The second is procedural: even a probabilistic system becomes dangerous when users treat a candidate match as if it were a verified identification.

For machine learning engineers, the lesson is that fairness controls cannot end at model evaluation. High-stakes systems need input-quality gates, subgroup performance reporting, clear uncertainty communication, and operational rules that require independent evidence before action is taken.

## Protected Attributes and Law

The legal review compares protected or sensitive information across Peru, the European Union, and the United States. The exact legal frameworks differ, but the engineering concern is consistent: characteristics such as race, ethnicity, health information, sex-related information, and other protected categories require careful handling in automated decision systems.

The document also makes an important point about **proxy variables**. A model may omit a protected attribute while still reconstructing part of it through fields such as ZIP code, language, school, name, employment history, or other correlated signals. This is why a feature can be predictive and still be difficult to justify for a particular use case.

This material is included as a fairness-engineering study, not as legal advice. Production decisions involving protected attributes should be reviewed under the law and regulatory guidance that apply to the specific jurisdiction and business process.

## Representation vs. Measurement Bias

Representation bias and measurement bias are related, but they are not the same problem.

**Representation bias** asks whether the training data adequately covers the people, contexts, or behaviors the model will encounter. If a group is rare or absent in training data, aggregate performance can look acceptable while that group experiences much higher error rates.

**Measurement bias** asks whether the features and labels actually measure the concept the model is supposed to learn. Historical arrests used as a proxy for criminal behavior, healthcare spending used as a proxy for clinical need, or engagement used as a proxy for content quality can encode prior structural conditions into the target itself.

The distinction matters because the mitigations are different. Representation problems call for better coverage, sampling, and subgroup evaluation. Measurement problems require questioning the proxy, label, data-generation process, and sometimes the business objective itself.

## Importance of Fairness and Bias in AI

Fairness is not an optional layer added after a model reaches an acceptable accuracy score. In decision systems, the distribution of errors can affect access to credit, employment, healthcare, public services, or personal liberty. A model can therefore meet a conventional performance target while still creating unacceptable outcomes for a subgroup.

Across the projects in this repository, several recurring engineering principles emerge:

- **Aggregate metrics are not enough.** Accuracy, AUC, or total error should be disaggregated across relevant groups and intersections.
- **Fairness can fail without explicit use of a protected attribute.** Proxy variables, historical patterns, and different feature distributions can reproduce disparities indirectly.
- **The label itself can be biased.** If the target is a poor proxy for the real outcome, better modeling can make the wrong objective more efficient rather than more fair.
- **Fairness metrics involve trade-offs.** Improving equal opportunity, demographic parity, false-positive parity, calibration, or another criterion can change business risk and other fairness measures.
- **Human processes are part of the system.** Review workflows, escalation rules, documentation, and how users interpret a model output can reduce or amplify harm.
- **Monitoring must continue after deployment.** Population drift, policy changes, and changing data sources can alter subgroup performance over time.

## What This Repository Demonstrates

From an engineering perspective, this repository shows how I approach fairness as part of the model lifecycle: define the harm, inspect the data-generating process, keep protected attributes available for controlled auditing when appropriate, evaluate subgroup metrics, make threshold trade-offs explicit, document limitations, and connect technical findings to governance decisions.

The notebook contains the hands-on modeling workflow. The case documents provide the surrounding business, legal, and operational context that determines whether a technically reasonable model is actually responsible to deploy.

> **Note:** The legal material in this repository is educational work and should not be treated as legal advice.
