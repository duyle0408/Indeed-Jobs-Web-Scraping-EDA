![image](https://github.com/user-attachments/assets/c7f950a0-7608-46cd-bfaf-6faa585c56ba)

# Indeed Job Scraping, EDA & NLP Analysis

## Executive Summary

### 1. Situation
As a recent graduate from the Master's of Science in Business Analytics program, I am currently on the job hunt for an entry-level position as a Data Analyst.

### 2. Task
By taking on an end-to-end project, I aim to collect data from the Indeed web page, perform exploratory data analysis and text analytics to uncover the keywords provided in the job description, in order to see which jobs are the right fit for me.

### 3. Action

#### 3.1: Data Collection
We start by initiating the GET method to make the call to the Indeed server and fetch the landing page for search result: "Entry Level Data Analyst".
Then, use Selenium as a web driver to open the link itself, and BeautifulSoup's "HTML parser" to read all the HTML contents of the landing page.
![image](https://github.com/user-attachments/assets/32d898c7-50d5-4dcc-a202-7dfc3f005928)

After some manual examination, there are 15 job postings a.k.a job cards, per page. And there are about 65 pages in total, meaning there are about 975 listings that we are able to scrape.
Here's a general picture of what one job card looks like:
![image](https://github.com/user-attachments/assets/18759ba6-c9b6-4522-9211-d6c1631a729f)

A job post is typically divided into two columns. The summary (on the left side) and the full details (summary included, on the right side). Now, it would be so much easier if we had just scraped all the summary, but we would be missing out on a detailed job descriptions . And since we wanted to get as much data as possible for NLP purposes, I chose the longer route. This means for every job card on a page, I would have to scrape all the details available, including any part that starts after "Job Description". There are two steps involved to do this. Since each "details" section is an external link that leads to another page, we first have to collect all those external links for all 65 pages, then parse through them again to get all the details we want

Now, in order to do that, we need to find the 'href' tags located inside every job cards, and add the prefix "https://www.indeed.com/" to complete the full link.
![image](https://github.com/user-attachments/assets/b04471fc-0d15-4fc5-91a4-d67186c04c39)

We successfully retrieved all the links for the first page, and stored it in a list. Fortunately, whenever we go to the next page, the "start" number within the URL increases by 10, and repeats for every next pages until the end. This makes automating the data collecting process easier when we can write a For-loop to get all the pages.
![image](https://github.com/user-attachments/assets/63578c83-b60d-47ef-af41-6ede56ee5a23)
![image](https://github.com/user-attachments/assets/8e1aab2e-4aed-4fc3-b7ff-2e89cfc1103a)

After that, we'll gather the details of each page by parsing with BeautifulSoup, including company name, rating, location, salary, job title, job description, etc.
![image](https://github.com/user-attachments/assets/67a04a78-0128-4f19-b455-221232c5b09f)

If we try and scrape the job details on all 65 pages (15 jobs per page), the website will deny our request call. Thus, we will have to separate it into 2 scrape sessions, and producing two dataframes. Then, we will consolidate those dataframes at the end and save into one single CSV file.
![image](https://github.com/user-attachments/assets/599cd73b-5231-4f8d-a3fd-a9193da8165b)
![image](https://github.com/user-attachments/assets/738074e7-bd78-468d-a937-63c0bb549dd3)

![image](https://github.com/user-attachments/assets/8d6f2e58-f1e1-4497-9593-cc369acfd7b0)
And of course, since not every job postings will have the same details on every section, there will be nulls in the dataset.

And we have now completed the data extraction process from Indeed!
![image](https://github.com/user-attachments/assets/90e9bbf3-588b-446e-a3b3-c1052e5d93cc)

Let's begin inspecting the raw dataset and clean it as much as possible

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
- Word Cloud visualization.
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
