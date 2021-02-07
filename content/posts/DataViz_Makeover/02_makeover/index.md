---
title: "DataViz Makeover #2"
date: 2021-02-19
description: tbd.
menu:
  sidebar:
    name: DataViz Makeover 02
    identifier: Dataviz-makeover
    parent: DataViz-Makeover    
    weight: 99
math: true
---

# Willingess to vaccinate against Covid-19


*This was written as part of the requirements for the Visual Analytics module for [MITB](https://scis.smu.edu.sg/master-it-business).*

---



## 1. The original visualisation

{{< img src="/posts/DataViz_Makeover/02_makeover/images/fig1.png" align="left" >}}
*Figure 1*




## 2. Critiques and suggestions for current visualisation
### 2.1 Clarity


### Aesthetics



## 3. Proposed Design
### 3.1 Sketch



### 3.2 Advantages of Proposed Design



## 4 Final visualisation
### 4.1 Dashboard


### 4.2 Main observations




## 5. Data visualisation steps
Of the 30 files, 14 files were excluded as the “vac_1” field was not available, i.e the vaccine survey was not conducted in these countries. Please see full list of cleaning methods in xx.

### 5.1 Data Cleaning and Preparation
**Data cleaning with Excel**

**1) Denmark, Finland, Norway, Sweden**  
Employment status were split into 7 columns, see figure below.  

*Figure*  

As such, the following Excel formula was used to combined the 7 columns to get field "employment_status".  

 
**2) Israel**
Values for household_size, household_children and employment_status were missing. We have included “NA” values for these field.  

**Data Cleaning and Extraction with R**  
The following script was used to   
1) extract selected 11 columns - age, gender, household size, household children, employment status, vac 1, vac2_1, vac2_2, vac2_3, vac2_6 and vac_3.  
2) add new column with country name
3) merge all 16 files into 1

```
library(dplyr)
library(tidyr)

**extract these columns only**
header = c("age","gender", "household_size", "household_children", "employment_status" ,"vac_1",	"vac2_1", "vac2_2",	"vac2_3","vac2_6",	"vac_3") 

**create function to extract selected columns**
clean_files <- function(file){
  df <- read.csv(file)
  sub_df <- subset(df, select = header)
  c_df <- cbind(sub_df, country = file)
  clean_df <- c_df %>% filter(c_df$vac_1 != " ")
}

**get list of files**
cs_files <- dir("./data") 
my_cs_files <- paste0("./data/",cs_files)

my_cs_data <- NULL
for (file in my_cs_files) {
  temp <- clean_files(file)  
  temp$country <- sub(".csv", "", file) 
  my_cs_data <- rbind(my_cs_data, temp) 
}

**remove ./data/ from country column**
my_cs_data <- my_cs_data %>% 
  dplyr::mutate(country = 
                  stringr::str_replace(country, 
                                       pattern = "./data/" , 
                                       replacement = "")) 
                                       
**check number of files**
my_cs_data %>% 
  dplyr::distinct(country) %>% 
  base::nrow()

write.csv(my_cs_data, file = 'clean/clean_countries.csv') 


```


### 5.2 Data visualisation steps







---
[Background vector created by freepik](https://www.freepik.com/vectors/background).
