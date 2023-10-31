# Austine-Crime-Analysis-in-Bigquery-SQL-
Austine Crime Analysis in Google Bigquery with Inbuilt SQL flavor.

# Data Source & Table info
Data Source:     BigQuery Public Data
Table ID:        bigquery-public-data.austin_crime.crime
Created:         Jun 6, 2017, 10:51:04 PM UTC+5:30
Last modified:   Oct 30, 2023, 5:38:26 AM UTC+5:30

# Exploratory Data Analysis Insights
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
Bulgary and Theft are the major crimes happened all time, which is 90% more than of all Crimes_reported.




