---
title: "Hotel booking cancellations"
date: 2020-09-20
description: An analysis of guests’ booking and cancellation trends for two Portuguese hotels.
menu:
  sidebar:
    name: 01 Hotel booking
    identifier: exploratory
    weight: 30
---

An analysis of guests’ booking and cancellation trends for two Portuguese hotels.

---

*These reports were written as part of the requirements for the Data Analytics Lab module for [MITB](https://scis.smu.edu.sg/master-it-business).*

For executive report, please view : [Executive report - hotel booking](https://drive.google.com/file/d/1PF6ZHf-r5Fm_WzqlCgfGxuBDRdVKsV4A/view?usp=sharing)

## 1. Overview
**Changing Landscape of the Hotel Industry**
According to [D-Edge](https://www.d-edge.com/the-rise-of-direct-bookings-over-otas/), the rise of online travel agents (OTAs) has caused hotels in Europe to experience a shift in distribution channel mix – in particular, from the websites of hotels, to OTAs (particularly Booking.com). The market share of Booking.com increased by 4.7% from 43.6% in 2014 to 48.3% in 2018, while that of hotels’ websites declined by 6.3% from 27.2% in 2014 to 20.9% in 2018.  

From a revenue standpoint, this shift is not necessarily a concern as Booking.com’s reservation revenue index grew by 62.4%, compared to the hotels’ websites which declined by 12.5% over 5 years ([D-Edge](https://www.d-edge.com/the-rise-of-direct-bookings-over-otas/)).  

With the emergence of OTAs and their free cancellation policy, there has been a corresponding increase in cancellations. On average, cancellation rate in Europe rose by 7.1% from 32.5% in 2014 to 39.6% in 2018 ([D-Edge](https://www.d-edge.com/the-rise-of-direct-bookings-over-otas/)). Given that travelers are accustomed to free cancellation policies, hotels should take necessary steps to mitigate cancellation risk by using guests’ booking data.


## 2. Objectives
The main objective is to identify insights through analysing guests’ booking behaviour and cancellation patterns, so as to enable hoteliers to take the necessary action to reduce cancellations and optimise occupancy, and thus profits.  

In identifying behaviour patterns, we will study the cancellation rate against customer profile, distribution channel, length of stay, lead time, seasonality and others.  

This study involves using JMP Pro 15 to process the data, exploratory data analysis to identify trends as well as insights, and confirmatory analysis to support our findings.  

## 3. Data
### 3.1 Dataset
The datasets were extracted from “Hotel booking demand datasets” by [ScienceDirect](  https://www.sciencedirect.com/science/article/pii/S2352340918315191). The two datasets consist of booking data from Jul-15 to Aug-17 (25 months) of two hotels in Portugal – an Algarve resort hotel (H1) and a Lisbon city hotel (H2). 

### 3.2 Data Preparation
Given that the two datasets have identical structures, data reorganisation was not required. Original datasets were imported into JMP and stacked to form a consolidated dataset. A new column was created to list the file name (H1.csv and H2.csv) for hotel identification.   

To ensure completeness of the consolidated dataset, the dataset was checked to ensure that there were 31 columns and 119,390 rows (H1: 40,060 rows and H2: 79,330 rows).  

Next, in the data cleaning and transformation process, we identified several data issues and took steps to rectify these issues to meaningfully analyse the data. Please refer to section 3.2.1.  

Finally, the dataset was reduced by removing variables that were irrelevant to this study. 

**3.2.1 Data Quality Issues Identified**  
  
**(a) Variable values lack context**  
The variables ‘IsCanceled’ and ‘IsRepeatedGuest’ are categorical data but has numeric values (0 and 1) that represents (No and Yes). This labelling is not self-explanatory and requires the reader to infer or constantly refer to legend. Without any context, such labelling may potentially lead to misinterpretation.  
  
Hence, for ease of reference and readers’ clarity, values were recoded as follows:

{{< img src="/posts/projects/exploratory/images/fig1.png" align="left" >}}
*Figure 1*  

**(b) Inaccurate Data Types**  
2 variables were recoded to the correct attributes, please see figure 2. We did not correct attributes for ‘IsCanceled’ and ‘IsRepeatedGuest’.  
{{< img src="/posts/projects/exploratory/images/fig2.png" align="left" >}}
*Figure 2*

**(c) Missing values**  
i.	Variable ‘Children’ - 4 missing values  
Missing values accounted for <1% of total. Given that the proportion of missing values are insignificant, missing values will not skew the analysis. Hence, we have relabelled all missing values to “NA”.  

**(d) Data is segregated into multiple columns**  
**i) Date**  
We have concatenated ‘ArrivalDateYear’, ‘ArrivalDateMonth’ (in character form, i.e July), and ‘ArrivalDateDayofMonth’ to form “Arrival Date”, formatted in m/y format.  
There were 2 steps to this process:  
    1)	recoding ArrivalDateMonth into numerical values (i.e July - 7), and  
    2)	concatenate these 3 variables
  
  
**ii) Customer segments**  
“Customer Segment” was formulated to profile travellers into 5 types of travellers – Day Trippers, Solo, Couple, Family and Groups. Values were derived using the formula below.  

With this, trends between types of travellers and cancellation rates can be observed.  
{{< img src="/posts/projects/exploratory/images/fig3.png" align="left" >}}  
*Figure 3*  

**iii) No of nights**  
We have concatenated ‘StaysInWeekendNights’ and ‘StaysInWeekNights’ to obtain the total length of stay/booking. This column was created using the formula below:  
{{< img src="/posts/projects/exploratory/images/fig4.png" align="left" >}}  
*Figure 4*

**iv) Room assigned**  
Where assigned rooms differ from reserved ones – due to upgrading by hotel, request to change and others, a new column indicating “Diff room” and “Same room” has been created for this using the formula below.   
With this, we can observe how cancellation rate trends with room change.   
{{< img src="/posts/projects/exploratory/images/fig5.png" align="left" >}}  
*Figure 5*  

**(d) Ghost booking – 97 bookings**  
Closer examination of the data revealed 97 records of ghost booking where occupants were 0 (day tripper), length of stay > 0 and had subsequently checked out. We have filtered out these records using “Row Selection” under the Table function.  
  
As we are not able to explain the reason for such combination, we have excluded these records for our analysis. This matter will be raised for further investigation.   
{{< img src="/posts/projects/exploratory/images/fig6.png" align="left" >}}  
*Figure 6*

**(e) Too many classes**  

i.	Agent
{{< img src="/posts/projects/exploratory/images/fig7.png" align="left" >}}  
*Figure 7*  
‘Agent’ represents the ID of respective travel agencies; there are 334 levels. The sheer number of IDs makes it difficult to produce meaningful analysis. Null values indicate that these bookings do not originate from travel agents and are therefore NOT considered as missing values.  

Thus, we have recoded number values to “travel agent” and NULL values to “non-agent. With this, we are able observe cancellation patterns between travel agents and non-agents. 
  
ii.	Company
{{< img src="/posts/projects/exploratory/images/fig8.png" align="left" >}}  
*Figure 8*  
  
Similarly, ‘Company’ represents ID of respective companies; there are 353 levels, thus we have recoded number values to “company” and NULL values to “non-company”.


iii. Country  
{{< img src="/posts/projects/exploratory/images/fig9.png" align="left" >}}  
*Figure 9*    

Refers to nationality of hotel guests. With 178 levels, it is difficult to analyse cancellation rates for all countries. Hence for a more meaningful analysis, we have retained the top 8 countries, which accounts for ~80% of total population, and grouped the rest as “Others”.   

iv.	Meal  
{{< img src="/posts/projects/exploratory/images/fig10.png" align="left" >}}  
*Figure 10*  

Refers to meal packages. According to Antonio, Almeida and Nunes (2018), ‘SC’ and ‘Undefined’ are considered as ‘no meal’, we have grouped them accordingly.  
  
v.	Market Segment  
{{< img src="/posts/projects/exploratory/images/fig11.png" align="left" >}}  
*Figure 11*   
  
We have recoded to group “Aviation”, “Complementary” and “Undefined” together on basis that individually account for <1% of total.

vi.	Distribution channel  
{{< img src="/posts/projects/exploratory/images/fig12.png" align="left" >}}  
*Figure 12*  
   
“Aviation”, ‘complementary’ and ‘undefined’ were grouped together.  

**(f) Extreme outliers**  
In order to meaningfully analyse the data, extreme outliers were removed on basis that the average guests do not conform to these behavioural patterns, thus retaining the data may skew the analysis.	  
  
i) Adults  
Excluded 3 observations with >30 adults – account for <1% of population and will not affect analysis.  
{{< img src="/posts/projects/exploratory/images/fig13.png" align="left" >}}  
*Figure 13*  

ii) Children  
An observation with 10 babies were excluded as it appears to be one off.  
{{< img src="/posts/projects/exploratory/images/fig14.png" align="left" >}}  
*Figure 14*  

iii) Babies  
Similarly, we have excluded two separate bookings – 2 adults and 10 babies, 1 adult and 9 babies.  
{{< img src="/posts/projects/exploratory/images/fig16.png" align="left" >}}  
*Figure 15*
 

iv) LeadTime  
Two observations – 737 and 709 days were excluded.  
{{< img src="/posts/projects/exploratory/images/fig17.png" align="left" >}}  
*Figure 16*

## 4. Insights

# 4.1 Cancellation rates differ by hotel – City 41.7% and Resort 27.8%
{{< img src="/posts/projects/exploratory/images/fig18.png" align="left" >}}  
*Figure 17*  
  
The cancellation rate for the two hotels were 37% across 25 months. This is relatively consistent with the average cancellation rate in [Europe](https://www.d-edge.com/how-online-hotel-distribution-is-changing-in-europe) - 34.8% in 2015, to 41.3% 2017.  
  
However, further investigation revealed that City hotel’s cancellation rate of 41.7% was significantly higher compared to Resort hotel of 27.8%. See figure 18.  
  
Thus, we will analyse cancellation rate for the two hotels separately, with a view to identifying cancellation patterns for respective hotels.  

{{< img src="/posts/projects/exploratory/images/fig19.png" align="left" >}}  
*Figure 18*    

{{< img src="/posts/projects/exploratory/images/fig20.png" align="left" >}}  
*Figure 19*   

Interestingly, although City hotel had a higher average cancellation rate, the rate has been relatively consistent across the 25 months. In contrast, Resort hotel’s cancellation rate has been steadily increasing.

# Seasonality
# 4.2 Cancellation fluctuated across the months due to seasonality.

For City hotel, we observed some seasonality during the years; bookings peaked around Sep/Oct and May/June. Similarly, cancellation rates fluctuated during the year (figure 21).   
  
{{< img src="/posts/projects/exploratory/images/fig21.png" align="left" >}}  
*Figure 20*    

{{< img src="/posts/projects/exploratory/images/fig22.png" align="left" >}}  
*Figure 21*     
  
Similarly, bookings for resort hotel had peaked in Sep/Oct; other busy months included April-16 and August-17.  
While cancellation rates tend to fluctuate across the year, peak cancellation months were between July and August - the summer months.
  
{{< img src="/posts/projects/exploratory/images/fig23.png" align="left" >}}  
*Figure 22*    

{{< img src="/posts/projects/exploratory/images/fig24.png" align="left" >}}  
*Figure 23*   

# Customer demographics
# 4.3 Couples accounted for ~70% of bookings, but form the biggest group to cancel for City Hotel.

{{< img src="/posts/projects/exploratory/images/fig25.png" align="left" >}}  
*Figure 24*   
  
Guests’ demographics were similar for both hotels. Couples accounted for ~69% of total booking for both hotels.

{{< img src="/posts/projects/exploratory/images/fig26.png" align="left" >}}  
*Figure 25*  

Despite the similarity in guests’ profile, the cancellation rate by customer segment differs for each hotel.   
For City Hotel, couples cancelled the most (45%). In contrast, for Resort Hotel, day trippers had the highest cancellation rate of 66.7%, although day trippers’ bookings were <1% of total. 

# 4.4 Portuguese Nationals formed the highest cancellation group for both hotels.
{{< img src="/posts/projects/exploratory/images/fig27.png" align="left" >}}  
*Figure 26*  
  
Based on our observations, the Portuguese nationals, the largest proportion of guests for both hotels (39% to 44%), had the highest cancellation rate among all countries – 64.9% for City, and 42.2% for Resort.  
  
This suggests that cancellation rate is not independent of nationality of guests.
  
*4.4.1 Is cancellation independent of guests’ nationality? (Hypothesis testing)*  
  
To validate our analysis, we have performed the Chi-Square test. The Chi-Square’s results are reliable as the counts (see Contingency table) of all Countries are >5. Using a confidence level of 95% (α = 0.05), our hypothesis was defined as:  
  
- H0 = There is no association between the guests’ nationality and cancellation.
- H1 = There is an association between the guests’ nationality and cancellation.
     
Since both hotels has similar cancellation trends by nationality, hypothesis was tested on a consolidated level.  
  
{{< img src="/posts/projects/exploratory/images/fig28.png" align="left" >}}  
*Figure 27*  
  
{{< img src="/posts/projects/exploratory/images/fig30.png" align="left" >}}  
*Figure 28*  

{{< img src="/posts/projects/exploratory/images/fig.29" align="left" >}}  
*Figure 29*

    
With the p-value 0.001 < critical value 0.05, there is no statistical evidence to support the claim that cancellation rates are independent of nationality.  

# 4.5 Portuguese couples and solo travellers - extremely high cancellation rate of 64-70%

{{< img src="/posts/projects/exploratory/images/fig31.png" align="left" >}}  
*Figure 30*  
  
Portuguese couples and solo travellers, who accounted for 37.7% of total bookings, were the driving force of high cancellation rates.  

{{< img src="/posts/projects/exploratory/images/fig32.png" align="left" >}}  
*Figure 31*

# Distribution channel
# 4.6 Cancellation rate was the highest for TA/TO and lowest for direct.

{{< img src="/posts/projects/exploratory/images/fig33.png" align="left" >}}  
*Figure 32*  

{{< img src="/posts/projects/exploratory/images/fig34.png" align="left" >}}  
*Figure 33* 

TA/TO, the largest channel, had a significantly high cancellation rate of 41%, as compared to the rates of other channels of 17% - 22%.  
Although ‘MarketSegment’ variable segregated TA/TO into online and offline, we did not use this variable as there were undefined terms and we were unable to identify which channel the bookings had originated.  
  
*4.6.1 Is cancellation independent of distribution channel? (Hypothesis testing)*  
  
To validate our hypothesis, we performed the Chi-Square test as both variables are categorical variables. The Chi-Square result is reliable as the counts (see Contingency table) are >5. Using a confidence level of 95% (α = 0.05), our hypothesis was defined as:  
-	H0 = There is no association between the distribution channel and cancellation.  
-	H1 = There is an association between the distribution channel and cancellation.  
  
{{< img src="/posts/projects/exploratory/images/fig35.png" align="left" >}}  
*Figure 34* 

With the p-value 0.001 < critical value 0.05, we can conclude that cancellation rates are not independent of the distribution channel.

# Guests’ booking patterns
# 4.7 Cancellation rate increased with bookings for short term stay (0-18 nights), but decreased with longer stays ( > 18 nights)  
  
{{< img src="/posts/projects/exploratory/images/fig36.png" align="left" >}}  
*Figure 35*  

Interestingly, figure 35 suggests that cancellation rate is positively correlated with length of stay, until a certain point, then longer stays become negatively correlated with cancellation rate.  
To further observe the correlation of cancellation rate and length of stay, we have analysed duration of stay by short (0 – 18 nights) and long-term stay (18 to 69 nights). Since both hotels have similar trends, we analysed them on a consolidated level.  
  
 
{{< img src="/posts/projects/exploratory/images/fig37.png" align="left" >}}  
*Figure 36* 

Further investigation revealed that there is  
i)	a weak-moderate positive linear relationship for short-term stay (r = 0.435).  
ii)	a moderate negative linear relationship for long-term stay (r = -0.608).  
  
# 4.8 Cancelled bookings have longer lead time on average.

{{< img src="/posts/projects/exploratory/images/fig38.png" align="left" >}}  
*Figure 37*

Lead time refers to the number of days between system recorded date of booking and arrival date.
We observed that cancelled bookings for both hotels tend to have longer lead time. The mean lead time for cancelled (145 days) was 1.8x of non-cancelled bookings (80 days).  
This seems to indicate that the bookings with longer lead time have a higher cancellation rate.   
  
*4.8.1 Is there a difference in the average lead time for cancelled and non-cancelled? (Hypothesis testing)*  

To decide on our hypothesis testing method, we had to determine if (a) variance is equal and (b) distribution of lead time is normal.  

a)	Variance is unequal  
  
JMP performed 5 different tests for the equality of variances. As shown in figure 38, all tests have the same conclusion - p-values 0.001 < critical value 0.05. Thus, there is sufficient evidence to reject null assumption that variances are equal. Therefore, this data will be analysed using an unequal variance test.  

{{< img src="/posts/projects/exploratory/images/fig39.png" align="left" >}}  
*Figure 38* 

b)	Distribution of Leadtime is not normal 
  
To test normality, we have performed the Anderson-Darling Goodness of Fit Test with confidence level of 95%. With p-value 0.001 < critical value 0.05, there is no statistical evidence to support that lead time’s distribution is normal. Thus, this data will be analysed using a non-normal test.  

{{< img src="/posts/projects/exploratory/images/fig40.png" align="left" >}}  
*Figure 39* 

Given that the data failed to conform to equal variance and normal distribution assumption, the Welch test was used to perform our hypothesis testing.  
Since both hotels have similar trends, we tested our hypothesis on a consolidated basis. Using a confidence level of 95%, our hypothesis was defined as follows:  
-	H0 = There is no difference between the average lead time for cancelled and not cancelled bookings.  
-	H1 = There is a difference between the average lead time for cancelled and not cancelled bookings.  


{{< img src="/posts/projects/exploratory/images/fig41.png" align="left" >}}  
*Figure 40* 


Test result (figure 40) with p-value 0.0001 < our critical value 0.05. Hence, there is statistical evidence to reject the null hypothesis. Thus, we can conclude that the average lead time for cancelled and not cancelled bookings is different.  

# 4.9 Bookings with reassigned rooms had fewer cancellations
  
{{< img src="/posts/projects/exploratory/images/fig42.png" align="left" >}}  
*Figure 41*

{{< img src="/posts/projects/exploratory/images/fig43.png" align="left" >}}  
*Figure 42* 

“Same room” bookings are bookings where reserved and assigned rooms were of the same type. While for “Diff room” bookings, reserved and assigned rooms were of different type.  
  
Reasons for reassignment, or when assigments were made, were not provided. For this analysis, we have assumed that all reassignments were made prior to check-in as there were combinations of ‘diff room’ and reservation status of ‘cancelled’/’no show’.  
  
Figure 41 indicates that bookings with reassigned rooms had a much lower cancellation rate of ~5% compared to bookings with same rooms of 33% - 45%.  

# 4.10 Recurring guests cancelled less

{{< img src="/posts/projects/exploratory/images/fig44.png" align="left" >}}  
*Figure 43* 

{{< img src="/posts/projects/exploratory/images/fig45.png" align="left" >}}  
*Figure 44* 

Cancellation rate for City Hotel for repeat guests was 21.8% and non-repeat guests 42.3%. While for Resort Hotel, cancellation rate for repeat guests was 6.2% and non-repeat guests 28.7%.
However, repeated guests only accounted for 2-4% of respective hotels’ booking.
 
{{< img src="/posts/projects/exploratory/images/fig46.png" align="left" >}}  
*Figure 45*

## 5. Intrepretation of results
**Location matters.**
Cancellation rate for city hotel was higher (42%) versus resort’s (28%). Interestingly, the cancellation rate throughout the 25 months for City Hotel has remained consistently around this level (42%) while that of Resort hotel had increased from 26% to 31%.   

**Expect seasonality.**  
Cancellation rates fluctuate on a monthly basis and tend to peak between July to August - summer months.   
 
**Couples are crucial.**  
Couple travellers accounted for ~69% of the bookings, but have a high cancellation rate of 45% for City Hotel and 30% for Resort hotel.  
 
**Particularly Portuguese couples and solo travellers.**  
These travellers, who make up 37% of total bookings, drove cancellation with rates of 65% for couples and 77% for solo travellers.  
 
**OTAs drives cancellation.**  
OTAs, which accounts for 82% of bookings, were main drivers of high cancellations with rate of 41%.
In contrast, direct channels (12% of total booking) had a cancellation rate of 18%.  
 
**Length of stay.**  
Cancellation increases with short term stay (0 - 18 days) until a certain point, then decreases with longer stays (> 18 days).  
   
**Early bookers cancel more.**  
On average, lead time for cancelled bookings (~145 days) are 1.8 times of non-cancelled bookings (80 days).   
   
**Satisfied guests.**  
Guests who were reassigned to different rooms from their reserved rooms had a cancellation rate of ~5%. Reasons for reassignment and when reassignments were made was not stated. Low cancellation rate suggests that guests were satisfied with the reassignment.  
  
**So, they come back!**  
Repeat guests cancel less than new guests.  
 


