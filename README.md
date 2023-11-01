# Austine-Crime-Analysis-in-BigQuery-SQL-
Austine Crime Analysis in Google BigQuery with Inbuilt SQL flavor.

# Data Source & Table info
Data Source:     BigQuery Public Data

Table ID:        bigquery-public-data.austin_crime.crime

Created:         Jun 6, 2017, 10:51:04 PM UTC+5:30

Last modified:   Oct 30, 2023, 5:38:26 AM UTC+5:30

# Exploratory Data Analysis with Insights
## 1. Top Crimes by their no. of times happpend.
```
SELECT description Crime, count(description) as Crime_reported
FROM `bigquery-public-data.austin_crime.crime` 
group by 1
order by 2 desc
limit 20;
```
![image](https://github.com/mustafaCLI/Austine-Crime-Analysis-in-Bigquery-SQL-/assets/121651184/621e15a5-bad2-4431-b8c6-902402b64843)
## Insight:
Burglary and Theft are the major crimes happened all time, which is 90% more than of all Crimes_reported.

## 2. Top Crimes by clearance_status (not Cleared)
'''
with ct as
(SELECT description, clearance_status, count(description) as cnt
FROM `bigquery-public-data.austin_crime.crime` 
group by 2, 1
)
select *
from ct
pivot (
sum(cnt) for clearance_status IN ( 'Not cleared', 'Cleared by Arrest', 'Cleared by Exception')
)
order by 2 desc
limit 15;
'''
![image](https://github.com/mustafaCLI/Austine-Crime-Analysis-in-Bigquery-SQL-/assets/121651184/5d457cb7-a463-40f4-8334-64a7441c2537)
## Insight:
It seems clearly more than 60% cases are pending or not solved for all.

## 3. Top Crimes by % of total crimes than crimes status.   


