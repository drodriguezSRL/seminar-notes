# Adversity- and adversary-robust adaptive positioning systems with integrity
[CADR-RAS webinars](https://www.adelaide.edu.au/defence-security/institutes-centres/cadr-ras/webinar-recordings)

by Michael Mildford and Connor Malone (15 April 2025)

What I hope to learn:
1. How to verify localization estimates (under adversity: lighting, weather, etc.)? 
2. How to adapt our approach to localization when adversities are identified?


## Verifying localization estimates
📑 Key paper (read whenever need to): 
- [Improving Visual Place Recognition Based Robot Navigation By Verifying Localization Estimates](https://arxiv.org/abs/2407.08162)

**Goal**: to create a localization integrity monitor to define a threshold to identify trusworthy vs untrustworthy estimates. 

It should integrate seamlessly with your localization pipeline. 

Expected output: accept or reject latest estimate.

Their work is based on training a neural network (NN) to 1) take the vectors ouput by the localization module, 2) extract statistical features from those vectors (key), and 3) use the NN to verify whether to trust localization

**(?)** What other "integrity monitors" exist out there?

❌ They didn't provide much details on how this NN is designed...moved on to results. Bummer. Should check key paper above.

Based on results, NN seems relatively robust when identifying adversities and attacks.

### How to attack a NN? 

Fast Gradient Sign Method ([FGSM](https://medium.com/@zachariaharungeorge/a-deep-dive-into-the-fast-gradient-sign-method-611826e34865)) - sophisticated adversarial attach to NNs, very subtle to human eye

### What's next?
- how to differentiate between an attack and an adversity?
- design and train an adversarail attach detector
- deployment in real scenarios 

Nice keyword: "adversarially-resilient" positioning and navigaton

❌ not so much info on how to deal with adversities or attacks after the fact 

Parting comment: it's very hard to define experimetal paradigms to understand whether good estimates were a result of good adaptation to bad original estimates or due to good native estimates. Non-trivial how to ultimately validate your approach.

