---
layout: post
author: Name
title: "Applied Data Science Project Documentation"
categories: ITD214
---
## Project Background

### Overview of the British Airways Customer Feedback Dataset

This project is based on a dataset containing customer feedback for British Airways, collected from AirlineQuality through web scraping. It includes both quantitative and qualitative data, providing a comprehensive view of passenger experiences. Key attributes in the dataset include overall ratings, detailed review texts, traveler types, service ratings (e.g., seat comfort, cabin staff service, ground service), and recommendations.

### Business Goal

Based on the existing information, the primary business goal would be to improve British Airways' business by 10% by enhancing customer satisfaction based on past customer reviews. 

This can be accomplished by making targeted improvements in the service areas highlighted in customer feedback. By identifying the key factors that drive customer satisfaction and dissatisfaction, the airline can address specific issues and enhance the overall customer experience.

To achieve this goal, a series of business objectives have been established, as outlined below (see table). 

### Business Objectives

| S/N                    | Business Objective                | Individual  |
|------------------------|-----------------------------------|--------|
| 1             | To reduce response time by 10% by identifying significant areas of concern through topic modelling and association rule mining for automation of replies. | Yan   |
| 2                 | To analyse review topics for the four different seat types for a more targeted marketing approach, improving business by 10%           | Carlin   |
| 3                | To identify areas of customer satisfaction for marketing purposes, to improve business by 10% | Bridget   |
| 4               | To reduce negative review sentiments by 10% to improve customer satisfaction and demand.  | Vivienne   |

The main objective of focus for this project is to reduce response time by 10% by identifying significant areas of concern through topic modelling and association rule mining for automation of replies (S/N 1 in table).

This can be achieved by identifying the top 4 areas of concern that constitute the highest volume of complaints/negative reviews. Subsequently, the top 3 most impactful clusters that should be prioritised in the design of the automated responses will be identified. The suitability of the topics should be reviewed since this mode of response may not necessarily be appropriate for all areas of concern. 

## Work Accomplished
The approach for the project can be summarised as below:
- Data Pre-processing
- Modelling 
  - Employ Topic Modelling (LDA model) to identify potential common areas of concern.
  - Use Association Rule Mining to understand relationship between identified areas of concern (e.g. seat comfort, food and beverages) and client’s preference to recommend the airline.
- Model Comparison and Evaluation 

Each step is detailed below.  

### Data Preparation

The dataset consists of the following fields:  
- *OverallRating*: The overall rating given by the customer.
- *ReviewHeader*: The header or title of the customer's review.
- *Name*: The name of the customer providing the feedback.
- *Datetime*: The date and time when the feedback was posted.
- *VerifiedReview*: Indicates whether the review is verified or not.
- *ReviewBody*: The detailed body of the customer's review.
- *TypeOfTraveller*: The type of traveler (e.g., Business, Leisure).
- *SeatType*: Class of the traveler (e.g. Business, Economy).
- *Route*: The flight route taken by the customer.
- *DateFlown*: The date when the flight was taken.
- *SeatComfort*: Rating for seat comfort.
- *CabinStaffService*: Rating for cabin staff service.
- *GroundService*: Rating for ground service.
- *ValueForMoney*: Rating for the value for money.
- *Recommended*: Whether the customer recommends British Airways.
- *Aircraft*: The aircraft used for the flight.
- *Food&Beverages*: Rating for food and beverages.
- *InflightEntertainment*: Rating for inflight entertainment.
- *Wifi&Connectivity*: Rating for onboard wifi and connectivity.

The data preparation process revolved around cleaning and transforming the dataset as well as conducting text preprocessing for the 'ReviewBody' field. The data preparation steps are summarised below.

#### Data Pre-processing: 
- Convert ‘Datetime’ and ‘DateFlown’ from string to datetime format.
  - ‘Datetime’ and ‘DateFlown’ are not in datetime format
- Removal of values for ‘OverallRating’, ‘CabinStaffService’, ‘SeatComfort’, where missing values make up less than 10% of total dataset.
  - Missing values were detected in several fields, including Datetime (~20.5%), TypeOfTraveller (~20.8%), Route (~20.9%), DateFlown (~21%), SeatComfort (~3.1%), CabinStaffService (~3.4%), GroundService (~22.9%), Aircraft (~48.1%), Food&Beverages (~10.4%), InflightEntertainment (~31.1%), Wifi&Connectivity (~83.5%).

#### Text Pre-processing:
- Convert all text within the review body to lowercase to normalise the reviews before tokenization.
- Removal of punctuation (including special characters) to reduce noise in the dataset.
  - Presence of non-alphabetical characters (e.g. Couldnâ€™t, KeflavÃ­k).
  - Presence of punctuation in text dataset (e.g. !()-[]{};:'"\,<>./?@#$%^&*_~).
- Removal of numbers from reviews.
  - Figures in the review are rather specific and may not necessarily provide additional information on the broad topic.
- Tokenize words in ‘ReviewBody’ column.
- Remove stop words and domain stop words.
  - Several domain stop words pertaining to British Airlines were found, i.e. ba, british, airways
- Removal of tokens made up of less than 3 characters.
  -
- Lemmatization was conducted to normalise them into a single base form.
- Map POS tags to WordNet POS Tags to facilitate lemmatization.
- Lemmatize tokens with POS Tagging.
  - No stemming was performed as it is important to retain context-specific terms for further analysis.
- Perform POS Tagging
  - Remove of specific parts of speech (including CC, IN, DT, PRP, AUX, UH)

The cleaned dataset was then used to perform topic modelling and association rule mining.  

Prior to the modelling, further data preprocessing steps were performed:
- Filtering of reviews with OverallRating <=4 & VerifiedReview = True
- Filtering of relevant columns for various modelling.
  - 'SeatComfort', 'CabinStaffService', 'Food&Beverages', 'GroundService','Recommended' for association rule mining
  - 'CleanText' for Topic Modelling

### Modelling
The modeling approach will involve two techniques: topic modeling and association rule mining. For topic modeling, two different models will be employed - the Latent Dirichlet Allocation (LDA) model and the BERTopic model.

#### Topic Modelling 
Using the cleaned dataset, the 'CleanText' field is vectorised using Term Frequency (TF-IDF) to create the word representation of the reviews. TF-IDF is useful as it can emphasize terms that are most representative of a topic as instead of those that are too common, especially since terms that are rare and specific to a document get higher scores. Subsequently,two models were used for topic modelling, namely the Latent Dirichlet Allocation (LDA) model as well as BERTopic model. 

##### Latent Dirichlet Allocation (LDA) Model 
The LDA model is a probabilistic model that identifies hidden topics within a collection of documents by representing each document as a mixture of topics and each topic as a distribution of words.

The LDA model was trained using the vectorised document. In order to find the optimal number of topics, a perplexity chart was generated between a range of 1 to 20 topics. The optimal number of topics was identified as 7.

Based on Intertopic Distance Map, Topic 1,2, 3 and 4 are the most prominent areas of concern and are relatively distinct as they do not overlap or overlap minimally.  
The relevant words featured in these four topics mainly relate to *seat comfort, cabin service, ground service and food and beverages*.

##### BERTopic Model 
As a comparison, the BERTopic model, which uses BERT embeddings and clustering algorithms to identify and extract topics from text data, was employed to train the vectorised document as well. 

Using the optimal number of topics derived from the LDA model, the BERTopic model similarly generated 7 topics, which mainly related to the same areas of concern, namely *seat comfort, cabin service, ground service and food and beverages*.

#### Association Rule Mining 
Upon identifying the four key areas to target, association rule mining was used to identify the top 3 areas to prioritise. 

Using the dataset cleaned earlier, binary encoding was conducted by converting categorical and numerical data into boolean indicators (True/False) to prepare the dataset for association rule mining.

Subsequently, the Apriori Algorithm was used to generate frequent itemsets and association rules. The top two rules that reflected high lift, confidence and support leading to clients not recommending the airline mainly pertained to cabin staff service, seat comfort and food and beverages. Thus, these areas could be prioritised for the design of automated responses among the 4 areas of concern identified previously.   

### Evaluation
An evaluation of the two models - LDA and BERTopic models - employed for topic modelling is provided below. 

#### Topic Modelling 

The model’s effectiveness in generating distinct and coherent topics may have been influenced by the presence of the following terms that may not be useful for topic modelling:
Sentiment-related terms (e.g. happy, frustrated) 
Adjectives cannot be removed wholesale as some are important in interpreting the topic (e.g. narrow). 
Country or flight specific terms (e.g. London, Heathrow) 
Nouns cannot be removed entirely as many are related to the topics surfaced. 

Comparison with BERTopic Model

Though the average coherence score is higher for BERT (BERT: 0.443 vs LDA: 0.372), the overall topics surfaced were comparable across both models. 


## Recommendation and Analysis
Based on topic modeling, the top four areas of concern identified were seat comfort, ground service, cabin service, and food & beverages. 

Further analysis through association rule mining revealed that *seat comfort, cabin service, and food & beverages* should be prioritized as the three key aspects for the design of automated responses.

With the narrowed scope of concerns, the following are possible aspects that British Airlines could address through automated responses:
- Cabin Staff Service
  - In-flight service info
  - Flight attendant assistance
  - Comfort and safety details
- Seat Comfort
  - Seat upgrade requests
  - Seat feature details
  - Comfort tips
  - Complaint resolution (offer channels for clients to provide feedback)
- Food & Beverages
  - Menu details
  - Quality and availability issues
  - Service timing
  - Feedback collection (offer channels for clients to provide feedback)

## AI Ethics
In this project, the following potential data science ethics issues may surface:
- Privacy: The use of customer reviews may raise privacy concerns if personally identifiable information (PII) is not adequately anonymized or if data is collected without user consent. Ensuring that data is de-identified and used in compliance with privacy regulations is essential.The data provides areas such as 
- Fairness: There may be a risk of bias in the data, which could lead to unfair conclusions or recommendations. For example, if certain demographics are over- or under-represented in the reviews, the resulting models may not fairly represent all customer experiences.
- Accuracy: Misclassification of topics or incorrect association rules could lead to ineffective or even harmful business decisions.Ensuring the accuracy of the models is crucial to avoid making misleading decisions based on incorrect data interpretations. 
- Accountability: It is important to establish clear accountability for how data is used and decisions are made. Any automation of responses or service adjustments based on the model's outputs should be carefully monitored and evaluated to ensure it does not negatively impact customer service quality.

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 
