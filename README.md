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

## 3. Top Crimes share %  than total crimes by description.  

``` sql
select t2.description, t2.All_Crime_reported,  
concat(round(((t1.not_cleared) * 100)/(t2.All_Crime_reported),2),"%") as not_clreared,
concat(round(((t1.cleared_by_exception) * 100)/(t2.All_Crime_reported),2),"%") as cleared_by_exception,
concat(round(((t1.cleared_by_arrest) * 100)/(t2.All_Crime_reported),2),"%") as cleared_by_arrest 
from
(with ct as
(SELECT description, clearance_status, count(description) as cnt
FROM `bigquery-public-data.austin_crime.crime` 
group by 2, 1
)
select *
from ct
pivot (
sum(cnt) for clearance_status IN ( 'Not cleared' as not_cleared, 
'Cleared by Arrest' as cleared_by_arrest, 
'Cleared by Exception' as cleared_by_exception))) as t1
join 
(SELECT description, count(description) as All_Crime_reported
FROM `bigquery-public-data.austin_crime.crime` 
group by 1) as t2
on t1.description =  t2.description
order by 2 desc,3 desc
limit 20;
```
![image](https://github.com/mustafaCLI/Austine-Crime-Analysis-in-Bigquery-SQL-/assets/121651184/2edb7037-26e5-4b46-932e-c7f62e49c50e)
## Insight:
Clearly seen more than 80% of crimes are not solved yet, amongst max are related to theft description.
## Q4. Top 10 Crimes description by % which are not cleared yet.
``` sql
select t2.description, t2.All_Crime_reported,  
concat(round(((t1.not_cleared) * 100)/(t2.All_Crime_reported),2),"%") as not_clreared,
from
(with ct as
(SELECT description, clearance_status, count(description) as cnt
FROM `bigquery-public-data.austin_crime.crime` 
group by 2, 1
)
select *
from ct
pivot (
sum(cnt) for clearance_status IN ( 'Not cleared' as not_cleared, 
'Cleared by Arrest' as cleared_by_arrest, 
'Cleared by Exception' as cleared_by_exception))) as t1
join 
(SELECT description, count(description) as All_Crime_reported
FROM `bigquery-public-data.austin_crime.crime` 
group by 1) as t2
on t1.description =  t2.description
order by 3 desc
limit 10;
```
![image](https://github.com/mustafaCLI/Austine-Crime-Analysis-in-Bigquery-SQL-/assets/121651184/e2fe8b2a-bf89-4ad1-9e7f-4444e69e91d4)

## Insight:
Again theft related crimes are in top 10 which are not cleared. Means more than 90% of top cases/ crimes are pending. 

## Q5. Top 10 Crimes description by % which have been cleared.
``` sql
select t2.description, t2.All_Crime_reported,  
concat(round(((t1.not_cleared) * 100)/(t2.All_Crime_reported),2),"%") as not_clreared,
from
(with ct as
(SELECT description, clearance_status, count(description) as cnt
FROM `bigquery-public-data.austin_crime.crime` 
group by 2, 1
)
select *
from ct
pivot (
sum(cnt) for clearance_status IN ( 'Not cleared' as not_cleared, 
'Cleared by Arrest' as cleared_by_arrest, 
'Cleared by Exception' as cleared_by_exception))) as t1
join 
(SELECT description, count(description) as All_Crime_reported
FROM `bigquery-public-data.austin_crime.crime` 
group by 1) as t2
on t1.description =  t2.description
order by 3 desc
limit 10;
```
![image](https://github.com/mustafaCLI/Austine-Crime-Analysis-in-Bigquery-SQL-/assets/121651184/e2fe8b2a-bf89-4ad1-9e7f-4444e69e91d4)

## Insight:
Again theft related crimes are in top 10 which are not cleared. Means more than 90% of top cases/ crimes are pending. 





