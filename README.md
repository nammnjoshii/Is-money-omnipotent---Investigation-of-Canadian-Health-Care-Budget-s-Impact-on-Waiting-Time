#Title: "Is money omnipotent - Investigation of Canadian Health Care Budget’s Impact on Waiting Time"
#Author: Nammn Joshii
#Date: "October 06, 2019"


# Introduction 

Inez Rudderham, a 33 year-old woman from Nova Scotia, recently gained national attention. In a video on her Facebook page, she unfolds her heart-breaking story that she went undiagnosed with stage three anal cancer for two years, because of her lack of access to a family doctor. Unfortunately, this is not an isolated incident. In 2018, Canada’s single-payer healthcare system has forced over a million patients to wait for essential medical treatments.

# Problem Statement

 The average treatment waiting time in Canada is 21 weeks after referral from general practitioner.  A heart breaking revelation emerged after Fraser institute dug deeper into this matter, only to find that 72% of the morality cases due to such delays were actually preventable. Longer waiting time is a nationwide challenge for the Canadian Healthcare system. It is a growing concern and has significant impacts on Canadian people’s welfare. We truly believe this is a meaningful topic to investigate. 

In this project, we will focus on the Canadian healthcare system. Specifically, the primary focus of our project is to investigate the relationship between the healthcare budget and waiting time. 

It may seem trivial to assume the relationship is negative, but there are some other interesting questions we are trying to answer in this project. For example: How strong the correlation is? Is the relationship linear?  Is there a marginal diminishing effect for waiting time when more and more budgets are put into the system? 

The ultimate goal of our project is to provide remedial suggestions for both public and private healthcare participants in Canada to shorten the waiting time for medical services, and hopefully to promote welfare for the whole society .


#  Data Resources 

We started our data search with following criteria: the availability of needed variables, the scope and time span of the databases, the quality of the data, and whether the source is trusted. 

Specifically, in this project, we are investigating the relationship between the healthcare budgets and the waiting time for health care services. These two will be the independent and dependent variables in our study and are our main targets to search for. 

In terms of the scope and time span, since we are interested in longer waiting time, a distinct issue of Canadian healthcare system, we limit our scope to the nation. Ideally, the dataset will have provincial data, so that we will be able to generate more insight by comparing data across Canada. For time span, our proposed time span of the study is five years. However, in the data searching process we tried to find the databases with the longest time span possible to give us more flexibility to trim and accommodate different time spans in the two variables. We will generate our final clean database using the overlapped portion of the data we collect.   

Finally, about the data quality and trustworthiness of the data. We put our focus not only on the data itself, but also the support documents come with it. We carefully read the description files to find the definitions and methodologies conducted in the data collection process. We tried to exclude datasets with too much N/A values. We also take a look at the trustworthiness of the organization that provides the data.

Based on the above selection criteria, our final chosen data are collected from the Canadian Institute for Health Information (CIHI). Founded in 1994, CIHI is a not-for-profit organization that provides a good collection of Canadian healthcare system databases, measurements, and analyses report. The CIHI is also a reliable data source and is commonly used for research. In Josephs, K., & Fahey, J. (2009), the authors conclude that its databases are relatively accurate and compared favourably to other available data sources. 


### National Health Expenditure Data, 1975 to 2018 

Our primary independent variable is the medical budget. Our data resource is from the Canadian Institute for Health Information (CIHI).
(https://www.cihi.ca/sites/default/files/document/nhex-series-b-2018-en.xlsx)

The data of total health expenditure by provinces/territories is the representative indicator of this factor, which includes total health expenditure, in millions of current dollars, for columns we have 10 provinces and 2 territories in Canada, and for column range from 1975 to 2018. 
(10 provinces and 3 territories are respectively Newfoundland and Labrador, Prince Edward Island, Nova Scotia, New Brunswick, Quebec, Ontario, Manitoba, Saskatchewan, Alberta, British Columbia, Yukon, and Northwest Territories).Key sugnificance of this dataset is the detailed total health expenditure 10 provinces. We use these data as the representative indicator of medical budget and then create the database.


| Column                    | Meaning                          |
|---------------------------|----------------------------------|
| year                      | Year of the Dataset (1975-2018)  |
| [NL -- Nvt.]              | Province or territory (13 cols)  |
| Values within each cell   | Expenditure allocated            |


# Data Model and Management

## Waiting Times for procedures in Canada by province. 2008 to 2018 

Our primary dependent variable is the Waiting Time data. Our data resource is from the Canadian Institute for Health Information (CIHI).
(http://waittimes.cihi.ca/spreadsheets/Wait%20Times%20Export%20Data%202019_EN.xlsx)

This extensive waiting time data is categorized by provinces in canada, Volumes of procedures affected by it and types of procedure. 
(Types of Procdures : Cataract,	Bypass Surgery,	Radiation Therapy,	CT Scan,	MRI Scan,	Bladder Cancer Surgery,	Breast Cancer Surgery,	Colorectal Cancer Surgery,	Lung Cancer Surgery,	Prostate Cancer Surgery)

Key research significance of this data is that it is the primary dependent variable for the problem statement and it helps quantify the core problem. 


| Column                    | Meaning                          |
|---------------------------|----------------------------------|
| Data Year                 | Year of the Dataset (2008-2018)  |
| Province [NL -- Nvt.]     | Province or territory (13 cols)  |
| Volume	                  | Volume of Procedures             |
| % Meeting  Benchmark      | % meeting Benchmark Waiting Time |
|50th Percentile (in Days)  | Median Waiting Time              |
|90th Percentile (in Days)  | 90th Percentile of Waiting Time  |


# Analysis 

## Analysis 1 : Budget vs Avg Waiting Time


From the interaction between Budget vs Avg Waiting Time, we can establish that the amount of medical finances differs greatly depending on which province we analyze. An interesting fact is that the increase in budget amount is rather stable for each region. 


## Analysis 2 : Province vs Avg Waiting Time

The interaction between Province & Avg Waiting Time establishes that the increase in waiting time is not a regular trend in Canada, but rather a feature in several provinces. Different provinces have different waiting time trends and the largest deviation within years is spotted in British Columbia, New Brunswick and Prince Edward Island.


## Analysis 3 : Year vs Avg Waiting Time

The interaction Year & Avg Waiting Times, we can suggest that, overall, each province experienced an increase in waiting time in 2018 compared to 2013. However, there is no stable percent of increase annually, meaning that a specific trend could affect the amount of waiting time in a particular year of observation and in a particular region.


## Correlation between Waiting Time and Budget

We test the correlation between Waiting Time and Budget using "cor.test" function and then plot a scatter diagram using "scatter.smooth" function.


Pearson's product-moment correlation:

data:  Merged_Final$Avg50thP and Merged_Final$Budget
t = -4, df = 52, p-value = 0.0006
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 -0.6 -0.2
sample estimates:
 cor 
-0.5 

This leds to an interesting finding that there is a significant negative correlation between waiting time and healthcare medical budget (appr coef -0.5). Whenever the budget increases for a million Canadian dollar, the amount of waiting time, on average, decreases by 0.5 days. 

The distribution within the graph can give us a clue that a particular trend (e.g. the dots grouped on the upper left corner) exists within a particular group of observations.


## Regression Analysis

To understand Regression between Budget and Waiting Time we used "lm" function and then "summary" function to review its results.

Call:
lm(formula = Avg50thP ~ Budget, data = Merged_Final)

Residuals:
    Min      1Q  Median      3Q     Max 
-22.541  -6.259  -0.196   7.578  23.487 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)    
(Intercept) 51.1050302  1.9141095   26.70  < 2e-16 ***
Budget      -0.0001926  0.0000526   -3.66  0.00059 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 10 on 52 degrees of freedom
Multiple R-squared:  0.205,	Adjusted R-squared:  0.19 
F-statistic: 13.4 on 1 and 52 DF,  p-value: 0.000585

# Conclusion

In conclusion, we can establish that, although medical budget has an impact on the waiting time for patients in Canada, it seems that another major trigger can influence the amount of days that patients have to wait for their treatments. In terms of medical budget, we found that there is a significant negative correlation between waiting time and healthcare medical finances (appr -0.5).

By grouping the data by provinces, we established that there is an effect of the amount of healthcare budget on the waiting time, though it should be noted that other possible trends and factors may bear influence on the waiting time amount. Based on the provided graphs, we can assume that a possible phenomenon can exist only within certain province, which can lead to a severe increase of the waiting time in healthcare system. A possible trend could be the aging population, lack of medical equipment of specialists required in the given region.


# Discussion: Negative or Positive Relationship?

In the first iteration of our analysis, we did a regression analysis for all the data points in our database. We found a significant negative correlation between budget and waiting time. The result is consistent with our initial assumption.

However, when we plot our data points by province, the results surprised us: the provincial data shows a weak positive relation between the budget and the waiting time- a very counterintuitive result. Does it mean that the more budget is causing longer waiting time in Canada? 

We re-examined our original model again, and found some possible issues about this result:
1.	Our original model (regression) is oversimplified. It considers only one independent variable- the budget, without any control variables. This may lead to a problem that there are too many external factors (especially for the ones come from the inherent differences among provinces, for example, the total population, density, aging of the population, etc). Therefore, it does not make sense to include all the data points across Canada in our regression model. Plotting a line for each province and one for Canada nationwide respectively could give us more accurate information about the relationship between budget and waiting time.   
2.	 Correlation does not necessarily mean causation. Since we did not include any econometric treatment to eliminate the simultaneity between the independent variable and dependent variable (e.g. a time lag). The simple regression analysis we ran can only show correlation, but does not have the ability to show the causality. 

After considering the two issues above, we propose there might be a reverse causality exists, that means, it is not that budget affect waiting time. It is the longer waiting time forcing the Canadian government to put more and more budget in its healthcare system. However, unfortunately, due to some other reasons (facilities availability, more patents due to the aging population), the waiting time is still rising across Canada. This theory, however, requires further research of the possible outcomes and correlations.      

The above discussion also gave us some directions for the potential future extensions of the Study. For example, more control variables can be in the model to decrease the impact from the externalities. Also, a time lag method could be beneficial to reveal the causality between the independent and dependent variable.

Thank You

# References: 

1. National Health Expenditure Trends, 1975 to 2018, CIHI (Nov 2018)
2. Wait times for priority procedures in Canada, CIHI (Mar 2019)
