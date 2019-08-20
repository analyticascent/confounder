# The Confounder Pipeline Process Explained

&nbsp;

**General Summary:** Confounder is a [natural language processing](https://en.wikipedia.org/wiki/Natural_language_processing) tool that uses supervised [machine learning](https://towardsdatascience.com/the-7-steps-of-machine-learning-2877d7e5548e) to infer the absence or presence of certain information in raw text. In plain English, this means it uses techniques similar to those used in spam filtering to classify text by what kind of information it contains.

This allows someone to see what criteria are met by various documents about a topic without having to read them by hand:

![three criteria for research](https://raw.githubusercontent.com/analyticascent/confounder/master/images/research_methodology.png)

It is primarily focused on checking for certain statistical errors related to claims about one thing (**X**) affecting something else (**Y**). For example, it could be used to check if a [confounding variable was omitted](https://youtu.be/EhcWQmg9EeE) in an analysis, or whether [random sampling](https://www.youtube.com/watch?v=LttLBhTOVvo) was used; those in addition to a variety of other features discussed in section 1 (*Content Criteria*).

&nbsp;

**Consider this scenario:** Did a study claiming that *obtaining a four-year degree* (**X**) leads to a *million dollars more* in lifetime earnings (**Y**) subtract the cost of tuition to get that result? Or whether those that complete such schooling were already likely to be successful for other reasons? What about "super earners" skewing average earnings (thus making the *median* lifetime earnings more reliable of a figure)?

For each of those questions, text passages that do or don't take those into account are gathered and used to train Confounder to tell the difference between the two. You can then track news articles, academic studies, blog posts, and even social media comments to see where and how often these kinds of errors pop up.

It can also be used to take a taxonomy of arguments (or even a FAQ list), and semi-automate the process of tagging statements made online with pre-defined responses. This requires an existing knowledge base to work from, in addition to the training data you would need to "show" Confounder what to look for.

Below are the steps it would take to implement Confounder as a binary text classification tool that can be monetized. One special focus right now is helping smaller news sites and blogs that want to flag errors/omissions in larger publications, as well as helping academic researchers save time and grant money. **The end goal is to provide a service that benefits clients to a far greater degree than they would be charged.** 

Each "pipeline" provided will consist of **1)** criteria that certain content will be checked against, **2)** training data labeled according to that criteria, **3)** a trained model deployed as a *data pipeline*, **4)** *updates* sent to clients about what Confounder is *detecting*, and **5)** a *price model* that only charges clients for the information they can *actually use*.

&nbsp;

## 1. **Content Criteria:** *what will Confounder check for?*

Before Confounder can even be used, we need to determine what information does a client want to check for the presence of in a news article or academic study. For policy issues, it's often just a matter of listing all the possible *trade-offs involved* as well as the *confounding variables* that conceal them. **But generally, any criteria about statistical claims (X leads to Y) can boil down to these:**

&nbsp;

1. **Variables:**
    * What are the X and Y variables in question? (this is truly what defines the topic the criteria is for)
    * Are units of measurement for them invariant? ("mass shooting" and "terrorist attacks" are not invariant but individual deaths are, also consider what base rate fallacy means when choosing metrics)
    * If using any composite variables, how were they formed? (how you combine or weigh the components can change the results)
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
    * Does X really come before Y or is it vice versa? (hospitals don't generally *cause* sickness, instead sick people *go to hospitals*)

&nbsp;

But many clients may be more focused on finding *specific statements* and matching them with *responses* in a point-counterpoint format: **If** a body of text contains statement X, **then** tag it with response Y.

This is closer to traditional "fact-checking" and easier for non-specialists to understand, but such criteria can often be more subjective than those that check for statistical errors, so **it must be stressed that this approach is not the main focus for Confounder in the long-term.**

&nbsp;

## 2. **Training Data:** *what does Confounder need to learn from?*

Without training data, Confounder is nothing more than the software equivalent of a rocket without fuel. To understand why, readers should know what supervised machine learning is and how it differs from standard programming techniques.

&nbsp;

**Conditional Statements:** Traditional programming generally consists of code that represents a series of **If-Then-Else** statements. A program takes *input* from a source, executes a *series of steps* with that data that are specified with the *If-Then-Else* statements, and then *outputs* the result. This is the heart of computer science - input is manipulated and results in a new output. This format works well for situations where the data in question takes on rigidly predictable forms. A simple example could be determining if a number is even or odd. This is a *low-dimensional* problem that requires very little code to solve - the corresponding Python code for this problem is simple for even non-programmers to follow:

```python
def is_even(n):
    if n % 2 == 0:
        return "Even"
    else:
        return "Odd"
```

The first line names the function and takes in a variable (**n**), the next checks if dividing the input by **2** results in *no remainders* (which would make it even), the third says to return **Even** if that condition is true, and the fourth and fifth lines specify that the code should return **Odd** if the condition is false. This is a simple classification problem that requires very little code. But what about a *high-dimensional* problem with *unstructured data*, such as infering the content of a document?

As most can imagine, writing a series of "If-Then-Else" conditional statements for *any potential arrangement of words* is just not feasible. Additionally, *raw text alone* does not have the kind of *structure* a computer can readily work with. *For these reasons, supervised machine learning techniques come into play in order for Confounder to operate.*

&nbsp;

**Learning by Example:** To pull this off, the text must be *vectorized* in order to have something structured enough for a program to classify documents by. In other words, the text is *quantified* by things such as how often unique words and/or multi-word sequences appear in a document (known as *n-grams*). Resulting values can be used as a "statistical fingerprint" for distinguishing text samples from each other. From there we simply need a rule (algorithm) that defines which "fingerprints" correspond to documents containing something or not. With enough examples fed into the algorithm(s), Confounder can eventually "learn" to tell the difference between categories of text the examples have been labeled by.

The fuller details of how Confounder utilizes machine learning techniques is discussed in the demo notebook, but for now most readers will likely grasp **this key distinction:** *Supervised machine learning involves **showing a program examples** of various things so it can **learn to distinguish them** when classifying new samples.* This means if Confounder is trained to check documents against a particular criteria using examples that are labeled by that same criteria, users will no longer need to execute the same process by reading new documents *themselves*.

&nbsp;

**Training Corpus:** Before Confounder can be trained and deployed as a data pipeline, we need to extract, transform, and load training data into the text classifier. **1)** Data sources must be decided upon (usually with input from the client), **2)** text samples from those sources must be gathered, **3)** then labeled by what criteria it meets or fails. **4)** It then must be converted to raw text with any format irregularities removed, and then **5)** a CSV file is produced with columns that contain the raw text for each training document in addition to labels for what information they do or do not contain.

&nbsp;

**Deciding Sources:** This will vary more than any other step in the process of creating training data because what gets used in this step will depend on client wishes. Right now two client profiles are of interest, the first is *individual owners of reader-funded sites* who want to track errors/omissions in *larger online publications*. By enabling clients to put out more content that takes this focus, they can potentially draw in more revenue from donations/subscriptions and pay a smaller cut to finance the ongoing development of Confounder. The other user segment is academic researchers who wish to perform a methodological review of existing literature and wish to save time and grant money.

&nbsp;

**Gathering/Labeling Samples:** If a given source is a public-facing website, webscraping is usually sufficient to get the text samples needed. For academic journals, it's more likely that PDFs will be used which will then be converted to raw text format. For now, this is a step that requires some manually finding examples through traditional web searches (or if a client already has a collection of links to articles or PDFs, that can help too). The obvious reason for the need to have manual sample collection take place at this stage is because Confounder *needs training data* before it even "knows" what to check for later on.

For this pipeline stage, the goal is to find enough examples of documents about a specific topic that do contain a piece of information (as well as ones that lack it entirely) so that Confounder can be trained to tell the difference. This step may have to be revisted multiple times in order to boost classification accuracy.

&nbsp;

**Corpus File Formatting:** Once enough training documents have been gathered and labeled, they are then converted into a consistent raw text format that can be pasted into a CSV (comma separated values) file that contains a series of columns for each relevant feature (title of the article, author, data, source, as well as what criteria it met or failed). This CSV file is fed into Confounder for model development.

&nbsp;

## 3. **Optimization & Deployment:** *how is Confounder put to use?*

Now that the training data is gathered, labeled, and formatted, it can then be read in by Confounder to train various classification models that infer the content of new documents. **This is an interative stage that aims to do the following:**

* Achieve classification accuracy of 95% or higher for all the features documents are to be checked for
* Develop crawlers/scraping tools that can find the kind of documents a client hopes to have analyzed
* Deploy both of the above pipeline components as a tool that "flags" articles as they become available

&nbsp;

**Model Optimization:** Like any other supervised machine learning program, Confounder requires the iterative modification of certain parameters in order to achieve high accuracy (ideally 95% or higher in classifying errors/omissions) with *minimal overfitting* to the training data. Understanding what this means requires some background knowledge of [the bias/variance trade-off](https://en.wikipedia.org/wiki/Bias%E2%80%93variance_tradeoff) in machine learning, the least readers need to know is the following:

* A predictive model that *overfits* too much to training data does well with *that data*, but not with *new data* (bias)
* Models that *underfit* fail to have much predictive power with *any data at all*, training or otherwise (variance)
* The best models manage to find a balance between these two extremes, and they require repeat tests to develop

![bias-variance visual](https://raw.githubusercontent.com/analyticascent/confounder/master/images/overfitting_underfitting.png)

Technical specifics of what must be done in order for Condounder to achieve high model accuracy are described in the demo notebook file contained in the code repository. Such details are beyond the scope of this document.

&nbsp;

**Model Deployment:** Once predictive accuracy of at least 95% or higher is reached, the trained model can be [deployed in the form of a Flask app](https://towardsdatascience.com/develop-a-nlp-model-in-python-deploy-it-with-flask-step-by-step-744f3bdd7776). A client pipeline will depend on a crawler/scraper that pulls articles/studies/posts from chosen sources containing certain keywords, flags them for any errors or omissions, and a human makes the final call as to how relevant and reliable the results are.

This process is purposefully biased towards **reducing false positives** when flagging documents. Omissions detected in online articles or academic studies are the *minimum* that can be found.

&nbsp;

## 4. **Revenue Model:** *what are clients actually charged for?*

##### [This section is redacted on public repositories, largely because the specifics are in too much of a flux]
