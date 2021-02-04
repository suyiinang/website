---
title: "Predicting H1N1 Vaccination"
date: 2020-11-15
description: Predicting H1N1 vaccination based on flu survey.
menu:
  sidebar:
    name: Predicting H1N1 vaccination
    identifier: Predictive
    weight: 97
math: true
---

# Predicting H1N1 vaccination based on flu survey.

*This was written as part of the requirements for the Data Analytics Lab module for [MITB](https://scis.smu.edu.sg/master-it-business).*

---

For executive report, please view: [Executive Report - Predicting H1N1 vaccination](https://drive.google.com/file/d/1Gw1I4vGezWTbzbLreE9eg5JNGADqHbHz/view?usp=sharing)


## 1.	Introduction  
The H1N1 outbreak in April 2009 swept across the world and caused a global pandemic. [CDC](https://www.cdc.gov/flu/pandemic-resources/2009-h1n1-pandemic.html) estimated that the H1N1 virus claimed the lives of 151,700 – 575,400 people worldwide during its first year of circulation. A vaccine for the H1N1 flu was subsequently available in October 2009.   

The objective of this study is to build a predictive model to predict how likely individuals are to receive their H1N1 vaccination. Individuals with low likelihood of being vaccinated, of whom would require a more interventional approach by public health to incentivise them to be vaccinated. The predictive model is based on information such as individuals’ social, economic and demographic background as well opinions on risks and vaccine effectiveness.   

## 2. 	Data  
### 2.1 	Dataset  
The dataset originates from the [National 2009 H1N1 Flu Survey](https://www.cdc.gov/nchs/nis/data_files_h1n1.htm) (NHFS) conducted between Oct-09 and Jun-10 in the United States. The dataset has 26,707 observations and 38 variables. 

### 2.2	Setting up SAS Enterprise Miner  
Step 1: Create a new project called: Assign3  

{{< img src="/posts/projects/04_predict/images/fig1.png" align="left" >}}  
*Figure 1*  

Step 2: Create new library  
{{< img src="/posts/projects/04_predict/images/fig2.png" align="left" >}}  
*Figure 2*

Step 3: Create New Diagram - Flu vaccination model  
{{< img src="/posts/projects/04_predict/images/fig3.png" align="left" >}}  
*Figure 3*  

### 2.3	Import and save data  
Given that the dataset provided, flu_data, is in JMP file, I have imported the dataset using the “File Import” node under the Sample toolbar.  
{{< img src="/posts/projects/04_predict/images/fig4.png" align="left" >}}  
*Figure 4*

{{< img src="/posts/projects/04_predict/images/fig5.png" align="left" >}}  
*Figure 5*  

Next, using the “Save Data” node under “Utility”, I have named the file as “flu_data” under the “Filename Prefix” option and saved the data into the SAS Library I created previously, Flu_data. 

{{< img src="/posts/projects/04_predict/images/fig6.png" align="left" >}}  
*Figure 6*

### 2.4	Create data source  
Next, data source was created. In step 4 of the data source wizard (figure 8), I had customised settings using the ‘Advanced’ option. In the Advanced Advisor Options (figure 9), I changed two properties – i) Class Level Count Threshold, to account for binary data and ii) Missing Percentage Threshold from 50 to 40.   

{{< img src="/posts/projects/04_predict/images/fig7.png" align="left" >}}  
*Figure 7*  

{{< img src="/posts/projects/04_predict/images/fig8.png" align="left" >}}  
*Figure 8*  
  
{{< img src="/posts/projects/04_predict/images/fig9.png" align="left" >}}  
*Figure 9*     
From the column metadata (figure 9), the following were observed (boxes in red):  
1)	Respondent_id variable captured as ID    
2)	All variables with 2 levels captured as Binary   
3)	3 variables were rejected - high percentage of missing values (missing values for these variables were 45 – 50%, my cut-off was 40%)   
Finally, I set “h1n1_vaccine” to Target.

### 2.5 	Data exploration   
2.5.1 	Adjustments to variables  
{{< img src="/posts/projects/04_predict/images/fig10.png" align="left" >}}  
*Figure 10*  

**i)	Ordinal variables (8 variables)**  
From the description of the dataset, I understand that the following variables are ordinal in nature as the survey questionnaire required individuals to select a rating for their answers based on a number scale. I have cross checked this through examination of their distribution. As such, the level of these variables was updated to ordinal.  
{{< img src="/posts/projects/04_predict/images/fig11.png" align="left" >}}  
*Figure 11*   
  
**ii)	Hhs_geo_region variable**  
Hhs_geo_region distribution revealed a random string of text. According to the dataset description, respondents’ residences were classified using a 10-region geographic classification defined by the US Dept of Health and Human Services (HHS). However, I reviewed the [10 regions of HHS](https://www.hhs.gov/about/agencies/iea/regional-offices/index.html) and was unable to clearly identify these 10 regions. Additionally, I tried to identify these regions by reviewing the documentations for the NHFS 2009 . Hence, I have excluded these variables from my model on basis of the garbage in, garbage out (GIGO) concept - poor data quality will affect the accuracy of my model.  
{{< img src="/posts/projects/04_predict/images/fig15.png" align="left" >}}  
*Figure 12*  
   
Summary of variables.  
{{< img src="/posts/projects/04_predict/images/fig16.png" align="left" >}}  
*Figure 13*

2.5.2 	Missing values  
Excluding rejected variables, I observed that several variables have missing values of 0.08% – 16.5%. Nonetheless, no imputation or replacement was done to prevent distortion of the target. I am aware that these missing values may potentially affect my regression model but will not affect my recursive partitioning model.  
{{< img src="/posts/projects/04_predict/images/fig17.png" align="left" >}}  
*Figure 14*  
  
2.5.3	Check for complete and quasi-complete separation  
{{< img src="/posts/projects/04_predict/images/fig18.png" align="left" >}}  
*Figure 15*    

By using the default setting of the Multiplot node, variables were checked for any signs of complete and/or quasi-complete separation. Quasi-complete and complete separation variables must be excluded from the predictive model when performing logistic regression model as they will prevent the convergence of the maximum likelihood estimates for the coefficient and ultimately distorting the model.  

I did not observe any complete or quasi-complete separation. 

2.5.4	Understand variables’ importance  
{{< img src="/posts/projects/04_predict/images/fig19.png" align="left" >}}  
*Figure 16*   

Default settings of StatExplore was used to understand the importance of variables on the target. Given that the target and independent variables are mainly binary and nominal, the chi-square results were examined.  
  
The Chi-square barplot suggests that the doctor_rec_h1n1 is the best predictor. While the Worth chart indicated that there are many useful predictors (worth > 0.01) with doctor_rec_h1n1 being a good predictor as it is the only variable with > 0.05 worth.  
{{< img src="/posts/projects/04_predict/images/fig20.png" align="left" >}}  
*Figure 17*    

{{< img src="/posts/projects/04_predict/images/fig21.png" align="left" >}}  
*Figure 18*

## 2.6 Data Partition

{{< img src="/posts/projects/04_predict/images/fig22.png" align="left" >}}  
*Figure 19*  

{{< img src="/posts/projects/04_predict/images/fig23.png" align="left" >}}  
*Figure 20*

Finally, prior to building my predictive models, the data was partitioned into   
-	Training: 40%  
-	Validation: 30%   
-	Test: 30%  
I have kept the default partitioning method, the stratified method, which ensured that the proportion of vaccine and no vaccine was allocated proportional across the different dataset.  
  
{{< img src="/posts/projects/04_predict/images/fig24.png" align="left" >}}  
*Figure 21*   

From the partition summary, figure 21, number of observations were all above 5000, the minimum sample size for each dataset.   

{{< img src="/posts/projects/04_predict/images/fig231.png" align="left" >}}  
*Figure 22*   

While results of the summary statistics for class targets indicated that the percentage between vaccine and no vaccine received is proportionate across the different dataset.  

## 3.	Predictive models  
I have built 11 predictive models - 5 logistic regression and 6 recursive partitioning (Decision Trees) for my testing and selection.  
{{< img src="/posts/projects/04_predict/images/fig25.png" align="left" >}}  
*Figure 23*   
  
**Confusion matrix for results interpretation**

{{< img src="/posts/projects/04_predict/images/fig26.png" align="left" >}}  
*Figure 24*    
True Negative is when an **unvaccinated** individual was predicted to be **unvaccinated.**.  
False Negative is when a **vaccinated** individual was predicted to be **unvaccinated**.  
False Positive is when an **unvaccinated** individual was predicted to be **vaccinated**. (Worst case)  
True Positive is when a **vaccinated** individual was predicted to be **vaccinated**.  


### 3.1 Logistic regression models

{{< img src="/posts/projects/04_predict/images/fig27.png" align="left" >}}  
*Figure 25*    

{{< img src="/posts/projects/04_predict/images/fig28.png" align="left" >}}  
*Figure 26*    
Filtering selections via variable selection  
Given that I am building a predictive model, variable selection was used instead of variable clustering. Variable selection is best when identifying variables that are useful for predicting the target variables while variable clustering is best for choosing best variables for clustering analysis.
  
Given that my dataset is binary in nature, I have selected both R and Chi-square for my target model, see figure 26.  
  
A total of 10 variables were retained, the remaining variables were rejected due to small R and Chi-square.  


{{< img src="/posts/projects/04_predict/images/fig29.png" align="left" >}}           
*Figure 27*  

**Regression type**  
Given that my target is in binary, all my regression models are logistic regression (instead of linear regression) as it predicts the probability that a binary target will acquire the event of interest as a function. While the other option – linear regression predicts the value of an interval target. 
  
**Selection of model and criterion**  
There are 4 types of models for us to select – backwards, forward, stepwise and none (default).
For logistic regressions without variable selection, all methods were used except for the forward method was not included as results were the same as stepwise regression.  
  
For logistic regressions after variable selection, backward and forward methods were not included as results were the same as VR basic and stepwise regression respectively.  
  
For the selection criterion, I used the ‘Validation Misclassification’, which selects the model with lowest misclassification rate for my stepwise and backward models. This criterion was selected given my aim of building decision prediction that predict the likelihood of an individual being vaccinated (yes/no).


{{< img src="/posts/projects/04_predict/images/fig30.png" align="left" >}}  
*Figure 28*  

**Summary of results - logistic regression models**  
{{< img src="/posts/projects/04_predict/images/fig31.png" align="left" >}}  
{{< img src="/posts/projects/04_predict/images/fig33.png" align="left" >}}  
{{< img src="/posts/projects/04_predict/images/fig34.png" align="left" >}}  
*Figure 29*  

**Interpretation of results – logistic regression**  
Comparing the training and validation data percentage, I observed that there are slight signs of overfitting for regression model 3,4 and 5 as target percentage for True Negative is slightly smaller than training data, but this is still acceptable as the two True Negative percentages are within 5% range.  
In terms of misclassification rate, regression model 4 has the lowest misclassification rate of 14.77%.   
However, regression model 1 has the highest True Negative percentage of 95.09% and 95.27%, and True Negative observations of 7,999 and 6,012.  

### 3.2 Recursive Partitioning (Decision Trees)
{{< img src="/posts/projects/04_predict/images/fig35.png" align="left" >}}          
*Figure 30*  
  
In order to find the best tree, I created 6 different decision trees model by varying the Nominal and Ordinal Target Criterion, Method and Assessment Measure.   
  
All trees were set at maximum branch of 5 and maximum depth of 11, except for tree 6, where I used the default branch and depth number – 2 branches and 6 depth.   

**i)	Nominal & Ordinal Target criterion**  
The choice of purity measure largely depends on the target’s data type. Given that my target is binary (categorical), the Gini Index and Entropy are more appropriate measures than ProbChisq (the 3rd option for Nominal Target criterion that I did not use). Hence, I selected these two for my decision trees.  
  
**ii)	Method**  
I used two methods – Largest and Assessment. The largest method gives the fullest tree, while the assessment method returns the best assessment value based on the selected assessment measure (iii) below, which in my study would be misclassification and lift.
  
**iii)	Assessment measure**  
The assessment measure has 4 options – decision, misclassification, average square error and lift. Given that my target is in binary, misclassification and lift would be more appropriate measures for my decision trees.  
  
The other two measures were not selection as (a) The ‘Average Square Error’ is more appropriate when the target is continuous, and (b) the ‘Decision’ measure maximises the largest average profit if defined previously, if not, the measure would be set to ‘Misclassification’ given that my data is binary. Since I did not define any Decision previously, the measure would revert to ‘Misclassification’ and would produce the same results as my ‘Misclassification’ trees, thus redundant.  


{{< img src="/posts/projects/04_predict/images/fig36.png" align="left" >}}   
*Figure 36*  
  
**Summary of Recursive Partitioning Results**
{{< img src="/posts/projects/04_predict/images/fig37.png" align="left" >}}
{{< img src="/posts/projects/04_predict/images/fig38.png" align="left" >}}  
{{< img src="/posts/projects/04_predict/images/fig39.png" align="left" >}}  
*Figure 37*  

**Interpretation of results – decision trees**  
My results showed that model 10 has the lowest misclassification rate, however there are signs of overfitting as the target percentage of the validation data of 87.46% is more than 5% lower than training data percentage of 93%. Hence, I did not include this model for the  final model comparison.  
  
Similar to the  regression models, there are slight signs of overfitting for all other models but still acceptable as the difference in target percentage of true negative is within 5%.  
  
Excluding model 10, I observed that model 6 has the lowest misclassification rate of 13.55%, while model 11 has the best performance in terms True Negative outcome percentage of 93.93% and 94%, and observations of 7,902 and 5,932.

## 4. 	Model comparison
{{< img src="/posts/projects/04_predict/images/fig40.png" align="left" >}}  
*Figure 38*  
All the 11 models were compared using the model comparison node.   
I have selected misclassification rate for the  Selection and Grid Selection Statistics as the model is an accuracy model.  
For the Selection Table, Test data was used as a comparison given that I seek to understand how well the selected model performs when applied to new data.  
See figure 38 for changes made to the node property.  

### 4.1 	Model comparison results and model selection  
In assessing the models, I looked at   
    a)	Misclassification rate – minimise.  
    b)	Specificity - maximise.  

*a)	Misclassification rate*  
Based on misclassification rate performance, Model 11 outperformed all other models with the lowest classification rate of 15.15%. The misclassification rate among all models were quite close, ranging from 15.15% to 15.84%.   

{{< img src="/posts/projects/04_predict/images/fig41.png" align="left" >}}  
*Figure 39* 

**b)	Specificity**  
Given the objective is to identify individuals that did not get vaccinated (h1n1 = 0), I want to maximise the Specificity Rate: TN / (TN + FP), otherwise also known as the True Negative Rate.
Based on this assessment, Model 9 performed the best with the highest Specificity percentage for validation data. Further, Model 9’s misclassification rate is the 3rd lowest of 15.20%.  

{{< img src="/posts/projects/04_predict/images/fig42.png" align="left" >}}  
*Figure 40* 

{{< img src="/posts/projects/04_predict/images/fig43.png" align="left" >}}  
*Figure 41* 

**ROC curve of Model 9 and 11**
{{< img src="/posts/projects/04_predict/images/fig44.png" align="left" >}}  
*Figure 42*

{{< img src="/posts/projects/04_predict/images/fig45.png" align="left" >}}  
*Figure 43* 

ROC index for Model 9 is 0.837, while ROC index for Model 11 is 0.85.  
Both models are strong models as they both >0.7.  
  
Given the above assessment, model 9 is deemed to be the best performing model on basis that it produces the highest Specificity rate, 3rd lowest misclassification and high ROC index.  

### 4.2 	Model improvement  
From a public health standpoint, it is more important to have a low False Positive rate - those not likely to be vaccinated but was predicted to be vaccinated. It is more detrimental to misclassify the individual as False Positive as compared to False Negative. The cost of a False Positive is an individual left unvaccinated to spread the virus, or worst succumb to the virus. While the cost of a False Negative is additional follow up with individuals who are already vaccinated. True Negative rate is inversely related to False Positive.  
  
Hence, to improve the True Negative rate, Cut-off node was added to the selected model, Model 9. To obtain the optimal cut-off value, the Cut-off User Input was varied and the node was rerun several times.  

{{< img src="/posts/projects/04_predict/images/fig46.png" align="left" >}}   
*Figure 44*


{{< img src="/posts/projects/04_predict/images/fig47.png" align="left" >}}  
*Figure 45*


{{< img src="/posts/projects/04_predict/images/fig48.png" align="left" >}}  
*Figure 46*


{{< img src="/posts/projects/04_predict/images/fig48.png" align="left" >}}  
*Figure 47*

Given the results from figure 46, the cut-off point would largely depend on the government’s benchmark and how widespread the virus is.   
  
Increasing True Negative would decrease False Positive Rate. However, there is a trade off when choosing different cut-off points – misclassification increases when cut-off increases. This means that the number of wrongly predicted increase, namely False Negative increase. For example, although the model is able to predict fewer number False Positive, more action is required to due to higher number of False Negative prediction.   
  
Using “No cut-off” version, 80.9% of cases need following-up, of which 5828 individuals are not vaccinated (True Negative) and 655 are vaccinated (False Negatives). 
  
Using the “Cut-off 0.62”, 90.3% of cases need following-up, of which 6092 individuals are not vaccinated and 1144 are vaccinated.
  
Using the “Cut-off 0.79”, 91.8% of cases need following-up, of which 6145 individuals are not vaccinated and 1207 are vaccinated.  
  
In short, as the cut-off point increase, public health officers will be following up on more cases at the cost of a lower False Positive cases. For example, between the “No cut-off” and “Cut-off 0.62” officials are would need to follow-up on additional 753 Negative cases (7236 - 6483) at cost of reducing the number of False Positive cases by 263 (482 – 219).  
  
Hence, ultimately the cut-off point depends on governments’ benchmark, public health policy and resources available to follow-up on cases.  


## 5. 	Conclusion  
The 11 models created share similar misclassification rate ranging from 15.15% to 15.85%.  

Based on my assessment, model 9 is deemed to be the best performing model on basis that it produces the highest Specificity, 3rd lowest misclassification and high ROC index.  

The model can be further refined by varying the cut-off point, which would largely depend on the public health policies in place.  

{{< img src="/posts/projects/04_predict/images/fig50.png" align="left" >}}  
*Figure 48*

---

Health vector created by [freepik](https://www.freepik.com/vectors/health)
