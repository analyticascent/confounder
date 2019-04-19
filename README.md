# Confounder
### *Inferring Errors of Omission*

&nbsp;

&nbsp;&nbsp; One of the most common varieties of information used for [decision-making](https://online.csp.edu/blog/business/decision-making-process) are claims about *how two variables are related,* known as [regression analysis](https://news.mit.edu/2010/explained-reg-analysis-0316). Articles and studies that attempt to infer such relationships between two variables often suffer from formal mistakes. For example, some may include *poor metrics* for the variables being analyzed, overlook *confounding variables* that distort how they are related, or fail to demonstrate the *order of causation* between the two. These can be easily summarized as *the three C's* of regression analysis: *Correlation, Confounding, and Causation.*

&nbsp;&nbsp; ***Confounder* is a machine learning program that uses binary text classification to infer whether chosen pieces of information are present in a body of text or not.** This can be used to match responses to preselected statements (similar to traditional "fact-checking"), but the *main* focus is vetting statistical claims.

![](http://resources.esri.com/help/9.3/arcgisengine/java/GP_ToolRef/Spatial_Statistics_toolbox/scatterplots.png)

### What Do Reliable Statistical Inferences Depend On?
---

&nbsp; **1. Well-Defined Variables:** All studies (and news articles) that use regression analysis must define the X (manipulated/independent) and Y (responding/dependent) variables with metrics that have as little variance as possible.

&nbsp; **2. Effective Sampling:** Broadly speaking, larger samples are preferable to smaller ones. And techniques such as [random control trials](https://www.youtube.com/watch?v=LttLBhTOVvo) are helpful for many kinds of research. Heterogeneity within samples can give [misleading results](https://www.autodeskresearch.com/publications/samestats).

&nbsp; **3. Considers Confounding:** Any [additional variables](https://www.youtube.com/watch?v=b4jhrK03zhs) that may distort how X appears to cause Y need to be accounted for. This is a common failure among studies, yet easy to infer the absence of - hence the project name.

&nbsp; **4. Acknowledges Trade-Offs:** A trade-off can be thought of as another Y variable. For example, staying up late (X) may give your more time to study (Y), but that benefit could be offset from being exhuasted in class the next day.

&nbsp; **5. Sorts Cause from Effect:** Does X influence Y, or the other way around? [Time series analysis and panel data](https://www.youtube.com/watch?v=NCDgJRTvYsY) can help sort out cause from effect by seeing whether changes in one variable come before another. Correlations alone cannot answer this.

&nbsp;

### Example Scenario: Assessing the impact of college education on lifetime earnings
---

To get an idea of how *Confounder* works in practice, consider the claim that recipients of a 4-year degree typically earn a million dollars more over their lifetime:

&nbsp;

![college earnings graph](http://www.incontext.indiana.edu/2009/mar-apr/images/earnings_fig2.gif)

&nbsp;

**That claim (and above chart) results from omitting multiple methodological errors and omissions, which include:**

* The sunk cost of not working as much before obtaining the degree - **(trade-off)**
* Any tuition costs including interest on student loans, residency, etc - **(trade-off)**
* Super-earner outliers skewing the average for degree recipients - **(sampling issue)**
* Different degrees lead to very different lifetime earnings - **(sampling issue)**
* Jobs for high-earning majors tend to be in more expensive cities - **(trade-off)**
* Those that do complete college may already be prone to succeed - **(cause/effect)**

&nbsp;

&nbsp; **Confounder's Workflow:** Pick a *topic*, and come up with a list of *things to check for* (like the topic and criteria listed above). Then gather *sample* documents about that topic, and *label them* by which listed factors they mention. This will be used to train a text classifier to tell which of that information is absent or present in a given document. The classifier is then trained and optimized for accuracy, which then gets deployed as a pipeline that can save you the trouble of having to check new documents against that criteria by hand.

**The final result is a tool capable of screening large collections of documents against a criteria that is specific to the chosen topic. Users are only limited by computing power - not time, or effective reading speed.**

&nbsp;

*For a more detailed summary of how a Confounder deployment works in practice, read [this markdown file](https://github.com/analyticascent/confounder/blob/master/confounder-pipeline.md).*
