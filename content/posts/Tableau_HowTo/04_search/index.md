---
title: "Search box"
date: 2021-06-07
description: Search box to lookup text
menu:
  sidebar:
    name: Search box
    identifier: Search box
    parent: Tableau How to
    weight:  100
math: true
---

---

*Documenting my Tableau learning journey.*

---


Look up Profit and Quantity of Specific customer.


<div class='tableauPlaceholder' id='viz1623077669575' style='position: relative'><noscript><a href='#'><img alt='Lookup Profit and Quantity by Customers using search box ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Se&#47;Searchbox&#47;Sheet1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='Searchbox&#47;Sheet1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Se&#47;Searchbox&#47;Sheet1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1623077669575');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


Full visualisation available on [Tableau Public](https://public.tableau.com/views/Searchbox/Sheet1?:language=en-US&:display_count=n&:origin=viz_share_link).  

Other use cases - [Tableau Public](https://public.tableau.com/views/sentiment_analysis_16182051054700/Dashboard1?:language=en-US&:display_count=n&:origin=viz_share_link)

## Good for
Looking up text.

## How to create - step by step

To illustrate this search function, I have used the EU superstore dataset (Tableau's sample dataset).

### 1) Set up table to anaylse

Here is a relatively simple table that shows profit and quantity by customer name.

![](images/fig1.png)


But how we quickly look up a certain customer along with their profit and quantity sold?

By using a search box function!

### 2) Set up search parameter and calculated field

i) Create Parameter - the search box.


![](images/fig2.png)


ii) Show parameter

Right click on the parameter and select 'Show Parameter'


![](images/fig4.png)


A box like this will appear on the right hand corner of your screen.


![](images/fig5.png)


ii) Create calculated field.


![](images/fig3.png)


Drag [text filter] to the Filters pane and check True.

![](images/fig6.png)

### 3) Perform search


![](images/gif1.gif)


# And.. there you have it! Search box function to look up text.


---
I would like to thank Prof Kam of Singapore Management University for the inspiration for this series.


People vector created by [pch.vector](https://www.freepik.com/vectors/people)