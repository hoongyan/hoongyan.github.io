---
layout: post
author: Name
title: "Applied Data Science Project Documentation"
categories: ITD214
---
## Project Background

### Overview of the British Airways Customer Feedback Dataset

This project is based on a dataset containing customer feedback for British Airways, collected from AirlineQuality through web scraping. It includes both quantitative and qualitative data, providing a comprehensive view of passenger experiences. Key attributes in the dataset cover overall ratings, detailed review texts, traveler types, service ratings (e.g., seat comfort, cabin staff service, ground service), and recommendations.

Columns in the Dataset:
OverallRating: The overall rating given by the customer (1-10 scale).
ReviewHeader: A brief title summarizing the customer's review.
Name: Name of the customer.
Datetime: Date and time when the feedback was posted.
VerifiedReview: Indicates whether the review is verified.
ReviewBody: Detailed text of the customer’s review.
TypeOfTraveller: The type of traveler (e.g., Business, Leisure).
SeatType: Class of the traveler (e.g., Business, Economy).
Route: The flight route taken by the customer.
DateFlown: Date when the flight was taken.
Service Ratings: Numerical ratings for aspects like SeatComfort, CabinStaffService, GroundService, Food&Beverages, InflightEntertainment, and Wifi&Connectivity.
Recommended: Whether the customer recommends British Airways (yes/no).
Aircraft: Model of the aircraft used for the flight.

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

Business Objective of Focus: To reduce response time by 10% by identifying significant areas of concern through topic modelling and association rule mining for automation of replies.

The objective is to reduce the response time to customer complaints by 10%. This will be achieved by identifying significant areas of concern through topic modeling and association rule mining. By automating responses to frequently mentioned issues, British Airways can improve customer service efficiency, address concerns more promptly, and enhance customer satisfaction. Additionally, by focusing on common complaints, the airline can proactively manage service quality and reduce the number of negative reviews.

## Work Accomplished
Document your work done to accomplish the outcome

### Data Preparation
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit. Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu. Mauris lobortis nulla et felis ullamcorper bibendum. Phasellus et hendrerit mauris. Proin eget nibh a massa vestibulum pretium. Suspendisse eu nisl a ante aliquet bibendum quis a nunc. Praesent varius interdum vehicula. Aenean risus libero, placerat at vestibulum eget, ultricies eu enim. Praesent nulla tortor, malesuada adipiscing adipiscing sollicitudin, adipiscing eget est.

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
