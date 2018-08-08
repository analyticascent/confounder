# Confounder - readme

#### Machine learning meets methodological review

&nbsp;

*I am working on this under the tentative hope that it will serve as a capstone for a data science immersive course. But more importantly, this is something I've hoped to make for several years - long before I knew what data science even was. For now I will be using a simple classification model (multinomial naive bayes). As part of an immersive course I hope to use neural networks and ensemble techniques to enhance accuracy.*

---

&nbsp;

## 0. General Summary

**Technical Summary:** Confounder is a [supervised machine learning](https://www.mathworks.com/help/stats/supervised-learning-machine-learning-workflow-and-algorithms.html) program that uses [binary text classification](https://en.wikipedia.org/wiki/Binary_classification) to infer the statistical methodology of large collections of news articles and/or academic studies.

**Plain English Summary:** Confounder is a program that takes examples of documents that do and don't contain certain pieces of information, and uses those as training data to enable it to check the content of new documents you don't have time to personally read from start to finish. You can use it to determine the *sampling* techniques used, what *confounding* variables were controlled for, which *trade-offs* (if any) were discussed, and whether any *time-series* analysis was used to sort out which variable affected the other.

To start with, you need to decide on a question about the impact of one variable (manipulated) is on another (responding). You then need to come up with a criteria you want to check for in news articles or academic studies on that topic - these have to be things that fit a "yes/no" threshold (e.g. they either mentioned a particular confounding variable or they didn't).

From there, you must gather enough sample documents to train Confounder to recognize the difference between new documents that do contain a piece of information you want to check for and ones that don't. You repeat this process for each of the things you wish Confounder to be able to check for.

After training Confounder (which is essentially a text classifier) with enough examples and tuning various settings to boost accuracy, it can be used to perform a "methological review" of news articles and academic studies you haven't read yet. This can be useful for anyone that wants to review a large number of documents containing statistical inferences to see which ones are likely to contain the most robust findings.

**I must emphasize that this is not "fact-checking" software, Confounder merely analyzes the content of unread documents to determine the absence or presence of certain information so users can infer what methodologies were used to reach conclusions. Checking for *omissions* is far easier to do than getting software to judge the "truth value" of various statements.**

This program is only as good as the criteria you come up with and the training data you feed into it, so users must be aware of what criteria applies to *any* statistical inference before they make one that is domain-specific. Greater detail and usage scenarios are laid out below.

&nbsp;

## 1. What is Confounder?

In statistics, a *confounding variable* is a variable that distorts what the true relationship is between two variables. Good studies are supposed to control for these using a variety of techniques, including random sampling and time-series analysis. Because [omitted-variable bias](https://en.wikipedia.org/wiki/Omitted-variable_bias) is so common - yet easy to check for using a simple "yes/no" classification - the program has been named after this type of variable.

For [over 175 years](https://en.wikipedia.org/wiki/Mill's_Methods), the problem of confounding variables - along with two other key methodological issues - has been known to be critical in how we draw statistical inferences - a brief history of the development of such criteria can be found here: http://changingminds.org/explanations/research/conclusions/inferring_cause.htm

In modern terms, this triad of standards is described below:

![method of residue in modern terms](https://github.com/analyticascent/confounder/blob/master/Research%20Methodology.png)

To make it easier for readers to memorize these three issues, I will refer to them as the "three C's" - *correlation, confounding, and causation.*

* **Correlation:** A statistical claim must *accurately measure* the two variables being compared and show that a *correlation exists* between the two.

* **Confounding:** Any confounding variables that might distort the true relationship between whatever X and Y variables are being compared must be controlled for.

* **Causation:** While not 100% sufficient to claim causality, *time-series analysis* is useful for determining if the original X variable is what influences the other and not vice versa.

Although this three-part criteria is important, a less abstracted five-part version has been developed to make it easier to understand what any topic-specific criteria should take into account. This is because trade-offs and sampling issues are important in judging the significance of any claim.

&nbsp;

---

### What Reliable Statistical Inferences Do:

**1. Define Their Variables:** All studies (and often news articles) that assert that one thing influences something else must clearly define what the X (manipulated/independent) and Y (responding/dependent) variables are that are being compared.

**2. Effective Sampling:** Broadly speaking, larger samples are preferable to smaller ones and techniques such as random control trials are often helpful for many kinds of research. Heterogeneity within sample groups is also an issue.

**3. Account for Confounders:** Any additional variables that may distort how X appears to cause Y need to be accounted for. This is a common failure among studies, yet easy to infer the absence of - hence the project name.

**4. Acknowledge Trade-Offs:** A trade-off can be thought of as another Y variable. Example - requiring cars to have tank-like durability (X) may reduce driver deaths (Y), but it may lead to higher costs that prevent them from getting produced at all.

**5. Use Time Series Analysis:** Does X influence Y, or could it be the other way around? Time series analysis (seeing whether changes in one variable come before another) can help answer this question.

&nbsp;

![Statistical Claims Criteria](https://raw.githubusercontent.com/analyticascent/confounder/master/Statistical%20Claims%20Criteria%20-%20Print.png)

&nbsp;

Readers should definitely view this article on research methodology, especially it's interactive: <a href="https://fivethirtyeight.com/features/science-isnt-broken/" target="_blank">**Science Isn't Broken**</a>

A page with just the p-hacking interactive can be found here: https://projects.fivethirtyeight.com/p-hacking/index.html

&nbsp;

## 2. Confounder Usage in Practice

*Conceptually* this project follows the following procedural steps for any given topic of research:

* **Criteria Development:** A domain-specific criteria should be made to classify documents with
* **Training Corpus:** Create a CSV file with text of articles labeled by errors/omissions made
* **Coding & Execution:** Read the CSV file into an Ipython notebook coded to classify the text

The *criteria development* involves coming up with a list of things you want to tech a document for the presence of. Do you want random control trials to be used? Do you want a study to avoid using heterogenous samples that don't see the forest for the trees? Do you know of some confounding variables that need to be controlled for? What about trade-offs that either need to be mentioned or avoided altogether by using different metrics? And last but not least, do you want to check if time-series analysis was used to determine if one variable truly affected another and not the other way around?

**Developing a strong criteria to check documents against is critical for Confounder to be useful - and each element you check for must be verifiable using binary text classification alone.**

*Check the [criteria folder](https://github.com/analyticascent/confounder/tree/master/criteria) of this code repo for some examples of domain-specific criteria.*

For instance, consider the list of five factors related to the impact of college education on earning. They consist of trade-offs, omitted variables, along with the question of cause of cause and effect:

&nbsp;

**Usage Scenario:** *What is the impact of college education on lifetime earnings? Does a 4-year degree really get you a million dollars more over your working life?*

<a href="http://www.youtube.com/watch?feature=player_embedded&v=V122ICNS8_0
" target="_blank"><img src="http://img.youtube.com/vi/V122ICNS8_0/0.jpg" 
alt="ABC 20/20 - College is a Ripoff" width="480" height="360" border="10" /></a>

&nbsp;

**The Criteria:** 

1. **Sunk Costs:** Not working as much during the 4-years of schooling subtracts from future earnings.

2. **Tuition Costs:** Both the direct cost of tuition as well as interest on student loans subtracts from future salaries.

3. **Outlier Grads:** Super-earner outliers skew the average for degree recipients (such as Michael Jordan w/Geography degree).

4. **Aggregation:** Aggregating all majors and all non-degree holders into two groups overlooks differences majors can play.

5. **Causation Order:** Did college make the student successful or do successful students make it through college? Those that complete may already be prone to succeed beforehand.

&nbsp;

The next step is to collect various articles and/or studies that meet or fail those various criteria. That resulting training set is key if Confounder is to be accurate at predicting the kinds of errors and omissions future text passages have made. No programming knowledge is necessary to perform those steps, thus anyone with domain knowledge about (or for that matter, a serious interest in) a given topic is encouraged to give input.

&nbsp;

## 3. How Confounder Works

In order for machine learning to work with unstructured data (such as raw text), the data must be preprocessed into something structured. In the case of text classification, the raw text is *vectorized* - which means each unique vocabulary term (as well as unique word sequences in many cases) is quantified.

The end result is something called *document-term matrices*. These are statistical fingerprints for how different documents differ by how often various words appear. The image below gives a good sense of what that looks like under the hood:

![Document-Term Matrix](http://mlg.postech.ac.kr/static/research/nmf_cluster1.PNG)

Confounder's operating assumption boils down to this: *documents that contain certain pieces of information will have term frequencies that are distinct from those that lack them.* Any studies featured in a meta-analysis that described what the study did or did not account for can easily be used to train a classifier. If academic studies on a topic that... 

* Do not effectively establish a statistical association between hypothesized independent and responding variables
* Fail to account for all statistically significant confounders - or control variables of any kind
* Do not accurately distinguish the order of causation between the two variables (conflating cause and effect)

...are lexically distinct enough from studies on the same topic that *do* manage to meet the three criteria, then there is no reason a machine learning program cannot be trained with sample studies to identify flawed studies from robust ones. How true this turns out to be may depend on the topic in question in addition to how authors of a study choose to write about it.

**Current testing has been promising thus far. For example, getting a classifier to distinguish if an article or study about college wage gains mentioned tuition cost or not is incredibly easy to do without overfitting to the training data alone.*

&nbsp;

## 4. In Summary: Relevant Steps and Future Plans

The end goal of this project - once adequate training sets exist for various topics - is for Confounder to serve as a means for conducting a *meta-analysis* of relevant research and *autosummarize* the findings. Below are ten steps that must be executed for reliable results. The first five involve gathering the training data for the supervised machine learning program put to use in the second five steps. 

&nbsp;

 **1.** *Decide on an area of causal research (does X cause y?)*

 **2.** *Determine how X and y are measured in existing studies*

 **3.** *If proxies of any kind are used, determine accuracy*

 **4.** *List all statistically significant control variables*
 
 **5.** *Determine how causal order of variables may be sorted*
 
 --
 
 **6.** *Gather as much research articles related to #1 above*
 
 **7.** *Find which studies meet the* **measurement** *criteria*
 
 **8.** *Find which studies controlled for what* **confounders**
 
 **9.** *Find which studies performed* **time-series analyses**
 
 **10.** *Autosummarize results as a generated meta-analysis*
 
 &nbsp;
 
 Steps #1-5 are predominantly a *human* workload, while #6-10 in theory can be done through *classifiers* as part of a *supervised machine learning* program. The training data could be studies from an existing meta-analysis (which may already have done the first five steps to a degree). This could then be used to train various classifiers to take in any *new* studies and see whether they meet the methodological criteria stressed above. 
 
---
 
#### NOTE: Bear in mind that there is no realistic way a program can ever do all the above ten steps by hand (let alone act as "fact-checking" software). Anyone who claims otherwise is either trying to peddle hype, or maybe just has a shallow understanding of deep learning. One analogy used by [Hilary Mason (former chief data scientist at Bitly)](http://www.pcmaconvene.org/features/the-mindset-you-need-to-develop-according-to-data-expert-hilary-mason/) is that machine learning programs can tell you whether A or B is correct, but not what those two should be in the first place (using an A/B test as an example). Software will forever be limited in answering second-order questions as well.

#### When it comes to policing information on social media, [this blog post](https://stratechery.com/2016/fake-news/) is an excellent summary of the challenges such an activity would face in practice. You can consolidate arguments with software, but software cannot and does not do the thinking for you.
