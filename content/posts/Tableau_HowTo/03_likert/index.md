---
title: "Likert Scale"
date: 2021-03-09
description: Singapore's perception towards Covid-19 vaccine
menu:
  sidebar:
    name: Likert Scale
    identifier: Likert Scale
    parent: Tableau How to
    weight:  100
math: true
---

---

*Documenting my Tableau learning journey.*

---

## Likert Scale

Survey on mental wellness in Singapore.

<div class='tableauPlaceholder' id='viz1615607707206' style='position: relative'><noscript><a href='https:&#47;&#47;suyiinang.netlify.app&#47;posts&#47;tableau_howto&#47;03_likert&#47;'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Li&#47;Likertscalechart_SurveyonmentalwellnessinSingapore&#47;Dashboard1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Likertscalechart_SurveyonmentalwellnessinSingapore&#47;Dashboard1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Li&#47;Likertscalechart_SurveyonmentalwellnessinSingapore&#47;Dashboard1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1615607707206');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';} else { vizElement.style.width='100%';vizElement.style.height='1277px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

Full visualisation available on [Tableau Public](https://public.tableau.com/profile/suyiinang#!/vizhome/likert_16153800261360/Dashboard1?publish=yes).  


## Good for
Analysing survey data

## How to create - step by step
I have used the Covid-19 tracker data for Singapore from [YouGov](https://github.com/YouGov-Data/covid-19-tracker).

**Data Cleaning - MS Excel**

As there are quite a number of survey questions, I have only retained 4 questions relating to mental health (PHQ questions) and some demographic data.

Blank observations were removed from my final dataset.

**Data Preparation - Tableau**

1) Pivot data
![](images/gif1.gif)    

2) Rename headers 
![](images/fig2.png)    

3) Create score 
![](images/fig3.png)    

4) Create alias for score
![](images/fig4.png)    

5) Create alias for Question
![](images/fig5.png)    

6) Create age group
![](images/fig6.png)   

### Likert Scale with neutrals by the side
1) Create calculated fields
- No of records

![](images/fig7.png)   

- Count positive/negative/neutral
Due to the nature of the responses, I have categorised the responses 3 types of sentiments:
|Sentiments| Responses|
|----|-----|
| Positive | Not at all|
| Neutral | Prefer not to say |
| Negative | Several days, More than half the days, Nearly everyday |

![](images/fig8.png)   

- Sentiment percentage

![](images/fig10.png)   

2) Arrange variables
![](images/fig11.png)   

3) Change chart type to "Bar", Select dual axis and synchronize axis, remove measure names.
![](images/gif2.gif)   

4) Add neutral %
![](images/fig12.png)   

5) Fix axis of neutrals to align both charts
![](images/fig13.png)   

6) Format chart according to preference.



Here you have a likert scale chart with neutrals by the side. 
![](images/L2.png)   


However, given that the percentage of neutrals are relatively small, it may be more meaningful to have neutrals between the positive and negative responses

### The usual likert scale
1) Create calculated fields
- Count positive/negative/neutral

![](images/fig14.png)   

- Sentiment percentage

![](images/fig15.png)   

2) Put it together
![](images/fig16.png)   

3) Repeat step 3 as mentioned above - Change chart type to "Bar", Select dual axis and synchronize axis, remove measure names.

4) Sort % score accordingly.
![](images/fig17.png)   

There you have a likert scale chart!


## Adding some interactivity
1) Add [Question] and [Endtime] to Filters. Select show filter for both.

For Question - select Single Value (dropdown) for [Endtime] select Range of Dates.

![](images/fig18.png)   


# And.. there you have it! Likert scale showcasing survey results.
![](images/L1.png)   

---
I would like to thank Prof Kam of Singapore Management University for the inspiration.
