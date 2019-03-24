# The Confounder Pipeline Process Explained

**General Summary:** Confounder is a [natural language processing](https://en.wikipedia.org/wiki/Natural_language_processing) tool that uses supervised [machine learning](https://towardsdatascience.com/the-7-steps-of-machine-learning-2877d7e5548e) to *infer the absence or presence of certain information in raw text.* In plain English, this means it uses techniques similar to those used in spam filtering to classify text by what kind of information it contains. *This allows someone to see what criteria are met by various online articles about a topic without having to check them all by hand.* It is primarily focused on checking for certain statistical errors related to claims about one thing (**X**) affecting something else (**Y**).

For example, it could be used to check if a [confounding variable was omitted](https://youtu.be/EhcWQmg9EeE) in an analysis, or whether [random sampling](https://www.youtube.com/watch?v=LttLBhTOVvo) was used; those in addition to a variety of other features discussed in section 1 (*Content Criteria*).

**Consider this scenario:** Did a study claiming that *obtaining a four-year degree* (**X**) leads to a *million dollars more* in lifetime earnings (**Y**) subtract the cost of tuition to get that result? Or whether those that complete such schooling were already likely to be successful for other reasons? What about the problem of "super earners" skewing the average earnings (and thus making the *median* lifetime earnings more reliable of a figure)?

For each of those questions, you would gather aricles/studies that meet or fail the criteria and use those to train Confounder to tell the difference between them. You can then track news articles, academic studies, blog posts, and even social media comments to see where and how often these kinds of errors pop up.

It can also be used to take a taxonomy of arguments (or even a FAQ list), and semi-automate the process of tagging statements made online with pre-defined responses. This requires an existing knowledge base to work from, in addition to the training data you would need to "show" Confounder what to look for.

Below are the steps it would take to implement Confounder as a binary text classification tool that can be monetized. One special focus right now is helping smaller news sites and blogs that want to flag errors/omissions in larger publications, as well as helping academic researchers save time and grant money. **The end goal is to provide a service that benefits clients to a greater degree than what would be charged to them.**

Each "pipeline" provided will consist of **1)** content *criteria*, **2)** training data labeled according to that criteria, **3)** a *trained model* deployed as an *application*, **4)** *updates* sent to clients about what Confounder is *detecting*, and **5)** a *price model* that allows clients to *benefit more* from Confounder than *what they are charged*.

&nbsp;

## 1. **Content Criteria:** *what will Confounder check for?*
Before Confounder can even be  we need to determine what information does a client want to check for the presence of in a news article or academic study. For policy issues, it's often just a matter of listing all the possible *trade-offs involved* as well as the *confounding variables* that conceal them. **But generally, any criteria about statistical claims (X leads to Y) can boil down to these:**

&nbsp;

1. **Variables:**
    * What are the X and Y variables in question? (this is truly what defines the topic the item list is for)
    * Are units of measurement for them invariant? ("mass shooting" and "terrorist attacks" are not invariant but individual deaths are, also consider what base rate fallacy means when choosing metrics)
    * If using any composite variable, how was it formed? (how you combine or weigh the components can change the results)

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
    * Does X really come before Y or is it vice versa? (hospitals don't generally *cause* sickness; instead it's sick people go to hospitals)

&nbsp;

The above is the primary focus for what Confounder was developed for: *checking the statistical methodology used to reach a conclusion.* **But for many clients, they may be more focused on finding *specific statements* and matching them with *responses* in a point-counterpoint format:** *If* a body of text contains **statement X**, *then* tag it with **response Y**.

This is closer to traditional "fact-checking" which makes it easier for clients to understand how it works. But it can often be more subjective than the approach of checking for statistical errors, *which is Confounder's main focus.*
