# A Framework for Statistical Methodology
### *Summarizing how we reliably infer or negate causality*

&nbsp;

![research methodology](https://github.com/analyticascent/confounder/raw/master/Research%20Methodology.png)

&nbsp;

Pictured above is a simple three-part framework for how we infer the relationship (if any) between one variable and another. The goal of this guide is to expand on those in greater detail so readers grasp what the operating principles behind **Confounder** are. They are universal to any cause/effect claims, and the *criteria* used for deciding if text samples about a topic are accurate must derive from that framework.

Developing an accuracy criteria based both the three principles above as well as errors specific to a topic is essentiall the *feature engineering* phase of putting **Confounder** to use. That step will be discussed in a different markdown file.

---

&nbsp;

## 1. Defining Your Metrics

&nbsp;

## 2. Check for Missing Variables

&nbsp;

## 3. Use Time-Series Analysis

&nbsp;

---

&nbsp;

## Final Considerations

The next step in putting **Confounder** to use is to begin the feature engineering phase. This is where a *topic* is selected and a *criteria* is put together that maps the framework above to that particular subject:

&nbsp;

* **What Subject:** *How does* **X** *influence* **Y**?

* **Measurement:** *How do we sample and quantify* **X** *and* **Y**?*

* **Confounding:** *What other variables have to be controlled for?*

* **Time-Series:** *What do trends across time reveal about cause and effect?*

&nbsp;

The end result is a listed criteria of possible errors that stem from those questions. You can use it to check articles or studies on a topic for errors by hand. Once enough samples that meet or fail those criteria are gathered, **Confounder** can use those as a training set to predict errors in newly collected articles.
