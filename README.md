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

<br>

---

## ANALYSIS

I first checked the total number of customers in the company and the number of customers who have churned.

I created a **pivot table** and dragged the newly created columns total counter and churn counter in the value section. The total number of customers was **7043** from which **1869** customers had churned.

Then to check the churn rate, I created a **calculated field** in the pivot table called **churn rate** by dividing churned customers by total number of customers.

The churn rate is **27%**.

![Screenshot 2024-11-01 225454](https://github.com/user-attachments/assets/36984d33-f7f5-4fe9-8dab-cf06dcfc3356)

<br>

## Exploratory Data Analysis (EDA)

### 1. Descriptive Statistics

I performed  EDA to understand the **distribution of key variables** such as monthly charges, total revenue, and tenure

- **Monthly Charges**: The average monthly charge was $64.77, with a median of $70.35 and a mode of $20.05. The standard deviation of $30.09 indicates a wide range of 
    charges, suggesting diverse service usage across customers.

- **Total Revenue**: The mean total revenue per customer was $3,034, indicating a broad distribution of earnings per customer based on service tenure and consumption 
    patterns.

- **Tenure in Years**: The average tenure was 3 years, showing how long customers typically stay with the company. The low standard deviation (2 years) suggests that 
    customer retention is fairly consistent across the base.

- **Churn Score**: The mean churn score of 59 reflects the overall risk level of customers leaving, with a wide range indicating varying churn tendencies.

- **Satisfaction Score**: The average satisfaction score was 3, highlighting the overall customer sentiment. The standard deviation 1 shows a mix of satisfied and 
    dissatisfied customers.

- **Age**: The mean customer age was 47 years, indicating that the typical customer base is middle-aged. The standard deviation of 17 years reflects significant age 
    diversity among customers, spanning from younger adults to older individuals (30 to 64 years) 
 
### 2. Correlation Matrix

In addition to descriptive statistics, I also created a correlation matrix to explore **relationships between key variables**: monthly charges, total revenue, tenure in years, churn score, and satisfaction score. If the correlation is 1 or close to 1 then its a **positive correlation**, if its (-1) or close to (-1) then its a **negative correlation** and 0 in case of **no correlation**. The key findings of the correlation are:

- **Monthly Charges and Total Revenue (0.59)**: A strong positive correlation was observed, indicating that higher monthly charges are directly associated with higher total 
    revenue.

- **Tenure in Years and Churn Score (-0.22)**: A negative correlation exists, suggesting that customers with longer tenures are less likely to churn.

- **Satisfaction Score and Churn Score (-0.50)**: There is a negative correlation, meaning that higher satisfaction scores are linked with lower churn scores, reflecting 
    the importance of customer satisfaction in retention.

- **Monthly Charges and Churn Score (0.13)**: A moderate positive correlation shows that customers with higher monthly charges tend to have a higher risk of churning.

<br>

## Visualization

After EDA I started to visualize the data through **pivot table and charts** to understand more about the various churn reasons, and what impact did the variables had on **churn rate and revenue**.  

- **Average Total revenue by Customer Status**

Total revenue generated by the customers : **$21.37M**

The majority of revenue came from customers who had stayed, while a smaller portion came from those who had churned, and an even smaller portion from new customers who had  recently joined. This emphasizes the importance of retaining existing customers to maintain revenue stability.

- **Churn reasons**

Examining churn reasons is crucial to identify the major reasons for churn. I first created a pivot table and bar chart displaying all the churn reasons.

I found that the most common reasons for customer churn are **competitor companies offering better devices** and **better overall offers**, followed by **attitude of the support person** and **dissatisfaction**.

Once I understood the reasons behind customer churning, I exlored how different variables in the data affected reveneu snd churn rate.

- **Analysis as per Contract type**

  


















