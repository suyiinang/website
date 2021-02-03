---
title: "Understanding the Stars"
date: 2020-12-01
description: Augmenting Numerical Data with Textual Analysis to Identify Key Determinants of Airbnb Review Scores
menu:
  sidebar:
    name: 06 Understanding the Stars
    identifier: text
    weight: 30
---

Augmenting Numerical Data with Textual Analysis to Identify Key Determinants of Airbnb Review Scores

**By: Ang Su Yiin, Anne Nguyen Nhi Thai An, Toh E-Lynn**

*These reports were written as part of the requirements for the Data Analytics Lab module for [MITB](https://scis.smu.edu.sg/master-it-business).*

---

For post, please view : [Poster](https://drive.google.com/file/d/1BIwU2oUqKrYxyTnZSbpzDUyPL4Gsan7n/view?usp=sharing)

## Abstract 
Text analytics provides powerful tools for transforming large amounts of unstructured data into quantitative variables, allowing researchers to contribute unique insights to business decision-making. In this study, we use textual data from reviews provided by Airbnb guests and descriptions of listings by Airbnb hosts to augment existing analyses of structured variables associated with Airbnb listings. Utilizing text mining techniques, we procure top terms by relevance from reviews and listing descriptions. These unstructured variables are combined with other structured variables describing various host and listing characteristics. We then employ an array of multiple linear regression and regression tree models with Binary Document Term Matrix and Term Frequency Inverse Document Frequency variants to identify the key determinants of review scores. Evaluating these models in accordance with their lowest average square error, the optimal model is determined to be a regression tree, parametrized by 2 branches, 6 depth, 100 leaf size, 100 rules and 100 split size. The key determinants obtained from the optimal model are predominately host related – superhost status, number of host listings, host tenure, host response time, pricing, and smooth check-in. Following our analysis, we suggest several insights and recommendations specific to the Airbnb sharing-economy of Singapore.

## Introduction
Widely described as the most disruptive innovation of tourism in recent times, Airbnb has enjoyed exponential growth after its entry into the short-term accommodation market in 2008. In 2019, almost 7 million listings were placed on Airbnb, generating over [USD 4.7b in global revenue](https://www.businessofapps.com/data/airbnb-statistics/). Closer to home, Airbnb revealed that its guests contributed $411m to Singapore’s economy via host payouts and daytime spending in 2017. Indeed, Singapore has been reported to be one of “Airbnb’s most penetrated markets globally”, with almost [1.5 million Singaporeans using Airbnb listings overseas](https://vulcanpost.com/641967/airbnb-singapore-report-2017/#:~:text=Singapore%20was%20also%20reported%20to,Singaporeans%20using%20Airbnb%20listings%20overseas.&text=Locally%2C%20hosts%20welcomed%20350%2C000%20guests,hosts%20sharing%20their%20primary%20residence).  

Sharing platforms like Airbnb play an important intermediating role in connecting hosts and guests who would not ordinarily be able to interact with each other in the absence of the platform.  However, the large number of listings on Airbnb entails strong competition amongst hosts for potential guests, who may also be willing to opt for a hotel or serviced apartment. Thus, our results have important implications for Airbnb hosts who seek to remain attractive to potential guests.

## Literature Review  
Given the importance of review scores in host profitability, a large body of literature has attempted to identify the key determinants of an Airbnb guest’s experience with a given accommodation. The methodological approaches adopted by these studies have largely diverged into two paths. 
  
First, several studies have focused on structured variables in their identification strategies. Employing surveys with a five-point Likert-type scale, Yang et.al found several important factors in determining review scores for hotels in Taiwan: the quality of the service, room cleanliness, and provision of certain amenities.  The authors recommended that resort hotels needed to improve the quality of amenities provided, while business hotels needed to improve their transportation services to/from airports. Other studies have focused on the effect of observable (non-survey) data on review scores. Zhu et.al focused on independent variables published by Airbnb to determine their effect on Airbnb ratings across 43 cities. They established that good communication, space and provision of information about the listings’ environment were the primary determinants of Airbnb guest satisfaction. 

Second, the heavy reliance on survey data and other structured variables has been criticized. As Li et.al have pointed out, survey data is only limited to fixed questions posited by the researcher, so other important factors may be left out. To avoid these problems, a number of studies have focused on the analysis of unstructured variables, primarily through text analytics techniques. Cheng and Jin used sentiment analysis to illustrate how three attributes – location, the availability of amenities and the characteristics of a given host were the key attributes of an Airbnb experience in Sydney.  Tussyadiah and Zach analysed Airbnb data from Oregon, in the US. Utilizing lexical analysis, they found that Airbnb guests tend to put more focus on the environment of the listings and specific features of the property by frequently emphasizing keywords like “place”, neighborhood”, “location”, “downtown”, “room” and “space” in reviews.  Through clustering these keywords, they suggested that the location cluster can influence the Airbnb review scores.

Despite the ubiquity of literature on the determinants of Airbnb reviews, few studies have combined the use of both unstructured and structured variables in the same analysis. Furthermore, studies relying on unstructured variables have suggested that there may be substantial differences across countries, perhaps due to cultural and socioeconomic factors. Our paper attempts to contribute to the literature in two ways. First, we introduce a methodological innovation of combining both types of variables in our analysis. Second, we aim to examine whether certain determinants are unique to Singapore’s Airbnb context.

## Data Preparation
The overall flow of the analysis process is as summarized in Figure 1. The two main inputs are listings and reviews data which were obtained from [InsideAirbnb’s](http://insideairbnb.com/get-the-data.html) archive dated 28/12/2019,  to avoid exogenous effects attributable to the COVID-19 pandemic.

Listings data consists of majority of listings characteristics with a total of 8,000 observations and 106 variables. This is supplemented by reviews data which can be linked back to listings data through the listings’ unique IDs; this has 108,685 observations in total.

{{< img src="/posts/projects/01_airbnb/images/fig1.png" align="left" >}}
*Figure 1*

## Cleaning of Structured Variables
Since accessibility to public transport is an important determinant, distance to the nearest train station is calculated using geodesic distance as an approximation, with coordinates of train stations obtained from [GitHub](https://github.com/hxchua/datadoubleconfirm/blob/master/datasets/mrtsg.csv), carried out in R with the use of the [geodist R package](https://cran.r-project.org/web/packages/geodist/vignettes/geodist.html) (Annex I). Further, distance to city center is also calculated with the city centre used being Fullerton Hotel  (Annex II). 
Out of all text fields describing the listing, ‘description’ was most complete and thus retained. Other text fields were excluded. 

{{< img src="/posts/projects/01_airbnb/images/fig2.png" align="left" >}}
*Figure 2*

Observations with missing ‘review_scores_rating’ values were removed due to this being the target variable. There were a high number of observations with high and identical ‘host_total_listings_count’ (Figure 2), and identical ‘description’ text coming from the same host (Figure 4). The repeated observations could be due to the host listing several rooms within the same properties, or having identical listings to boost search outcomes. Extreme outliers of ‘host_total_listings_count’ >= 239 were excluded, as well as observations with duplicate ‘description’ text rows. 

{{< img src="/posts/projects/01_airbnb/images/fig3.png" align="left" >}}
*Figure 3*

{{< img src="/posts/projects/01_airbnb/images/fig4.png" align="left" >}} 
*Figure 4*

The variable ‘price_per_pax’ was created to compare value for money, calculated as total of price and cleaning fees per head accommodated. Extreme upper outliers above SGD800 were excluded (Figure 5). Observations with low price_per_pax values less than SGD5 were also excluded as these listings were either no longer available, or were backpackers’ hostels which advertised ‘price’ as price per bed space, while declaring number of guests accommodated using the whole property’s capacity, thereby artificially lowering the ‘price_per_pax’ calculation. 

{{< img src="/posts/projects/01_airbnb/images/fig5.png" align="left" >}}
*Figure 5*

‘Amenities’ consists of up to 74 different items, with the [most important being Wifi, air-conditioning, kitchen, and parking](https://www.airbnb.com.sg/resources/hosting-homes/a/the-best-amenities-to-offer-right-now-203 ). Excluding parking due to h[igh cost of driving](https://www.straitstimes.com/singapore/transport/true-cost-of-driving) in Singapore, binary variables were created for WiFi/Internet, air-conditioning, and kitchen, together with an overall ‘amenities_count’. Other relevant variables created include ‘host_tenure’, ‘host_response_rate_pct’, ‘listing_age’, ‘pct_recent_reviews’ to capture various aspects of host and property. 

## Text Cleaning
First-pass text-analysis in JMP Text Explorer shows a substantial number of foreign reviews and listing descriptions being misclassified as English. [Google’s ‘cld3’ R package](https://cran.r-project.org/web/packages/cld3/cld3.pdf) is used to detect text language (Annex II). Approximately 19.9% of the review and 6.5% of listing descriptions were in foreign languages.
Since each listing may have multiple reviews, reviews in English belonging to the same listing with available review scores are concatenated together. 

Using SAS JMP Pro’s Text Explorer function, data wrangling of reviews and listing descriptions is conducted by tokenizing, stemming, reclassifying irrelevant terms like “a”, “the” as stopwords, correcting misspells and grouping synonyms via recode function. From the terms obtained from data wrangling, we added phrases, which provide positive/negative context to respective term, and created a document term matrix (DTM). DTM records the importance of a term’s occurrence via two possible measures: Binary, and Term Frequency- Inverse Document Frequency (TFIDF). In binary, a ‘1’ represents a term’s presence in the document and ‘0’ its absence. TFIDF represents how important the term is to the specific document in the corpus, discounting for how common it is across all documents:


{{< img src="/posts/projects/01_airbnb/images/f5.png" align="left" >}}
where	TF: Term frequency within the document
nDoc: Number of documents in the corpus
nDocTerm: Number of documents that contains the term 

The obtained Binary-DTM and TFIDF-DTM (each containing 50 terms/phrases) are thus the textual scores obtained from reviews and descriptions for each listing, compiled into a single dataset together with structured variables for model building purposes. 

## Final set of variables
The final dataset for analysis consists of 3,425 observations, 1 dependent variable being review scores, 30 independent variables representing structured data, 200 variables representing textual data from the generated DTMs, with some other variables for reference.

## Analytical Methods
## Exploratory and confirmation data analysis
After data cleaning has been conducted under cleaning of structured variables, exploratory data analysis (EDA) and confirmatory data analysis (CDA) are conducted.

**Review scores**
The overall score, ‘review_scores_rating’, is capped at 100 and has a long-tail left-skewed distribution, suggesting that most guests benchmark the experience at the maximum score and start deducting marks for negative experiences. The distribution is consistent across all 6 component sub-scores imposed by Airbnb.

{{< img src="/posts/projects/01_airbnb/images/fig6.png" align="left" >}} 
*Figure 6*

{{< img src="/posts/projects/01_airbnb/images/fig7.png" align="left" >}}
*Figure 7*

**Geographical distribution of Airbnbs**
A geographical distribution of Airbnbs within Singapore shows that most residential areas in Singapore have Airbnbs, with a high concentration near town center as indicated by 4 distinct hot spots: (1) Geylang, (2) Kallang/Rochor, (3) Orchard/Singapore River/River Valley/Museum, and (4) Outram. While (3) is around the main shopping belt area centered on Orchard, and (4) at Outram is primarily residential area near where historical and tourist sites are located, the Kallang/Rochor and Geylang hot spots indicate a sweet spot for setting up Airbnbs, taking advantage of relatively low real estate prices which translate to lower listing price, while still staying relatively close to town. This is further evident in Figure 8. showing Kallang/Rochor pricing belonging to the middle third, and Geylang in the bottom third of ‘price_per_pax’. 

{{< img src="/posts/projects/01_airbnb/images/fig8.png" align="left" >}}
*Figure 8*

{{< img src="/posts/projects/01_airbnb/images/fig9.png" align="left" >}} 
*Figure 9*

{{< img src="/posts/projects/01_airbnb/images/fig10.png" align="left" >}} 
*Figure 10*

While hotel rooms and shared rooms are typically concentrated nearer to the city center, entire home/apartment and private rooms are available further away in the residential suburbs.

**Property characteristics**

{{< img src="/posts/projects/01_airbnb/images/fig11.png" align="left" >}} 
*Figure 11: Review score rating by room type*

Room type has a strong influence over review scores: properties offering more privacy and space enjoy a significant boost in scores compared to shared rooms (Figure 11). This suggests that guests do not benchmark their expectations relative to the physical constraints of the properties; rather, they rate listings based on the positive experience as a whole. 
 
{{< img src="/posts/projects/01_airbnb/images/fig12.png" align="left" >}} 
*Figure 12: Scores by crucial amenities*

Figure 12 shows that listings with well-provisioned crucial amenities also receive higher scores, consistent with existing literature. 

**Host characteristics**

{{< img src="/posts/projects/01_airbnb/images/fig13.png" align="left" >}} 
*Figure 13*

Figure 13 suggests that verified hosts tend to have higher review scores. Anderson-Darling Test for normality, and Levene Test for the homogeneity of variances are first conducted with resultant p values <0.05, showing that review scores are not normally distributed and do not have equal variances. Welch’s Test is thus carried out.
 
{{< img src="/posts/projects/01_airbnb/images/fig14.png" align="left" >}} 
*Figure 14*

{{< img src="/posts/projects/01_airbnb/images/fig7.png" align="left" >}} 
*Figure 15*
Welch tests return p-values <0.05, indicating that whether the host’s identity is verified causes a significant difference in review scores of the listings. In particular, Figure 13 suggests that being a verified host increases mean review scores by 1 point on average (from 91.3 to 92.3).

# Model Building
All independent continuous variables are checked for multi-collinearity issues. Only pairwise correlation between ‘accommodates’ and ‘beds’ is considerably high above 0.7 (Figure 16), thus ‘beds’ is removed from the list of variables imported into Enterprise Miner for model building. 
 
{{< img src="/posts/projects/01_airbnb/images/fig7.png" align="left" >}} 
*Figure 16*

For 29 structured independent variables and 200 DTM-derived variables, a rule of thumb for minimum sample size for building regression model is 10 times the number of independent variables, which is satisfied.  We aim to build an explanatory model, thus model evaluation is measured by strength-of-fit (Average Squared Errors), and statistical significance of coefficients. 

Model building & selection is conducted via 2 steps:
•	First, models with all structured variables and either TFIDF or Binary DTM variables are constructed with review_scores_rating as the target, each with either multiple linear regression or binary regression tree to determine whether TFIDF or Binary DTM is better.  
•	Second, the chosen DTM variables coming from either reviews or listing together with structured variables are run to determine best key determinants of overall review_scores_rating

# Model Comparison
**Step 1**
To distinguish between TFIDF and Binary DTM, 6 different models were built (see Table 1 for comparison). Result reveals that Model 6 - Binary DTM regression tree provided a better fit (lowest validation ASE) compared to Binary DTM linear regression and TF-IDF models. Given that the TFIDF algorithm assigns more weight to rare terms, TFIDF DTM would penalize top terms as terms were pre-processed to remove stopwords and irrelevant words (see Text Cleaning section). Thus, we have selected model 6 as a base for step 2 – model optimization.

{{< img src="/posts/projects/01_airbnb/images/tab1.png" align="left" >}} 
*Table 1*

{{< img src="/posts/projects/01_airbnb/images/fig17.png" align="left" >}} 
Figure 17: Score ranking overlay for binary and TFIDF models
*Figure 17*

**Step 2**
Model 6 was further calibrated by varying the splitting rules, node properties and method. 
Of the 4 regression trees (Table 2), model 7 was the best performing model with a validation ASE of 84.9 using 6 variables. 

{{< img src="/posts/projects/01_airbnb/images/tab2.png" align="left" >}} 
(Note: Models’ properties used are default settings unless otherwise stated above.)
*Table 2*

{{< img src="/posts/projects/01_airbnb/images/fig18.png" align="left" >}}  
*Figure 18: Score ranking overlay for binary regression trees*

# Results and discussion 

{{< img src="/posts/projects/01_airbnb/images/fig19.png" align="left" >}} 
*Figure 19: Model 7 - score ranking matrix*

The optimal binary regression tree model has relatively good fit (Figure 19), especially at higher range of review scores, with ASE = 85.
 
{{< img src="/posts/projects/01_airbnb/images/fig20.png" align="left" >}} 
*Figure 20: Model 7 - variable importance*
 
{{< img src="/posts/projects/01_airbnb/images/fig21.png" align="left" >}}  
*Figure 21: Model 7 regression tree*

From the optimal model (Figure 20 & Figure 21), we obtained 6 variables of importance. These variables are interpreted as key determinants in helping hosts maximize their review scores:
-	Host_is_superhost: the superhost status results in higher review scores. Superhost status is given by Airbnb as a reflection of several desirable host characteristics.  One limitation that may arise is the possibility that superhost status is granted because of superior reviews, leading to bilateral causality. However, we understand that the superhost status is not updated frequently, so the causal chain from superhost status to review scores is likely to be stronger. In other words, superhost status may be seen as a signal of quality, and hosts should aim to sustain this status by fulfilling all requirements set out by Airbnb. 
-	Price_per_pax: the higher the price per pax, the higher the review scores, which suggests that while guests may appreciate value-for-money, they also consider the higher price a signal for the higher quality of the Airbnb and do not punish a listing for being expensive per se.  
-	Review_checkin_binary: The appearance of the term “check-in” in review text suggests that guests place significant emphasis on the check-in experience: that it should be speedy, fuss-free, and well-communicated.
-	Host_total_listings_count: The higher the number of listings a host manages, the lower the review scores, suggesting a dilution in attention and management, and thus deteriorating quality of an individual experience.
-	Host_tenure: the longer the host has been on Airbnb, the higher the review scores. This length of time allows hosts to accumulate more experience in managing Airbnb listings, as well as a reputation for good service. Furthermore, poor listings are unlikely to succeed in competing with stronger listings over time.
-	Host_response_time: while there is a range of possible response times, it is most important that the host’s response is made within 1 hour. 
Somewhat counterintuitively, location-related variables and amenities are not key factors in determining review scores. A plausible reason for this is that Singapore's efficient transport network and small land-area may alleviate guest concerns regarding transportation to areas of interest.  

# Futher work
There are several potential avenues for improvements:
-	Apart from overall review scores, Airbnb also provides scores focusing on 6 different aspects of the experience. Further exploration on relative weightings amongst these aspects can be carried out.
-	Given that Singapore is multilingual and multicultural, the cultural/racial dimension of Airbnb matching can be further explored. In our own analysis, we detected a substantial number of non-English reviews, which may provide valuable insights that have not been covered in this analysis. These reviews can be further augmented by image processing of host’s profile pictures to infer racial information, as has been done in the USA.  
-	More sophisticated textual analysis techniques may be employed. For example, singular value decomposition applied to text mining can reveal the latent structure of a text corpus as opposed to simple DTM, which contains a lot of noise. Alternatively, latent Dirichlet allocation may also reveal the relevant set of topics and topic mixtures in review and description texts. 

# Conclusion
Based on model building of textual & structured variables, we identified key factors influencing review scores in Singapore to be predominantly host-related: superhost status, number of host listings, host tenure, host response time, pricing, and smooth check-in. We also identified DTM produced from Binary weighting scheme as sufficient compared to TFIDF in producing the optimal model, which was determined to be a binary regression tree.




