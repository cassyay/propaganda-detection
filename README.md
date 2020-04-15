# Classifying types of propaganda  
## Final project for [DS4a Summit](https://www.correlation-one.com/ds4a) hosted by Correlation One <br>

[![Screenshot-136.png](https://i.postimg.cc/KvYNtQwX/Screenshot-136.png)](https://postimg.cc/YjJYHNt8)

- Code for baseline model test, baseline models with SMOTE, and baseline models with SMOTE for top 5 most labeled classes is available

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
- Comparison model: LSTM, LSTM with word embeddings 
- Features: ngrams, word embeddings, tfidf, Urban Dictionary 

An LSTM (Long Short Term Memory) network is a type of RNN that is capable of remembering surrounding context.  Therefore they are able to learn long-term dependencies [[5]](https://colah.github.io/posts/2015-08-Understanding-LSTMs/).  Their structure allows them to overcome both vanishing gradients and exploding gradients. LSTM models are useful for data that has its meaning affected by surrounding context, as opposed to only being determined by its own value.

### Analysis
To measure accuracy we used the F1 score, which is the weighted average of precision and recall:

The F1-score is useful for dealing with imbalanced datasets because it finds an equal balance between precision and recall [[6]](https://sebastianraschka.com/faq/docs/computing-the-f1-score.html). Precision is the ratio of true positives to true positive and false negatives; recall is the ratio of true positives to false negatives and true negatives:

[![Screenshot-139.png](https://i.postimg.cc/DyWBqtLR/Screenshot-139.png)](https://postimg.cc/ppHfvc0B)

For data with multiple classes, the weighted, or macro, F1 score is used to determine accuracy.  The macro F1 takes the individual scores (PRE) of the k number of classes:

[![Screenshot-140.png](https://i.postimg.cc/2ygj5Cpv/Screenshot-140.png)](https://postimg.cc/CnHpPTxL)

### Results 
For the datset with 14 classes: 
- Logistic regression (LR) without word embeddings, and with SMOTE had the highest F1 score, however the linear classifier (LC) without SMOTE scored about the same
- The LSTM model scored lower than the LC, with and without SMOTE.  LSTM with SMOTE scored only slightly higher than LR without SMOTE
- SMOTE had the largest effect on the LR model

For the dataset with 5 classes:
- Overall, scores were much higher for 5 classes than for 14 classes
- LR with SOMTE scored the highest, LSTM with word embeddings and SMOTE was roughly the same score as LR with SMOTE
- SMOTE had the largest effect on the LSTM model 

For SMOTE:
- Without SMOTE, the majority of predicted classes were for the top 3 classes, and the classes with less cases were getting zero TP/FP classifications.  Most of the accuracy was because the model was only predicting the top 3 classes, and therefore getting the majority correct
- With SMOTE, the classes with less cases were getting classified more, indicating that using SMOTE allowed for more accuracy of all 14 classes

### Summary 
The dataset we used was imblanaced and had few cases for some of the classes.
- SMOTE oversampling helped some of the smaller classes become classified more often
- Having more gold labels would be more effective than SMOTE

Automating propaganda detection is one of the more difficult cases in AI for many reasons.
- Propaganda context is dependent on a culture's history, current issues, facts, language, etc.  Being able to detect propaganda requires an understanding of several constantly changing factors that make it difficult to fully automate  
- Propaganda is not always fully explicit, as a major component of propaganda is manipulation
- This case has 14 classifications of propaganda, however there are many more that have not been considered 
- Much more resources would be necessary to build a functional NLP model to detect propaganda
