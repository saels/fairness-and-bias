# Protected attributes and law

## Why are protected attributes important to avoid in your models?

It is important to avoid using protected attributes in models for legal and ethical reasons. Many entities prohibit using these attributes in credit, employment or insurance to avoid unfair impacts because of the data. Even when these attributes could be legal to use in your area, using them can amplify historical discrimination, producing systematically worse outcomes for certain groups regardless of intent.

As I live in Peru, I have researched our laws and compare them to the US and EU data protection laws. Peru has the law 29733 (Personal Data Protection Law) with its regulation, overseen by ANPD (National Authority for the Protection of Personal Data). This law define the sensitive data as the personal data consisting of biometric data that can identify the data subject such as racial or ethnic origin; economic income; political, religious, philosophical or moral opinions or beliefs; trade union membership; and information relating to health or sex life. This data requires explicit written consent for processing it, except in cases where the law requires it and this serves important reasons of public interest. Comparing it to the EU data protection laws (GDPR (Art. 9) + national anti-discrimination law + AI Act), the definition for sensitive data is similar to the one defined in GDPR (special category data) and requires explicit legal basis to collect the data, in that way is similar to the default posture of Peru. However, EU has also the AI Act, which add risk-based obligation for "high-risk" AI systems such as credit scoring or employment and it includes bias-testing requirements, making the law in EU stronger than the law in Peru.

Comparing witht the US, I could see that the data is not a single federal data protection law, because different institutions and states will apply different protections according to their reach. Protected classes are defined per-statute. Disparate impact doctrine matters even without intent. The law in US allows the data to be used but the use of this data must be careful, working in a different way than EU and Peru laws, where the limits are in the collection of data.

## Incorrect use of protected information examples

Amazon's recruiting tool in 2018 was trained to search the best candidates over a ten year period to find key terms and attributes, however, the model learned to penalize resumes containing the word "women's" (e.g. "women's chess club"). The model didn't use sex as an input feature, but it was reconstructed from correlated text patterns. This happened also because when you analyse the data, the most successful candidate in the past according to it was likely to be man and white, making the data biased and, because the bias was not addressed, the model ended to be unfair. (Source: https://medium.com/cut-the-saas/case-study-how-amazons-ai-recruiting-tool-learnt-gender-bias-657ff88d818c)

In 2019, Obermeyer and its colleagues present the results of their research, finding that a widely used algorithm for healthcare risk-prediction had an implicit racial bias. This algorithm helped hospitals and insurance companies identify which patients will benefit from “high-risk care management” programs, which provide chronically ill people with access to specially trained nursing staff and allocate extra primary-care visits for closer monitoring. One of the variables used was cost, but this variable was demostrated to be the responsible to develop the bias. The reasons to that were that race and income are highly correlated because black patients historically had less access to care and thus lower recorded spending for the same level of illness. This make the model to underestimate the needs of the patients, putting the same risk score with black patients sicker than white patients. (Source: https://www.scientificamerican.com/article/racial-bias-found-in-a-major-health-care-risk-algorithm/)

## Highly correlated variables to protected attributes

Race/ethnicity -> zip code, surnames, language preference, school attended, arrest record (proxies for policing intensity), credit history depth (proxies for historical access to banking)

Sex/gender -> first name, certaing product purchase history, pronoun usage, some health conditions

Age -> graduation year, years of work experience, certain product usage patterns

Disability -> employment gaps, certain medical codes, accommodation requests

Religion -> dietary preference, leave patterns, certain affiliations

This variables could be inappropriate to use because they could have strong statistical correlation with a protected variable or, even if its individually weak, when combined they could reconstruct the protected attribute. Appart from that, these variables distribution could reflect past discrimination, for example, arrest records reflect over-policing of certain neighborhoods not just criminal behaviour. Finally, for certain businesses, some variables could be used, but in others the same variable will not have a justification to be used, for example, zip code might predict commute time for a logistic model, but using it as credit risk feature is much harder to justify given its correlation with race.
