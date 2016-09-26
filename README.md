# Confounder - draft 1.0

### *Automating methodological reviews of existing research*

&nbsp;

**Confounder** is a proof-of-concept in unstructured data analysis. The aim is to reduce the time it takes to analyze existing bodies of quantitative research on a topic; specifically in the context of determining what the findings of more reliable studies tend to be. *Quantitative* research refers to any study that attempts to find the association (or lack thereof) between one variable (**X**) and another (**y**). A study is considered to be more *reliable* if it more accurately measures *causal* in addition to *responding* variables, accounts for more significant *controlled* variables, and also makes a careful effort to find the *causal order* between both variables (ruling out that **y** is actually what causes **X**).

![Research Methodology Criteria](https://raw.githubusercontent.com/analyticascent/confounder/master/Research%20Methodology.png)

The three methodological issues refered to above will be called **measurement,** **confounding,** and **time series errors** throughout this whitepaper. The project is particularly focused on simulating a *meta-analysis* of existing causal research on a topic--performed as a *methodological review* of existing evidence.

Additionally, **aggregation** and **sampling errors** can also be taken into account, but it must be stressed that the magnitude of such flaws is more open to interpretation than the three methodological issues pictured above. Project inspiration stems largely from an article on scientific and statistical methodology: [**Science Isn't Broken**](http://fivethirtyeight.com/features/science-isnt-broken/)

[Confounders](https://en.wikipedia.org/wiki/Confounding) could be described as being additional variables that may distort the true causal relationship between causal and responding variables. Accurate studies require that as many statistically significant confounders are accounted for, otherwise the claim that "**X** causes **y**" could be false. Many things must be taking into account before causality can be inferred:

![Variables](https://significantlystatistical.files.wordpress.com/2014/12/slide-31.png "Variable Types")

*Conceptually* this project follows the following procedural steps for any given topic of research:

* List all potential confounders that should have been controlled for in a study or article making a causal claim
* Determine what keywords or raw text patterns are associated with accounting for those confounders (or failing to)
* Write scripts which will check for the absense or presence of those phrases and/or text patterns in passages

Right now, testing is under way with the use of an IPython notebook that converts sample studies into document-term matrices which are then analyzed by a multinomial naive Bayes classifier in Scikit-Learn. Studies featured in a meta-analysis on a given topic will be used as a train/test set.

![Document-Term Matrix](http://mlg.postech.ac.kr/static/research/nmf_cluster1.PNG)

The working assumption behind the early testing is rather blunt: *Good studies will have term frequencies that are distinct from bad ones.* Any studies featured in a meta-analysis that described what the study did or did not account for can easily be used to train a classifier. If academic studies on a topic that... 

* Do not effectively establish a statistical association between hypothesized independent and responding variables
* Fail to account for all statistically significant confounders - or control variables of any kind
* Do not accurately distinguish the order of causation between the two variables (conflating cause and effect)

...are lexically distinct enough from studies on the same topic that *do* manage to meet the three criteria, then there is no reason a machine learning program cannot be trained with sample studies to identify flawed studies from robust ones. How true this turns out to be may depend on the topic in question in addition to how authors of a study choose to write about it.

#### Applications for Economic, Scientific, or Sociological Research

Unstructured data analysis could be used to identify word patterns that indicate whether a confounding factor in a study has been accounted for. From there various forms of text analysis can be used to infer if those adjustments have been made. It may be possible to check for common signs of unreliable research using certain phrases as features for machine learning.

![Scientific Errors](http://www.compoundchem.com/wp-content/uploads/2014/04/A-Rough-Guide-to-Spotting-Bad-Science-2015.png "A Rough Guide to Spotting Bad Science")

___

## In Summary: clarifying relevant procedural steps

So how exactly would a working version of this get put to use? Below are ten steps that must be executed for reliable results. The first five involve gathering the training data for the supervised machine learning program put to use in the second five steps. 

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
 
 **10.** *Autosummarize results as automated meta-analysis*
 
 Steps #1-5 are predominantly a *human* workload, while #6-10 in theory can be done through *classifiers* as part of a *supervised machine learning* program. The training data could be studies from an existing meta-analysis (which may already have done the first five steps to a degree). This could then be used to train various classifiers to take in any *new* studies and see whether they meet the methodological criteria stressed above. 
 
#### Bear in mind that there is no such thing as a program that can do all ten steps by hand (let alone act as "factchecking" software). One analogy used by Hilary Mason (former data scientist at Bitly) is that machine learning programs can tell you whether A or B is correct, but not what those two should be in the first place. Software will forever be limited in answering second-order questions.
