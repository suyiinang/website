---
title: "Cycle Plots"
date: 2021-02-09
description: Cycle Plots for Singapore's tourist arrival by country
menu:
  sidebar:
    name: Cycle Plots
    identifier: cycle plot
    parent: Tableau How to
    weight: 100
math: true
---

---

*Documenting my Tableau learning journey.*

---

## Cycle plots
{{< img src="https://public.tableau.com/profile/suyiinang#!/vizhome/CycleplotSingaporestouristbycountry/Dashboard1" align="left" >}}
Full visualisation available at [@suyiinang](https://public.tableau.com/profile/suyiinang#!/vizhome/CycleplotSingaporestouristbycountry/Dashboard1).

## Used for 
- useful for analysing seasonality / cyclical patterns

## How to create - step by step
I have used the monthly international visitor arrivals by country data from [data.gov.sg](https://data.gov.sg/dataset/total-visitor-international-arrivals-to-singapore?resource_id=83063203-ff81-4764-a9dc-c4e209921fe7).

**Step 1 - Date column in correct data type**
Make sure data column is in the "Date" data type.
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig2.png" align="left" >}}

**Step 2 - Data in flat file format**
Here my download data is already in flat file format, ie stacked downwards, hence no further transformation is required.  

However, if your data is across the columns (see figure 3 below), you will need to pivot the data into a flat file. (Don't worry! Tableau makes this very easy).  
Select the necessary columns, right click and select 'Pivot' and there you have it!
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig3.png" align="left" >}}

**Step 3 -  Filter Date**
My current dataset has data from year 1978 to 2015, which may be too overwhelming.  
For this exercise, I only want data from 2005 to 2015. (SARS affected Singapore's tourism in 2004, hence I want to exclude that as it is a anomaly.)  
To do so, I dragged the "Month" field to the Filters panel > Range of Dates and applied filter according to figure below.  
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig4.png" align="left" >}}  
  
Right click and show filter. Here you can move the slider according to the dates you want.  
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig4_1.png" align="left" >}}


**Step 4 - Populate columns and rows**
Populate rows according to the figure below. 
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig5.png" align="left" >}}

Your chart should now look like this:  
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig6.png" align="left" >}}

**Step 5 - Filter country**  
To see the cycle plot by country, add country into the Filters panel, select one country > right click > show filter. The list of country should be to the right of the chart.  
Click on the arrow button of the Country filter and select "Single Value (list)".  
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig7.png" align="left" >}}

**Step 6 - Add reference line**  
Right click on y-axis > add reference line > fill according to the figure below.  
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig8.png" align="left" >}}
This shows me the average visitors per month across the years.  

**Step 7 - Create dynamic title**  
I want a dynamic title that changes according to my country filter. 
{{< img src="/posts/Tableau_Howto/01_cycleplot/images/fig9.png" align="left" >}}
Use the "Insert" dropdown to insert field name.

There have you it! An interactive cycle plot.

---
I would like to thank Prof Kam of Singapore Management University for the inspiration.
