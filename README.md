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
library(dplyr)
library(janitor)
library(readr) # used for reading a csv file.
```

```{r}
# Displaying and setting-up working directory
getwd()
setwd("C:\\Users\\dambe\\Desktop\\Portfolio Project")
```

```{r}
# Loading dataset. I am inserting 'na' where the columns values are empty.
m1<-read.csv("1_March_2022.csv", na="")
m2<-read.csv("2_April_2022.csv",na="")
m3<-read.csv("3_May_2022.csv",na="")
m4<-read.csv("4_June_2022.csv",na="")
m5<-read.csv("5_July_2022.csv",na="")
m6<-read.csv("6_August_2022.csv",na="")
m7<-read.csv("7_Sept_2022.csv",na="")
m8<-read.csv("8_Oct_2022.csv",na="")
m9<-read.csv("9_Nov_2022.csv",na="")
m10<-read.csv("10_Dec_2022.csv",na="")
m11<-read.csv("11_Jan_2023.csv",na="")
m12<-read.csv("12_Feb_2023.csv",na="")
```

```{r}
# Comparing column names of each files before combining them into single dataset.
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
```{r}
# combining multiple datasets to a single large dataset.
combined_trip <- bind_rows(m1, m2, m3, m4, m5, m6, m7, m8, m9, m10, m11, m12);
View(combined_trip)
```
# Processing data for analysis #
```{r}
#Verify the data for consistency
head(combined_trip)
nrow(combined_trip)
ncol(combined_trip)
glimpse(combined_trip)
```
```{r}
# Dropping any rows with NA/empty values
combined_trip2 <- remove_empty(combined_trip, c("rows", "cols"))%>%
  drop_na()
```
```{r}
# Inspecting the the cleaned data 
glimpse(combined_trip2)
str(combined_trip2)
```
```{r}
# Add columns date, month, day, year and hour of each ride
# https://www.statmethods.net/input/dates.html more on date formats in R found at that link
combined_trip2$Date <- as.Date(combined_trip2$started_at)
combined_trip2$Month <- format(as.Date(combined_trip2$Date), "%m")
combined_trip2$Day <- format(as.Date(combined_trip2$Date), "%d")
combined_trip2$Year <- format(as.Date(combined_trip2$Date), "%Y")
combined_trip2$Day_of_Week <- format(as.Date(combined_trip2$Date), "%A")
combined_trip2$Hour <- hour(combined_trip2$started_at)
combined_trip2$Ride_Length <- difftime(combined_trip2$ended_at,combined_trip2$started_at,units = "min") #calculating ride_length in minutes
```
```{r}
#Inspecting additional columns and structure of column
head(combined_trip2)
str(combined_trip2)
```
```{r}
# Convert "ride_length" from Factor to numeric for easy calculations
combined_trip2$Ride_Length <- as.numeric(as.character(combined_trip2$Ride_Length))
is.numeric(combined_trip2$Ride_Length)
str(combined_trip2)
```

**Inspecting and removing bad data**
```{r}
#Checking ride length less than 0
nrow(subset(combined_trip2, Ride_Length<0))
```
```{r}
# Removing row with ride_length less than 0.
combined_trip2 <- combined_trip2[!(combined_trip2$Ride_Length<0),]
```
```{r}
#Checking if any bicycles were used for test/by company for maintenance
nrow(subset(combined_trip2,start_station_name == "HQ QR"))
str(combined_trip2)
```
```{r}
#removing unwanted columns from the data set
combined_trip2 <- subset(combined_trip2, select = -c(started_at, ended_at,start_station_id, end_station_id,start_lat, start_lng,end_lat, end_lng))
str(combined_trip2)
```

**Exporting cleaned data set for further analysis**
```{r}
write.csv(combined_trip2,"Final_Cleaned_Trip_Data.csv", row.names = TRUE)
```
# Descriptive Analysis #
*Descriptive analysis on ride_length (all figures in minutes*
```{r}
mean(combined_trip2$Ride_Length)
median(combined_trip2$Ride_Length)  #median ride length
max(combined_trip2$Ride_Length) #max ride length
min(combined_trip2$Ride_Length) # shortest ride length
```
