# Data Jobs Salary And Skills Analysis #

## Project Background ##
After did a small research on data jobs trend in 2023 and make it into a dashboard, in this project I dive deeper to analyze skills that needed to become a data analyst and its correlation with the salary offered. Check out my previous salary dashboard project to get more information about the begining of this project by clicking this link below : 

[Salary Dashboard Project](https://github.com/Dwisetiyawan/Salary-Dashboard-Project)

The focus of this analysis is to know what skills needed to become a data analyst, skills vs salary correlation, and the median salary of top ten skills.

## Summary ## 

The most mentioned skills for Data Analyst role are SQL, Excel, Python, and Tableau with skill likelihood 52% , 40% , 29% , and 28% respectively. Data analyst role mentioned at least 3 skills required for this role. The median salary tend to be higher with more skills required, however, different level of role also affect the salary for each role in data jobs. Python as one of the most skills mentioned for Data Analyst has the highest median salary at USD 98,500. 

## Key Insights ## 

The top 10 skills for Data Analyst is as shown by the chart below : 

![Data Analyst Skills](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/Data%20Analyst%20Skills.jpg)

SQL, Excel, Python are top 3 skills with skill likelihood (the percentage of each skill mentioned in every data analyst job postings) 52% , 40% , and 29%. Beside that, Tableau and Power BI as the most common data visualization tools are on the 4<sup>th</sup> and 6<sup>th</sup> position with skill likelihood 28% and 17%.

Skills vs salary correlation is shown by the chart below : 

![Salary vs Skills](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/Salary%20vs%20Skills.jpg)

Each job posting mentioned skills required for the job. Senior Data Scientist has the highest median salary with USD 155,000 and 5.3 skills mentioned per job, followed by Senior Data Engineer with median salary USD 147,500 and 8.1 skills mentioned per job . For Data Analyst the median salary is USD 90,000 with 3.6 skills mentioned per job.  As shown on the chart above, more skills tend to have higher salary, but it is weakly correlated with R below 0.8 (0.46). The other factor possibly the experience that increase the salary for senior role in data jobs. However, for Data Analyst, even for the senior role the median salary is still lower than Data Engineer and Data Scientist role. 

The median salary for the top 10 skills is shown by the chart below :

![Salary Skills](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/Salary%20Skills.jpg)

The objective of the chart above is to show median salary of each skill that mentioned on the job postings. SQL, Excel, Python, and Tableau as the most mentioned skills for data analyst job have median salary USD 92,500 , USD 84,500 , USD 98,500 , and USD 95,000 respectively. Python has the highest median salary, however, it is likely to be needed for more data scientist or data engineer role. 

## Recommendations ## 

As for an aspiring data analyst, SQL, Excel, Python, and Tableau are the skills that need to be acquired, since those skills are the most mentioned skills for this role. However, there is a possibility different skill would also required for data analyst role, or one of the skill mentioned above is not required or subtituted by another skill.

## Caveats ## 

- This analysis used 32K job postings data in 2023 that I got from free Excel course on **Luke Barrouse** youtube channel
- The raw data contain information about job title, job location, job schedule type, average yearly & hourly salary, job country,        company, job posted date, job posted platform, and skills related. 
- The raw data had already cleaned up, so I did not do data cleaning

## Skills Used ##

- Power Query :
    
    1. Extract : used Power Query to extract original data (data_salary_all.xlsx) and create 2 queries : 
        
        a. data_jobs_salary : contain all the data jobs information
        
        b. data_jobs_skills : listing the skills for each job id
    2. Transform :  transformed each query by changing column types, removing unnecessary columns, cleaning text to eliminate specific words, and trimming excess whitespace
    
        ![data_jobs_salary](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/data_jobs_salary_transform.jpg)

        ![data_jobs_skills](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/data_jobs_skills_transform.jpg)

    3. Load : loaded both transformed queries into the workbook
        ![data_jobs_salary](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/data_jobs_salary_load.jpg)

        ![data_jobs_skills](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/data_jobs_skills_load.jpg)

- Power Pivot : 
created a data model by integrating the data_jobs_all and data_jobs_skills tables into one model, created relationship between two tables using the job_id column

    ![data_model](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/data_model.jpg)

- Pivot Table & DAX

    1. Pivot Table : created a PivotTable using the Data Model created before with Power Pivot

        ![pivot_table](https://github.com/Dwisetiyawan/Salary-And-Skills-Analysis-Project/blob/main/Documentation/pivot_table.jpg)

    2. DAX : calculate the median salary, job count, skill count, skills likelihood 
    
    ```
    Median Salary := MEDIAN(data_jobs_all[salary_year_avg])
    ```
    ```
    Job Count 1:=DISTINCTCOUNT('data_jobs_salary 1'[job_id])
    ```
    ```
    Skill Count:=COUNT(data_jobs_skills[job_skills])
    ```
    ```
    Skill Likelihood:=DIVIDE([Skill Count];[Job Count 1])
    ```

- Pivot Chart : create PivotChart (bar, scatter, and combo) to plot visualize skill likelihood, median salary vs avg skills per job,  median salary, and skill likelihood (%) from my PivotTable