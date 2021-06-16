# Loan Performance Analysis

<ul>
1. [Overview](#overview)
2. [The Data](#the-data)
3. [Data Summary](#data-summary)
4. [Portfolio Profit Analysis](#portfolio-profit-analysis)
5. [Prepayment Analysis](#prepayment-analysis)
6. [Charge Off Rate Analysis](#charge-off-rate-analysis)
7. [Conclusion](#conclusion)
8. [Sources](#sources)


## Overview <a name="overview"></a>
To ensure continuous portfolio profitability, we analyze loan data to measure current loan performance and identify any underlying risks


![cross-river](https://user-images.githubusercontent.com/74626307/122107942-a4269c80-cde9-11eb-93b9-a01dad561fad.jpg)



**Goals**
1. Provide insights into how the loans are performing
2. Identify additional data fields needed to create a more comprehensive report


## The Data <a name="the-data"></a>
I used the data from the Servicing Data Tape sheet in the Fintech Data Analyst Assessment excel workbook. It had 19999 records and 27 data fields for each record. First, I removed the four records with no report date. The report date is the date that the data was sourced. Since the practical application of this data relies on it being sourced at a known time, I can't use records with no report date. 

Next I looked through the data and found some loan records that do not make sense:


![Loan 13](https://user-images.githubusercontent.com/74626307/122025071-086c4080-cd97-11eb-9f44-2253fedfad45.png)


Because of some missing data fields, it's difficult to figure out exactly what is happening with this loan. Loan # 13 has a 7/6/2020 start date. The lack of a payment date and cumulated interest indicates that this loan was not paid back, neither in prepayment, nor in the terms of the loan. That would make it delinquent, but the 0 days past due and $0 ending balance indicates that the loan was paid. The loan hasn't been charged-off, so it sits in limbo until I have more information on it. 


I created an outline of all the possible statuses that a loan can be in and how it would be indicated in the data:

  
![Loan Statuys Chart](https://user-images.githubusercontent.com/74626307/122027146-db209200-cd98-11eb-8eb8-e79faa34ea0b.png)


**Charged-Off (CO)** is for loans that have been marked as being charged-off.

**Paid in Full (PIF)** is for loans that have been fully paid. It is indicated by not being charged off and having $0 ending balance on Jan 2021 with a non-blank last payment date so I can confirm that the loan was paid on. Loan 13 didn't have a payment date so I was not comfortable making the assumption that it is paid in full. 

**Ongoing on Time (OT)** is for loans that are currently active and are on time with payments as of Jan 2021. It is indicated by not being charged off, having a positive ending balance and being 0 days past due. 

**Ongoing Delinquent (OD)** is for loans that are currently active and are late with payments as of Jan 2021. It is indicated by not being charged off, having a positive ending balance and being more than 0 days past due.

**N/A** is for any loan that does not fit into these categories.


![Loan Status Bar Chart](https://user-images.githubusercontent.com/74626307/122028358-f4760e00-cd99-11eb-8b8c-db6e64ea4ab6.png)


918, or 4.59% of our data set falls into the N/A category. I'm removing these loans from the data set for my analysis because I cannot accurately figure out what is happening with these loans. If I misplace them, they will skew the results. 


## Data Summary <a name="data-summary"></a>
Before analyzing the data, we are going to take a look at the portfolio from a bird's eye view.


**Credit Spread**


The most important indicator of loan performance is the borrower's credit score. We're going to look at the portfolio credit score spread to see if there are any abnormalities. 


![image](https://user-images.githubusercontent.com/74626307/122029842-3bb0ce80-cd9b-11eb-9394-5c9664588a8f.png)


![Portfolio Credit Spread](https://user-images.githubusercontent.com/74626307/122030307-a9f59100-cd9b-11eb-8122-63f68254b78a.png)


There is a nice clean spread in the portfolio. Most of the portfolio (53%) sits right in the middle in the "Good" category. "Fair" and "Very Good" both have totals that cancel each other out, as they are an equivalent at ~19.80%. A small amount (6.75%) sits in the "Excellent" category. The average FICO score in the data is 712 and the average American FICO score is 711 which puts this portfolio right in line with the national average. 


**Term Spread**

  
![Portfolio Term Spread](https://user-images.githubusercontent.com/74626307/122030637-f3de7700-cd9b-11eb-815f-3bc41cf79f2e.png)

A majority of the loans are set at either 12 or 24 month terms. Those tend to be the most common. Otherwise, the terms are spread out without any abnormalities. 


  
## Portfolio Profit Analysis <a name="portfolio-profit-analysis"></a>
  
It's time to look at dollars invested and the profit from those dollars. 


![Expected Collections](https://user-images.githubusercontent.com/74626307/122156474-09ed4580-ce37-11eb-9d8c-f194cea8ba48.png)



In total, the portfolio's principle is $24 million. Assuming everyone paid on time with no issues, the portfolio should expect to see 4 million in interest, resulting in a 16.86% profit margin.


![Current Collections](https://user-images.githubusercontent.com/74626307/122156587-428d1f00-ce37-11eb-8545-b74b6f2a35fa.png)


The data analyzed does not provide the sum of principle payments made on the loans. To find principle paid, I took the total loan amount of non-charged-off loans and subtracted ending balance of January 2021. I found current interest paid by adding up cumulated interest.
  
 
 
![Expected and Current Collections](https://user-images.githubusercontent.com/74626307/122156597-47ea6980-ce37-11eb-8470-ead1fcb0a351.png)



![Expected and Current Collections Graph](https://user-images.githubusercontent.com/74626307/122031363-a1ea2100-cd9c-11eb-8451-d30ebb013b06.png)


Currently, based on our collected interest we only have a 8.71% profit margin. We've also collected 38% of our principle back but have only collected 19% of the interest expected. There could be many reasons for this:
  - Expected result. Short term loans finish earlier and tend to payout less interest than long term loans. 
  - Abnormal amounts of prepayments. I would need prepayment data to get exact figures, but I will do a rough estimation based on the given data. 
  - High delinquency and charge-off rates. People might not be paying their loans. This requires further analysis. 

  
## Prepayment Analysis <a name="prepayment-analysis"></a>

While there is no way to know exactly the dollar amount of prepayments with the given data, we can get a rough estimation by comparing the expected paid in full accounts to the actual paid in full accounts. We're going to bring back the loan status chart, take out the N/A's and show it as a percentage of the whole.


![Loan Status 2](https://user-images.githubusercontent.com/74626307/122155649-67809280-ce35-11eb-8d38-1ae168ce9cfe.png)


As of January 2021, 24.31% of the loans in the portfolio are paid in full. Since we have the start date and term numbers, we can map out how many loans in the portfolio we expect to be completely paid at any time.


![Percent Loans Completed](https://user-images.githubusercontent.com/74626307/122155874-d8c04580-ce35-11eb-861e-8fde9a1a5e48.png)


As of January 2021, only 6.07% of the loans should be paid in full. This means that this portfolio is suffering from a lot of prepayment issues which could explain the gap between principle collected and interest collected. 


## Charge Off Analysis <a name="charge-off-rate-analysis"></a>

A key metric in determining loan portfolio performance is the charge-off rate. The given data only provides the charge-off amounts for loans charged-off in Jan 2021. For a more in-depth and exact analysis, I would need the charge-off amounts for all the charge-off loans. For this analysis, I estimated. If a charged-off loan had no "last pay date", I assumed that the borrower made no payments and the full amount was charged-off. If a charged-off loan had a last pay date, I'd subtract payments from the total based on how many months passed between the last pay date and start date. This is a rough estimation that doesn't take into account: prepays, previously missed payments before last payment, extra interest added due to lack of payment. 


![Charge Off and Delinquency Rate Table](https://user-images.githubusercontent.com/74626307/122032166-613ed780-cd9d-11eb-90d7-cf857d297ef5.png)

 
Current charge-off rate is 0.52%. According to the federal reserve, the 2020 average charge-off rate for commercial banks is 2.5%, meaning this portfolio is performing far better than average. However, we need to take a look at the delinquency rate because today's delinquents are tomorrow’s charged-off accounts. The portfolios delinquency rate is at 3%, above the national average of 2.5%. Next, we want to take a look at what will happen to the charge-off rate over time if every delinquent account eventually charges off.


![Charge Off Rate Graph](https://user-images.githubusercontent.com/74626307/122032269-76b40180-cd9d-11eb-87fd-f3865b4eafb3.png)

  
This chart shows the projected charge-off rate if every delinquent loan charges off. In January 2022, the delinquency rate will jump to 1.47%. In two years, it jumps to 3.13%, surpassing 2020 national average. In three years, the charge-off rate reaches 3.62%. There is a high risk that this portfolio starts to charge-off more accounts and do worse than the average commercial bank. 


## Conclusion <a name="conclusion"></a>
Considering the incompleteness of the data, it's difficult to come to any concrete conclusions. 

Overall, the portfolio seems to be performing poorly relative to an average portfolio. The profit margin in January 2021 for this portfolio is lower than what you would expect. With with more information, I can figure out exactly how much principle and interest the portfolio should have collected by January 2021. Still, the high prepayment rate, high delinquency rate and EXPECTED high charge-off rate indicates that this portfolio is performing poorly.


## Next Step

Additional Data Fields Needed
- Amortization Schedule: I can use the amortization schedule to calculate percisely the amount of principle + interest the portfolio should have collected at any point.
- Prepayment #'s: Prepayment's throw off everything. If something is prepaid, we don't get interest on it. All exact calculations require knowing what loans were prepaid and by how much.
- Charge-Off #'s: I used a method to figure out how many dollars were charged off, but it would be better if I had the exact numbers. Additionally, if Cross River has estimates for how many delinquent accounts end up being charged-off, I could make a better charge-off estimation.  
- Principle paid: This would help tremendously to find exactly how much principle we have collected. It will also shed light on what was going on with the loans that seemingly made no sense. 


## Sources <a name="sources"></a>
https://www.federalreserve.gov/releases/chargeoff/chgallsa.htm
https://www.federalreserve.gov/releases/chargeoff/delallsa.htm
https://www.valuepenguin.com/average-credit-score


