# Criteria Examples

To get a better idea of what Confounder could be used to check for, this folder will be used to store methodological criteria on a variety of topics.

For public policy issues, it's often just a matter of listing all the possible *trade-offs involved* as well as the *confounding variables* that conceal them. **But generally, any criteria about statistical claims (X leads to Y) can boil down to these:**

&nbsp;

1. **Variables:**
    * What are the X and Y variables in question? (this is truly what defines the topic the criteria is for)
    * Are units of measurement for them invariant? ("mass shooting" and "terrorist attacks" are not invariant but individual deaths are, also consider what base rate fallacy means when choosing metrics)
    * If using any composite variables, how were they formed? (how you combine or weigh the components can change the results)

2. **Sampling:**
    * What size? (almost always more is typically better, but only if the sample is representative)
    * What techniques? (random control trials for instance can help make them representative)
    * What about outliers or heterogeneity? (you should avoid missing the forest for the trees)

3. **Confounders:**
    * Are you taking into account other variables that might affect Y? (some topics have too many to draw reliable conclusions)

4. **Trade-Offs:**
    * Are there any side-effects of X to take into account? (staying up late gives time to study, but may affect class performance)

5. **Time-Series:**
    * What was the slope of change before and after change(s) to X?
    * Does X really come before Y or is it vice versa? (hospitals don't generally *cause* sickness, instead sick people *go to hospitals*)
