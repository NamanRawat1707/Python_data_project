# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?
To find out the most demanded skills for the top 3 most popular data roles , i have filtered out the ones which were the most popular and got 5 skills for those 3 roles. This query highlights the most popular job titles and their top skills, which showcases the skills to be paid most attention to.

View my Notebook here: [2_SKILLS_DEMANDED.IPYNB](2_PROJECT\2_SKILLS_DEMAND.IPYNB)

#### Visualize the Data
``` python
fig, ax = plt.subplots(len(job_titles),1)
sns.set_theme(style='ticks')
for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax = ax[i], hue='skill_count', palette='magma')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0,78)

    for n, v in enumerate (df_plot['skill_percent']):
        ax[i].text(v +1  , n , f'{v:.0f}%',va='center')

    if i!= len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of skills requested in US Job Postings',fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()
```

### Results:
 ![Visualization of Top Skills](2_PROJECT\Images\skills_demanded_all-data_roles.png)

### Insights:
1. SQL and Python are the most universally sought-after skills across all three roles, with Python being especially critical for Data Scientists (72%) and Data Engineers (65%).

2. Cloud platforms like AWS and Azure are key for Data Engineers but are not listed for the other roles.

3. Excel is still highly relevant for Data Analysts but not for Data Scientists or Data Engineers.

4. While R has decent demand for Data Scientists, it is not required for the other two roles.

## 2. How are in-demand skills trending for Data Analysts?

#### Visualize Data
```python
df_plot = df_DA_IND_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()


plt.title('Top trending skills for Data Analysts')
plt.ylabel('Likelihood in Job posting')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2,df_plot.iloc[-1,i], df_plot.columns[i])
plt.show()
```
### Results:

 ![Trending Top Skills for Data Analyst in India](2_PROJECT\Images\dataanalyst_trending_over_time.png)
 *Graph showing the trending top skills for Data Analyst in India in 2023*

 ### Insights:
 1. SQL remains the most demanded skill, however it seems to move in a downward trend.
 2. Excel experiences a significant increase in demand starting around Septmeber.
 3. Both Python and Tableau have stable demand throughout the year.

 ## 3. How well do jobs and skills pay for Data Analysts?

 ### Salary Analysis 

 #### Visualize Data
 ```python
 sns.boxplot(data=df_IN_top6, x='salary_year_avg', y='job_title_short',order=job_order)
plt.title('Distribution of Data Analyst Yearly salary in India')
plt.xlabel('Yearly Salary')
plt.ylabel('No. of jobs')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda y , pos : f"${int(y/1000)}K"))
plt.xlim(0,700000)
plt.show()

```
### Results:
![Salary Analysis for the Data Analyst Roles in India](2_PROJECT\Images\salary_analysis.png)

### Insights:
- There is a significant variance in salaries across the job titles. Data Scientists, Machine learning Engineers and Data Engineers have the highest salary potential around 200K (USD), which signifies that high value is placed on advanced data skills.

- Senior Data Engineers and Software Engineers have a surmountable amount of outliers on the higher salary limit highlighting that excellent skills may land a high pay. In contrast, Analyst Roles show more consistency in their high and low salary with much fewer outliers.

- The median salary increases significantly with seniority and experience in their roles. Senior Roles (such as Senior Data Engineer and Data Sceintists) have higher salary medians and potential than their junior counterparts.

### Highest Paid and in-demand Skills for Data Analysts
#### Visualize Data
```python
# Top 10 highest paid skills fro data analyst
fig, ax = plt.subplots(2,1)
sns.set_theme(style='ticks')

sns.barplot(data=df_DA_Ind_top_pay, x='median', y=df_DA_Ind_top_pay.index, ax=ax[0], hue='median', palette='viridis')
ax[0].legend().remove()


# Top 10 Most In-Demand Skills for Data Analyst
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, ax=ax[1],hue='median',palette = 'mako')
plt.show()
```
### Results:
![In demand and Highest Paying skills for Data analysts in India](2_PROJECT\Images\Indemand.png)
*Two separate graphs are shown for visualizing the highest paid skills and the most in-demand skills*

### Insights:
- Thw top chart shows that technical skills such as `neo4j`, `Databricks` and `Scala`are connected with higher salaries with most reaching atleast 160K, suggesting that advanced technical proficiency in these skills may allow potential for higher salaries.

- The bottom chart shows the most in-demand skills, Skills such as `PowerBI`, `Spark`, `Excel` and `Tableau` are the most in demand. Though not reaching the same salary potential as the highest paying skills as mentioned above. This clearly shows that experience in these skills is still sought out for employability in data roles.

- There is a clear difference between the highest paying skills and the most in-demand skills, Data analysts that are aiming to gain the most out of the skills, They should learn a diverse set of high-paying and in-demand skills including both advanced and foundational skills in their skillset. 

## 4. What is the most Optimal skill to learn for Data Analysts?

### Visualize Data
```python
from adjustText import adjust_text
sns.scatterplot(
    data = df_plot,
    x = 'Skills_percent',
    y = 'median_salary',
    hue = 'technology'
)
plt.show()
```

### Results:
![Most_optimal_skills_to_learn](2_PROJECT\Images\optimal_skills.png)
*A scatter plot visualizing the most optimal skills (High paying & In-Demand) for data analyst in India to learn.*

### Insights:
- The scatter plot shows that the most optimal skills to learn are `Programming-tools`(colored "Blue") and `analyst-tools`, they have a higher salaries compared to other clusters.

- `Analyst-tools`(colored "Green") are abundant in job postings and offer mid-high salary ranges, highlighting that data analysis and visualization tools are in-demand in the market. Though not having the highest salaries, they have the higher percentage of job-postings.

- `Database-tools`(colored "Orange") such as SQL server and Oracle do not have high salary potential and neither have the job postings, MongoDB (A no-sql database) has a high salary ceiling but extremely low in percentage of job-postings.