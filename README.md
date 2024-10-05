# Programming Languages Trends Analysis

## Overview
This repository contains a Jupyter notebook that analyzes trends in programming languages based on data retrieved from StackExchange. The notebook explores the number of posts per language over time, visualizing the data to provide insights into the popularity of various programming languages.

## Get the Data

You can either use the provided `QueryResults.csv` file or obtain fresh data by running an SQL query on StackExchange. Follow this link to run the query from [StackExchange](https://data.stackexchange.com/stackoverflow/query/675441/popular-programming-languages-per-over-time-eversql-com) to generate your own CSV file.

### SQL Query

```sql
SELECT dateadd(month, datediff(month, 0, q.CreationDate), 0) AS m, 
       TagName, 
       COUNT(*) AS post_count
FROM PostTags pt
JOIN Posts q ON q.Id = pt.PostId
JOIN Tags t ON t.Id = pt.TagId
WHERE TagName IN ('java','c','c++','python','c#','javascript','assembly','php','perl','ruby','visual basic','swift','r','object-c','scratch','go','swift','delphi')
AND q.CreationDate < dateadd(month, datediff(month, 0, getdate()), 0)
GROUP BY dateadd(month, datediff(month, 0, q.CreationDate), 0), TagName
ORDER BY dateadd(month, datediff(month, 0, q.CreationDate), 0)

