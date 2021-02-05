---
title: "Post-COVID Recovery for SIA"
date: 2020-11-18
description: Spreadsheet modeling
menu:
  sidebar:
    name: Post-COVID Recovery for SIA
    identifier: modeling
    weight: 96
math: true
---

# Optimizing Passenger-Cargo Fleet Allocation

*By: Ang Su Yiin, Gabriella Pauline Djojosaputro, Gordy Adiprasetyo, Kendra Luisa Baylon Gadong, Nguyen Nhi Thai An, Ulysses Chong Min Zhen*  

*These reports were written as part of the requirements for the Spreadsheet Modeling module for [MITB](https://scis.smu.edu.sg/master-it-business).*

---

For executive report, please view: [Executive Report](https://drive.google.com/file/d/17p2WRqtOOMQZ02qUpxHlfI5-GlJbnYPo/view?usp=sharing)

## 1.	Problem Statement  
With the halt of international travel due to COVID-19, the global aviation industry is one of the industries that was hit the worst. Border controls and travel restrictions were put in place, and the demand for air travel continued to be severely impacted. In Singapore, the airline operations are at standstill given all flights are international. Since passenger aircrafts sit idly due to the pandemic, [airlines started operating those aircrafts to cargo-carrying ones as an alternative revenue stream](https://www.straitstimes.com/singapore/transport/coronavirus-sias-scoot-modifies-aircraft-to-carry-out-cargo-deliveries). Passenger airlines said in a [survey](https://asianaviation.com/covid-19-airlines-look-to-keep-some-planes-flying-by-pivoting-from-passengers-to-cargo/) that 43% of them will keep their passenger-cargo ratio, 37% said airlines will place a greater emphasis on cargo, and 19% said airlines will make a permanent shift to cargo.  
  
With that, this study aims to optimize the aircraft allocation of airlines’ fleets according to the post COVID-19 aviation industry environment through data modelling. Given a certain size of aircraft fleet, the study aims to help airline companies allocate how many aircrafts should be used for passengers, cargo, or how many should be put to storage. Additionally, a price point where an aircraft should be scrapped rather than put in storage will also be estimated. In this project, the focus is on Singapore Airlines (SIA) operations.   

## 2.	Data sources  
Data is obtained from a variety of sources covering financial and operational aspects of SIA:  
•	Financial Reports: from [SIA website](https://www.singaporeair.com/en_UK/sg/about-us/information-for-investors/financial-results/)   
•	Fleet Information: from [mainlymiles](mainlymiles.com), [centreforaviation](centreforaviation.com), and [planespotters](planespotters.net)  
•	Covid-19 daily new cases per capita: from https://ourworldindata.org/covid-cases  
•	Historical Singapore Visitor Arrivals by Country: from https://www.ceicdata.com/en  

## 3.	Influence diagram and Black Box model
### 3.1.	Black Box Model  

{{< img src="/posts/05_SIA/images/fig1.png" align="left" >}}
*Figure 1*  

{{< img src="/posts/05_SIA/images/fig2.png" align="left" >}}
*Figure 2*

{{< img src="/posts/05_SIA/images/fig3.jpg" align="left" >}}
*Figure 3*  

{{< img src="/posts/05_SIA/images/fig4.png" align="left" >}}
*Figure 4*

## 4.	Computation and Analysis  
The spreadsheet model is built for the purpose of making the following computations and analyses:  
•	Each year from 2020 until 2025, compute optimum allocation of aircrafts by respective operation unit to maximize profits  
•	Compute scrap price for stored aircrafts  
Each sub-component as outlined in the influence diagrams is explained in further detail below.  

### 4.1	Forecasting COVID recovery rate by country from 2021 to 2025  
Based on the current number of [COVID cases per capita](https://ourworldindata.org/covid-cases), each country is assigned a risk profile based on a [traffic light system](https://www.dw.com/en/coronavirus-what-the-eus-new-traffic-light-system-means/a-55265476) adapted from the European Center for Disease Prevention and Control (ECDC). Each country is assigned a traffic light (Green, Yellow, Red) based on the rate of new infections per 100,000 inhabitants in the past 14 days:  
  
-	Green is for countries reporting less than 1 new infection per 100,000 inhabitants.  
-	Yellow is for countries reporting greater than 1 new infection per 100,000 inhabitants and trend of daily new cases is going down.  
-	Red is for countries reporting greater than 25 new infections per 100,000 inhabitants or countries reporting greater than 1 new infection per 100,000 inhabitants and trend of daily new cases is going up.  
  
There are two sets of opening dates: **partial** (business travel only) and **full** [(365 days after vaccine is available)](https://www.bmj.com/content/371/bmj.m3846). Each country in the green and yellow category will be assigned two opening dates based on the traffic light profile. Countries in the red category will only have one reopening date – fully reopening date.  

{{< img src="/posts/05_SIA/images/fig5.png" align="left" >}}
*Figure 5*  

For Yellow bucket countries, daily new cases are projected using a curve-fitting approach with a Log-Normal distribution  to meet the asymmetric feature of the distribution of daily new cases of COVID-19. The formula for the Log-Normal Distribution (Fig. 6) and Yellow bucket country Maldives curve-fitting example is illustrated in Fig. 7 and 8.

{{< img src="/posts/05_SIA/images/fig6.png" align="left" >}}
*Figure 6*

{{< img src="/posts/05_SIA/images/fig7.png" align="left" >}}
*Figure 7*  

Using Solver, the curve-fitting approach minimizes the error from the fitted value and the observed daily COVID case per million by changing the parameters peak height a, peak position b, and width c. (Fig. 7). Then, an estimated partial reopening date for a yellow bucket country is forecasted when the daily new case per million is down to one case. For Maldives, the partial reopening date is 1 January 2021. This approach is done for all yellow bucket countries.  

{{< img src="/posts/05_SIA/images/fig8.png" align="left" >}}
*Figure 8*  

After assigning each country with a traffic light profile and estimated reopening dates, recovery rates will be based on the country’s opening status.  SIA recovery rate is currently at [1.5%](https://sg.news.yahoo.com/changi-airport-now-worlds-58th-busiest-serving-15-of-usual-passenger-volume-ong-ye-kung-075644907.html) based on current rate of passenger volume in Changi Airport. Partial reopening dates are matched with a 16.5% recovery rate based on [Singapore Airlines optimistic forecast](https://www.singaporeair.com/en_UK/sg/media-centre/news-alert/?id=k88gnin9) on returning to approximately 15% of its passenger capacity from pre-COVID levels.   
  
This model assumes that SIA recovery is progressive for all countries, which means that full recovery rate at 100% is expected in December 2025. To summarize the recovery rate calculation, recovery rate per country over time (in months) is forecasted linearly from 1.5% from today to partial reopening date and to 16.5% from the fully open date based on vaccine and to 100% by end of 2025.  

{{< img src="/posts/05_SIA/images/fig9.png" align="left" >}}
*Figure 9*     

For each country, forecasted recovery rate by end of year is calculated by taking the average of recovery rates for that particular year. Historical data of [visitor arrivals](https://www.ceicdata.com/en) from SIA destination countries are extracted to then forecast number of visitors per year based on recovery rates (Fig. 10).  

{{< img src="/posts/05_SIA/images/fig10.png" align="left" >}}
*Figure 10*   

Overall forecasted recovery rate and recovery rates per traffic light profile are summarized in Table 2 with visual representation in Fig. 11.  
{{< img src="/posts/05_SIA/images/fig11.png" align="left" >}}
*Figure 11*   

{{< img src="/posts/05_SIA/images/fig12.png" align="left" >}}
*Figure 12*  
  
### 4.2	Forecasting cargo demand  
Cargo demand is assumed to remain constant for the period of 2021 to 2025 and will be the same as [2019 demand](https://www.singaporeair.com/saar5/pdf/Investor-Relations/Financial-Results/News-Release/nr-q4fy1920.pdf). This assumption is reasonable because as more passenger aircrafts are grounded during COVID-19 and its recovery period, cargo transportation can mostly be done only by [cargo aircrafts](https://etradeforall.org/icao-air-cargo-resilience-in-the-times-of-covid-19/), therefore the demand for cargo services of SIA will [not drop](https://mainlymiles.com/2020/07/23/analysis-singapore-airlines-cargo-only-flights-using-passenger-aircraft-in-july/). Conservative assumption of constant instead of increasing demand is also adopted to simplify analysis, since obtaining accurate approximation of increase in demand requires in-depth studies on the cargo transportation market for the next 5 years.

### 4.3	Forecasting costs for passenger service, cargo service and storage  
For passenger and cargo services, the following steps are taken to calculate their per aircraft costs in 2019:  
1.	Total expenses for passenger and cargo services are retrieved from SIA Financial Reports FY19. (FRFY19)  
2.	Number of aircrafts for 2019 are [retrieved](https://www.planespotters.net/airline/Singapore-Airlines).  
3.	Costs per aircraft for passenger and cargo services are obtained by dividing total expenses by number of aircrafts in 2019.  
  
For storage:  
1.	SIA’s idle aircrafts are parked at Alice Spring, Australia. Parking charges are calculated per Maximum Takeoff Weight (MTOW) of the aircraft.  
2.	An average tonnage for all aircraft is obtained.   
3.	Storage cost per aircraft is obtained by multiplying (1) and (2)  
  
Total expenses are broken down into fuel and non-fuel costs for sensitivity analysis purposes. This breakdown is available in FRFY19 for passenger service but not cargo service. As such, the breakdown for cargo services is assumed to be the same as passenger service. Costs are assumed to be the same for non-fuel costs for years 2021 to 2025.  

### 4.4	Compute the optimum allocation of aircrafts to maximize profits by respective operation unit  
From FRFY19, passenger revenue and total passenger served are obtained, and from these the average ticket price per passenger is calculated. Yield for cargo services are obtained directly from FRFY19. Yield are assumed to remain constant for the years 2021 to 2025.  
  
Another pivotal statistic that was retrieved from FRFY19 is [Load Factor (LF)](https://centreforaviation.com/analysis/reports/singapore-airlines-2017-outlook-further-pressure-on-yields-as-premium-position-is-reinforced-321257), which measures capacity utilization of aircrafts. Several factors [affect LF](https://seekingalpha.com/article/3452476-4-reasons-airline-load-factors-will-never-reach-100) such as passenger distribution which is dependent on network routing. When the model allocates passengers and cargo into aircrafts for years 2021 to 2025, average LF will not exceed LF of year 2019 as we assume similar passenger distribution and flight routing.  
  
Using this and previous calculations, a revenue maximizing model is developed and is solved using Solver.  

{{< img src="/posts/05_SIA/images/fig13.png" align="left" >}}
*Figure 13*  

{{< img src="/posts/05_SIA/images/fig15.png" align="left" >}}
*Figure 14*  
   
GRG Non-linear solver method was first used but resulted in local optimum solutions. Given the complexity of the model and to be able to arrive at global optimum solution, Evolutionary solving method was chosen and used with the below specifications:  
{{< img src="/posts/05_SIA/images/fig16.png" align="left" >}}
*Figure 15*


### 4.5	For stored aircrafts: compute scrap price – if offer price is above scrap price, the aircrafts should be sold instead of stored.
  
Scrap price is computed from the net present value of projected yearly cashflow for each aircraft. The cashflow for each year is determined by the number of useful years left and the number of years it is allocated to storage. The projected cashflow assumes that when there is a need to put an aircraft into operation, the newest aircraft will be deployed first.   
  
 It has two possible values:  
1.	Storage cost: Computed using Alice Spring’s storage fee based on the aircraft’s [MTOW](https://www.alicespringsairport.com.au/airport-charges)   
2.	Expected yearly profit if not stored: Obtained from the base model  

{{< img src="/posts/05_SIA/images/fig17.png" align="left" >}}
*Figure 16*   

The last year of useful life’s cashflow is the sum of expected book value at retirement and storage cost or expected profit, depending on the storage allocation. The expected book value is calculated from the purchase cost minus the depreciation along the course of its useful life. The depreciation value is estimated from [SIA’s financial report](https://www.singaporeair.com/saar5/pdf/Investor-Relations/Annual-Report/annualreport1920.pdf).  

## 5.	Results  
Overall, SIA’s profit is highly dependent on passenger demand recovery rate.  
{{< img src="/posts/05_SIA/images/fig18.png" align="left" >}}
*Figure 17*    

Given that all countries are only forecasted to reopen in Dec-2022, a large proportion – 93% (125/133) of aircrafts are allocation to storage initially, and gradually allocation to passenger services as passenger demand recovers.  
{{< img src="/posts/05_SIA/images/fig19.png" align="left" >}}
*Figure 18*   

## 6.	Trade-offs and sensitivity
### 6.1	Sensitivity of fuel cost on total profit  
{{< img src="/posts/05_SIA/images/fig20.png" align="left" >}}
*Figure 19*    

Total profit is more sensitive to changes in fuel cost in the later years due to more aircrafts being in service. Based on figure 16, a 2.5% increase in fuel cost would result in losses, hence proper risk mitigation strategies, for example hedging fuel cost and dynamic seat pricing, must be in place to preserve profits.  
  
### 6.2 	Sensitivity of passenger demand recovery rate on total profit  
{{< img src="/posts/05_SIA/images/fig21.png" align="left" >}}
*Figure 20*    

The sensitivity analysis of passenger demand recovery reveals that total profit highly sensitive to the vaccine availability date.  
Given that the vaccine release date is uncontrollable and uncertain at the date of this report, SIA should take the necessary steps to manage cash flow.  

### 6.3	Trade off analysis   
{{< img src="/posts/05_SIA/images/fig22.png" align="left" >}}
*Figure 21*

Profits would turn negative beyond a certain level of over allocation to passenger services due to supply outstripping demand for seats. As demand is the limiting factor, every additional plane allocated reduces profit. That being said, SIA may decide to allocate more aircrafts to passenger services to increase route offering for other business or technical reasons.  

## 7.	Model limitations and assumptions  
*Operating Costs*  
-	Model does not account for any redundancies and pay cut as projected cost is based on 2019 cost.  
-	Model does not account for any changes in flight operating cost (e.g. different number of flights per aircraft per year) as it is based on 2019 cost.  

*Aircrafts*  
-	SIA retires its plane at [25 years old](https://www.iata.org/contentassets/ffbed17ac843465aad778867cb23c45c/bipad.pdf).  
-	All aircraft purchases are put on [pause](https://www.forbes.com/sites/willhorton1/2020/05/02/singapore-airlines-seeks-fleet-flexibility-in-talks-for-aircraft-deferrals-and-sale-and-leaseback), and no plans of acquisition of smaller airlines or new subsidiaries.  
-	Model does not account for any sale of planes.  
-	Almost all aircraft types operated by SIA are similar enough to be counted homogeneously in modeling output in terms of routing and allocation. [All aircraft models](https://mainlymiles.com/2020/04/19/singapore-airlines-fleet-april-2020/), less the A380 or Boeing 747, are twin-engine-wide-bodied aircraft with similar range and passenger carrying capacity. This is aligned with the industry shift to use smaller twin-engine-wide-bodied aircrafts to service routes instead of larger jets with twice the capacity (such as A380 or Boeing 747) due to increase demand in non-hub airports.   

*Passenger Recovery Rate*  
-	SIA recovery rate will be based on the [31 countries](https://www.singaporeair.com/en_UK/sg/plan-travel/destinations/where-we-fly/) where airline has operating flights. Country’s future performance in COVID recovery projected is based on number of cases per capita as of 26 Oct 2020 and projected vaccine availability.  
-	Vaccine distribution timeline to reach herd immunity is assumed to be [1 year](https://www.bmj.com/content/371/bmj.m3846).  
-	COVID-19 recovery rate per country assumed to be progressive – full recovery by end of year 2025.  

Cargo Demand  
-	Model does not account for any changes in cargo as it is based on 2019 demand.  

---

Background photo created by [onlyyouqj](https://www.freepik.com/photos/background) at freepik
