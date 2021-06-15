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
I used the data from the Servicing Data Tape sheet in the Fintech Data Analyst Assesment excel workbook. It had 19999 records and 27 data fields for each record. First, I removed the four records with no report date. If I don't know when that data was taken, I can't use it. Next, because vital information is missing, it isn't easy to figure out what exactly is happening with all the loans.

![Loan 13](https://user-images.githubusercontent.com/74626307/122025071-086c4080-cd97-11eb-9f44-2253fedfad45.png)

For example, loan # 13 has a 7/6/2020 start date. The lack of a payment date and cumulated interest indicates that this loan was not paid back, neither in prepayment, nor in the terms of the loan. That would make it deliquent, but The 0 days past due and $0 ending balance indicates that the loan was paid. The loan hasn't been charged-off, so it sits in limbo until I have more information on it. 

I created an outline of all the possible status' that a loan can be in and how it would be indicated in the data:
  
![Loan Statuys Chart](https://user-images.githubusercontent.com/74626307/122027146-db209200-cd98-11eb-8eb8-e79faa34ea0b.png)

Charged-Off (CO) is for loans that have been marked as being charged-off.

Paid in Full (PIF) is for loans that have been fully paid. It is indicated by not being charged off and having $0 ending balance on Jan 2021 with a non-blank last payment date so I can confirm that the loan was paid on. Loan 13 didn't have a payment date so I was not comfortable making the assumption that it was paid in full. 

Ongoing on Time (OT) is for loans that are currently active and are on time with payments as of Jan 2021. It is indicated by not being charged off, having a positive ending balance and being 0 days past due. 

Ongoing Delinquent (OD) is for loans that are currently actove and are late with payments as of Jan 2021. It is indicated by not being charged off, having a positive ending balance and being more than 0 days past due.

Anything that does not fit these four categories is marked as N/A.

![Loan Status Bar Chart](https://user-images.githubusercontent.com/74626307/122028358-f4760e00-cd99-11eb-8b8c-db6e64ea4ab6.png)

918, or 4.59% of our data set falls into the N/A category. I'm removing these loans from the data set for my analysis because I cannot accurately figure out what is happening wtih these loans.


## Data Summary <a name="data-summary"></a>
Before analysing the data, we are going to take a look at the portfolio from a birds eye view.
  
**Credit Spread**
The most important indicator of loan performance is the borrowers credit score.

<580	  Poor
580-669	Fair
670-739	Good
740-799	Very Good
>800	  Excellent

![image](https://user-images.githubusercontent.com/74626307/122029842-3bb0ce80-cd9b-11eb-9394-5c9664588a8f.png)

<INSERT PORTFOLIO CREDIT SPREAD CHART>
  
The spread is average. 53% of people are in Good. Almost the equivilant is between Fair and Very Good at almost 20%. Excellent has 6.75% and poor has none. It's scewed upwards if you think Good is average.
 
**Term Spread**
When analyzing, we're going to thinking about timeframes and when we should expect the payments, so we take a look at the terms spread
  
<INSERT TERMS CHART>
  
It's spread nicely. <INSERT ANOTHER COMMENT>
  
  
## Portfolio Profit Analysis <a name="portfolio-profit-analysis"></a>
Next we're going to look at the $ invested and the profits from that investment.

<INSERT TABLE WITH EXPECTED COLLECTIONS>

The expected profit margin in this portfolio is 16.86%- We loaned out 24mill and expect 4mill back in interest payments on top of principle
  
<INSERT TABLE WITH CURRENT COLLECTIONS>
 
The data does not provide sum of all principle payments made on the loan. To find principle paid, I took the total loan amount of un-charged-off loans and subtracted ending balance of January 2021. I found current interest paid by adding up cumulated interest.
  
<INSERT TABLE WITH BOTH COLLECTIONS>
<INSERT GRAPH WITH BOTH COLLECTIONS>

Currently, based on our collected interest we only have a 8.71% profit margin. There could be many reasons for this:
  - Abnormal amounts of prepayments
  - Could be expected numbers: low term loans finish first and they tend to payout less interest than long term loans (If provided with a database with all of the amortization schedules, I could find out exactly how much interest/principle we should have at this point)
  - Could be high deliquency and charge-off rate

  
  
## Charge Off Analysis <a name="charge-off-rate-analysis"></a>
The charge-off rate is a key metric in judging the performance of a loan portfolio. The data only provides the charge-off amounts for loans charged-off in Jan 2021. For a more in-depth and exact analysis, I would need the amount charged-off for all the loans. For this data set, I estimated. If a loan had no "last pay date", I assumed that the borrower made no payments and the full amount was charged-off. If a loan had a last pay date, I'd substract payments from the total based on how many months passed between the last pay date and start date. This is a rough estimation that doesn't take into account: prepays, previously missed payments before last payment, extra interest added due to lack of payment. 

<INSERT TABLE WITH CHARGE-OFF RATE AND DELIQUENCY RATE>
 
Current charge-off rate is 0.52%. According to the federal reserve, the 2020 average charge-off rate for commercial banks is 2.5%, meaning this portfolio is performing far better than average. However, we need to take a look at the deliquency rate because today's deliquents are tommorows charged-off accounts. The portfolios deliquency rate is at 3%, above the national average of 2.5%. Next, we want to take a look at what will happen to the charge-off rate over time if every deliquent account eventually charge's off.
  
<INSERT CHARGE OFF RATE GRAPH>
  
This chart shows the projected charge-off rate if every deliquent loan charges off. We only are going out three years because 99%+ of the portfolio should be closed out by then. In Jan 2022, the deliquency rate will jump to 1.47%. In two years, it jumps to 3.13%, surpassing 2020 national average. In three years, the charge-off rate reaches 3.62%. 
