# Confounder - readme

#### Inferring Errors of Omission and the Content of Causal Studies Through Machine Learning

&nbsp;

*I am working on this under the tentative hope that it will serve as a capstone for a data science immersive course. But more importantly, this is something I've hoped to make for several years - long before I knew what data science even was. For now I will be using a simple classification model (multinomial naive bayes). As part of an immersive course I hope to use neural networks and ensemble techniques to enhance accuracy.*

---

&nbsp;

## 1. What is Confounder?

Confounder is a proof-of-concept in unstructured data analysis. It is operationally similar to a spam filter in the sense that it can be trained to categorize text by certain features. This tool pre-screens text samples to determine if certain methodological errors have been made - specifically in articles or studies which claim that one variable (**X**) influences another (**Y**).

**Please note that this is not "fact-checking" software and no such thing can exist (see final paragraph); it merely screens content to determine if it is even worth your time.**

Analysis on a topic is more *reliable* if it **accurately measures** *manipulated* as well as *responding* variables, accounts for a *greater number* of significant **controlled variables**, and also makes a careful effort to find the **causal order** between both variables - *ruling out that "Y" is actually what causes "X."*

![Research Methodology Criteria](https://raw.githubusercontent.com/analyticascent/confounder/master/Research%20Methodology.png)

The three methodological issues refered to above will be called **measurement,** **confounding,** and **time series errors** throughout this readme. For the most part, checking for missing variables in news articles or blog posts will be the easiest implementation of this tool. As for advanced use, this project is particularly focused on semi-automating a *meta-analysis* of existing causal research on a topic - one that attempts to sort what studies accurately accounted for which of the three issues.

**Aggregation** and **sampling issues** (quantity and systematic error) could in theory also be checked for, but it must be stressed that the magnitude of such flaws are more open to interpretation than the three methodological issues pictured above. Whether a study falls prey to the [Yule-Simpson effect](http://www.wsj.com/articles/SB125970744553071829) or some form of [ecological fallacy](http://www.socialresearchmethods.net/kb/fallacy.php) is likely too much of a second-order problem that can't easily be deduced from word patterns alone. Sampling quantities are often explicitly stated (often in the absract), but deducing sampling bias may also be too hard to infer using natural language processing alone.

---

### What Good Studies Do:

**1. Define Their Variables:** All studies (and often news articles) that assert that one thing influences something else must clearly define what the X (manipulated/independent) and Y (responding/dependent) variables are that are being compared.

**2. Effective Sampling:** Broadly speaking, larger samples are preferable to smaller ones and techniques such as random control trials are often helpful for many kinds of research. Heterogeneity within sample groups is also an issue.

**3. Account for Confounders:** Any additional variables that may distort how X appears to cause Y need to be accounted for. This is a common failure among studies, yet easy to infer the absence of - hence the project name.

**4. Acknowledge Trade-Offs:** A trade-off can be thought of as another Y variable. Example - requiring cars to have tank-like durability (X) may reduce driver deaths (Y), but it probably will come at the expense of things such as cost and fuel efficiency.

**5. Use Time Series Analysis:** Does X influence Y, or could it be the other way around? Time series analysis (seeing whether changes in one variable come before another) can help answer this question.

&nbsp;

![Statistical Claims Criteria](https://raw.githubusercontent.com/analyticascent/confounder/master/Statistical%20Claims%20Criteria%20-%20Print.png)

&nbsp;

*Readers should definitely view this article on research methodology, especially it's interactive:* <a href="https://fivethirtyeight.com/features/science-isnt-broken/" target="_blank">**Science Isn't Broken**</a>

&nbsp;

## 2. Where the Name Came From

[**Confounders**](https://en.wikipedia.org/wiki/Confounding) could be described as being additional variables that may distort the true causal relationship between causal and responding variables. As a simple example, consider a claim that [ice cream consumption leads to higher crime rates](http://icbseverywhere.com/blog/2014/10/the-logic-of-causal-conclusions/). The confounder (missing variable) in this case is the season (summer). People spend more time outdoors (and thus availability for crime rises) during the summer *and* they tend to consume more cold goods - for rather obvious reasons.

![Ice cream vs Crime monthly correlation](http://icbseverywhere.com/blog/wp-content/media/2014/10/Icecream.png)

Accurate studies require that as many statistically significant confounders are accounted for, otherwise the claim that "**X** causes **y**" could be false. Many things must be taking into account before causality can be inferred but the project is titled **Confounder** because checking for missing variables is the easiest (and often most crucial) step in making accurate inferences.

![Scientific Errors](http://www.compoundchem.com/wp-content/uploads/2014/04/A-Rough-Guide-to-Spotting-Bad-Science-2015.png "A Rough Guide to Spotting Bad Science")

&nbsp;

## 3. Confounder in Theory and Practice

*Conceptually* this project follows the following procedural steps for any given topic of research:

* **Feature Engineering:** List confounders that should have been accounted for in passages
* **Training Corpus:** Create a CSV file with text of articles labeled by errors/omissions made
* **Coding & Execution:** Read the CSV file into an Ipython notebook coded to classify the text

Right now, testing is under way with the use of an IPython notebook that converts sample studies into document-term matrices which are then analyzed by a multinomial naive Bayes classifier in Scikit-Learn. Studies featured in a meta-analysis on a given topic will be used as a train/test set.

![Document-Term Matrix](http://mlg.postech.ac.kr/static/research/nmf_cluster1.PNG)

The operating assumption boils down to this: *Good studies will have term frequencies that are distinct from bad ones.* Any studies featured in a meta-analysis that described what the study did or did not account for can easily be used to train a classifier. If academic studies on a topic that... 

* Do not effectively establish a statistical association between hypothesized independent and responding variables
* Fail to account for all statistically significant confounders - or control variables of any kind
* Do not accurately distinguish the order of causation between the two variables (conflating cause and effect)

...are lexically distinct enough from studies on the same topic that *do* manage to meet the three criteria, then there is no reason a machine learning program cannot be trained with sample studies to identify flawed studies from robust ones. How true this turns out to be may depend on the topic in question in addition to how authors of a study choose to write about it.

&nbsp;

## 4. Applications, and How (non-technical) Users Can Help

Unstructured data analysis could be used to identify word patterns that indicate whether a variable in a study has been accounted for. From there various forms of text analysis can be used to infer if those adjustments have been made. It may be possible to check for common signs of unreliable research using certain phrases or word transitions as features for machine learning.

The remaining questions however are just what research issues this could be used for, and how other people might be able to assist in the applied use of Confounder. Even people with an entirely non-technical background can help choose issues to test with, as well as add to any existing list of missing variables already in use.

For demo purposes, three major test cases will be examined for new user demonstration. They are selected because they are quantifiable cause and effect topics that a large amount of test articles can be used to build a training corpus.


* **Yule-Simpson Effect:** Male/female average wage and job satisfaction figures might be falling prey to this

* **Supply & Demand:** Checking minimum wage studies for omissions can better test theories about demand curves

* **Research Review:** An existing meta-analysis could serve as a training set to automate more research review

A non-technical user can easily contribute to this project, mainly by adding to (or creating from scratch) missing variable lists or collecting sample articles that meet or fail those various criteria. For instance, consider the list of five factors related to the impact of college education on earning. They consist of trade-offs, omitted variables, along with the question of cause of cause and effect:

**Question:** *What is the impact of college education on lifetime earnings? Does a 4-year degree really get you a million dollars more over your working life?*

<a href="http://www.youtube.com/watch?feature=player_embedded&v=V122ICNS8_0
" target="_blank"><img src="http://img.youtube.com/vi/V122ICNS8_0/0.jpg" 
alt="ABC 20/20 - College is a Ripoff" width="480" height="360" border="10" /></a>

**The Criteria:** 

&nbsp;

1. **Sunk Costs:** Not working as much during the 4-years of schooling subtracts from future earnings.

2. **Tuition Costs:** Both the direct cost of tuition as well as interest on student loans subtracts from future salaries.

3. **Outlier Grads:** Super-earner outliers skew the average for degree recipients (such as Michael Jordan w/Geography degree).

4. **Aggregation:** Aggregating all majors and all non-degree holders into two groups overlooks differences majors can play.

5. **Causation Order:** Did college make the student or vice versa? Those that complete college may be prone to succeed beforehand.

&nbsp;

The next step is to collect various articles and/or studies that meet or fail those various criteria. That resulting training set is key if Confounder is to be accurate at predicting the kinds of errors and omissions future text passages have made. No programming knowledge is necessary to perform those steps, thus anyone with domain knowledge about (or for that matter, a serious interest in) a given topic is encouraged to give input.

&nbsp;

## 5. In Summary: Relevant Steps and Future Plans

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
