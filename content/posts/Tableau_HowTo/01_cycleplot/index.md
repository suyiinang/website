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

Here we can see that visitors from the UK are typically lower in the months of May and June, and higher in March.  

<div class='tableauPlaceholder' id='viz1612865326246' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Cy&#47;CycleplotSingaporestouristbycountry&#47;Dashboard1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='CycleplotSingaporestouristbycountry&#47;Dashboard1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Cy&#47;CycleplotSingaporestouristbycountry&#47;Dashboard1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1612865326246');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else { vizElement.style.width='100%';vizElement.style.height='727px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>



## Good for
Analysing seasonality / cyclical patterns

## How to create - step by step
I have used the monthly international visitor arrivals by country data from [data.gov.sg](https://data.gov.sg/dataset/total-visitor-international-arrivals-to-singapore?resource_id=83063203-ff81-4764-a9dc-c4e209921fe7).

**Step 1 - Date column in correct data type**  
Make sure data column is in the "Date" data type.
![](images/fig2.png)  

**Step 2 - Data in flat file format**  
Here my download data is already in flat file format, ie stacked downwards, hence no further transformation is required.  

However, if your data is across the columns (see figure 3 below), you will need to pivot the data into a flat file. (Don't worry! Tableau makes this very easy).  
Select the necessary columns, right click and select 'Pivot' and there you have it!  
![](images/fig3.png)  

**Step 3 -  Filter Date**  
My current dataset has data from year 1978 to 2015, which may be too overwhelming.  
For this exercise, I only want data from 2005 to 2015. (SARS affected Singapore's tourism in 2004, hence I want to exclude that as it is a anomaly.)  
To do so, drag the "Month" field to the Filters panel > Range of Dates and apply filter according to the figure below.  
![](images/fig4.png)    
  
Right click and show filter. You can move the slider according to the dates desired.  
![](images/fig4_1.png)  


**Step 4 - Populate columns and rows**  
Populate rows according to the figure below.  
![](images/fig6.png)  

**Step 5 - Filter country**    
To see the cycle plot by country, add country into the Filters panel, select one country > right click > show filter. The list of countries should be to the right of the chart.    
Click on the arrow button of the Country filter and select "Single Value (list)".  
![](images/fig7.png)  

**Step 6 - Add reference line**   
Right click on y-axis > add reference line > fill according to the figure below.  
![](images/fig8.png)  
This shows me the average visitors per month across the years.   

**Step 7 - Create dynamic title**   
I want a dynamic title that changes according to my country filter.  
![](images/fig9.png)  
Use the "Insert" dropdown to insert field name.  

# And... there have you it! An interactive cycle plot ready for analysis!  

---
I would like to thank Prof Kam of Singapore Management University for the inspiration.
