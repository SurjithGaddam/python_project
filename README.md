# Overview

Welcome to my exploration of the data job market, with a focus on data analyst roles. This project stems from a desire to better understand and navigate the job market. It examines top-paying and high-demand skills to identify optimal opportunities for data analysts.

The analysis is based on data from Luke Barousse's Python Course, offering a comprehensive foundation with details on job titles, salaries, locations, and key skills. Using Python scripts, I investigate critical questions, including the most sought-after skills, salary trends, and the balance between demand and compensation in data analytics.

# The Questions
Below are the questions I want to answer in my project:

What are the skills most in demand for the top 3 most popular data roles?
How are in-demand skills trending for Data Analysts?
How well do jobs and skills pay for Data Analysts?
What are the optimal skills for data analysts to learn? (High Demand AND High Paying)
Tools I Used
For my deep dive into the data analyst job market, I harnessed the power of several key tools:

##### Python: 
The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
##### Pandas Library:
 This was used to analyze the data.
##### Matplotlib Library:
 I visualized the data.
##### Seaborn Library: 
Helped me create more advanced visuals.
##### Jupyter Notebooks: 
The tool I used to run my Python scripts which let me easily include my notes and analysis.
##### Visual Studio Code:
 My go-to for executing my Python scripts.
##### Git & GitHub: 
Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.
# Data Preparation and Cleanup
This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

# Import & Clean Up Data
I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.

# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
Filter US Jobs
To focus my analysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.

df_US = df[df['job_country'] == 'United States']
# The Analysis
## 1. What are the most demanded skills for the the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing whihch skills I should pay attention to depending on the role I'm targeting. 

View my noteboook with detailed steps here: [2_skill_Demandt.ipynb](https://github.com/SurjithGaddam/python_project/blob/main/3_project/2_skill_Demandt.ipynb)


### Visualize Data 
'''
fig, ax = plt.subplots(len(job_titles),1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short']== job_title].head(5)
    sns.barplot(data= df_plot, x='skill_percent',y='job_skills', ax=ax[i], hue='skill_count', palette='dark:salmon_r')
   '''
   ### Results

   ![Visualization of Top Skills](https://github.com/SurjithGaddam/python_project/blob/main/3_project/images/skills_demand.png)
   
   *Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*

   ###  Insights 
   The chart provides insights into the likelihood of specific skills being requested for three key data roles in U.S. job postings: Data Analyst, Data Engineer, and Data Scientist. Here are some key takeaways:
   Data Analyst:
Top Skills:
SQL (51%) is the most in-demand skill for Data Analysts, highlighting its importance in querying and managing databases.
Excel (41%) is highly relevant for tasks like data cleaning, reporting, and analysis.
2. Data Engineer:
Top Skills:
SQL (68%) and Python (65%) dominate, showcasing their central role in data extraction, transformation, and pipeline development.
Cloud and Big Data Tools:
AWS (43%) is frequently mentioned, emphasizing the importance of cloud computing.
3. Data Scientist:
Top Skills:
Python (72%) is overwhelmingly the most requested skill, reflecting its dominance in machine learning and data analysis.
SQL (51%) and R (44%) are also important for data manipulation and statistical analysis.
Visualization and Statistical Tools:
SAS and Tableau (both 24%) are less commonly requested, suggesting their more niche applications.

General Observations:
SQL and Python are critical across all three roles, with higher demand for SQL in engineering and analytical roles and Python dominating in data science.
Cloud and big data tools (e.g., AWS, Azure, Spark) are more relevant to Data Engineers.
Visualization tools like Tableau are more prominent for Data Analysts, while Data Scientists emphasize programming and statistical skills.

## 2. How are in-demand skills trending for Data Analysts?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [3_skills_trend.ipynb](https://github.com/SurjithGaddam/python_project/blob/main/3_project/3_skills_trend.ipynb)

### Visualize Data 

''' python
 df_plot =df_DA_US_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelyhood in Job Postings')
plt.xlabel('2023')
plt.legend().remove()
'''

![Trending Top Skills for Data Analyst in the US](https://github.com/SurjithGaddam/python_project/blob/main/3_project/images/skills_trend.png)

*Line Chart visualizing the trending top skills for data analysts in the US in 2023.*

### Insights:
Here are insights from the line chart showing the trends of top skills for Data Analysts in the US:
Key Observations:
SQL:
Most Dominant Skill: Consistently the most sought-after skill across all months, peaking early in the year (~60%) and gradually declining toward December (~50%).
Indicates its foundational role in data querying and management for Data Analysts.
Excel:
Stable Demand: Excel maintains a steady demand (~40%), with a slight dip mid-year but a sharp increase toward December (~45%).
Suggests its continued relevance for reporting and data analysis tasks.
Python:
Moderate Demand: Python fluctuates around ~30% throughout the year, with no significant peaks or drops.
Highlights its growing importance for automation and data manipulation.
Tableau:
Steady but Less Emphasized: Demand for Tableau remains relatively stable (~25–30%) with minor fluctuations.
Indicates its use for visualization but not as critical as SQL or Excel.
Power BI:
Lowest Demand: Power BI starts at ~20% and remains fairly consistent throughout the year.
Reflects its niche use compared to other tools but growing adoption in certain sectors.
General Trends:
SQL and Excel: Lead the way in demand, with SQL slightly declining and Excel recovering toward the year's end.
Python and Tableau: Have moderate and consistent demand, highlighting their secondary but essential roles.
Power BI: Shows consistent, though lower, relevance compared to Tableau.

# 3. How well do jobs and skills pay for Data Analysis?
To identify the highest-paying roles and skills, I only got jobs in the United States and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most.

View my notebook with detailed steps here:
[4_salary_analysis](3_project\4_salary_analysis.ipynb)

''' python 
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order, color='brown')
sns.set_theme(style='ticks')

plt.title('Salary Distributions in the United States')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000)
ticks_X = plt.FuncFormatter(lambda y, pos: f'${int(y/100)}k')
plt.gca().xaxis.set_major_formatter(ticks_X)
plt.show()
''''
## Results 

![Salary Distributions of Data Jobs in the US](https://github.com/SurjithGaddam/python_project/blob/main/3_project/images/Salary_analysis.png)

*Box plot visualizing the salary distributions fo the top 6 data job titles.*

# Insights 
Salary Insights for Data-Related Roles (Boxplot):
Higher Salaries:
Senior Data Scientists and Senior Data Engineers have the highest medians, with outliers earning $600K+.
Mid-Level Roles:
Data Scientists and Data Engineers show similar ranges, with more variability in Data Engineer earnings.
Entry-Level Roles:
Senior Data Analysts earn more than Data Analysts, but both have the lowest medians.
Trends:
Salaries cluster around the median, but outliers significantly raise the top end for all roles.
Key Takeaway: Senior roles lead in pay, while entry-level roles are more consistent with fewer extreme earners.

### Hightest Paid & Most DEmanded Skills for Data Analysis

'''python
from matplotlib.ticker import FuncFormatter
fig, ax = plt.subplots(2, 1)
sns.set_theme(style="ticks")

# Top 10 highest paid skills for Data Analysts
sns.barplot(data=df_DA_top_pay, x="median", y=df_DA_top_pay.index, hue="median", ax=ax[0], palette="dark:brown_r")
ax[0].legend().remove()
ax[0].set_title("Top 10 Highest Paid Skills for Data Analysts")
ax[0].set_xlabel("")
ax[0].xaxis.set_major_formatter(FuncFormatter(lambda x, _: f'{int(x/1000)}K'))
'''

## Result 
![The Hightest Paid & Most In-Demand Skills for Data Analysts in the US](https://github.com/SurjithGaddam/python_project/blob/main/3_project/images/Highestpaid_%26_most_demand_skills.png)

*Graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US.*

## insights 

Top 10 Highest Paid Skills

High-paying skills: dplyr, bitbucket, gitlab, solidity ($175K–$200K USD).
Niche tools like Hugging Face, Cassandra, and VMware offer premium pay for specialized expertise.
Cutting-edge technologies (e.g., solidity, linked to blockchain) drive top compensation.
Top 10 In-Demand Skills

Most sought-after: Python, Tableau, and SQL Server for analytics and visualization.
Tools like Excel and PowerPoint are essential despite lower pay.
R, SQL, and SAS remain key for statistical and database work.
Key Takeaway: Specialized skills offer higher pay, while foundational tools ensure wide demand across industries.

### 4. What is the most optimal skill to learn for Data Analysts?
To identify the most optimal skills to learn ( the ones that are the highest paid and highest in demand) I calculated the percent of skill demand and the median salary of these skills. To easily identify which are the most optimal skills to learn.

View my notebook with detailed steps here: [5_optimal_skills.ipynb](3_project\5_optimal_skills.ipynb)

''' python
rom adjustText import adjust_text
sns.scatterplot(
    data=df_plot,
    x='skills_percent',
    y='median_salary',
    hue='technology'
)
sns.despine()
sns.set_theme(style='ticks')

texts =[]         
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skills_percent'].iloc[i],df_DA_skills_high_demand['median_salary'].iloc[i],txt))
![Most Optimal Skills for Data Analysts in the US](https://github.com/SurjithGaddam/python_project/blob/main/3_project/images/optimal_skills.png)

*A scatter plot visualizing the most optimal skills (high paying and high demand) for data analysts in the US.*
### Insights
High Salary, Low Demand: Specialized skills like Oracle and Go ($90K–$98K) are less in demand (<20%).
Balanced Salary and Demand: Python, SQL Server, Tableau, and Power BI provide good pay (~$92K–$96K) with moderate demand (20%–30%).
High Demand, Lower Salary: Foundational skills like SQL, Excel, and PowerPoint are in high demand (up to 60%) but offer lower salaries (~$82K–$90K).
Low Salary, Low Demand: Word has minimal relevance (~$82K, <10%).
Key Insight: SQL and Python balance strong demand and competitive pay, while niche skills offer higher salaries in specialized roles.

# What I Learned
Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualization. Here are a few specific things I learned:

##### Advanced Python Usage:
 Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
##### Data Cleaning Importance: 
I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.
##### Strategic Skill Analysis: 
The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.
# Insights
This project provided several general insights into the data job market for analysts:

##### Skill Demand and Salary Correlation: 
There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialized skills like Python and Oracle often lead to higher salaries.
##### Market Trends:
 There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
##### Economic Value of Skills:
 Understanding which skills are both in-demand and well-compensated can guide data analysts in prioritizing learning to maximize their economic returns.
# Challenges I Faced
This project was not without its challenges, but it provided good learning opportunities:

##### Data Inconsistencies: 
Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.
##### Complex Data Visualization:
 Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.
#####Balancing Breadth and Depth: 
Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.
# Conclusion
This deep dive into the data analyst job market has been highly insightful, shedding light on the key skills and trends driving this dynamic field. The findings enhance understanding and offer practical guidance for those aiming to grow their careers in data analytics. As the industry evolves, ongoing analysis will be crucial to staying ahead. This project serves as a strong foundation for future studies and emphasizes the importance of continuous learning and adaptability in the data domain.
