# Analyzing Potential Harm within AI: The Robert Williams case

## Context

In January 2020, the Detroit Police Department was investigating the theft of five watches from a Shinola store. The detectives in charge of the case selected a low-quality frame from the store's cameras and loaded it to a facial recognition system provided by the enterprise DataWorks Plus. The algorithm returned the picture of Robert Williams as a candidate match, then, the detectives used this result to ask the store security guard (who didn’t witness the crime) to choose between six different driver licenses the most similar to the same frame and he chose the one from Robert Williams. With this information, the police arrested Williams on his front lawn in front of his wife and daughters. Finally, he was held 30 hours before the case was dropped for insufficient evidence.

The arrest was not only a technical failure, but also a human one. The facial recognition system was assumed to be 100% correct, when it was more likely to have errors than have a good output, beginning with the low-quality input used. There was no further corroboration like alibi check or comparison of physical details and the human steps done to avoid the error, were made in a way that only rubber-stamped the machine’s output. 

## Possible mistakes from developers

Using datasets that have proportionally more light-skinned faces than darker-skinned faces to train the model, make the accuracy for the second group to be less than the first one. The low-quality input (source image) is known to degrade facial recognition accuracy; however, the model allowed the prediction even in that condition. Finally, the system offered a probabilistic candidate list without warning clearly that the output is a lead, not a ground truth and, combined with a process that didn’t require independent corroborating evidence, lead to a wrongful arrest.

## Protected attributes and their contribution

The law doesn’t allow facial recognition models to use any protected attributes, like race in this case; however, the issue was on a previous step: the data used to train the model. This data had underrepresentation of Black individuals, producing higher false match rates for that group. This issue is also addressed by Gender Shades audit, which found that commercial gender-classification systems misclassified darker-skinned women (34.7%) way more than lighter-skinned men (0.8%).

## Prediction errors across demographics and how to check for these disparities

This case highlights the importance of accurately checking the prediction errors across demographics, because it can impact greatly in the lives of the people. Prediction error on a model is an aggregated indicator, however, having the indicators across demographics or groups will show if your model is fair with all groups. To check for these disparities in this case, the results must be sliced by race, sex and skin tone and by the intersection of these (e.g. darker-skinned women) and check the accuracy by group to see if the accuracy is the same for every group.

## Improvement

The best solution possible would be for the models to always use well-balanced demographic data which in most of the cases must be created from scratch; however, creating new datasets instead of using older ones is costly and many enterprises might not be able to do it. In those cases, prioritization of false negative rates or false positives rates as metrics to balance in the outputs for each group will help to reduce the harm. For this scenario, balancing FPR will produce less harm than leaving the model as is. However, even with these improvements, the models are not perfect, and users must treat the outputs carefully and use them only as recommendations, specially in cases where the harm would be great to the individuals or groups affected.

Sources:
https://www.npr.org/2020/06/24/882683463/the-computer-got-it-wrong-how-facial-recognition-led-to-a-false-arrest-in-michig
