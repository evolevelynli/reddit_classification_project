# Web APIs & Classification

---

## Project Challenge Statement

### Goal: 
#### 1. Using Reddit's API, collect posts from three subreddits: AskWomen, AskMen, Relationship_Advice. 
#### 2. NLP to train a classifier on which subreddit a given post came from. This is a binary classification problem.

---

### Subreddits 

1. r/AskMen  
2. r/AskWomen 
3. r/RelationshipAdvice

---

### Datasets: 
1. AskMen vs AskWomen (0, 1)
2. Relationship Advice vs AskWomen (1, 0)

---

## Table of Contents 

This Notebook is broken down into different sections for analysis purpose. The following links are connected to differenct section within the Notebook for simple navigation. 

---

## Contents:
- [01_Reddit_API_Data_Collection](https://git.generalassemb.ly/evolevelynli/project_3/blob/master/code/01_Reddit_API_Data_Collection.ipynb)
- [02_Data_Cleaning](https://git.generalassemb.ly/evolevelynli/project_3/blob/master/code/02_Data_Cleaning.ipynb)
- [03_Baseline_Models](https://git.generalassemb.ly/evolevelynli/project_3/blob/master/code/03_Baseline_Models.ipynb)
- [04_Model1_MenWomen_DF_With_Best_Parameters](https://git.generalassemb.ly/evolevelynli/project_3/blob/master/code/04_Model1_MenWomen_DF_With_Best_Parameters.ipynb)
- [05_Model2_WomenRelationship_DF_With_Best_Parameters](https://git.generalassemb.ly/evolevelynli/project_3/blob/master/code/05_Model2_WomenRelationship_DF_With_Best_Parameters.ipynb)
- [06_Models_Intepretation](https://git.generalassemb.ly/evolevelynli/project_3/blob/master/code/06_Models_Intepretation%20.ipynb)

---

## The Model 
---

The Models : 
So far, there are many different models we can use to achieve the goal of classification. Without using all of them, there is no way we can understand which model works better. Therefore, I used seven models that I consider as appropriate for the goal of classification. Here is a list of all seven of them: 

1. CountVectorizer Model With Logistic Regression
2. CountVectorizer Model With Multinomial NB
3. TFIDF Model With Logistic Regression
4. TFIDF Model With Multinomial NB
5. Random Forest Model Feature Extraction
6. Extra Tree Model Feature Extraction
7. AdaBoost classifier Model Feature Extraction

After fitting all the models, I noticed that some models perform better than others. For example, the multinomial naive Bayes model works well in general, and the AdaBoost classifier model is overfitting in both datasets. With the above observation, I decided to combine all seven models and build one ensemble model. The following scores are the train and test score for each ensemble model I constructed for two datasets. 



For AskMen and AskWomen Dataset with Target = AskWomen

```
train score 0.92
test score 0.73

```

For AskMen and AskWomen Dataset with Target = AskMen

```
train score 0.87
test score 0.74

```
For AskWomen and Relationship Advice Dataset with Target = AskWomen 

```
train score 0.999
test score 0.976
```
For AskWomen and Relationship Advice Dataset with Target = Relationship Advice
```
train score 0.993
test score 0.982

```

---

## Classification Result For Different Models: 
---

### AskMen AskWomen Dataset: 

![image result](../images/AskMenWomen_modeleval.png)


### AskWomen Relationship Advice Dataset: 

![image result](../images/AskWomenRelationship_modeleval.png)

---

## Key Takeaways

---

At the end of this project, I focus on understanding the question why with the same model apply to two different datasets, model perform well on one but not on the other. To understand the model, we made a hypothesis regarding the content of the subreddits. if two subreddits have a lot of in common, the model will perform poorly in distingushing one from the other. On the other hand, if two subreddit have different content and keywords, the model is better at picking up the different keywords regrading the different topics, and be better at distingushing the difference. 

Although this concept seems to be a common sense to us human beings, to fully understand how to model works, I decided to jump into this rabbit hole and figure out if the model actually works the same way as we assume it to work. 

After a long process of teasing out the keywords and coeffients, I have come to the conclusion that the model works better when there are less overlap keywords between subreddits. I also notice couple other things that are quite interesting: 
1. The most common words in a subreddit are not necessary the ones the model pick up as the key identifiers. This phenomenon can be due to the fact that we use TFIDF to tease out the most impactful words instead of the ones that are most common. 
2. Although the train test score gap of the model is large when it comes to similar content, the model is still quite good at picking up the difference between two subreddits. We can see this from looking at the overlap of the top features. Up to the top 300 features, the overlaping features between the similar subreddits is only 1% for Logistic regression model.
3. When a model become more complex, the intepretation of the model start to become more complex and less easy to understand. 