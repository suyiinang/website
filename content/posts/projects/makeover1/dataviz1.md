---
title: "DataViz Makeover #1"
date: 2021-01-26
description: Making over a chart from the Singapore Labour Force (2019) report.
menu:
  sidebar:
    name: DataViz Makeover 01
    identifier: Dataviz makeover
    weight: 94

---

# Making over a chart from the Singapore Labour Force (2019) report.


*This was written as part of the requirements for the Visual Analytics module for [MITB](https://scis.smu.edu.sg/master-it-business).*

---

For my first DataViz makeover, I have used data from the [Ministry of Manpower of Singapore](https://stats.mom.gov.sg/Pages/Labour-Force-In-Singapore-2019.aspx), which analyses Singapore’s labour force to understand shifts in the labour market to facilitate better decision making.  

## 1) The original visualisation

{{< img src="/posts/projects/makeover1/images/fig1.png" align="left" >}}
*Figure 1: Chart 6 of Labour Force in Singapore 2019 report (page 22)*

Notes:  
- LFPR refers to the proportion of working-age population that engages actively in the labour market, either by working or looking for work. Source: [MOM](https://stats.mom.gov.sg/Pages/Labour-Force-Summary-Table.aspx)  
- Share of residents refers to the age distribution of the labour force.


Before making over the selected visualisation, it is important to have a clear understanding of the context of the visualisation and its key takeaways which are dependent on:  
- **Who**: [Individuals, businesses and primarily policy-makers, to help improve the well-being and optimisation of workers.](https://stats.mom.gov.sg/Pages/Labour-Force-In-Singapore-2019.aspx)  
- **What**: Understanding the shift in Singapore’s labour force from the respective age bands over the past 10 years (2009 to 2019).  
-	**How**: Showing that labour force distribution and participation rate of older workers (55 and over) has increased, which resulted in the increase in labour force’s median age.

## 2) Critiques and suggestions for current visualisation
### 2.1 Clarity


|S/N | Critiques                     | Comments             |
|----|-------------------------------|----------------------|
|1   | **Chart title is not precise** – The title *“Resident labour force by age”* does not drive the message of “the increase in median age of labour force”. The chart refers to the share of labour force and is accompanied by a rather convoluted commentary on labour force participation rate (LFPR) of the different age bands and share of resident’s labour force, making it difficult to grasp the main message quickly. | **Change title** to “The shift in Singapore’s labour force distribution and participation rate by age from 2009 to 2019”. |
|2   | **Figures per commentary and chart are inconsistent** - The commentary quoted percentages that are aggregates of several age bands (i.e 25 to 54), while the chart uses 5-year intervals (i.e 25 to 29, 30 to 34, etc). This inconsistency hinders cross referencing between the commentary and the table. | Keep both **consistent**. Age bands must match for both chart and commentary. |
|3   | **Axis title not properly labeled** – ‘Share of labour force' was not labeled on the y axis. This leaves room for misinterpretation and/or requires the reader’s extra time to peruse the chart, all of which draws attention away from the main message. | It would be clearer and more quickly understood to the reader if both the **y-axis** was **appropriately labeled**. |


### 2.2 Aesthetics


|S/N | Critiques                     | Comments             |
|----|-------------------------------|----------------------|
|4   | **Chart title’s font size and location** - title of the chart should precede the commentary so that the reader is mentally prepared going into the more detailed commentary. Font size of title should be bigger than the commentary.| Move title of chart above and commentary below. |
|5   | **Commentary is too long** – the reader has to read through the whole paragraph to understand the main idea of the visualisation. | **Shorten commentary** to only the key message. Highlight by using **colour, bold or underline** key takeaways. |
|6   | **Line chart may not be the most appropriate chart** – From the chart, the reader can clearly see that there is an increase in percentage for those 55+, but the reader has to cross reference to the table below to get an idea of how much it declined by. Furthermore, it is difficult to see which age band increased/decreased the most. | Given that the main message is to highlight the significant increase and decrease in share of labour by the respective age groups, leading to the increase in median age, a more appropriate graph would be a **stacked bar chart**. |
|7   | **Figures in table are redundant**- It is redundant to include all the figures in the table – why make the chart in the first place if one need to reads all the numbers in the table to understanding it. |	Remove table – only **showcase key figures** to drive the main idea.|
|8   | **Median age label clutters**- too long, distracting and clutters the graph. | Remove median age label. Since there are only two text, **include these figures into the commentary**. |
|9   | **The heavy shading of the table competes for attention.** The table is meant to support the main message hence shading should be kept minimal. Furthermore, the monotone shading does not add value (unlike a heat map which showcases the increase/decrease trends in values). | **Remove shading**. Colour should always be intentional - use shading only to highlight key figures. |
|10  | **Different alignments for source and notes** make the whole visualisation look disorganised. |	**Align** these two either to the left or right to establish sense of unity and cohesion. |

## 3) Proposed Design
### 3.1 Sketch
{{< img src="/posts/projects/makeover1/images/fig2.jpg" align="left" >}}
*Figure 2: Sketch of proposed design*

### 3.2 Advantages of proposed design
i)	Clear title – shows how the participation rate and distribution of Singapore’s labour force has shifted by age bands from 2009 to 2019.  
ii)	Chart titles tell the big picture story, followed up with short commentary to provide more context.   
iii)	Shows how labour force has changed across the 10 years instead of 2 year points as shown in the original visualisation.  
iv)	Figures and age bands per commentary and chart are consistent for easy cross referencing.  
v)	Axis are properly labeled – LFPR% and share of labour force.  
vi)	Only selected figures (2009 and 2019) are shown to highlight the shift.  
vii)	Colours are consistent throughout the dashboard.     

## 4) Data visualisation steps
In remaking the existing visualisation, I used  
i) Table 5 (Resident Labour Force Participation Rate by Age and Sex, 2009 - 2019), and  
ii) Table 7 (Resident Labour Force Aged Fifteen Years and Over by Age and Sex, 2009 - 2019)  
from the [Ministry of Manpower of Singapore](https://stats.mom.gov.sg/Pages/Labour-Force-Tables2019.aspx).

### 4.1 Data preparation

**Data: Table 5 - LFPR**

1) Remove unnecessary columns  
Delete columns A, B, D, F, H, J, L, M, N, P, R, T, V, X, Z.  
{{< img src="/posts/projects/makeover1/images/fig3.png" align="left" >}}
*Figure 3: Remove unnecessary columns*

2) Remove empty rows  
Delete rows 1 to 4 and 19.
{{< img src="/posts/projects/makeover1/images/fig4.png" align="left" >}}
*Figure 4: Remove empty rows*

3) Rename header  
Rename header from “Age (Years)” to “Age band”.
{{< img src="/posts/projects/makeover1/images/fig5.png" align="left" >}}
*Figure 5: Rename header*

4) Delete unnecessary tabs  
Remove tabs T5_F and T5_M.  
Save and rename file as T5_T_clean.

**Data: Table 7 - Labour force**  

1) Tidy data  
Repeat steps 1 to 4 as done for Table 5 above.

2) Pivot data  
Import file into Tableau, select all the years, right click and select “Pivot”.
{{< img src="/posts/projects/makeover1/images/fig6.png" align="left" >}}
*Figure 6: Pivot data*

3) Rename headers  
Rename ‘Pivot Field Names’ to ‘Year’.
Rename ‘Pivot Field Values’ to ‘Labour force’.
{{< img src="/posts/projects/makeover1/images/fig7.png" align="left" >}}
*Figure 7: Rename headers*

4) Change data type  
Change Year data type to “Date”.

5) Export file to csv  
Save file as "T7_T_pivot".

### 4.2 Data visualisation
Import both T5_T_clean and T7_T_pivot into Tableau.  

**Data source tab - T5_T_clean**  

1) Import into Tableau & create flat file  
Inspect imported data: Upon importation, the LFPR from 2009 to 2019 are spread across multiple columns. As such, we want to create a flat file - select the columns from 2009 to 2019, right click and select pivot.
{{< img src="/posts/projects/makeover1/images/fig8.png" align="left" >}}
*Figure 8: Pivot data*

2) Rename headers  
Rename ‘Pivot Field Names’ to ‘Year’.  
Rename ‘Pivot Field Values’ to ‘LFPR%’.  
{{< img src="/posts/projects/makeover1/images/fig9.png" align="left" >}}
*Figure 9: Rename headers*

3) Change data type  
Change ‘Year’ data type from string to Date.  
{{< img src="/posts/projects/makeover1/images/fig10.png" align="left" >}}
*Figure 10: Change data type*

4) Import T7_T_pivot  
Inspect imported data to ensure data is in flat file format and data types are correct.

**LFPR% tab**  

1) Create line chart  
Drag [Year] and [LFPR%] to Columns and Rows respectively.  
{{< img src="/posts/projects/makeover1/images/fig11.png" align="left" >}}
*Figure 11: Create line chart*

2) Apply filter  
Drag [Age band] to Filters panel, and check these 4 values: 15- 24, 25-54, 55-64, 65+.  
{{< img src="/posts/projects/makeover1/images/fig12.png" align="left" >}}
*Figure 12: Appy filter*

3) Apply colour  
Drag [Age band] to colour, change colours according to figure 13.  
Update ‘Automatic’ to ‘Line’.  
{{< img src="/posts/projects/makeover1/images/fig13.png" align="left" >}}
*Figure 13: Apply colour*

4) Update view  
Update view from ‘Standard’ to ‘Entire View’.

5) Add annotation  
I only want to highlight points on 2009 and 2019. Hence for points on
    -	2009: Right click on each of the points (4 in total) and select Annotate > Point. In the “Edit Annotation” panel, write “<SUM(LFPR%)>%” and colour font according to the age band colour done previously.  
    -	2019: Right click on each of the points (4 in total) and select Annotate > Point. In the “Edit Annotation” panel, write “<Age band> <SUM(LFPR%)>%” and colour font according to the age band colour done previously.
  
6) Format annotation  
Remove borders and shading.

7) Rename y-axis  
Rename y-axis to “Labour Force Participation Rate (LFPR%)”.

8) Add title  
Add title: More Singapore residents across all age groups work. *<font size 14>*  
However, the increase in older workers' (55-64 and 65+) participation rate of 9ppt and 11.6ppt was triple that of younger workers' (15 - 24 and 25 - 54) of 3.6ppt and 3.3ppt! *<font size 10>*

**Share of LP**  

1) Create new age band group  
Right click [Age band] > Create > Group.  
Group and rename according to figure below.  
{{< img src="/posts/projects/makeover1/images/fig14.png" align="left" >}}
*Figure 14: Group age bands*

2) Apply filter	Filter out “Total”  
Add colour	Drag [Age band] to colour.  
Check and ensure that colour is consistent with tab “LFPR%”.  
Reduce opacity to “60%".

3) Create stacked bar chart  
Drag [Labour force] and [Year1] to Columns and Rows respectively.  
Convert to percentage : Right click [SUM(Labour force)] > Quick Table Calculation > Percent of Total.  
Convert to stacked bar : Right click [SUM(Labour force)] > Compute using > Age band (group). 

{{< img src="/posts/projects/makeover1/fig15.png" align="left" >}}
*Figure 15: Create stacked bar chart*

4) Change view  
From “Standard” to “Fit height”.

5) Rename x-axis  
Rename to “Share of labour force (%)”.  
Remove y-axis	Right click > Hide field labels for row.

6) Remove grid lines  
Using Format Lines panel.

7) Add annotation  
Drag mouse pointer and select the 2009 and 2019 bars > right click > Mark labels > Always show.

8) Add title  
Add title : Singapore's labour force gets older.The median age has increased from 41 in 2009 to 44 in 2019 due to the gradual shift towards older workers (55-64 and 65+ band) over the past 10 years.

**Dashboard 1**  

1) Add title  
Add title : “The shift in Singapore's labour force distribution and participation rate by age bands 2009 to 2019” with grey background, white text and font size 23.

2) Add commentary  
Using Objects > Text > drag to bottom of title and add:  
“Although labour force participation rate (LPFR) across all age groups has increased from 2009 to 2019, the significant increase in older workers' (55-64 and 65+) participation has shifted the labour force's distribution towards an older labour force. This shift is due to multitude of reasons, namely aging population due to low birth rates, extended retirement age, longer average lifespan, etc.” 

3) Add sheets  
Add sheet “LFPR%” to the left and “Share of LF” to the right. Retain one age band legend, place it at the bottom of “share of LF”.

4) Add source  
Using Objects > Text > drag to bottom left and add :  
“Source: Ministry of Manpower Singapore (https://www.mom.gov.sg/)  
Original report:https://stats.mom.gov.sg/Pages/Labour-Force-In-Singapore-2019.aspx  
The raw data: https://stats.mom.gov.sg/Pages/Labour-Force-Tables2019.aspx”

5) Add author  
Add text to bottom left corner and add text : “DataViz Makeover #1 by @suyiinang” align left.

## 5) Final visualisation
### 5.1 Snapshot of dashboard  
{{< img src="/posts/projects/makeover1/images/fig16.png" align="left" >}}
**Figure 16: Dashboard**
*Full visualisation available at [Tableau Public](https://public.tableau.com/profile/suyiinang#!/vizhome/DataViz_16116824631860/Dashboard1)*

### 5.2 Main observations
- Labour force participation rate (LFPR) has increased across all age bands since 2009. While younger workers (15 – 24 and 25 – 54) experienced a slight increase of 3.6ppt and 3.3ppt since 2009, the increase in older workers’ (55-64 and 65) participation was **triple** that of younger workers, increasing by 9ppt and 11.6ppt since 2009.
- Participation rate of 15 - 24 workers tended to fluctuate more than the other age bands.
- LFPR for older workers (55-64 and 65) seemed to have experienced a steep increase in 2011.
- The shift in labour force’s distribution was mainly due to shift from the 25-54 age band to the 55-64 and 65+ age band. While the share of labour force for the 15 -24 age band was quite stable (share of 8-9%) across the 10 years.
- Given that the financial crisis happened in 2008/2009, 2009 may not give the best numbers to use as a base comparison as is it historically lower compared to other years. As such, the increase in participation of old workers may be due to workers re-joining the workforce as the economy recovers, of which leads to the shift in the share of labour force towards older workers.


