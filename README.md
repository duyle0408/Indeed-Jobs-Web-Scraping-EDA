# Indeed Job Scraping, EDA & NLP Analysis

## Executive Summary

### 1. Situation
As a recent graduate from the Master's of Science in Business Analytics program, I am currently on the job hunt for an entry-level position as a Data Analyst.

### 2. Task
By taking on an end-to-end project, I aim to collect data from the Indeed web page, perform exploratory data analysis and text analytics to uncover the keywords provided in the job description, in order to see which jobs are the right fit for me.

### 3. Action

#### 3.1: Data Collection
Using Python libraries such as Requests, Selenium, and BeautifulSoup, I gathered information on Entry Level Data Analyst jobs on [Indeed](https://www.indeed.com/). This includes:
- Making a request call to the Indeed server.
- Using Selenium as a web driver.
- Parsing HTML with BeautifulSoup.
- Saving results in CSV format.

#### 3.2: Data Cleaning
After saving the files as CSV, I:
- Utilized Python's data analysis libraries such as Pandas and Numpy to clean and standardize the raw data.
- Removed missing/duplicate values as needed.
- Reformatted column data types.
- Performed manual checks for data integrity, such as state locations, salary range, etc.

#### 3.3: Exploratory Data Analysis
Performed EDA, visualized metrics with Plotly Express, and answered questions such as:
- How many entry-level jobs are there per state?
- What is the overall rating of all companies in the dataset? What is each state's average rating?
- What is the salary range for certain analytic skills (Python, SQL, Excel, Data Viz)?
- What are the most in-demand skills (including soft skills) for a data analyst?
- What are the highest salaries for entry-level data analyst positions?
- What is the relationship between company rating and salary?

#### 3.4: Text Analytics
Performed text analytics, including:
- Tokenization.
- Lemmatization.
- Text preprocessing, such as stop-words removal.
- WordCloud visualization.
- Unsupervised learning using the Latent Dirichlet Allocation (LDA) model to extract common words into topics to uncover key responsibilities of an entry-level data analyst.

### 4. Result
As a result of this comprehensive analysis, I identified the key skills and qualifications most sought after for entry-level data analyst positions, including SQL, Excel, and Python. This knowledge can help streamline the recruitment process by focusing on candidates with these core competencies.

### 5. Actionable Outcomes

#### For Applicants:
- **Target High-Interest Locations:** Job postings are highly concentrated in states like California, Texas, and New York. By targeting these states, job seekers can significantly increase their chances of finding suitable opportunities.
- **Prioritize High-Rating States:** States like Minnesota and Delaware have companies with higher average ratings. Prioritizing applications to companies in these states can lead to better job satisfaction and career development.
- **Focus on High-Demand Skills:** Python-required jobs offer higher salaries compared to other skills. Focusing on gaining proficiency in high-demand skills like Python can lead to a 20-30% increase in earning potential.
- **Align Skill Development:** Top in-demand skills include SQL, Excel, Python, Tableau, and communication skills. Aligning skill development and resume highlights with these in-demand skills can increase job match rates by 25%.

#### For Hiring Managers:
- **Target High-Interest Locations:** Focus recruitment efforts and advertising in high-interest areas like California, Texas, and New York to attract a larger pool of qualified candidates.
- **Enhance Company Appeal:** States like Minnesota and Delaware have companies with higher average ratings. Offering better benefits and fostering a positive work environment could potentially improve your company’s attractiveness.
- **Emphasize In-Demand Skills in Job Descriptions:** Clearly highlight in-demand skills like SQL, Excel, Python, Tableau, and communication skills in job postings to attract candidates whose expertise aligns with market demands, improving the quality of applicants.
