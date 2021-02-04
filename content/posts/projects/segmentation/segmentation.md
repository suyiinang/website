---
title: "Market segmentation of Philippines’ market"
date: 2020-10-18
description: Market segmentation of Philippines’ market based on expenditure patterns of households.
menu:
  sidebar:
    name: 02 Market segmentation
    identifier: segmentation
    weight: 2
---

Market segmentation of Philippines’ market based on expenditure patterns of households.

*These reports were written as part of the requirements for the Data Analytics Lab module for [MITB](https://scis.smu.edu.sg/master-it-business).*

---

For executive report, please view : [Executive Report - Segmentation](https://drive.google.com/file/d/1O3CCnBVoUOHd7w_96sEVDVMNkkwEbDcA/view?usp=sharing)

## 1. Objective  
This report aims to group the Philippines’ consumer market into target segments based on similar spending patterns on hypermarket items using clustering methods in JMP. With reference to the characteristics of each cluster, we aim to align the target segment for an international hypermarket chain.  

## 2.	Data   
### 2.1 	Dataset and Approach  
The dataset uses the [2018 Family Income and Expenditure Survey (FIES 2018)](https://psa.gov.ph/content/final-2018-family-income-and-expenditure-survey-fies-press-release-and-2018-fies-final) undertaken by PSA . In this survey, private households were interviewed nationwide; institutional populations are not within the scope of the data.   
  
Two files were provided – an excel file of 85 variables and 147,717 observations, and a data dictionary of the dataset in text file.  

### 2.2 	Data preparation  
2.2.1 	Update incorrect modelling type  
Several variables were recoded to the correct attributes, please see Figure 1.  

{{< img src="/posts/projects/segmentation/images/fig1.png" align="left" >}}
*Figure 1*  

2.2.2 	Check for missing data  
The ‘Missing Data Pattern’ function was used to check for missing data. Figure 2, an extract of results, shows that there is no missing data.  


{{< img src="/posts/projects/segmentation/images/fig2.png" align="left" >}}
*Figure 2*

2.2.3	Variables lack context
**i)	URB**   
URB refers to urban/rural and had values of 1 and 2. The metadata did not provide any explanation as to what 1 and 2 were. We deduced that 1 is urban while 2 is rural as W Prov value of 76, 75, 74 pertains to National Capital Region (NCR) districts that are located within Metro Manila.    

{{< img src="/posts/projects/segmentation/images/fig3.png" align="left" >}}  
*Figure 3*  

2.2.4	Derive new variables
**i)	Family size – FSIZE**  
There were several observations with decimal points. These observations are reasonable given that the survey was conducted over two separate visits and that there were Filipinos who did not spend the full year with their families.  
  
However, to avoid readers’ confusion, we have rounded up the figures. Subsequently, this variable was binned into a categorical variable under ‘Fam size’.  
{{< img src="/posts/projects/segmentation/images/fig4.png" align="left" >}}  
*Figure 4*

**ii)	Total income (less imputed rent)**  
{{< img src="/posts/projects/segmentation/images/fig5.png" align="left" >}}  
*Figure 5*  

Ideally, we would like to examine disposable income of households (total income less rent / mortgage less taxes). However, due to lack of data such as mortgage cost and taxes, we were unable to recompute the disposable income of households.  
  
As such, we took a conservative approach by defining income as total income (‘TONIC’) less imputed rent. We deemed imputed rent as not actual cash inflow given that the FIES 2018 report defined [imputed rent](http://www.psa.gov.ph/sites/default/files/FIES%202018%20Final%20Report.pdf) as an estimated amount that the owner of a dwelling unit would charge had the unit been rented out.  
  
Furthermore, we have not included the variable ‘other receipts’ in the total income, being irregular, such as winnings from gambling, sales of stocks, etc.  

**iii)	Per capita income (PCINC) new**  
{{< img src="/posts/projects/segmentation/images/fig6.png" align="left" >}}  
*Figure 6*

We have classified households into different income groups based on  
a)	Income groups from a discussion paper by [PIDS](https://pidswebs.pids.gov.ph/CDN/PUBLICATIONS/pidsdps1820.pdf), and   
b)	the [official poverty threshold in 2018](https://psa.gov.ph/poverty-press-releases/nid/138411) was PHP10,481 per month for family of five, which equates to ~PHP25,200 income per capita per year.  

**Income band**  
{{< img src="/posts/projects/segmentation/images/tab1.png" align="left" >}}  
 
The PCINC new variable was binned. To ensure that our figures are accurate, we have cross checked our figures with the PSA website where the poverty incidence was ~16%6. Given our poverty rate of 17.7% is relatively close to the official poverty rate, we have assumed that our calculations are valid. 
  
{{< img src="/posts/projects/segmentation/images/fig7.png" align="left" >}}  
*Figure 7*  

**v)	Combining variables**  
We have grouped the variables according to food categories listed on [Landmark’s website](https://www.metromart.com/shops/landmark-makati), a Philippines supermarket.  
  
a.	Meat + Fish  
{{< img src="/posts/projects/segmentation/images/fig8.png" align="left" >}}  
*Figure 8*  
  
b. Fruits & vegetables    
{{< img src="/posts/projects/segmentation/images/fig9.png" align="left" >}}  
*Figure 9*    

c. Food cupboard     
{{< img src="/posts/projects/segmentation/images/fig10.png" align="left" >}}  
*Figure 10*  

d. Beverages     
{{< img src="/posts/projects/segmentation/images/fig11.png" align="left" >}}  
*Figure 11*   
  
**vi) Total spent**      
{{< img src="/posts/projects/segmentation/images/fig12.png" align="left" >}}  
*Figure 12*  
   
For the purpose of this report, we have redefined the variable ‘total spent’ as the sum of a typical retailer’s items.  

**vii) Island**   
{{< img src="/posts/projects/segmentation/images/fig13.png" align="left" >}}  
*Figure 13*   
The variables ‘region’ was grouped and recoded into the 3 main islands.  

**viii)	Variables in percentage**    
Given that the range of expenditure on respective items are quite wide, we have transformed 9 variables into a percentage of total spent respectively for a better comparison. Please refer to figure 14 for details. These variables will be used for our K-Means Clustering.  

{{< img src="/posts/projects/segmentation/images/fig14.png" align="left" >}}  
*Figure 14*  

**ix)	Binning continuous into categorical variables**  
Continuous variables were transformed into categorical variables through binning. Given that the 2 variables, tobacco and alcohol, have substantial observations with zeros, we have binned these two according to zero and non-zero. The remaining 7 variables were binned with cut-points set at the 33.5 percentile (into low, medium and high).  

a)	Tobacco  
Binned into ‘non-smoker’ if tobacco = 0, and ‘smoker’ if tobacco > 0  
{{< img src="/posts/projects/segmentation/images/fig15.png" align="left" >}}  
*Figure 15*
 
b)	Alcohol  
Binned into ‘non-drinker’ if alcohol = 0 and ‘drinker’ if alcohol > 0  
{{< img src="/posts/projects/segmentation/images/fig16.png" align="left" >}}   
*Figure 16*

**2.2.5 	Unrelated variables**
Given that this study is to understand expenditure patterns for a hypermarket, we have only retained variables that are relevant – location, total income, family size, expenditure items that are typically sold by retailers (i.e., meat, bread, clothes, household furnishing, etc); items such as health, education, etc, were excluded.  

**2.2.6	Non customers – observations excluded **
Closer examination of the data revealed that there were 3 observations where total spent was zero. Since these are not customers of a hypermarket, we have excluded this from our customer segmentation analysis.  
{{< img src="/posts/projects/segmentation/images/fig17.png" align="left" >}}  
*Figure 17*  
  
## 3. 	Customer segmentation and analysis  
### 3.1 	K-means clustering  
Given that our dataset has >500 observations, hierarchical clustering will not be meaningful. As such, k-means clustering will be used to segment households based on the numerical variables.   

**3.1.1	Distribution analysis **
Since K-means clustering is very sensitive to outliers, distribution of variables must be reviewed to check for outliers and skewness to avoid clustering bias.  
  
The distribution analysis reveals that there is a high proportion of outliers for each variable, possibly reflecting the income divide in Philippines. As such, we did not exclude any outliers.  
Furthermore, we observed that the distributions are positively skewed.   
  
We will take these into consideration when performing the K-means analysis.  
{{< img src="/posts/projects/segmentation/images/fig18.png" align="left" >}}  
*Figure 18*    

**3.1.2	Examine correlation between variables ** 
The results revealed that the variables are not highly correlated <|0.8|. As such, we are able to use all these variables in the cluster analysis.   
{{< img src="/posts/projects/segmentation/images/fig19.png" align="left" >}}   
*Figure 19*   

**3.1.3	K-means for spending behaviour  **
Due to the high degree of skewness and number of outliers, columns were individually scaled when performing the k-mean analysis.  
The cluster comparison report revealed that the optimal number of clusters is 9 - the largest CCC. Subsequently, cluster summary of the optimal cluster (Ncluster = 9) was examined to ensure that there were no clusters with small number of observations. Figure 20 shows that the minimum number of observations within a single cluster was 3,337; hence, this K-means cluster analysis is reliable.  
{{< img src="/posts/projects/segmentation/images/fig20.png" align="left" >}}  
*Figure 20*    

{{< img src="/posts/projects/segmentation/images/fig21.png" align="left" >}}  
*Figure 21*   

{{< img src="/posts/projects/segmentation/images/fig22.png" align="left" >}}  
*Figure 22*  

{{< img src="/posts/projects/segmentation/images/fig23.png" align="left" >}}    
*Figure 23*

**3.1.4 	Interpretation of K-Means Clustering based on spending patterns  **
Households were segmented into 9 clusters according to their spending patterns.   
“The Dough Lovers” and “The Carnivores” are the two largest segments, accounting for 47% of the market. {{< img src="/posts/projects/segmentation/images/tab2.png" align="left" >}}  

### 3.2 Latent Class Analysis (LCA)  
Similarly, we attempted to cluster the market according to expenditure patterns. However, clusters by LCA did not yield very meaningful insights. 

{{< img src="/posts/projects/segmentation/images/fig24.png" align="left" >}}  
*Figure 23*   

{{< img src="/posts/projects/segmentation/images/fig25.png" align="left" >}}  
*Figure 24*   
  
### 3.3 	Exploring expenditure patterns   
Given the results from sections 3.1 and 3.2, as well as the stakeholders’ needs, latent class analysis may not be the appropriate clustering method for this dataset, which is predominantly continuous data. As such, we have used clusters obtained from K-Means for subsequent analysis.  
Clusters obtained from K-means were further recoded ranked by percentage in descending order.  
{{< img src="/posts/projects/segmentation/images/fig26.png" align="left" >}}  
*Figure 26*  

**3.3.1 Expenditure patterns differ by urban and rural areas** –   
*Dough Lovers was the top segment in the rural households whilst Carnivores in the urban households. Dough Lovers and Carnivores combined constitute the top 3 segments for this area.*  
{{< img src="/posts/projects/segmentation/images/fig27.png" align="left" >}}  
*Figure 27*    
{{< img src="/posts/projects/segmentation/images/fig28.png" align="left" >}}  
*Figure 27*  
Rural households were predominantly Dough Lovers, Carnivores and Hoarders.  
Urban households were predominantly Carnivores, Thirsty Hippos and Dough Lovers.  

**3.3.2	 Expenditure patterns were different across the islands** -   
*Luzon households are predominantly carnivores whilst Mindanao and Visayas households are predominantly Dough Lovers   *
{{< img src="/posts/projects/segmentation/images/fig29.png" align="left" >}}  
*Figure 29*  

{{< img src="/posts/projects/segmentation/images/fig30.png" align="left" >}}  
*Figure 30*  

Based on figure 29, we observed that spending patterns vary by Islands. Households in Luzon, which is the most populated Island accounting for 50% of the population, predominantly belong to the Carnivores cluster.   
Conversely, Mindanao and Visayas households are mostly Dough Lovers.  
Interestingly, in Luzon, combined expenditure of the top 3 segment is ~11% lower than that of Mindanao and Visayas, indicating that apart from spending on meat, the expenditure patterns in Luzon are more varied.  


**3.3.3	 Expenditure patterns differ by family size** – large families (>5) are predominantly Dough Lovers (34%).   
*2-5 member families were more inclined to be in the Carnivores cluster (23–26%). In single person households, the Herbivores cluster dominates (18%)* 

{{< img src="/posts/projects/segmentation/images/fig31.png" align="left" >}}  
*Figure 31*  

{{< img src="/posts/projects/segmentation/images/fig32.png" align="left" >}}  
*Figure 32*  
  
Large families with more than 5 members tend to be in the Dough Lovers and Carnivores clusters, spending a combined 56% on these 2 categories.  
Families with 2–5 persons tend to spend relatively more on meat and fish (Carnivores).  
In single person households, the Herbivores cluster is dominant.  
Singles tend to spread their expenditure, albeit tending slightly towards the Herbivores.   
It is interesting to note that as the family size increases from singles to 2-member to 4 to beyond 5-member, the spend moves from on herbivorous to carnivorous to dough items.  

**3.3.4	Expenditure patterns varies significantly across the income groups** - 
*Dough Lovers cluster was dominant in the poor household (52%), Carnivores were more prevalent in the low to middle-income households, while HouseProud and Fashionistas dominated the rich households.*

{{< img src="/posts/projects/segmentation/images/fig33.png" align="left" >}}  
*Figure 33*  

{{< img src="/posts/projects/segmentation/images/fig34.png" align="left" >}}  
*Figure 34* 

For the poor households, 51% belong to the Dough Lover cluster.  
The low and middle-income households are predominantly in the Carnivores clusters.  
Unsurprisingly, the HouseProud and Fashionistas clusters dominate the rich households, accounting for 39% and 31% respectively.  
We note that Philippines is a low-income country, whereby the low-income household accounts for 65% of the population. Retailers may want to take this into consideration when performing market feasibility studies.   
 
**3.3.5	Within each income group, willingness to spend differs by clusters. **
{{< img src="/posts/projects/segmentation/images/fig35.png" align="left" >}}  
*Figure 35* 

{{< img src="/posts/projects/segmentation/images/fig36.png" align="left" >}}  
*Figure 36*  

For the purpose of this study, range of spending was taken as a proxy for willingness to spend – the wider the range, the more willing households are to spending on these items.

Range of spending by income group:   

**a) Rich**  
-	Spent a wide range on furnishing (HouseProud), clothes (fashionistas) and for food items, the most on beverages (Thirsty Hippo)  
-	Spent a very narrow range on bread (Dough Lovers)
    
**b) Middle**  
-	Similar to the rich - Spent a wide range on furnishing (HouseProud), clothes (fashionistas) and beverages (Thirsty Hippo)  
-	However, they spent a moderate range on bread (Dough Lovers)  

**c) Low**  
-	Moderate spending range throughout all clusters  

**d) Poor**  
-	Narrow spending range throughout all clusters, except for bread, vegetables and fruits  
- Moderate spending range for bread, fruits and vegetables
  
## 4.	Summary of findings   
Households in Philippines can be segmented into 9 clusters based on spending patterns. Please refer to page 15 for a full list of clusters.   

Deeper analysis reveals that spending patterns varies according to:   

**1)	Urban and rural**  
-	Rural – Predominantly Dough Lovers, Carnivores and Hoarders, total 62.7%  
-	Urban - Predominantly Carnivores, Thirsty Hippos and Dough Lovers, total 58%

**2)	Island**  
-	Luzon - Carnivores, Hoarders and Dough Lovers, total 53.4%  
-	Mindanao - Dough Lovers, Carnivores and Hoarders, total 65.4%  
-	Visayas - Dough Lovers, Carnivores and Thirsty Hippo, total 64.9%

**3)	Family size**  
- Single: Herbivores  
- 2-5persons: Carnivores  
-	More than 5: Dough Lovers, Carnivores  

**4)	Income group**  
-	Poor: Spend more on bread (Dough Lovers)  
-	Low-Middle: Spend more on fish and meat (Carnivores)  
-	Rich: Spend more on furnishing (HouseProud) and clothes (Fashionistas)
 
**5)	Willingness to spend on:**  
-	Poor: Moderate spending range on bread, fruits and vegetables  
-	Low: Moderate spending range across all clusters  
-	Middle: Wide spending range on furnishing, clothes and beverages; Moderate spending range on bread  
-	Rich: Wide spending range on furnishing, clothes and beverages; Low spending range on bread  

Please refer to the executive slide deck for recommendations and other considerations.


