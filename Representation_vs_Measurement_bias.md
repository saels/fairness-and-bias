# Representation vs Measurement bias

## Representation Bias

It occurs when certain groups are underrepresented or entirely absent from a model’s training data, causing it to perform badly for those populations because it develops a distorted or incomplete picture for those populations.

One of the clearest illustrations comes from the Gender Shades study (2018) where it was discovered that commercial facial recognition systems achieved lower error rate for light-skinned men (0.8%) but poorly for darker-skinned women (34.7%). The systems were not programmed directly to favour lighter faces, but they used datasets that underrepresented darker faces, so the models internalized that a face must look like lighter ones. (Source: http://gendershades.org/overview.html)

Other case worth mentioning is the Pokémon GO case in 2016 were Niantic built the game’s geography from a predecessor game named Ingress, whose players base was mostly affluent and white people. That causes in Pokémon Go that the majority-white neighbourhoods averaged 55 Pokestops versus only 19 in majority-black neighbourhoods. This was not intended by design but because of the data used to train the model. (Source: https://www.khou.com/article/tech/is-pokemon-go-racist-how-the-app-may-be-redlining-communities-of-color/285-291957069)

In 2016, Microsoft Tay was a chatbot trained in real time from Twitter conversations and within 16 hours it had tweeted more than 95000 times racist and abusive comments. This was done by coordinated trolls that dominated its live training feed. The chatbot only did what was programmed to do, reflect whoever it heard most, but the input data was nor representative of healthy human dialogue. (Source: https://spectrum.ieee.org/in-2016-microsofts-racist-chatbot-revealed-the-dangers-of-online-conversation)

What makes representation bias dangerous is that aggregate accuracy metrics look acceptable while concealing sever failures for specific subgroups. The disparity is only visible when the results are disaggregated by race, gender, skin tone or geography.

## Measurement Bias

For this bias, the problem is not who is in the data, but how the data is collected and labelled. It arises when a model is trained on a proxy variable, easier to measure than the true outcome, but not necessarily equally valid across groups.

A clear illustration is COMPAS, an AI tool that predicted recidivism scores. These tools used past arrest records as a proxy for future criminal behaviour, but the arrest rate do not measure criminality alone, they capture policing intensity also. Because black communities have historically been over-policed, there have been more recorded arrests, inflating risk scores for black defendants without any increase in actual risk. The label was wrong before the model was built. (Source: https://mallika-chawla.medium.com/compas-case-study-investigating-algorithmic-fairness-of-predictive-policing-339fe6e5dd72)

The same mechanism was followed by healthcare cost algorithms that were widely used to allocate resources based on predicted future healthcare costs, treating cost as a proxy for clinical need. As black patients had historically faced greater barriers to care access, their recorded spending was lower than white patients with equal illness severity. (Source: https://www.nature.com/articles/d41586-019-03228-6)

Another case is social media recommendation engines used by platforms like Facebook. These are optimized for engagement as a proxy for content quality; however, this proxy does not distinguish between real and valuable content from triggering outrage or fear content. Internal Facebook documents confirmed that misinformation and toxic content were disproportionately prevalent among reshares and that 64% of all extremist group joins where caused by its recommendation tools. (Source: https://library.queens.edu/misinformation-on-social-media/algorithms)

## Conclusion

The broader lesson is that fairness requires attention at every stage of the pipeline. Representation bias calls for deliberate data collection seeking the data that could balance the train dataset while measurement bias calls for scrutiny of the outcome variable itself, asking whether the label, feature or proxy measures equally across all groups. Together these two biases explain a striking pattern across the analysed cases where none of them were set out with malicious intent, but the bias produced an undesired result.
