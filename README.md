# Confounder
A hobby project for identifying confounding factors and excessive aggregation made in articles, studies, and blog posts. This is a demo on what unstructured data analysis can do for science, industry, and public policy.

The inspiration for this project stems largely from an article on scientific and statistical methodology: [**Science Isn't Broken**](http://fivethirtyeight.com/features/science-isnt-broken/)

[**Confounder:**](https://en.wikipedia.org/wiki/Confounding) This could be described as being an additional variable that may distort the true causal relationship between a dependent and independent variable. Confounders present a major problem for studies that are supposed to control for variables that may distort cause and effect relationships. Accurate studies require that as many confounders are accounted for.

![Variables](https://significantlystatistical.files.wordpress.com/2014/12/slide-31.png "Variable Types")

Conceptually this project follows the following procedural steps for any given topic of research:

* List all potential confounders that should have been controlled for in a study or article making a causal claim
* Determine what keywords or raw text patterns are associated with accounting for those confounders (or failing to)
* Write scripts which will check for the absense or presence of those phrases and/or text patterns in passages

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

All the above script does is convert raw text into a list of words, then check if a keyword is present in that list. What confounder will consist of however is more focused on machine learning. Early testing will likely utilize a naive bayes classifier and/or logistic regression model to avoid having to manually list terms and check them one by one (which is a drawback of the method demonstrated above).

Once a suitable program is developed, all someone would need is domain knowledge of the research area to effectively use it.
