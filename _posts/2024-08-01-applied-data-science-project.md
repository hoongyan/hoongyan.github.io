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

<img width="697" alt="Screenshot 2024-08-25 at 9 50 51 PM" src="https://github.com/user-attachments/assets/00850108-996a-4018-8ebf-77bf5895102e">

- Removal of values for ‘OverallRating’, ‘CabinStaffService’, ‘SeatComfort’, where missing values make up less than 10% of total dataset.
  - Missing values were detected in several fields, including Datetime (~20.5%), TypeOfTraveller (~20.8%), Route (~20.9%), DateFlown (~21%), SeatComfort (~3.1%), CabinStaffService (~3.4%), GroundService (~22.9%), Aircraft (~48.1%), Food&Beverages (~10.4%), InflightEntertainment (~31.1%), Wifi&Connectivity (~83.5%).
<img width="267" alt="Screenshot 2024-08-25 at 9 52 00 PM" src="https://github.com/user-attachments/assets/c01d6b4a-290b-4aa6-8a73-624ee6cf06f1">


#### Text Pre-processing:
- Convert all text within the review body to lowercase to normalise the reviews.
- Removal of punctuation (including special characters) to reduce noise in the dataset.
  - Presence of non-alphabetical characters (e.g. Couldnâ€™t, KeflavÃ­k).
  - Presence of punctuation in text dataset (e.g. !()-[]{};:'"\,<>./?@#$%^&*_~).
- Removal of numbers from reviews.
  - Figures in the review are rather specific and may not necessarily provide additional information on the broad topic.
  - Presence of numbers that possibly represent dates, prices, and flight numbers (e.g. 747-400, BA12)

<img width="610" alt="Screenshot 2024-08-25 at 9 53 58 PM" src="https://github.com/user-attachments/assets/1b0e1393-2d01-4765-8827-308387706244">

- Tokenize words in ‘ReviewBody’ column.

<img width="400" alt="Screenshot 2024-08-25 at 9 54 51 PM" src="https://github.com/user-attachments/assets/f7d1b155-65dd-4022-87cc-745fa1e4a57e">

- Remove stop words and domain stop words.
  - Several domain stop words pertaining to British Airlines were found, i.e. british airways/airline/aircraft, flight/flights, ba (acronym for British Airways), plane.

<img width="833" alt="Screenshot 2024-08-25 at 10 14 54 PM" src="https://github.com/user-attachments/assets/55fc7cb2-3267-4a87-9fb7-1983967dcbd0">
<img width="424" alt="Screenshot 2024-08-25 at 10 15 14 PM" src="https://github.com/user-attachments/assets/f83b702d-8077-4308-b436-9fb96fa8524e">

- Removal of tokens made up of less than 3 characters.
  - Words of with one or two characters are present and typically do not add meaningful information e.g. "us", "on", "h" (possibly after removal of numbers).

<img width="483" alt="Screenshot 2024-08-25 at 10 16 22 PM" src="https://github.com/user-attachments/assets/43092e06-64f0-4005-bdd1-63c58648236d">

- Lemmatization was conducted to normalise them into a single base form.
  - Words of various forms (possibly with similar meanings) are present and remain unstandardised, e.g. "fly" vs "flying" and "refused" vs "refusal" vs "refuse".
  - Note: No stemming was performed as it is important to retain context-specific terms for further analysis.

<img width="540" alt="Screenshot 2024-08-25 at 10 16 40 PM" src="https://github.com/user-attachments/assets/2e9489b7-6c13-434c-8023-a86315bd5a49">

- Perform POS Tagging
  - Remove specific parts of speech (including Conjunctions, Prepositions, Determiners, Personal Pronouns, Auxiliary Verbs, Interjections) which may not necessarily add meaningful information for subsequent modelling.

<img width="582" alt="Screenshot 2024-08-25 at 10 17 15 PM" src="https://github.com/user-attachments/assets/0d035c60-1187-4d7f-9afb-e9a8b404d0ce">

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

<img width="824" alt="Screenshot 2024-08-25 at 10 19 20 PM" src="https://github.com/user-attachments/assets/6f188098-e73f-44a2-96d7-1f9e8db3adf1">

##### Latent Dirichlet Allocation (LDA) Model 
The LDA model is a probabilistic model that identifies hidden topics within a collection of documents by representing each document as a mixture of topics and each topic as a distribution of words.

<img width="811" alt="Screenshot 2024-08-25 at 10 19 57 PM" src="https://github.com/user-attachments/assets/0df4f3a6-ba1d-4381-8639-5a095e858f8c">

The LDA model was trained using the vectorised document. In order to find the optimal number of topics, a perplexity chart was generated between a range of 1 to 20 topics. 

<img width="1055" alt="Screenshot 2024-08-25 at 10 20 26 PM" src="https://github.com/user-attachments/assets/9654e869-8c78-49c3-8b1c-fef31c8030e3">

The optimal number of topics was identified as 7, which was used to generate the final model. 

<img width="539" alt="Screenshot 2024-08-25 at 10 21 05 PM" src="https://github.com/user-attachments/assets/7570e54c-90d0-4709-98ae-f675efa671d7">

Based on Intertopic Distance Map, Topic 1,2, 3 and 4 are the most prominent areas of concern and are relatively distinct as they do not overlap or overlap minimally.  

<img width="494" alt="Screenshot 2024-08-25 at 10 21 32 PM" src="https://github.com/user-attachments/assets/7aa68fe9-1f59-453d-b31f-8554c0c966f1">

The relevant words featured in these four topics mainly relate to *seat comfort, cabin service, ground service and food and beverages*. Relevant terms for each topic are depicted in the charts below. 

*Topic 1*
<img width="1028" alt="Screenshot 2024-08-25 at 10 21 56 PM" src="https://github.com/user-attachments/assets/7d0e04b7-8613-44a4-a895-d63132a0cf99">

*Topic 2*
<img width="1010" alt="Screenshot 2024-08-25 at 10 22 16 PM" src="https://github.com/user-attachments/assets/3d05476c-1731-41ea-afe9-65ad515eccda">

*Topic 3*
<img width="1019" alt="image" src="https://github.com/user-attachments/assets/03a332a6-5d4f-4476-b075-acab4e92e082">

*Topic 4*
<img width="1019" alt="image" src="https://github.com/user-attachments/assets/70de3021-d9dc-43ac-81c9-1d6e086a169d">

##### BERTopic Model 
As a comparison, the BERTopic model, which uses BERT embeddings and clustering algorithms to identify and extract topics from text data, was employed to train the vectorised document as well. 

Using the optimal number of topics derived from the LDA model, the BERTopic model similarly generated 7 topics, which mainly related to the same areas of concern, namely *seat comfort, cabin service, ground service and food and beverages*.

<img width="474" alt="image" src="https://github.com/user-attachments/assets/7f47dea4-983f-494e-b3ca-3c715bb2710a">

<img width="944" alt="image" src="https://github.com/user-attachments/assets/f16cab20-3962-4e37-a687-4ac392232170">

#### Association Rule Mining 
Upon identifying the four key areas to target, association rule mining was used to identify the top 3 areas to prioritise. This was conducted using the ratings provided for specific aspects of the flight, including seat comfort, cabin staff service, food & beverages and ground service.

Using the dataset cleaned earlier, binary encoding was conducted by converting categorical and numerical data into boolean indicators (True/False) to prepare the dataset for association rule mining.

<img width="588" alt="Screenshot 2024-08-25 at 10 34 50 PM" src="https://github.com/user-attachments/assets/18a7ecc0-2f00-4a99-b3c7-8cf765e7c97b">

Subsequently, the Apriori Algorithm was used to generate frequent itemsets and association rules. 

<img width="671" alt="Screenshot 2024-08-25 at 10 35 27 PM" src="https://github.com/user-attachments/assets/894c8e7c-aa70-416c-83fa-3c91c0a2e222">


The top two rules that reflected high lift, confidence and support leading to clients not recommending the airline mainly pertained to cabin staff service, seat comfort and food and beverages. Thus, these areas could be prioritised for the design of automated responses among the 4 areas of concern identified previously.   

<img width="696" alt="Screenshot 2024-08-25 at 10 35 06 PM" src="https://github.com/user-attachments/assets/30face6f-fc90-41e6-bd0f-b3d5a9958398">

<img width="1147" alt="Screenshot 2024-08-25 at 10 36 01 PM" src="https://github.com/user-attachments/assets/0795a285-4d06-4f19-9b54-8411094c2f2b">



### Evaluation

#### Topic Modelling 
An evaluation of the two models - LDA and BERTopic models - employed for topic modelling is provided below. 

Based on the coherence score for the LDA model as well as the average coherence score for the BERTopic model, it seems that the latter was the better model. 
  - LDA model: 0.3723
  - BERTopic model: 0.4623

Though this may be the case, both models had comparable results in terms of the areas of concern that were largely highlighted amongst the negative reviews. 

In addition, the LDA model’s effectiveness in generating distinct and coherent topics may have been influenced by the presence of the following terms that may not be useful for topic modelling:
- Sentiment-related terms (e.g. happy, frustrated) 
  - Adjectives cannot be removed wholesale as some are important in interpreting the topic (e.g. narrow). 
- Country or flight specific terms (e.g. London, Heathrow) 
  - Nouns cannot be removed entirely as many are related to the topics surfaced. 

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
- Privacy
  - There are personally identifiable information (PII) available in the dataset that should have been collated with consent. It is important for it to be adequately anonymized and used in compliance with privacy regulations. 
- Fairness
  - There may be a risk of bias in the data, which could lead to unfair business decisions. For example, if certain demographics are over- or under-represented in the reviews, the resulting models may not fairly represent all customer experiences.
- Accuracy
  - If there is a misclassification of topics or surfacing of incorrect association rules, ineffective business decisions may be made. Thus, it is crucial to ensure the accuracy of the models to avoid making misleading decisions based on incorrect interpretations. 
- Accountability
  - Any automation of responses or service adjustments based on the model's outputs should be closely monitored and evaluated to ensure it does impact the customer service quality negatively. This should also be reviewed with domain experts to ensure that the outputs are meaningfully and appropriately used. 

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 

https://github.com/hoongyan/itd214_proj

