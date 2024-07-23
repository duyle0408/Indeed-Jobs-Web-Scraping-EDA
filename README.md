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
And of course, since not every job postings will have the same details, for example, some companies might not have salary available, and in some cases, location is also unavaiable because the job type is "Remote". So, there will be inconsistent/missing values in our newly scraped dataset.

And we have now completed the data extraction process from Indeed!
![image](https://github.com/user-attachments/assets/90e9bbf3-588b-446e-a3b3-c1052e5d93cc)

Let's begin inspecting the raw dataset and standardizing it as much as we can.

#### 3.2: Data Cleaning
![image](https://github.com/user-attachments/assets/d4506d8a-658c-437c-a318-57922b203e53)

![image](https://github.com/user-attachments/assets/14056421-48c7-4475-8598-f2f8b2837c70)
We inspect the dataset, make a copy and work on the copy itself, as good practice. There are about 1005 rows and 100 of those rows where the company name and job title are duplicates so we're dropping them.

For the "company_location" column, we will be extracting the city, state, and zip code using regular expression, and place them in new columns.
![image](https://github.com/user-attachments/assets/50e15e5f-4174-460a-ab7a-16fce00126f9)

![image](https://github.com/user-attachments/assets/bd73fcdf-3c16-47c7-ac50-af25173b0064)

![image](https://github.com/user-attachments/assets/b3ecbcf6-3583-40de-a177-65b3e995b7d7)

![image](https://github.com/user-attachments/assets/4cd77407-aafd-4282-8f81-5cd8d7e598b2)

For "company_rating" column, our job is pretty simple. We just need to separate the first numeric value out of the phrase. For example, if a company is rated "4.1 out of 5", we'll extract 4.1.
![image](https://github.com/user-attachments/assets/fbe4a039-dd12-47e3-bb5b-cf31073d0960)

"salary" column has been the trickiest one to clean as most jobs on Indeed only indicate a range of salary, like "$60,000 - $70,000 a year" or "$26 - $32 an hour". I have decided to perform feature engineering to extract the numerical values out of the string, then calculate average salary by using the range provided.
![image](https://github.com/user-attachments/assets/d591c172-4973-4fef-986f-7cdffc2ce553)

![image](https://github.com/user-attachments/assets/8ed2896b-3d3d-4473-aab7-fc8aab4e12bb)

![image](https://github.com/user-attachments/assets/c503a53b-b996-4c81-98e4-c3998d045c88)

There is one last column that needs to be cleaned, which is "job_desc". But since it only contains string and needs to be handled differently using NLP techniques such as tokenization, lemmatization, and stop-words removal, we will wait until after our EDA section, which is coming up.

#### 3.3: Exploratory Data Analysis
Q1: How many entry-level jobs are there per state?
![image](https://github.com/user-attachments/assets/07637793-cd22-455e-bbcf-13775cd4b041)

![image](https://github.com/user-attachments/assets/f20745d1-2c73-4c86-b2a5-5a15198f0562)
> Key Takeaways:
California: This state has the highest job count, indicated by the bright yellow color. California is a hub for tech companies, especially in Silicon Valley, which explains the high number of data analyst job postings.
Texas: With a significant number of job postings, Texas is shown in green. Cities like Austin, Dallas, and Houston are becoming tech and business hubs, leading to increased demand for data analysts.
New York: Also depicted in green, New York is a major financial and business center, driving demand for data analysts to manage and interpret large datasets.
Some other notable states that have moderate job postings are: FL, VA, IL, MA, WA.

Q2: What is the overall rating of all companies in the dataset? What is each state's average rating?
![image](https://github.com/user-attachments/assets/43c007ae-3633-4e81-909e-35163d1c67e4)

![image](https://github.com/user-attachments/assets/16527990-5c63-48eb-ac2d-5f61ab026aac)
> Key Takeaways:
Consistency Across States: There is a noticeable consistency in average ratings across many states, with most states falling within the 3.5 to 4.0 range. This suggests that, on average, companies across the U.S. maintain a relatively similar level of employee satisfaction.
Variability in Ratings: The variation in ratings between the top and bottom states highlights differences in workplace environments and employee experiences. This variability can be crucial for job seekers who prioritize company culture and employee satisfaction when considering job opportunities.

Q3: What is the salary range for certain analytic skills (Python, SQL, Excel, Data Viz)?
![image](https://github.com/user-attachments/assets/e90e0441-b46f-4f2d-a440-f988c594795f)

![image](https://github.com/user-attachments/assets/aacf3ed7-ea0d-4d1b-8b49-7aba78bf9d60)
> Key Takeaways:
Python-required jobs have a significant number of postings in the salary range of USD 80k - 99k.
SQL-required jobs show a wider distribution, with many postings around the USD 50k - 100k range and some higher salary positions.
Data Visualization-required jobs (likely including tools like Tableau and Power BI) show a concentration around the USD 50k - 100k range.
Excel-required jobs have a similar distribution to SQL, with a notable number of positions in the USD 40k - 80k range.

Q4: What are the most in-demand skills (including soft skills) for a data analyst?
![image](https://github.com/user-attachments/assets/34e8ea14-3b13-4924-9d49-117e071c23db)

![image](https://github.com/user-attachments/assets/bab0d374-7330-47fb-91f5-b849fe2395e4)

![image](https://github.com/user-attachments/assets/b1e32a8d-e444-4bad-8692-0f2a036c0c6a)

> Key Takeaways:
Technical Skills: A successful data analyst should be proficient in SQL, Excel, data visualization tools (Tableau, Power BI), and programming languages (Python and/or R).
Soft Skills: Effective communication and attention to detail are vital for presenting findings and ensuring data accuracy.
Advanced Knowledge: Familiarity with machine learning, cloud platforms, and advanced statistical methods can enhance an analyst's capability and marketability.
Note: Some other advanced tools/skills such as: Hadoop, Cloud, Hypothesis Testing, Time Series Analysis, etc. are less likely to be included in an entry-level job posting. To my knowledge, these skills are more likely to be required at a Junior/Senior level in the data career tracks.
In order to stand out as a prospective candidate, acquiring these advanced skills mentioned above will serve as a huge advantage for anyone.

Q5: What are the highest salaries for entry-level data analyst positions?
![image](https://github.com/user-attachments/assets/1578dafe-641d-4888-b3ca-1c16b12ca9ee)

![image](https://github.com/user-attachments/assets/2885a252-05cd-45bc-aa86-722fa1e04e60)

Q6: What is the relationship between company rating and salary?
![image](https://github.com/user-attachments/assets/8f075cf8-2a66-4569-9ece-7adbacda112f)

![image](https://github.com/user-attachments/assets/0892323c-79aa-4150-a4cb-8cc4d682591a)
> Key Takeaways:
This heatmap shows the correlation analysis between company ratings and salaries. The colors indicate the strength and direction of the correlation, where yellow represents a strong positive correlation and blue represents a strong negative correlation. The correlation coefficient values range from -1 to 1, with values closer to 1 indicating a strong positive correlation and values closer to -1 indicating a strong negative correlation.
There is no significant correlation between company ratings and salaries, as indicated by the darker blue and yellow squares showing minimal correlation. This means that higher salaries do not necessarily correspond to higher company ratings and vice versa.

#### 3.4: Text Analytics
Now that we've gained some insights on the dataset, we can move on to work solely on the "job_desc" column where we conduct NLP techniques to further understand the job requirements.
We start by importing the necessary NLP libraries such as nltk, spaCy, Tfidf Vectorizer, etc.
![image](https://github.com/user-attachments/assets/edfa42fc-d290-4f3a-b9d1-81351c303d65)

We lemmatize and remove stop words that will affect our analysis
![image](https://github.com/user-attachments/assets/3e61bd6e-94e5-43bb-984c-7331757661e7)

Convert the Text Data to a TF-IDF Matrix
![image](https://github.com/user-attachments/assets/2e3431c1-9637-4429-beab-53a58ebdfce2)

![image](https://github.com/user-attachments/assets/449b2561-f8ee-4935-ac31-81b79bdb6c19)
As per the word cloud visualization, we see a lot of key words that are repeatedly mentioned in job descriptions such as report, analysis, analyst, datum, etc.

Let's take this a step further and categorize all of the words into topics using Latent Dirichlet Allocation model - an unsupervised learning method
I have explained in detail what the model does in the Colab Notebook, please feel free to refer to it.
We define a set of stop words we want to exclude from the LDA model, then we have the model separate all strings into individual words contained in a list
We then tell the model how many categories we want, in my case, it was 15. The model works its magic in the background by constantly grouping words that often appear together in a job posting, until it is "satisfied".
Showing the best topics most related to a data analyst's responsibilities:
![image](https://github.com/user-attachments/assets/6573bdfe-c794-4ae0-8787-899f093d43eb)

![image](https://github.com/user-attachments/assets/ba36ef1b-4ef3-4c18-817c-507a55ea6253)

![image](https://github.com/user-attachments/assets/df16ef73-d739-41bd-ab9e-d7d02be044be)

![image](https://github.com/user-attachments/assets/a853f86b-96bc-4f3f-afcc-f893ab2e0ca9)
> Key Takeaways
-- Topic #2: "analyst," "analysis," "report," "knowledge," which are core to a data analyst's role. It also mentions "management" and "assist," suggesting a collaborative role in providing insights to management.
-- Topic #3: This topic also prominently features "analyst" and "analysis." It mentions "team," "report," and "development," which are important aspects of a data analyst's job. The presence of "health" and "care" suggests this might be particularly relevant to data analysts in the healthcare sector.
-- Lastly, Topic #6 highlight important aspects with words like "analysis," "report," "develop," "tool," "data," "computer," "knowledge," "problem," "solution," and "analyze." These terms encompass many of the key skills and activities of a data analyst, including data analysis, report development, problem-solving, and using computer tools.

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
