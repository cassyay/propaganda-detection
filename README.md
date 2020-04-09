# Classifying types of propaganda  
### Final project for [DS4a Summit](https://www.correlation-one.com/ds4a) hosted by Correlation One <br>

- Dataset created by the [Propaganda Analysis Project](https://propaganda.qcri.org/)
- Contains 18 types of propaganda, reduced to [14 annotations](https://propaganda.qcri.org/annotations/definitions.html)

**Problem Statement** <br> 
News articles use specific techniques to convey their messages through propaganda where information is purposefully shaped to foster a predetermined agenda.  Our goal is to produce a model capable of spotting text fragments in which propaganda techniques are used in a news article. 
The question we want to explore is: What methods can be used to identify propaganda, and what sort of patterns and characteristics exist within each method?
There are 18 common methods that determine the different types of uses of propaganda in propaganda articles [[1]](https://propaganda.qcri.org/annotations/definitions.html)  
After developing a multiclass classifier to identify which types of propaganda are present in each article, we aim to further improve the model by identifying underlying patterns that are present in each category.  This includes:
Examining any similarities between classes, and whether there are shared characteristics among them 
Exploring any lexicon patterns that tend to indicate controversial/propaganda pieces (e.g., any words that repeatedly arise in articles flagged as propaganda)
Exploring any sentiment language that is used, and whether types of sentiments are used differently among different parties or in different scenarios.  
This project is as relevant as ever, given that fake news and propaganda is now easily created and distributed online, and has become a global problem [[2]](https://comprop.oii.ox.ac.uk/research/cybertroops2018/).  Despite its prevalence in platforms such as Facebook [[3]](https://www.amazon.com/Antisocial-Media-Disconnects-Undermines-Democracy/dp/0190841168) and WhatsApp [[4]](https://iscs-conference.com/wp-content/uploads/2019/10/ISCS_2019ConferenceProceedings.pdf), any action to identify and keep it under control has not kept pace.  It is a problem that will not disappear on its own, so further research to understand how to identify it is crucial.



[![Screenshot-136.png](https://i.postimg.cc/KvYNtQwX/Screenshot-136.png)](https://postimg.cc/YjJYHNt8)
