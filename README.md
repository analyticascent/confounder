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

