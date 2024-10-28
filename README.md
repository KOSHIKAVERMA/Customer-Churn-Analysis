# Customer Churn Analysis and Prediction - Telecommunication Company

<br>

**Customer churn** refers to the rate at which customers stop doing business with a company over a specific period. It's a key metric that reflects customer retention and helps measure how well a company is maintaining its customer base.

<br>

## INTRODUCTION

This project involves analyzing customer churn for a fictitious telecommunications company that provided **home phone** and **Internet services** to **7043 customers** in **California** in **Q3** (July, August, September). The objective is to understand the key factors that contribute to customer churn and provide recommendations to reduce churn and enhance customer retention.

<br>

---

## PROJECT OVERVIEW

The goal of this project is to answer the following key business questions:

1. What are the **primary drivers** of customer churn in the company?

2. How do customer **demographics** and **services** influence churn rates?

3. What **revenue** impacts are associated with churned customers?

4. How can the company **reduce** its churn rate?

Using descriptive statistics, correlation analysis, pivot tables, and charts, this project provides insights into the relationships between variables such as monthly charges, tenure, total revenue, customer satisfaction, and churn scores. I used **Excel** for exploratory data analysis **(EDA)**, **data visualization**, and **churn rate analysis**.

<br>

---

## DATA SOURCE

The dataset used for this analysis was downloaded from **Kaggle**. Here are short descriptions of some important columns in the dataset:

picture

**CustomerID** : A unique identifier for each customer in the dataset.

**Gender** : The customer's gender (Male/Female).

**SeniorCitizen** : Indicates if the customer is a senior citizen (Yes, No).

**Tenure** : The number of months the customer has stayed with the company.

**PhoneService** : Whether the customer has a phone service (Yes/No).

**MultipleLines** : Whether the customer has multiple phone lines (Yes/No).

**InternetService** : Type of internet service subscribed by the customer (DSL, Fiber optic, No).

**Contract** : The type of contract the customer has (Month-to-month, One year, Two year).

**PaperlessBilling** : Whether the customer opts for paperless billing (Yes/No).

**PaymentMethod** : The method the customer uses for payment (Electronic check, Mailed check, etc.).

**MonthlyCharges** : The amount the customer is charged each month.

**TotalCharges** : The total amount charged to the customer over the entire tenure.

**Satisfaction score** : A score (1-5) indicaing customer satisfaction level. 

**Churn label** : Indicates if the customer has churned (Yes/No). 

**Churn reason** : Reasons for customer churn.

<br>

---

## DATA CLEANING

Removed duplicates value.


<br>

---

## DATA PREPARATION

The first thing I did was converting the data into a **table**. A table includes any additional data that is added in the future by itself.

As I explored the data, I felt the need for adding few additional columns in the data that would further helped me in my analysis, the added columns are:

**1. Churn Counter :** 

The churn counter column would help in **quantitative analysis** by allowing easier aggregation, filtering, and calculation of churn-related metrics such as churn rate in pivot tables or charts.

``` sql
    If(Churn Label = 'Yes',1,0)
```

**2. Total Counter :**

This column tracks the presence of each customer (1 for every customer).  It's useful for creating total counts in calculations.

``` sql
    = COUNTIF(A:A7044,A2)
```

**3. Tenure in Years :**

Converting the tenure (which is in months) into years provided a more intuitive understanding of how long customers have stayed. To help in segmenting customers based on their longevity and understanding how tenure impacts churn behavior.

``` sql
    ROUNDUP(S2/12,0)
```

**4. Age brackets :**

Categorizing customers into age groups allowed for demographic analysis. This helped in identifying patterns or trends in churn behavior across different age groups and designing age-targeted retention strategies.

``` sql
    =IF([@Age]>=50,"Senior", IF([@Age]>=30, "Adults", " Young adults"))
```


**5. Grouped consumption :**

This column grouped customers based on their data or service usage, making it easier to analyze churn rates or revenue generation for different consumption levels.

``` sql
    =IF([@[Avg Monthly GB Download]]<5, "Less than 5 GB", IF([@[Avg Monthly GB Download]]< 10, "Between 5 and 10 GB", " 10 GB or more"))
```









