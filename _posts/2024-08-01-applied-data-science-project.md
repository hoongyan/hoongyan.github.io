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
  - Missing values detected in several fields.
    Datetime (~20.5%)
    TypeOfTraveller (~20.8%)
    Route (~20.9%)
    DateFlown (~21%)
    SeatComfort (~3.1%)
    CabinStaffService (~3.4%)
    GroundService (~22.9%)
    Aircraft (~48.1%)
    Food&Beverages (~10.4%)
    InflightEntertainment (~31.1%)
    Wifi&Connectivity (~83.5%)

  
#### Text Pre-processing:
- Convert all text within the review body to lowercase to normalise the reviews before tokenization.
- Removal of punctuation (including special characters) that serve as noise in the dataset.
- Removal of numbers from reviews.
  - Figures in the review are rather specific and may not necessarily provide additional information on the broad topic.
- Tokenize words in ‘ReviewBody’ column.
- Remove stop words and domain stop words
- Removal of tokens made up of less than 3 characters.
- Lemmatization was conducted to normalise them into a single base form.
- Map POS tags to WordNet POS Tags to facilitate lemmatization.
- Lemmatize tokens with POS Tagging.
  - No stemming was performed as it is important to retain context-specific terms for further analysis.
- Perform POS Tagging
  - Remove of specific parts of speech (including CC, IN, DT, PRP, AUX, UH)

The cleaned dataset was then used to perform topic modelling and association rule mining.  

### Modelling
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

### Evaluation
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## Recommendation and Analysis
Explain the analysis and recommendations

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## AI Ethics
Discuss the potential data science ethics issues (privacy, fairness, accuracy, accountability, transparency) in your project. 

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

## Source Codes and Datasets
Upload your model files and dataset into a GitHub repo and add the link here. 
