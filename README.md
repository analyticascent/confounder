# Confounder
A hobby project for identifying confounding factors and aggregation in statistical comparisons made in articles, studies, and blog posts. This is a demonstration of what unstructured data analysis can do for science, industry, and public policy.

The inspiration for this project stems largely from the greatest article about scientific and statistical methodology ever written: [**Science Isn't Broken**](http://fivethirtyeight.com/features/science-isnt-broken/)

[**Confounder:**](https://en.wikipedia.org/wiki/Confounding) I would describe this as being an additional variable that may distort the true causal relationship between a dependent and independent variable. Confounders present a major problem for studies that are supposed to control for variables that may distort cause and effect relationships. Accurate studies require that as many confounders are accounted for.

Conceptually this project follows the following procedural steps for any given topic of research:

* List all potential confounders that should have been controlled for in a study or article making a causal claim
* Determine what keywords or raw text patterns are associated with accounting for those confounders (or failing to)
* Write scripts which will check for the absense or presence of those phrases and/or text patterns in passages

