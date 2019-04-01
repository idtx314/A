---
layout: project
title: Machine Learning to Predict Crime
date: May 23, 2018
image: machine_learning/decision_tree.png
permalink: "project-9.html"
---

<!-- 
TODO:
Add a section on other work done during the course, like making learning algorithms from scratch.
The "Crime Type Predictor" section should include less about the dataset
Use data set

-->

<!-- Line before a table should be blank -->

|Key Skills & Tools             ||                    |
|:------------------------------||:-------------------|
|Programming Language (Python)  ||Machine Learning    |
|Large Scale Data Analysis      ||Group Coordination  |


## Repositories
[Github](https://github.com/)  
[Project Website](https://benbdon.wixsite.com/crimeml)  
<br />
<br />
<br />


## Introduction
In this project I worked with a partner to conceptualize a machine learning application, procured a data set, programmed a data pre-processing script, trained an array of machine learners, analyzed the efficacy of those learners. I also wrote detailed reports and status updates.  
Preparatory projects included implementing several machine learners from scratch and extensively studying the nature and applicability of machine learning methods to data analysis.  
<br />
<br />
<br />


## Concept Development
The project's core concept was to create a machine learner that could make predictions about crime, trained on data from the city of Chicago. Because of the complexity of the task, there was a very low probability of training an accurate machine learner. To counter this, the components of the project were designed to provide interesting results even if no accurate learner could be trained. The completed project focused on two main subjects, prediction of crime type and the Lunar Effect.  
<br />
<br />
>
>#### Crime Type Predictor
>The project's primary goal was to predict what type of crime was most likely to occur given a time and location of interest.  
>The dataset used in the project was compiled from the Chicago Police Department's "Citizen Law Enforcement Analysis and Reporting" system, which was acquired from the Kaggle.com website.  
>Six useful categories were identified in the data: Day of the week, Time of the day, IUCR (a classification code indicating the type of crime), location type, latitude, and longitude. IUCR was the most interesting category to predict, because such a learner might allow decisions to be made based on the potential severity of a crime at a given time and location.  
>Because successful prediction was unlikely, a variety of machine learning algorithms were trained to make IUCR predictions. Comparing different learners to each other would provide insight about what types of algorithm were best suited to this task, even if none of the learners were effective predictors.  
><br />
><br />
>
>#### The Lunar Effect
>The project's secondary goal was to determine whether the phase of the moon is a significant predictor of crime type.  
>In 1984 the British Medical Journal published a study detailing crime rates collected in India. The study indicated that crime rates rose drastically on full moon nights. Attempts to reproduce the results of this study have been mixed, but a belief in the "Lunar Effect" has taken root among emergency responders and medical personnel.  
>If the moon was indeed having an effect on crime in Chicago, it seemed likely that it would be a significant predictive factor in the type of crime commited, in much the same way that warm weather has been linked to increases in violent crime (Schinasi, 2017). Therefore, an additional goal was to train learners with added data on Lunar phase and compare their effectiveness to the learners trained without that data. It was expected that the Lunar Learners would be more accurate, or at least that Lunar phase would show up as a significant predictor in the results.  
><br />
><br />
><br />


## Project Execution
Completing the project required four major milestones to be achieved: Acquisition of the dataset, pre-processing of the dataset, training of machine learners, and analysis of results.  
<br />
<br />
>
>#### Data Acquisition
>In 2012, in response to the "Open Data Executive Order", the Chicago Police Department created the "Citizen Law Enforcement Analysis and Reporting", or "CLEAR", database. This publicly available data set contains millions of records on reported criminal activity dating back to 2001. The dataset is one of the most extensive released by any police deparment in the nation, and the CPD continues to update it with new information. Each crime record contains the information needed to identify the time, nature, and location of a criminal incident accurate to the city block. These properties and the machine friendly format of the data made the CLEAR database an ideal tool for this project.  
>Lunar phase data was acquired by using "moon.py", a public domain python module designed to mathematically calculate the phase of the moon for a given date.  
><br />
><br />
>
>#### Data Pre-Processing
>Upon our initial examination of the acquired data set, we found that it was in somewhat poor condition, having numerous entries that were obviously erroneous and a number of inconsistencies in labeling. In addition to these issues the set contained various headers and footers, along with a number of data categories that were irrelevant to our goals.  
>Short sections from the data and manual editing of the set were used to identify the main tasks that would need to be performed before processing, and a Python script was written in order to strip out uneccesary information and correct some of the more common errors. Error codes from attempted machine learner training were then used to identify remaining issues hidden deep in the data and these issues were corrected either manually in the original set or automatically by modifying the script.  
>Extensions to the pre-processor allowed the inclusion of Lunar phase data from moon.py and the collapsing of crime codes into shared categories.  
><br />
><br />
>
>#### Machine Learner Training
>In order to quickly train a variety of machine learners I made use of Weka, a tool that allows the use of a collection of training algorithms on any correctly formatted data set. Weka was set to use ten fold cross validation during training, with 10% of the input data set aside for validation. All data from the year 2018 was reserved for final testing of the trained learners, on the reasoning that the most relevant test would be whether a learner could predict the most recent crime data that was available.  
>I discovered quickly that Weka simply couldn't train most algorithms with a set of data as vast as the one that I was attempting to use. After evaluating how large a data set Weka could reliably handle, the training data was cut down to just the year 2017. It is of note that even with more than 11,000 entries the 2017 data is only a small fraction of the entire CLEAR database. As machine learners generally become more accurate when trained on more data, it's likely that this compromise reduced the accuracy of our learners by some amount.  
>The final collection of trained learners included examples of Boosting, Bagging, Nearest Neighbor, Bayesian, and Decision Tree learners. It was predicted that Nearest Neighbor and Decision Tree would be the best suited to the data and therefore the most accurate because we believed that physical adjacency would be a large predictive factor and that the data had been well prepared to remove irrelevant categories.  
>We used Decision Tree learners to evaluate the effect of Lunar phase data so that we could examine the depth at which the tree split on the phase category as well as the accuracy of the resulting learners. The depth of the split would indicate the importance of the new information in making accurate predictions.  
><br />
><br />
>
>#### Results Analysis
>The accuracy of the ZeroR algorithm is frequently used as a baseline to measure other machine learners against. ZeroR achieved about 9% accuracy when predicting the 2018 test data. The Decision Tree algorithm was among the more successful algorithms, achieving an almost 20% accuracy rate on test data, while the Nearest Neighbor algorithm fell short at only about 8% accuracy. Other predictors also achieved rates of approximately 20%, with the most effective algorithm being NaiveBayes at 20.42% accuracy.  
>Attempts were made to improve accuracy by pooling codes together but it was found that it became extremely difficult to defeat ZeroR, which simply chooses the most common classification in the result set as its prediction.  
>Lunar phase data appeared to have no effect at all on the accuracy of the Decision Tree learner, and indeed the algorithm appeared to ignore the new data entirely when choosing which categories to branch on. This would suggest that Lunar phase is not a significant predictive factor in crime type, though it provides no definitive information on crime frequency during full moon nights.  
>A full write up of the project results is available on our [website](https://benbdon.wixsite.com/crimeml).  
><br />
><br />
><br />



## Relevant Links
* [Weka](https://www.cs.waikato.ac.nz/ml/weka/)
* [Dataset on Kaggle](https://www.kaggle.com/currie32/crimes-in-chicago)
* [Chicago Data Portal](https://data.cityofchicago.org/)
* [moon.py](http://bazaar.launchpad.net/~keturn/py-moon-phase/trunk/annotate/head:/moon.py)
* [Schinasi, L. H., & Hamra, G. (2017). A Time Series Analysis of Associations between Daily Temperature and Crime Events in Philadelphia, Pennsylvania. Journal of Urban Health, 94(6), 892-900. https://doi.org/10.1007/s11524-017-0181-y](https://jhu.pure.elsevier.com/en/publications/a-time-series-analysis-of-associations-between-daily-temperature-)
