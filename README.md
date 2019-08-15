# Confounder
### *Inferring Errors of Omission*

&nbsp;

**Summary:** Here is a bullet point summary of the purpose of this project (technical details are [discussed elsewhere](https://github.com/analyticascent/confounder/blob/master/confounder-pipeline.md)).

* **What:** A program that can infer whether certain pieces of information are present in passages of text.
* **Why:** To infer the methodology that was used when claims about the relationship between two variables are made.
* **How:** Using supervised machine learning in the form of binary text classification (somewhat similar to spam filtering).
* **Who:** Anyone that wants to avoid checking for such information in news articles and studies *by hand* could make direct use of Confounder. It would be of special interest to journalists/editors, academic researchers (especially those performing [reviews of existing research](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC539417/)), or public policy analysts. Confounder could also be used (or contributed to) by anyone in general that wants to sort documents by what information they contain.

&nbsp;

### The Subject Matter of Confounder
---

One of the most common forms of information used for [decision-making](https://online.csp.edu/blog/business/decision-making-process) are claims about **how two variables are related**, known as [regression analysis](https://news.mit.edu/2010/explained-reg-analysis-0316). Pictured below are simple examples of regression analysis with different variables and different relationships between them:

&nbsp;

![](http://resources.esri.com/help/9.3/arcgisengine/java/GP_ToolRef/Spatial_Statistics_toolbox/scatterplots.png)

Articles and studies that attempt to infer such relationships may contain *formal errors*, not just fabricated figures. For example, some may include **poor metrics** for the variables being analyzed (sample size and technique issues for instance). They may overlook **confounding variables** that distort how the two main variables are related (this is often referred to as [omitted variable bias](https://www.youtube.com/watch?v=b4jhrK03zhs)). Last but not least, a statistical claim may fail to demonstrate the **order of causation** between the two variables in question (did X change before Y did, or vice versa?). 

**These can be summarized as *the three C's* of regression analysis:** *Correlation, Confounding, and Causation.* What *Confounder* does is utilize machine learning (through binary text classification) to infer whether chosen pieces of information are present in a body of text. This can be used to infer the *methodology* a passage of text used to reach a *statistical conclusion* about how two variables are related.

&nbsp;

### What Do Reliable Statistical Inferences Depend On?
---

&nbsp; **1. Well-Defined Variables:** All text passages that use regression analysis must clearly state the two variables being compared, and utilize invariant metrics for them (units of measure that always mean the same thing).

&nbsp; **2. Effective Sampling:** Broadly speaking, larger samples are preferable to smaller ones. And techniques such as [random control trials](https://www.youtube.com/watch?v=LttLBhTOVvo) are helpful for many kinds of research. Heterogeneity within samples can give [misleading results](https://www.autodeskresearch.com/publications/samestats).

&nbsp; **3. Considers Confounding:** Any [additional variables](https://www.youtube.com/watch?v=b4jhrK03zhs) that may distort how X appears to cause Y need to be accounted for. This is a common failure among studies, yet easy to infer the absence of - hence the project name.

&nbsp; **4. Acknowledges Trade-Offs:** A trade-off can be thought of as another Y variable. For example, staying up late (X) may give your more time to study (Y), but that benefit could be offset from being exhuasted in class the next day.

&nbsp; **5. Sorts Cause from Effect:** Does X influence Y, or vice versa? [Time series analysis and panel data](https://www.youtube.com/watch?v=NCDgJRTvYsY) can help sort cause from effect by seeing which variable changes before the other. Correlations alone cannot answer this.

&nbsp;

### Example Scenario: Assessing the impact of college education on lifetime earnings
---

To get an idea of how *Confounder* works in practice, consider the claim that recipients of a 4-year degree (X) typically earn a million dollars more over their lifetime (Y):

&nbsp;

![college earnings graph](http://www.incontext.indiana.edu/2009/mar-apr/images/earnings_fig2.gif)

&nbsp;

**That claim (and thus the above chart) is the result of multiple errors and omissions, which include:**

* The sunk cost of not working as much before obtaining the degree - **(trade-off)**
* Any tuition costs including interest on student loans, residency, etc - **(trade-off)**
* Super-earner outliers skewing the average for degree recipients - **(sampling)**
* Different degrees lead to very different lifetime earnings - **(sampling)**
* Jobs for high-earning majors tend to be in more expensive cities - **(trade-off)**
* Those that do complete college may already be prone to succeed - **(cause/effect)**

&nbsp;

&nbsp; **Confounder's Workflow:** Pick a topic, and come up with a list of things to check for (like the topic and criteria listed above). Then gather sample documents about that topic, and label them by which listed factors they mention. This will be used to train a text classifier to tell which of that information is absent or present in a given document. The classifier is trained and optimized for accuracy, then gets deployed as a data pipeline that can save you the trouble of having to check new documents against that criteria by hand. The documents can be online articles, PDF files, or any other raw text source.

**The final result is a tool capable of screening large collections of documents against a criteria that is specific to the chosen topic. Users are only limited by computing power - not time, or effective reading speed.**

&nbsp;

*For a more detailed summary of how a Confounder deployment works in practice, read [this markdown file](https://github.com/analyticascent/confounder/blob/master/confounder-pipeline.md).*
