# Classifying types of propaganda  
## Final project for [DS4a Summit](https://www.correlation-one.com/ds4a) hosted by Correlation One <br>

[![Screenshot-136.png](https://i.postimg.cc/KvYNtQwX/Screenshot-136.png)](https://postimg.cc/YjJYHNt8)

### Problem Statement <br> 
News articles use specific techniques to convey their messages through propaganda where information is purposefully shaped to foster a predetermined agenda.  Our goal is to produce a model capable of spotting text fragments in which propaganda techniques are used in a news article. 
The question we want to explore is: What methods can be used to identify propaganda, and what sort of patterns and characteristics exist within each method?
There are 18 common methods that determine the different types of uses of propaganda in propaganda articles [[1]](https://propaganda.qcri.org/annotations/definitions.html)
After developing a multiclass classifier to identify which types of propaganda are present in each article, we aim to further improve the model by identifying underlying patterns that are present in each category.  This includes:
Examining any similarities between classes, and whether there are shared characteristics among them 
Exploring any lexicon patterns that tend to indicate controversial/propaganda pieces (e.g., any words that repeatedly arise in articles flagged as propaganda)
Exploring any sentiment language that is used, and whether types of sentiments are used differently among different parties or in different scenarios.  
This project is as relevant as ever, given that fake news and propaganda is now easily created and distributed online, and has become a global problem [[2]](https://comprop.oii.ox.ac.uk/research/cybertroops2018/).  Despite its prevalence in platforms such as Facebook [[3]](https://www.amazon.com/Antisocial-Media-Disconnects-Undermines-Democracy/dp/0190841168) and WhatsApp [[4]](https://iscs-conference.com/wp-content/uploads/2019/10/ISCS_2019ConferenceProceedings.pdf), any action to identify and keep it under control has not kept pace.  It is a problem that will not disappear on its own, so further research to understand how to identify it is crucial.
<br><br>
### Data
**Dataset** <br>
The dataset created by the [Propaganda Analysis Project](https://propaganda.qcri.org/).  Since the dataset is being used for a contest, it is not yet publicly available.  The dataset contains 18 types of propaganda, reduced to [14 annotations](https://propaganda.qcri.org/annotations/definitions.html) <br>
**Labels** <br>
FLC (fragment level classification) labels were distinguished by beginning and end character locations in text. Examples of labels include:
- Casual Oversimplification: pinned blame for Steinle's death of illegal immigration and insufficiently aggressive deportation tactics
- Loaded Language: severe trouble
- Exaggeration/Minimalization: willing to bet the Guardian a million dollars and its editor's head that Manafort never met Assange

**Data Exploration** <br>
The dataset contained an uneven number of cases per class, with the most labeled class containing 2,058 labels and the least labeled class containing 72 labels.  The other classes fell in between the highest and lowest:
[![Screenshot-138.png](https://i.postimg.cc/rpsnHVkY/Screenshot-138.png)](https://postimg.cc/PLGQpkNm)  <br>

**Data Augmentation** <br>
We adjusted for the imbalanced dataset with two approaches:
- augmenting the data using an oversampling technique called SMOTE, which generates synthetic examples until all classes are an even size
- eliminating all but the top 5 most labeled classes
We ran separate analyses with SMOTE, with only the top 5 highest classes, and also combined SMOTE with reducing classes:
  * Unaugmented dataset with 14 classes
  * SMOTE with 14 classes
  * Unaugmented dataset with 5 classes 
  * SMOTE with 5 classes 

### Models 
Models were run with original dataset (14 classes), reduced dataset (5 classes), and SMOTE dataset
- Baseline models: Naive Bayes, Logistic Regression, and Linear Regression
- Comparison model: LSTM
- Features: ngrams, word embeddings, tfidf, Urban Dictionary 

### Analysis
To measure accuracy we used the F1 score, which is the weighted average of precision and recall:

