# Google Data Analytics Capstone Project
## Case Study on How Does a Bike-Share Navigate Speedy Success?  
**Author:** *Damber Singh Biswa*  
Date: 02/16/2023  
Note: Please refer to the files in this repository to find all the resources used for this project.  
***  
## Introduction:

**About the Data:**  
Cyclistic (fictional company) is a bike-sharing company based in Chicago, Divvy, operated by Lyft.  
Data source: [Divvy Tripdata](https://divvy-tripdata.s3.amazonaws.com/index.html)  
The data has been made available by Motivate International Inc. under this [license].(https://ride.divvybikes.com/data-license-agreement)

**Background information**  

Cyclistic offers a wide range of bike-share program that features over 5,800 bicycles spread over its 600 docking stations. It is found that most of the users ride for liesure and about 30% use them to commute to work each day. Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. Cycistics offers different pricing plans such as single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders and customers who purchase annual memberships are referred as Cyclistic members.  
  
Of late, Cyclistics concluded that annual members are much more profitbale than casual riders and believe that maximizing the number of annual members will be a key to company's future growth. Although the pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will
be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.  
  
**Business Task**  
Of late, the company finance analyst concluded that annual memnbers are much more profitable than casual riders and believe that maximizing the number of annual members will be a key to company's future growth. We will follow the **Ask, Prepare, Process, Analyse, Share, Act** process of data analysis to solve the business problem.

# ASK Phase #  
Key stakeholders for this project:  
* Lily Moreno - Director of Marketing
* Cyclistic Marketing Analystics team
* Cyclistic Executives

Key questions to ask:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?


# Preparing data for analysis #
Twelve months data from March 2022 to February 2023 have been downloaded from [Divvy Tripdata](https://divvy-tripdata.s3.amazonaws.com/index.html). The data is well organized in excel format. 
* Tools to be used for cleaning data: R
* Tool for visualization: R & Tableau

```{r}
# Installing libraries in R
# tidyverse for data wrangling, lubridate for formatting date and ggplot2 for visualization.
library(tidyverse) 
library(lubridate) 
library(ggplot2)
library(readr)
```

```{r}
# Displaying and setting-up working directory
getwd()
setwd("C:\\Users\\dambe\\Desktop\\Portfolio Project")
```

```{r}
# Loading csv files to RStudio
m1<-read.csv("1_March_2022.csv")
m2<-read.csv("2_April_2022.csv")
m3<-read.csv("3_May_2022.csv")
m4<-read.csv("4_June_2022.csv")
m5<-read.csv("5_July_2022.csv")
m6<-read.csv("6_August_2022.csv")
m7<-read.csv("7_Sept_2022.csv")
m8<-read.csv("8_Oct_2022.csv")
m9<-read.csv("9_Nov_2022.csv")
m10<-read.csv("10_Dec_2022.csv")
m11<-read.csv("11_Jan_2023.csv")
m12<-read.csv("12_Feb_2023.csv")
```

```{r}
# Comparing column names of each files.
colnames(m1)
colnames(m2)
colnames(m3)
colnames(m4)
colnames(m5)
colnames(m6)
colnames(m7)
colnames(m8)
colnames(m9)
colnames(m10)
colnames(m11)
colnames(m12)
```

