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

* Fail to account for sufficient confounders
* Do not effectively establish a statistical association between hypothesized independent and responding variables
* Do not accurately distinguish the order of causation between the two variables 

...are lexically distinct enough from studies on the same topic that *do* manage to meet the three criteria, then there is no reason a machine learning program cannot be trained with sample studies to identify flawed studies from robust ones. How true this turns out to be may depend on the topic in question in addition to how authors of a study choose to write about it.

#### Applications for Economic, Scientific, or Sociological Research

Unstructured data analysis could be used to identify word patterns that indicate whether a confounding factor in a study has been accounted for. From there various forms of text analysis can be used to infer if those adjustments have been made. It may be possible to check for common signs of unreliable research using certain phrases as features for machine learning.

![Scientific Errors](http://www.compoundchem.com/wp-content/uploads/2014/04/A-Rough-Guide-to-Spotting-Bad-Science-2015.png "A Rough Guide to Spotting Bad Science")

___

#### An Example for Laypersons

Below is a crude way of checking for a statistical error using a simple script - run it here to see results: https://repl.it/C4nL

```python
# A simple demo of how checking for the absence or presence of terms can indicate if
# an error was made in an article, study, or blog post on college degree earnings.

print
print
print 'This checks if the word *skewed* is in a string of text, which can be used to infer whether or not an article about college degree earnings took into account that a small handful of wealthy super-earners skew the average earnings of college degree recipients.'

article_1 = ['A college degree is worth a million over time.']

article_2 = ['The million dollar average is skewed by super-earners.']

# the code below turns the words in each sentence into a list of strings

word_list_1 = [word for line in article_1 for word in line.split()]

word_list_2 = [word for line in article_2 for word in line.split()]

print
print
print 'Did article_1 mention super-earners skewing average earnings?'
print
print '>>>', 'skewed' in word_list_1 # checks if 'skewed' is in the wordlist for article_1 [False]
print
print
print 'Did article_2 mention super-earners skewing average earnings?'
print
print '>>>', 'skewed' in word_list_2 # checks if 'skewed' is in the wordlist for article_2 [True]
print
print
print '-----------------------------------------------------------'
print
print
print 'article_1 says \"A college degree is worth a million over your lifetime.\"'
print
print 'article_2 says \"The million dollar average is skewed by super-earners.\"'
print
print
```

All the above script does is convert raw text into a list of words, then check if a keyword is present in that list. What confounder will consist of however is more focused on machine learning. Early testing is utilizing a naive bayes classifier to avoid having to manually list keywords and check them one by one (which is a drawback of the simple code demonstrated above).

Once a suitable program is developed, all someone would need is domain knowledge of the research area to effectively use it.
