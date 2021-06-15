# Loan Performance Analysis

1. [Overview](#overview)
2. [The Data](#the-data)
3. [Data Summary](#data-summary)
4. [Portfolio Profit Analysis](#portfolio-profit-analysis)
5. [Charge Off Rate Analysis](#charge-off-rate-analysis)


## Overview <a name="overview"></a>
**Goals**
1. Provide insights into how the loans are performing
2. Identify additional data fields needed to create a more comprehensive report


## The Data <a name="the-data"></a>
I used the data from the Servicing Data Tape sheet in the Fintech Data Analyst Assesment excel workbook. It had 19999 records and 27 data fields for each record. First, I removed the four records with no report date. The report date is the date that the data was sourced. Since the practical application of this data relies on it being sourced at a known time, I can't use the records with no report date. 


![Loan 13](https://user-images.githubusercontent.com/74626307/122025071-086c4080-cd97-11eb-9f44-2253fedfad45.png)


Next, because of some missing data fields, it's difficult to figure out exactly what is happening with every loan. For example, loan # 13 has a 7/6/2020 start date. The lack of a payment date and cumulated interest indicates that this loan was not paid back, neither in prepayment, nor in the terms of the loan. That would make it deliquent, but The 0 days past due and $0 ending balance indicates that the loan was paid. The loan hasn't been charged-off, so it sits in limbo until I have more information on it. 


I created an outline of all the possible status' that a loan can be in and how it would be indicated in the data:

  
![Loan Statuys Chart](https://user-images.githubusercontent.com/74626307/122027146-db209200-cd98-11eb-8eb8-e79faa34ea0b.png)


**Charged-Off (CO)** is for loans that have been marked as being charged-off.

**Paid in Full (PIF)** is for loans that have been fully paid. It is indicated by not being charged off and having $0 ending balance on Jan 2021 with a non-blank last payment date so I can confirm that the loan was paid on. Loan 13 didn't have a payment date so I was not comfortable making the assumption that it was paid in full. 

**Ongoing on Time (OT)** is for loans that are currently active and are on time with payments as of Jan 2021. It is indicated by not being charged off, having a positive ending balance and being 0 days past due. 

**Ongoing Delinquent (OD)** is for loans that are currently actove and are late with payments as of Jan 2021. It is indicated by not being charged off, having a positive ending balance and being more than 0 days past due.

**N/A** is for any loan that does not fit into these categories.


![Loan Status Bar Chart](https://user-images.githubusercontent.com/74626307/122028358-f4760e00-cd99-11eb-8b8c-db6e64ea4ab6.png)


918, or 4.59% of our data set falls into the N/A category. I'm removing these loans from the data set for my analysis because I cannot accurately figure out what is happening with these loans. If I misplace them, they will skew the results. 


## Data Summary <a name="data-summary"></a>
Before analysing the data, we are going to take a look at the portfolio from a birds eye view.


**Credit Spread**


The most important indicator of loan performance is the borrowers credit score. We're going to look at the portfolio credit score spread to see if there are any abnormalities. 


![image](https://user-images.githubusercontent.com/74626307/122029842-3bb0ce80-cd9b-11eb-9394-5c9664588a8f.png)


![Portfolio Credit Spread](https://user-images.githubusercontent.com/74626307/122030307-a9f59100-cd9b-11eb-8122-63f68254b78a.png)


There is a nice clean spread in the portfolio. Most of the portfolio, 53% is sits right in the middle in the Good category. An equivalent sits in the Fair and Very Good categories, cancelling eachother out. A small amount,. 6.75%, sit in the excellent category. The average FICO score in the data is 711 and the average American FICO score is 711 which puts this portfolio right in line with the national average. 


**Term Spread**

Part of this analysis is going to cover the state of the portfolio up until Jan 2021. We're going to look at the term spread of the portfolio before diving deeper. 
  
 
![Portfolio Term Spread](https://user-images.githubusercontent.com/74626307/122030637-f3de7700-cd9b-11eb-815f-3bc41cf79f2e.png)


  
  
## Portfolio Profit Analysis <a name="portfolio-profit-analysis"></a>
  
It's time to look at dollars invested and the profit from those dollars. 


![Expected Collections](https://user-images.githubusercontent.com/74626307/122031050-520b5a00-cd9c-11eb-99fa-810c10b8703c.png)


In total, the portfolio's principle is $24 million. Assuming everyone paid on time with no issues, the portfolio should expect to see 4 million in interest, resulting in a 16.86% profit margin.


![Current Collections](https://user-images.githubusercontent.com/74626307/122031346-9d256d00-cd9c-11eb-9eeb-40e32dd5b6f2.png)

The data analyzed does not provide the sum of principle payments made on the loans. To find principle paid, I took the total loan amount of non-charged-off loans and subtracted ending balance of January 2021. I found current interest paid by adding up cumulated interest.
  
  
![Expected and Current Collections](https://user-images.githubusercontent.com/74626307/122031095-5c2d5880-cd9c-11eb-87c0-541416c7b32c.png)


![Expected and Current Collections Graph](https://user-images.githubusercontent.com/74626307/122031363-a1ea2100-cd9c-11eb-8451-d30ebb013b06.png)


Currently, based on our collected interest we only have a 8.71% profit margin. There could be many reasons for this:
  - Abnormal amounts of prepayments. I would need prepayment data to figure this out. 
  - Nothing strange. Short term loans finish earlier and tend to payout less interest than long term loans. I would need a database with all the amortization schedules to find out exactly how much interest/principle should have been collected at this time
  - High delinquincy and charge-off rates. People might not be paying their loans. This requires further analysis. 

  
  
## Charge Off Analysis <a name="charge-off-rate-analysis"></a>

A key metric in determining loan portfolio perfromance is the charge-off rate. The given data only provides the charge-off amounts for loans charged-off in Jan 2021. For a more in-depth and exact analysis, I would need the charge-off amounts for all the charge-off loans. For this analysis, I estmated. If a charged-off loan had no "last pay date", I assumed that the borrower made no payments and the full amount was charged-off. If a charged-off loan had a last pay date, I'd substract payments from the total based on how many months passed between the last pay date and start date. This is a rough estimation that doesn't take into account: prepays, previously missed payments before last payment, extra interest added due to lack of payment. 


![Charge Off and Delinquency Rate Table](https://user-images.githubusercontent.com/74626307/122032166-613ed780-cd9d-11eb-90d7-cf857d297ef5.png)

 
Current charge-off rate is 0.52%. According to the federal reserve, the 2020 average charge-off rate for commercial banks is 2.5%, meaning this portfolio is performing far better than average. However, we need to take a look at the delinquency rate because today's delinquents are tommorows charged-off accounts. The portfolios deliquency rate is at 3%, above the national average of 2.5%. Next, we want to take a look at what will happen to the charge-off rate over time if every deliquent account eventually charge's off.


![Charge Off Rate Graph](https://user-images.githubusercontent.com/74626307/122032269-76b40180-cd9d-11eb-87fd-f3865b4eafb3.png)

  
This chart shows the projected charge-off rate if every deliquent loan charges off. We only are going out three years because 99%+ of the portfolio should be closed out by then. In Jan 2022, the deliquency rate will jump to 1.47%. In two years, it jumps to 3.13%, surpassing 2020 national average. In three years, the charge-off rate reaches 3.62%. 
