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



# Ubuntu no longer distributes chromium-browser outside of snap
#
# Proposed solution: https://askubuntu.com/questions/1204571/how-to-install-chromium-without-snap

# Add debian buster
cat > /etc/apt/sources.list.d/debian.list <<'EOF'
deb [arch=amd64 signed-by=/usr/share/keyrings/debian-buster.gpg] http://deb.debian.org/debian buster main
deb [arch=amd64 signed-by=/usr/share/keyrings/debian-buster-updates.gpg] http://deb.debian.org/debian buster-updates main
deb [arch=amd64 signed-by=/usr/share/keyrings/debian-security-buster.gpg] http://deb.debian.org/debian-security buster/updates main
EOF

# Add keys
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys DCC9EFBF77E11517
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 648ACFD622F3D138
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 112695A0E562B32A

apt-key export 77E11517 | gpg --dearmour -o /usr/share/keyrings/debian-buster.gpg
apt-key export 22F3D138 | gpg --dearmour -o /usr/share/keyrings/debian-buster-updates.gpg
apt-key export E562B32A | gpg --dearmour -o /usr/share/keyrings/debian-security-buster.gpg

# Prefer debian repo for chromium* packages only
# Note the double-blank lines between entries
cat > /etc/apt/preferences.d/chromium.pref << 'EOF'
Package: *
Pin: release a=eoan
Pin-Priority: 500


Package: *
Pin: origin "deb.debian.org"
Pin-Priority: 300


Package: chromium*
Pin: origin "deb.debian.org"
Pin-Priority: 700
EOF
     
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
Executing: /tmp/apt-key-gpghome.QhOVIFNucC/gpg.1.sh --keyserver keyserver.ubuntu.com --recv-keys DCC9EFBF77E11517
gpg: key DCC9EFBF77E11517: "Debian Stable Release Key (10/buster) <debian-release@lists.debian.org>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
Executing: /tmp/apt-key-gpghome.yZE1L332lu/gpg.1.sh --keyserver keyserver.ubuntu.com --recv-keys 648ACFD622F3D138
gpg: key DC30D7C23CBBABEE: "Debian Archive Automatic Signing Key (10/buster) <ftpmaster@debian.org>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
Executing: /tmp/apt-key-gpghome.1ZJqXYHzNg/gpg.1.sh --keyserver keyserver.ubuntu.com --recv-keys 112695A0E562B32A
gpg: key 4DFAB270CAA96DFA: "Debian Security Archive Automatic Signing Key (10/buster) <ftpmaster@debian.org>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
gpg: cannot open '/dev/tty': No such device or address
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
gpg: [stdout]: write error: Broken pipe
gpg: filter_flush failed on close: Broken pipe
gpg: cannot open '/dev/tty': No such device or address
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
gpg: [stdout]: write error: Broken pipe
gpg: filter_flush failed on close: Broken pipe
gpg: cannot open '/dev/tty': No such device or address
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
gpg: [stdout]: write error: Broken pipe
gpg: filter_flush failed on close: Broken pipe

!apt-get update
!apt-get install chromium chromium-driver
!pip3 install selenium
!pip install user-agent
!pip install webdriver_manager

from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium import webdriver

from bs4 import BeautifulSoup
import requests

from user_agent import generate_user_agent
import random
from random import choice
from time import sleep
import gzip
import io
from webdriver_manager.chrome import ChromeDriverManager
     
0% [Working]
            
Hit:1 http://deb.debian.org/debian buster InRelease

0% [Connecting to archive.ubuntu.com] [Connecting to security.ubuntu.com (185.125.190.81)] [Connecti
                                                                                                    
Hit:2 http://deb.debian.org/debian buster-updates InRelease

0% [Connecting to archive.ubuntu.com] [Connecting to security.ubuntu.com (185.125.190.81)] [Connecti
                                                                                                    
Hit:3 http://deb.debian.org/debian-security buster/updates InRelease

0% [Connecting to archive.ubuntu.com] [Connecting to security.ubuntu.com (185.125.190.81)] [Connecti
0% [Connecting to archive.ubuntu.com] [Connecting to security.ubuntu.com (185.125.190.81)] [Connecte
                                                                                                    
Hit:4 https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64  InRelease
Hit:5 https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/ InRelease
Get:6 http://security.ubuntu.com/ubuntu jammy-security InRelease [129 kB]
Hit:7 http://archive.ubuntu.com/ubuntu jammy InRelease
Get:8 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [128 kB]
Ign:9 https://r2u.stat.illinois.edu/ubuntu jammy InRelease
Hit:10 https://r2u.stat.illinois.edu/ubuntu jammy Release
Hit:12 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu jammy InRelease
Hit:13 https://ppa.launchpadcontent.net/graphics-drivers/ppa/ubuntu jammy InRelease
Hit:14 https://ppa.launchpadcontent.net/ubuntugis/ppa/ubuntu jammy InRelease
Hit:15 http://archive.ubuntu.com/ubuntu jammy-backports InRelease
Fetched 257 kB in 2s (132 kB/s)
Reading package lists... Done
W: Skipping acquire of configured file 'main/source/Sources' as repository 'https://r2u.stat.illinois.edu/ubuntu jammy InRelease' does not seem to provide it (sources.list entry misspelt?)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
chromium is already the newest version (90.0.4430.212-1~deb10u1).
chromium-driver is already the newest version (90.0.4430.212-1~deb10u1).
0 upgraded, 0 newly installed, 0 to remove and 45 not upgraded.
Requirement already satisfied: selenium in /usr/local/lib/python3.10/dist-packages (4.22.0)
Requirement already satisfied: urllib3[socks]<3,>=1.26 in /usr/local/lib/python3.10/dist-packages (from selenium) (2.0.7)
Requirement already satisfied: trio~=0.17 in /usr/local/lib/python3.10/dist-packages (from selenium) (0.26.0)
Requirement already satisfied: trio-websocket~=0.9 in /usr/local/lib/python3.10/dist-packages (from selenium) (0.11.1)
Requirement already satisfied: certifi>=2021.10.8 in /usr/local/lib/python3.10/dist-packages (from selenium) (2024.7.4)
Requirement already satisfied: typing_extensions>=4.9.0 in /usr/local/lib/python3.10/dist-packages (from selenium) (4.12.2)
Requirement already satisfied: websocket-client>=1.8.0 in /usr/local/lib/python3.10/dist-packages (from selenium) (1.8.0)
Requirement already satisfied: attrs>=23.2.0 in /usr/local/lib/python3.10/dist-packages (from trio~=0.17->selenium) (23.2.0)
Requirement already satisfied: sortedcontainers in /usr/local/lib/python3.10/dist-packages (from trio~=0.17->selenium) (2.4.0)
Requirement already satisfied: idna in /usr/local/lib/python3.10/dist-packages (from trio~=0.17->selenium) (3.7)
Requirement already satisfied: outcome in /usr/local/lib/python3.10/dist-packages (from trio~=0.17->selenium) (1.3.0.post0)
Requirement already satisfied: sniffio>=1.3.0 in /usr/local/lib/python3.10/dist-packages (from trio~=0.17->selenium) (1.3.1)
Requirement already satisfied: exceptiongroup in /usr/local/lib/python3.10/dist-packages (from trio~=0.17->selenium) (1.2.1)
Requirement already satisfied: wsproto>=0.14 in /usr/local/lib/python3.10/dist-packages (from trio-websocket~=0.9->selenium) (1.2.0)
Requirement already satisfied: pysocks!=1.5.7,<2.0,>=1.5.6 in /usr/local/lib/python3.10/dist-packages (from urllib3[socks]<3,>=1.26->selenium) (1.7.1)
Requirement already satisfied: h11<1,>=0.9.0 in /usr/local/lib/python3.10/dist-packages (from wsproto>=0.14->trio-websocket~=0.9->selenium) (0.14.0)
Requirement already satisfied: user-agent in /usr/local/lib/python3.10/dist-packages (0.1.10)
Requirement already satisfied: six in /usr/local/lib/python3.10/dist-packages (from user-agent) (1.16.0)
Requirement already satisfied: webdriver_manager in /usr/local/lib/python3.10/dist-packages (4.0.1)
Requirement already satisfied: requests in /usr/local/lib/python3.10/dist-packages (from webdriver_manager) (2.31.0)
Requirement already satisfied: python-dotenv in /usr/local/lib/python3.10/dist-packages (from webdriver_manager) (1.0.1)
Requirement already satisfied: packaging in /usr/local/lib/python3.10/dist-packages (from webdriver_manager) (24.1)
Requirement already satisfied: charset-normalizer<4,>=2 in /usr/local/lib/python3.10/dist-packages (from requests->webdriver_manager) (3.3.2)
Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests->webdriver_manager) (3.7)
Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.10/dist-packages (from requests->webdriver_manager) (2.0.7)
Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.10/dist-packages (from requests->webdriver_manager) (2024.7.4)

# Initialize the Chrome driver
service = Service(executable_path=r'/usr/bin/chromedriver')

options = Options()
options.add_argument("--headless")
options.add_argument("--no-sandbox")
options.add_argument('--disable-blink-features=AutomationControlled')
options.add_argument("window-size=1280,800")
options.add_argument(f"user-agent={generate_user_agent()}")

# Additional recommended options
options.add_argument("--disable-dev-shm-usage")
options.add_argument("--disable-infobars")
options.add_argument("--disable-extensions")
options.add_argument("--disable-gpu")
options.add_argument("--disable-popup-blocking")
options.add_argument("--incognito")
options.add_argument("--lang=en-US")  # Set language to English
options.add_argument('--disable-software-rasterizer')
options.add_argument('--log-level=3')
options.add_argument('--ignore-certificate-errors')
options.add_argument('--disable-logging')
options.add_argument('--disable-dev-shm-usage')
options.add_argument('--disable-browser-side-navigation')

# Initialize the driver
driver = webdriver.Chrome(service=service, options=options)

# Remove navigator.webdriver Flag using JavaScript
driver.execute_script("Object.defineProperty(navigator, 'webdriver', {get: () => undefined})")
     

driver.get("https://www.indeed.com/jobs?q=entry+level+data+analyst&vjk=7238bdf881623de7")
soup = BeautifulSoup(driver.page_source, "html.parser")
     

job_cards = soup.find_all('div', {'class':'job_seen_beacon'}) # correct number of job postings
     

len(job_cards)
     
15

#test job_cards variable
job_cards[0].a['href']
     
'/rc/clk?jk=5b8d5e35e0cba3fd&bb=10qeCN4-Zu6qgVBrA2lbTID5xCYD0Jo1ru8I3PyURwIHNNEKAWDk-sfu8CZVpQ2Q4R7ndJpO5IH-CPrMFgdZw5-rMEqcQPFfYgeCMEhn2AIDz_b35B2sBi88ugu6brgQ&xkcb=SoAW67M3-cwnGSbF450LbzkdCdPP&fccid=bd976cc171c690e0&vjs=3'

# Function to retrieve job links from a given page
def get_job_links(soup):
    job_cards = soup.find_all('div', {'class': 'job_seen_beacon'})
    jobs_href = []
    for card in job_cards:
        job_url = 'https://www.indeed.com' + card.a['href']
        jobs_href.append(job_url)
    return jobs_href
     

import time
# Open the first page and get job links
driver.get("https://www.indeed.com/jobs?q=entry+level+data+analyst&vjk=7238bdf881623de7")
time.sleep(5)  # Ensure the page is fully loaded
soup = BeautifulSoup(driver.page_source, "html.parser")
first_page_jobs = get_job_links(soup)
     

# navigating to the next page
next_page_url = 'https://www.indeed.com/'+ soup.find('a', {'aria-label':'Next Page'})['href']
print(next_page_url)
     
https://www.indeed.com//jobs?q=entry+level+data+analyst&start=10
Get URLs for pages 2-44

'''# code to get list of URLs for 2-44

all_next_pages = [f'https://www.indeed.com/jobs?q=entry+level+data+analyst&start={i}' for i in range(10,451,10)] # get jobs for pages 2-44

# Iterate over the list of URLs and apply the job links function
for url in all_next_pages:
    driver.get(url)
    time.sleep(5)  # Ensure the page is fully loaded
    soup = BeautifulSoup(driver.page_source, "html.parser")
    all_jobs = first_page_jobs.extend(get_job_links(soup))'''
     
'# code to get list of URLs for 2-44\n\nall_next_pages = [f\'https://www.indeed.com/jobs?q=entry+level+data+analyst&start={i}\' for i in range(10,451,10)] # get jobs for pages 2-44\n\n# Iterate over the list of URLs and apply the job links function\nfor url in all_next_pages:\n    driver.get(url)\n    time.sleep(5)  # Ensure the page is fully loaded\n    soup = BeautifulSoup(driver.page_source, "html.parser")\n    all_jobs = first_page_jobs.extend(get_job_links(soup))'
Get URLs for the rest of pages (45-64)

pages_remain = [f'https://www.indeed.com/jobs?q=entry+level+data+analyst&start={i}' for i in range(460,651,10)]

# Iterate over the list of URLs and apply the job links function
for url in pages_remain:
    driver.get(url)
    time.sleep(5)  # Ensure the page is fully loaded
    soup = BeautifulSoup(driver.page_source, "html.parser")
    all_jobs = first_page_jobs.extend(get_job_links(soup))
     

all_jobs = first_page_jobs
     

len(first_page_jobs)
     
315

first_page_jobs[0]
     
'https://www.indeed.com/rc/clk?jk=5b8d5e35e0cba3fd&bb=C9qa2qc-3b6AIa_ciOijjGK4SHxgiAFyp4H0AOKdeei-quLo2y2VSC0cmYiSkZ6ZzRga8eDf-wndCA_3XbtGzjAkLowHiCKWisswAXle2Oszk13T-lK-i7OMAqIlLHGh&xkcb=SoCk67M3-cwllK1fKR0LbzkdCdPP&fccid=bd976cc171c690e0&vjs=3'
Prototyping first link

driver.get(first_page_jobs[0])
soup = BeautifulSoup(driver.page_source, "html.parser")
     

company_name = soup.find('div',{'class': 'css-hon9z8 eu4oa1w0'}).span.a.text
company_name
     
'Columbia University'

job_title = soup.find('h1', {'class':'jobsearch-JobInfoHeader-title'}).span.text
job_title
     
'Data Analyst'

rating = soup.find('div',{'class':'css-1unnuiz e37uo190'}).span.text
rating
     
'4.1 out of 5'

company_location = soup.find('div',{'class': 'css-waniwe eu4oa1w0'}).text
company_location
     
'New York, NY'

salary = soup.find('div', {'id': 'salaryInfoAndJobType'}).find('span', {'class':'css-19j1a75 eu4oa1w0'}).text
salary
     
'$60,000 - $64,000 a year'

job_type = soup.find('div', {'id': 'salaryInfoAndJobType'}).find('span',{'class' :'css-k5flys eu4oa1w0'}).text.replace('-', ' ').lstrip()
job_type
     
'Full time'

job_desc = soup.find('div', {'id':'jobDescriptionText'}).find_all('p')

#clean job desc
job_desc = ' '.join([p.text.strip() for p in job_desc])

     

apply_link = soup.find('span', {'class':'css-1saizt3 e1wnkr790'}).a['href']
apply_link
     
'https://www.indeed.com/cmp/Columbia-University?campaignid=mobvjcmp&from=mobviewjob&tk=1i2ssf1b9g07b800&fromjk=5b8d5e35e0cba3fd'
Scraping Job Details & Save As CSV

import pandas as pd

def get_job_info(first_page_jobs):
    job_data = []

    for job in first_page_jobs:
        driver.get(job)
        time.sleep(5)  # Ensure the page is fully loaded
        soup = BeautifulSoup(driver.page_source, "html.parser")

        job_info = {}

        try:
            job_info['company_name'] = soup.find('div', {'class': 'css-hon9z8 eu4oa1w0'}).span.a.text
        except Exception as e:
            print(f"Error scraping company_name for {job}: {e}")
            job_info['company_name'] = None

        # Use company_name for subsequent error messages
        company_name = job_info.get('company_name', 'Unknown Company')

        try:
            job_info['job_title'] = soup.find('h1', {'class': 'jobsearch-JobInfoHeader-title'}).span.text
        except Exception as e:
            print(f"Error scraping job_title for {company_name}: {e}")
            job_info['job_title'] = None

        try:
            job_info['company_location'] = soup.find('div',{'class': 'css-waniwe eu4oa1w0'}).text
        except Exception as e:
            print(f"Error scraping company_location for {company_name}: {e}")
            job_info['company_location'] = None

        try:
            job_info['company_rating'] = soup.find('div',{'class':'css-1unnuiz e37uo190'}).span.text
        except Exception as e:
            print(f"Error scraping company_rating for {company_name}: {e}")
            job_info['company_rating'] = None

        try:
            job_info['salary'] = soup.find('div', {'id': 'salaryInfoAndJobType'}).find('span', {'class': 'css-19j1a75 eu4oa1w0'}).text
        except Exception as e:
            print(f"Error scraping salary for {company_name}: {e}")
            job_info['salary'] = None

        try:
            job_info['job_type'] = soup.find('div', {'id': 'salaryInfoAndJobType'}).find('span', {'class': 'css-k5flys eu4oa1w0'}).text.replace('-', ' ').lstrip()
        except Exception as e:
            print(f"Error scraping job_type for {company_name}: {e}")
            job_info['job_type'] = None

        try:
            job_desc = soup.find('div', {'id': 'jobDescriptionText'}).find_all('p')
            job_info['job_desc'] = ' '.join([p.text.strip() for p in job_desc])
        except Exception as e:
            print(f"Error scraping job_desc for {company_name}: {e}")
            job_info['job_desc'] = None

        try:
            job_info['apply_link'] = soup.find('span', {'class':'css-1saizt3 e1wnkr790'}).a['href']
        except Exception as e:
            print(f"Error scraping apply_link for {company_name}: {e}")
            job_info['apply_link'] = None

        job_data.append(job_info)

    driver.quit()
    return pd.DataFrame(job_data)
     
If we try and scrape the job details on all 65 pages (15 jobs per page), the website will deny our request call.

Thus, we will have to separate it into 2 scrape sessions, and producing two dataframes.

Then, we will consolidate those dataframes at the end and save into one single CSV file for further analysis


'''job_df_partial = get_job_info(first_page_jobs)
job_df_partial.to_csv('indeed_jobs_partial_1.csv', index=False)'''
     
"job_df_partial = get_job_info(first_page_jobs)\njob_df_partial.to_csv('indeed_jobs_partial_1.csv', index=False)"

job_df_remaining = get_job_info(all_jobs) # get jobs for pages 45 to 65
job_df_remaining.to_csv('indeed_jobs_remaining_1.csv', index=False)
     
Error scraping salary for Saint Francis Health System: 'NoneType' object has no attribute 'text'
Error scraping salary for Cass Information Systems Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for Parkhill: 'NoneType' object has no attribute 'find'
Error scraping job_type for Parkhill: 'NoneType' object has no attribute 'find'
Error scraping company_location for Headway.co: 'NoneType' object has no attribute 'text'
Error scraping job_type for Headway.co: 'NoneType' object has no attribute 'text'
Error scraping company_location for GitHub, Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for Serco North America: 'NoneType' object has no attribute 'text'
Error scraping salary for General Motors: 'NoneType' object has no attribute 'text'
Error scraping company_location for Cambium Learning Group: 'NoneType' object has no attribute 'text'
Error scraping salary for Cambium Learning Group: 'NoneType' object has no attribute 'text'
Error scraping salary for Albertsons Companies: 'NoneType' object has no attribute 'text'
Error scraping salary for Deloitte: 'NoneType' object has no attribute 'text'
Error scraping salary for Shellpoint Mortgage Servicing: 'NoneType' object has no attribute 'text'
Error scraping salary for ManTech: 'NoneType' object has no attribute 'text'
Error scraping job_type for Fresno County: 'NoneType' object has no attribute 'text'
Error scraping salary for SAIC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Millennium Consulting, Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for Millennium Consulting, Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for National Computer Systems: 'NoneType' object has no attribute 'find'
Error scraping job_type for National Computer Systems: 'NoneType' object has no attribute 'find'
Error scraping salary for Truist Bank: 'NoneType' object has no attribute 'text'
Error scraping company_rating for TRESUME: 'NoneType' object has no attribute 'span'
Error scraping salary for Kratos Defense: 'NoneType' object has no attribute 'text'
Error scraping salary for Family Service Association - Fall River: 'NoneType' object has no attribute 'text'
Error scraping company_rating for TRESUME: 'NoneType' object has no attribute 'span'
Error scraping company_location for Otcmarketpro: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Otcmarketpro: 'NoneType' object has no attribute 'span'
Error scraping company_location for CloudServiceTek: 'NoneType' object has no attribute 'text'
Error scraping company_rating for CloudServiceTek: 'NoneType' object has no attribute 'span'
Error scraping company_rating for West Virginia: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Quantbot Technologies LP: 'NoneType' object has no attribute 'span'
Error scraping company_location for COGNIZE TECH SOLUTIONS: 'NoneType' object has no attribute 'text'
Error scraping company_rating for COGNIZE TECH SOLUTIONS: 'NoneType' object has no attribute 'span'
Error scraping company_location for Asvil Galaxy Finserv Private Limited: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Asvil Galaxy Finserv Private Limited: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Education Dynamics, Inc.: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Intellectual Concepts LLC: 'NoneType' object has no attribute 'span'
Error scraping salary for Intellectual Concepts LLC: 'NoneType' object has no attribute 'find'
Error scraping job_type for Intellectual Concepts LLC: 'NoneType' object has no attribute 'find'
Error scraping company_location for DigitalTransGlobal: 'NoneType' object has no attribute 'text'
Error scraping company_rating for DigitalTransGlobal: 'NoneType' object has no attribute 'span'
Error scraping job_type for Zenith Services: 'NoneType' object has no attribute 'text'
Error scraping company_location for Asset Capital Market: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Asset Capital Market: 'NoneType' object has no attribute 'span'
Error scraping company_location for CapitalPlanHoldings: 'NoneType' object has no attribute 'text'
Error scraping company_rating for CapitalPlanHoldings: 'NoneType' object has no attribute 'span'
Error scraping company_location for PCS Global Tech: 'NoneType' object has no attribute 'text'
Error scraping company_rating for PCS Global Tech: 'NoneType' object has no attribute 'span'
Error scraping company_location for GlobalSoftSolution: 'NoneType' object has no attribute 'text'
Error scraping company_rating for GlobalSoftSolution: 'NoneType' object has no attribute 'span'
Error scraping company_rating for CloudSoftSync: 'NoneType' object has no attribute 'span'
Error scraping job_type for KnowBe4: 'NoneType' object has no attribute 'text'
Error scraping company_location for First Notch Technology LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for First Notch Technology LLC: 'NoneType' object has no attribute 'span'
Error scraping company_location for MJMC, Inc.: 'NoneType' object has no attribute 'text'
Error scraping company_rating for MJMC, Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for MJMC, Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for 806 Technologies, Inc.: 'NoneType' object has no attribute 'find'
Error scraping job_type for 806 Technologies, Inc.: 'NoneType' object has no attribute 'find'
Error scraping company_location for OPSTRA TECH: 'NoneType' object has no attribute 'text'
Error scraping company_rating for OPSTRA TECH: 'NoneType' object has no attribute 'span'
Error scraping company_location for DonorSearch: 'NoneType' object has no attribute 'text'
Error scraping salary for DonorSearch: 'NoneType' object has no attribute 'text'
Error scraping company_location for CDC Foundation: 'NoneType' object has no attribute 'text'
Error scraping company_location for First Notch Technology LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for First Notch Technology LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Fluz: 'NoneType' object has no attribute 'span'
Error scraping company_location for OPSTRA TECH: 'NoneType' object has no attribute 'text'
Error scraping company_rating for OPSTRA TECH: 'NoneType' object has no attribute 'span'
Error scraping company_location for BACloudSystems: 'NoneType' object has no attribute 'text'
Error scraping company_rating for BACloudSystems: 'NoneType' object has no attribute 'span'
Error scraping company_rating for TRESUME: 'NoneType' object has no attribute 'span'
Error scraping company_location for CDC Foundation: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Atlantictranstrading: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Arta Finance: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Trinity Technology Solutions: 'NoneType' object has no attribute 'span'
Error scraping company_location for Vibronyx: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Vibronyx: 'NoneType' object has no attribute 'span'
Error scraping salary for Vibronyx: 'NoneType' object has no attribute 'find'
Error scraping job_type for Vibronyx: 'NoneType' object has no attribute 'find'
Error scraping company_rating for Unacast: 'NoneType' object has no attribute 'span'
Error scraping salary for Facilisgroup, LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for PO&G Resources: 'NoneType' object has no attribute 'span'
Error scraping salary for PO&G Resources: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Ztek Consulting Inc.: 'NoneType' object has no attribute 'span'
Error scraping company_location for UtiliSave LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for UtiliSave LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Dhatronictech: 'NoneType' object has no attribute 'span'
Error scraping salary for Duty First Consulting: 'NoneType' object has no attribute 'text'
Error scraping salary for Hartford Hospital: 'NoneType' object has no attribute 'text'
Error scraping salary for Republican National Committee: 'NoneType' object has no attribute 'text'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=74ff505a98234679&bb=xA6npsmT2BX2MQecnR2rMmCg2qTKsG3hS7xPH4nm0mx8NZiNQFPDn4uNfA7lfiIPd8GGBea-TlLEfxuR2BgrABhTkKSXO1urHj7ERvI68BUPWtxT-b2hMVVKs0NwYQCh&xkcb=SoBl67M3-cwhQtbF450GbzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_location for None: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping salary for None: 'NoneType' object has no attribute 'text'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping salary for AAA Mid States: 'NoneType' object has no attribute 'text'
Error scraping company_rating for 365 Labs: 'NoneType' object has no attribute 'span'
Error scraping salary for Treatment Centers Hold Co, LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for NYC Health + Hospitals: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Innovative Object Solutions Inc: 'NoneType' object has no attribute 'span'
Error scraping salary for Innovative Object Solutions Inc: 'NoneType' object has no attribute 'text'
Error scraping salary for LIMRA: 'NoneType' object has no attribute 'text'
Error scraping salary for Big Thought: 'NoneType' object has no attribute 'text'
Error scraping company_location for ITRGroup: 'NoneType' object has no attribute 'text'
Error scraping company_rating for ITRGroup: 'NoneType' object has no attribute 'span'
Error scraping salary for Transcore, LP: 'NoneType' object has no attribute 'text'
Error scraping company_location for HHAeXchange: 'NoneType' object has no attribute 'text'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=7250cc02d31b1599&bb=esEb-HnDJJXhxMrlwj6enVRgE6xovxI7o8__BQSnYrH0XoCuA86tAJbP2YZJQtszcd-WT0VjZBANGYPSdhO2EK8CLsynWGNlbcPTCCN-MaDj0AKevUKO9EeKCcipB46K&xkcb=SoCS67M3-cwgVS1r4J0BbzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping salary for None: 'NoneType' object has no attribute 'find'
Error scraping job_type for None: 'NoneType' object has no attribute 'find'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping company_rating for Techpoint LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Steneral Consulting: 'NoneType' object has no attribute 'span'
Error scraping salary for Steneral Consulting: 'NoneType' object has no attribute 'text'
Error scraping salary for RippleMatch Opportunities: 'NoneType' object has no attribute 'find'
Error scraping job_type for RippleMatch Opportunities: 'NoneType' object has no attribute 'find'
Error scraping company_rating for LL Global, Inc: 'NoneType' object has no attribute 'span'
Error scraping salary for LL Global, Inc: 'NoneType' object has no attribute 'text'
Error scraping salary for Lynker Corporation: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Long Finch Technology: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Institutional Cash Distributors LLC: 'NoneType' object has no attribute 'span'
Error scraping job_type for Willdan: 'NoneType' object has no attribute 'text'
Error scraping salary for Children’s Hospital of Philadelphia: 'NoneType' object has no attribute 'text'
Error scraping company_rating for BriteVox Inc.: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Broadway Infotech: 'NoneType' object has no attribute 'span'
Error scraping salary for Allied National, LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Kiva Design: 'NoneType' object has no attribute 'span'
Error scraping salary for Kiva Design: 'NoneType' object has no attribute 'find'
Error scraping job_type for Kiva Design: 'NoneType' object has no attribute 'find'
Error scraping company_location for COGNIZE TECH SOLUTIONS: 'NoneType' object has no attribute 'text'
Error scraping company_rating for COGNIZE TECH SOLUTIONS: 'NoneType' object has no attribute 'span'
Error scraping salary for West 4th Strategy: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Stormberg Foods, LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Pereira O'Dell: 'NoneType' object has no attribute 'span'
Error scraping job_type for Pereira O'Dell: 'NoneType' object has no attribute 'text'
Error scraping salary for PMHCC Inc.: 'NoneType' object has no attribute 'find'
Error scraping job_type for PMHCC Inc.: 'NoneType' object has no attribute 'find'
Error scraping company_location for CADX Investments: 'NoneType' object has no attribute 'text'
Error scraping company_rating for CADX Investments: 'NoneType' object has no attribute 'span'
Error scraping company_rating for The Best Postcards: 'NoneType' object has no attribute 'span'
Error scraping company_location for Valvoline Global Operations: 'NoneType' object has no attribute 'text'
Error scraping salary for Valvoline Global Operations: 'NoneType' object has no attribute 'find'
Error scraping job_type for Valvoline Global Operations: 'NoneType' object has no attribute 'find'
Error scraping salary for DHL: 'NoneType' object has no attribute 'text'
Error scraping salary for National Louis University: 'NoneType' object has no attribute 'text'
Error scraping company_location for Tillster, Inc.: 'NoneType' object has no attribute 'text'
Error scraping company_rating for A3 Freight Payment: 'NoneType' object has no attribute 'span'
Error scraping company_rating for IV.AI: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Haverhill Management, LLC: 'NoneType' object has no attribute 'span'
Error scraping salary for Haverhill Management, LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for NextGen Solutions Corp: 'NoneType' object has no attribute 'span'
Error scraping company_rating for CliniWorks: 'NoneType' object has no attribute 'span'
Error scraping salary for CliniWorks: 'NoneType' object has no attribute 'find'
Error scraping job_type for CliniWorks: 'NoneType' object has no attribute 'find'
Error scraping company_location for US Radiology Specialists: 'NoneType' object has no attribute 'text'
Error scraping salary for US Radiology Specialists: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Tech Army: 'NoneType' object has no attribute 'span'
Error scraping salary for AbsoluteCARE Medical and Pharmacy: 'NoneType' object has no attribute 'find'
Error scraping job_type for AbsoluteCARE Medical and Pharmacy: 'NoneType' object has no attribute 'find'
Error scraping company_location for IMPaCT Care: 'NoneType' object has no attribute 'text'
Error scraping company_location for ERG: 'NoneType' object has no attribute 'text'
Error scraping job_type for ERG: 'NoneType' object has no attribute 'text'
Error scraping company_rating for The Prospective Group (TPG): 'NoneType' object has no attribute 'span'
Error scraping salary for The Prospective Group (TPG): 'NoneType' object has no attribute 'find'
Error scraping job_type for The Prospective Group (TPG): 'NoneType' object has no attribute 'find'
Error scraping company_rating for Helix Tech IT solution: 'NoneType' object has no attribute 'span'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=d9917ef1ce8f22d5&bb=RWY4Hx-fpwR47aQiQkslL7D7Pwwvot2L7IZpOfC5MTm2RghyVrylOgagyE_gr83V-6lWjeCgXrwWWGm_LdIT6o8LQV94PQc3cZxpkt7VN7rkj9GWCI6xmnUTxUBMN_d_&xkcb=SoDe67M3-cw9MB1fKR0JbzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping job_type for None: 'NoneType' object has no attribute 'text'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping company_rating for Department of the Prosecuting Attorney - City & County of Honolulu: 'NoneType' object has no attribute 'span'
Error scraping salary for McNichols: 'NoneType' object has no attribute 'text'
Error scraping company_rating for County of Lexington: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Marathon TS: 'NoneType' object has no attribute 'span'
Error scraping salary for Agile Defense: 'NoneType' object has no attribute 'find'
Error scraping job_type for Agile Defense: 'NoneType' object has no attribute 'find'
Error scraping company_rating for Blue Star Partners LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Good Times USA, LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Windsor Solutions, Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for Windsor Solutions, Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for MileOne Autogroup: 'NoneType' object has no attribute 'text'
Error scraping company_rating for NS IT Solutions LLC: 'NoneType' object has no attribute 'span'
Error scraping salary for NS IT Solutions LLC: 'NoneType' object has no attribute 'find'
Error scraping job_type for NS IT Solutions LLC: 'NoneType' object has no attribute 'find'
Error scraping company_location for Valsatech Corp: 'NoneType' object has no attribute 'text'
Error scraping company_rating for InterMetro Industries, Corporation: 'NoneType' object has no attribute 'span'
Error scraping salary for InterMetro Industries, Corporation: 'NoneType' object has no attribute 'text'
Error scraping salary for Genesis Logistics Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for Skanska USA: 'NoneType' object has no attribute 'text'
Error scraping salary for Fidelity & Guaranty Life Insurance Company: 'NoneType' object has no attribute 'find'
Error scraping job_type for Fidelity & Guaranty Life Insurance Company: 'NoneType' object has no attribute 'find'
Error scraping company_rating for AZH Consulting Corp: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Slide Insurance LLC: 'NoneType' object has no attribute 'span'
Error scraping salary for Slide Insurance LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Good Times USA, LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for CliniWorks: 'NoneType' object has no attribute 'span'
Error scraping salary for CliniWorks: 'NoneType' object has no attribute 'find'
Error scraping job_type for CliniWorks: 'NoneType' object has no attribute 'find'
Error scraping company_rating for KJ Media: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Trenton Health Team: 'NoneType' object has no attribute 'span'
Error scraping company_location for MERP Systems, Inc.: 'NoneType' object has no attribute 'text'
Error scraping company_location for IntelliBridge LLC: 'NoneType' object has no attribute 'text'
Error scraping salary for IntelliBridge LLC: 'NoneType' object has no attribute 'text'
Error scraping company_location for Wipro: 'NoneType' object has no attribute 'text'
Error scraping salary for Apria Healthcare LLC: 'NoneType' object has no attribute 'text'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=e5a9cf303873d1e0&bb=Ie_BgeqhV253KmIehfjlUq0zCpyVX5JJ_Ru6s2WtFovnD_3W975pWoAxAoa-ypwCwCrAAPk9M481siR8i0D6BaBCFmFDJ7AAX8tFfvomaqi1N7ZFv6p0fyZIzneewysM&xkcb=SoDN67M3-cw7RdXMNB0AbzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping salary for None: 'NoneType' object has no attribute 'find'
Error scraping job_type for None: 'NoneType' object has no attribute 'find'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping job_type for Supernal: 'NoneType' object has no attribute 'text'
Error scraping company_location for AHU Technologies Inc: 'NoneType' object has no attribute 'text'
Error scraping company_rating for AHU Technologies Inc: 'NoneType' object has no attribute 'span'
Error scraping salary for Pratt Industries: 'NoneType' object has no attribute 'find'
Error scraping job_type for Pratt Industries: 'NoneType' object has no attribute 'find'
Error scraping company_rating for American Unit Inc: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Ensunet Technology Group: 'NoneType' object has no attribute 'span'
Error scraping salary for Ensunet Technology Group: 'NoneType' object has no attribute 'text'
Error scraping salary for Edupoint Educational Systems LLC: 'NoneType' object has no attribute 'find'
Error scraping job_type for Edupoint Educational Systems LLC: 'NoneType' object has no attribute 'find'
Error scraping salary for Skanska USA: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Synergy Global Technologies Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for Synergy Global Technologies Inc.: 'NoneType' object has no attribute 'text'
Error scraping company_rating for InterMetro Industries, Corporation: 'NoneType' object has no attribute 'span'
Error scraping salary for InterMetro Industries, Corporation: 'NoneType' object has no attribute 'text'
Error scraping salary for MileOne Autogroup: 'NoneType' object has no attribute 'text'
Error scraping company_rating for RSHARMA: 'NoneType' object has no attribute 'span'
Error scraping company_location for MasterBrand Cabinets LLC: 'NoneType' object has no attribute 'text'
Error scraping salary for MasterBrand Cabinets LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Inszone Insurance Services: 'NoneType' object has no attribute 'span'
Error scraping salary for Avant, LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for TRESUME: 'NoneType' object has no attribute 'span'
Error scraping job_type for Universal Service Administrative Company: 'NoneType' object has no attribute 'text'
Error scraping salary for Avant, LLC: 'NoneType' object has no attribute 'text'
Error scraping company_rating for V2A Consulting: 'NoneType' object has no attribute 'span'
Error scraping salary for V2A Consulting: 'NoneType' object has no attribute 'text'
Error scraping job_type for New York City Economic Development Corporation: 'NoneType' object has no attribute 'text'
Error scraping company_rating for GeoSearch: 'NoneType' object has no attribute 'span'
Error scraping salary for GeoSearch: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Ampersand Solutions Group: 'NoneType' object has no attribute 'span'
Error scraping salary for Ampersand Solutions Group: 'NoneType' object has no attribute 'text'
Error scraping company_rating for ST Global LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for MyCareClub: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Annexa Inc.: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Capio Group: 'NoneType' object has no attribute 'span'
Error scraping company_location for Rapid Finance: 'NoneType' object has no attribute 'text'
Error scraping salary for Rapid Finance: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Network Technologies International, Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for Tempus: 'NoneType' object has no attribute 'find'
Error scraping job_type for Tempus: 'NoneType' object has no attribute 'find'
Error scraping salary for BakerRipley: 'NoneType' object has no attribute 'text'
Error scraping salary for The Greentree Group: 'NoneType' object has no attribute 'text'
Error scraping salary for TexasBank: 'NoneType' object has no attribute 'text'
Error scraping salary for Orlans PC: 'NoneType' object has no attribute 'text'
Error scraping salary for Entertainment Retail Enterprises: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Steneral Consulting: 'NoneType' object has no attribute 'span'
Error scraping salary for Steneral Consulting: 'NoneType' object has no attribute 'text'
Error scraping salary for Newport Mental Health: 'NoneType' object has no attribute 'text'
Error scraping job_type for Universal Service Administrative Company: 'NoneType' object has no attribute 'text'
Error scraping salary for Millennium Physician Group: 'NoneType' object has no attribute 'text'
Error scraping company_rating for OrangePeople: 'NoneType' object has no attribute 'span'
Error scraping company_location for The Greentree Group: 'NoneType' object has no attribute 'text'
Error scraping salary for The Greentree Group: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Entegra LLP: 'NoneType' object has no attribute 'span'
Error scraping salary for Entegra LLP: 'NoneType' object has no attribute 'text'
Error scraping company_rating for HDI Global Insurance Company: 'NoneType' object has no attribute 'span'
Error scraping salary for HDI Global Insurance Company: 'NoneType' object has no attribute 'find'
Error scraping job_type for HDI Global Insurance Company: 'NoneType' object has no attribute 'find'
Error scraping company_rating for Blue Star Partners LLC: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Apogee Capital Partners: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Quantam Solutions: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Revenova, LLC: 'NoneType' object has no attribute 'span'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=705a1887dda77285&bb=sNQCtVnp1eXOin1lKWEVRhH_qt2N9olpRzEe-GvWaI7f-W514pdEgLFtgAuR6UepdGl2x2kVQd6B8XHOd0qtpyey8unzIhnhW-E9u9Cr8hahLrI9MxKG9pOLE2duyOOI&xkcb=SoBI67M3-cw4MebgAB0ObzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping salary for None: 'NoneType' object has no attribute 'text'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping salary for Marken: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Collins Consulting: 'NoneType' object has no attribute 'span'
Error scraping company_rating for TechPoint LLC: 'NoneType' object has no attribute 'span'
Error scraping salary for Sungage Financial: 'NoneType' object has no attribute 'text'
Error scraping company_location for Sedulo Group: 'NoneType' object has no attribute 'text'
Error scraping company_rating for McLaren Industries: 'NoneType' object has no attribute 'span'
Error scraping company_rating for BBCH: 'NoneType' object has no attribute 'span'
Error scraping salary for BBCH: 'NoneType' object has no attribute 'text'
Error scraping salary for Phoenix International Holdings Inc: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Link Technologies: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Tech Aveev LLC: 'NoneType' object has no attribute 'span'
Error scraping job_type for Great Plains Tribal Leaders Health Board Inc: 'NoneType' object has no attribute 'text'
Error scraping company_rating for GSK HR SOLUTION: 'NoneType' object has no attribute 'span'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=fc9fb3ae89e7a8ca&bb=fHHkDaulF3SwY9u3scdCyuaL1Xco0sIMwb0LwzMnbj1IoKU0_FyYGu0STIz6NzFABBUgmuMbOAQdkymdtKuFWtnVI71JpYsNdstgRxltAboteR6ZwKWyXKxmnEDGIeIu&xkcb=SoD767M3-cw3FQ721R0IbzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping salary for None: 'NoneType' object has no attribute 'find'
Error scraping job_type for None: 'NoneType' object has no attribute 'find'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping company_rating for V2A Consulting: 'NoneType' object has no attribute 'span'
Error scraping salary for V2A Consulting: 'NoneType' object has no attribute 'text'
Error scraping salary for KIOTI Tractor: 'NoneType' object has no attribute 'text'
Error scraping salary for Live! Casino and Hotel Maryland: 'NoneType' object has no attribute 'text'
Error scraping salary for TransPak, Inc.: 'NoneType' object has no attribute 'text'
Error scraping salary for Goodwill Industries of Arkansas: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Evans Data Corp: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Kagr Llc: 'NoneType' object has no attribute 'span'
Error scraping salary for Kagr Llc: 'NoneType' object has no attribute 'text'
Error scraping company_rating for DigitalHire: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Brooksee Inc: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Family Support Services of Suncoast: 'NoneType' object has no attribute 'span'
Error scraping salary for Family Support Services of Suncoast: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Sentient Digital, Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for Sentient Digital, Inc.: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Cilable: 'NoneType' object has no attribute 'span'
Error scraping company_rating for NYC Health + Hospitals: 'NoneType' object has no attribute 'span'
Error scraping salary for TexasBank: 'NoneType' object has no attribute 'text'
Error scraping company_rating for V2A Consulting: 'NoneType' object has no attribute 'span'
Error scraping salary for V2A Consulting: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Valley Talent Co.: 'NoneType' object has no attribute 'span'
Error scraping salary for Valley Talent Co.: 'NoneType' object has no attribute 'text'
Error scraping salary for KIOTI Tractor: 'NoneType' object has no attribute 'text'
Error scraping company_rating for InfoLogitech: 'NoneType' object has no attribute 'span'
Error scraping company_rating for IT Excel: 'NoneType' object has no attribute 'span'
Error scraping salary for IT Excel: 'NoneType' object has no attribute 'find'
Error scraping job_type for IT Excel: 'NoneType' object has no attribute 'find'
Error scraping salary for TexasBank: 'NoneType' object has no attribute 'text'
Error scraping salary for Live! Casino and Hotel Maryland: 'NoneType' object has no attribute 'text'
Error scraping company_rating for Amador County: 'NoneType' object has no attribute 'span'
Error scraping company_name for https://www.indeed.com/rc/clk?jk=4e2e672eaee833c4&bb=ayFpGcLjFIv-JbD3Zf9-bbIFIa0SPgNl-VtYpPZ_eK5CRhu2uN-fz3Oy1KYAAxxh0Beb7hhXdsBskAexkAjlHY96gaYtbo6BdkHnfQVWAZhxLPGpsJTlh-as6dhFjzH1&xkcb=SoBN67M3-cw0ilbVJZ0abzkdCdPP&fccid=dd616958bd9ddc12&vjs=3: 'NoneType' object has no attribute 'text'
Error scraping company_rating for None: 'NoneType' object has no attribute 'span'
Error scraping apply_link for None: 'NoneType' object has no attribute 'a'
Error scraping salary for Affinity Federal Credit Union: 'NoneType' object has no attribute 'find'
Error scraping job_type for Affinity Federal Credit Union: 'NoneType' object has no attribute 'find'
Error scraping salary for Analytic Partners: 'NoneType' object has no attribute 'find'
Error scraping job_type for Analytic Partners: 'NoneType' object has no attribute 'find'
Error scraping company_rating for NLB Technology Services: 'NoneType' object has no attribute 'span'
Error scraping company_rating for Sentient Digital, Inc.: 'NoneType' object has no attribute 'span'
Error scraping salary for Sentient Digital, Inc.: 'NoneType' object has no attribute 'text'
Error scraping company_rating for HIGH BRIDGE CONSULTING LLC: 'NoneType' object has no attribute 'span'
Error scraping company_location for ERG: 'NoneType' object has no attribute 'text'
Error scraping salary for TransPak, Inc.: 'NoneType' object has no attribute 'text'
Joining 2 DataFrames

import pandas as pd

partial_df = pd.read_csv(r'//content/drive/MyDrive/Colab Notebooks/Personal Projects/Datasets/indeed_jobs_partial.csv')

remaining_df = pd.read_csv(r'/content/drive/MyDrive/Colab Notebooks/Personal Projects/Datasets/indeed_jobs_remaining.csv')
     

df = pd.concat([partial_df, remaining_df])
     

df.to_csv('indeed_jobs_entry_DA.csv', index=False)
     

import pandas as pd
df = pd.read_csv(r'/content/drive/MyDrive/Colab Notebooks/Personal Projects/Datasets/indeed_jobs_entry_DA.csv')
     

df.info()
     
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1005 entries, 0 to 1004
Data columns (total 8 columns):
 #   Column            Non-Null Count  Dtype 
---  ------            --------------  ----- 
 0   company_name      981 non-null    object
 1   job_title         1005 non-null   object
 2   company_location  944 non-null    object
 3   company_rating    744 non-null    object
 4   salary            545 non-null    object
 5   job_type          778 non-null    object
 6   job_desc          785 non-null    object
 7   apply_link        981 non-null    object
dtypes: object(8)
memory usage: 62.9+ KB

df1 = df.copy()
     
Cleaning & Standardizing "Company_Location"

dupes = df1[df1.duplicated(subset =['company_name','job_title'])].sort_values('company_name')
     
There are about 100+ rows where the company name and job title are the same


df1 = df1.drop_duplicates(subset =['company_name','job_title'], keep= 'first')
     

# List of alphabets to filter by
alphabets = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']

df1[df1['company_location'].str.startswith(tuple(alphabets), na=False)]
     
company_name	job_title	company_location	company_rating	salary	job_type	job_desc	apply_link
0	Columbia University	Data Analyst	New York, NY	4.1 out of 5	
64,000 a year	Full time	Position Summary A Data Analyst position is a...	https://www.indeed.com/cmp/Columbia-University...
3	The University of Iowa	Graduate Student Data Analyst	Iowa City, IA	4.1 out of 5	$22 an hour	Part time	The graduate student data analyst will be an i...	https://www.indeed.com/cmp/The-University-of-I...
4	Cass Information Systems Inc.	Data Analyst Associate (Remote)	Columbus, OH 43231	3.2 out of 5	NaN	Full time	Performs duties associated with our address c...	https://www.indeed.com/cmp/Cass-Information-Sy...
9	Stanford University	Data Analyst (50% Part-Time)	Stanford, CA	4.2 out of 5	
79,000 a year	Part time	Stanford University School of Medicine is worl...	https://www.indeed.com/cmp/Stanford-University...
10	Serco North America	Entry-Level Database Analyst	Norfolk, VA 23511	3.4 out of 5	NaN	Full time	If you love high profile and challenging proje...	https://www.indeed.com/cmp/Serco-29660aa5?camp...
...	...	...	...	...	...	...	...	...
994	GeekSI	Business Analyst	Tallahassee, FL	5.0 out of 5	
90,000 a year	Full time	GeekSI is seeking candidates matching our corp...	https://www.indeed.com/cmp/Geeksi-1?campaignid...
995	KS Management Services, LLC	Clinical Operation Analyst	Houston, TX	3.6 out of 5	
103,035 a year	Full time	Responsibilities The Clinical Operation Analys...	https://www.indeed.com/cmp/Kelsey--seybold-Cli...
996	Kros-Wise	Business Data Analyst	Norco, CA 92860	3.9 out of 5	
25 an hour	Full time	NaN	https://www.indeed.com/cmp/Kros--wise?campaign...
998	Analytic Partners	Marketing Science Analyst (August 5, 2024 Star...	Miami, FL	3.7 out of 5	NaN	NaN	NaN	https://www.indeed.com/cmp/Analytic-Partners?c...
1001	HIGH BRIDGE CONSULTING LLC	BI Analyst - Birst	Parsippany, NJ 07054	NaN	
40 an hour	Full time	Flexible work from home options available.	https://www.indeed.com/cmp/High-Bridge-Consult...
538 rows × 8 columns


df1[df1['company_location'].str.match(r'^\d', na=False)]
     
company_name	job_title	company_location	company_rating	salary	job_type	job_desc	apply_link
1	Saint Francis Health System	Financial Data Analyst (Entry Level)- Tulsa, O...	6600 South Yale Avenue, Tulsa, OK 74136	3.7 out of 5	NaN	Full time	NaN	https://www.indeed.com/cmp/Saint-Francis-Healt...
2	City of Baltimore, MD	Data Analyst - Baltimore City Information Tech...	3800 East Biddle Street, Baltimore, MD 21213	3.7 out of 5	
119,684 a year	Full time	NaN	https://www.indeed.com/cmp/City-of-Baltimore?c...
5	University of California San Francisco	DATA ANALYST	500 Parnassus Ave, San Francisco, CA 94143	4.1 out of 5	
94,200 a year	Full time	The final salary and offer components are sub...	https://www.indeed.com/cmp/University-of-Calif...
7	Chicago Public Schools	Data Analyst	42 W Madison St, Chicago, IL 60602	3.8 out of 5	$58,000 a year	Full time	Chicago Public Schools (CPS) is one of the lar...	https://www.indeed.com/cmp/Chicago-Public-Scho...
16	Insurance Fund, State	Data Analyst 1 (ITS)	15 Computer Drive West, Albany, NY 12205	NaN	
82,656 a year	Full time	NYSIF has a telecommuting program. The New Yo...	https://www.indeed.com/cmp/Statejobsny?campaig...
...	...	...	...	...	...	...	...	...
982	Vohra Wound Physicians	Business Analyst	3601 SW 160th Ave, Hollywood, FL 33027	3.5 out of 5	From $90,000 a year	Permanent, Full time	Healthcare Experience Required SUMMARY: The Bu...	https://www.indeed.com/cmp/Vohra-Wound-Physici...
990	Syracuse City School District	Management Analyst	725 Harrison Street, Syracuse, NY 13210	3.4 out of 5	
92,700 a year	Full time	ABOUT OUR DISTRICT: The Syracuse City School D...	https://www.indeed.com/cmp/Syracuse-City-Schoo...
997	Affinity Federal Credit Union	Data Analyst	73 Mountainview Blvd, Basking Ridge, NJ 07920	3.4 out of 5	NaN	NaN	In order to continually provide our members wi...	https://www.indeed.com/cmp/Affinity-Federal-Cr...
999	NLB Technology Services	SAP Data Analyst	26129 101st Road, Arkansas City, KS 67005	NaN	
90,000.00 a year	Full time	SAP Data Analyst Location:- Arkansas City, KS,...	https://www.indeed.com/cmp/Nlb-Technology-Serv...
1002	ECU Health	Business Intelligence Analyst III	2100 Stantonsburg Road, Greenville, NC 27835	3.7 out of 5	
131,456 a year	Full time	ECU Health About ECU Health Medical Center ECU...	https://www.indeed.com/cmp/Ecu-Health?campaign...
307 rows × 8 columns


# Initialize the new column
df1['company_city'] = ''

# Loop through each location and apply the logic
for idx, loc in enumerate(df1['company_location']):
    if pd.notna(loc):
        if loc.startswith(tuple('0123456789')):  # Check if it starts with a digit
            city = loc.split(',')[1] if len(loc.split(',')) > 1 else loc
        elif loc.startswith(tuple(alphabets)):  # Check if it starts with a letter
            city = loc.split(',')[0]
        else:
            city = loc
        df1.at[idx, 'company_city'] = city.strip()  # Assign the extracted city
     

# Initialize the new column
df1['company_state'] = ''

# Define a function to extract the state
def extract_state(loc):
    if pd.notna(loc):
        parts = loc.split(',')
        if loc.startswith(tuple('0123456789')):  # Check if it starts with a digit
            if len(parts) >= 2:
                return parts[2].split(' ')[1]
        elif loc.startswith(tuple(alphabets)) and loc.endswith(tuple('0123456789')):  # Check if it starts with a letter and ends with a digit
            if len(parts) > 1:
                return parts[1].split()[0]
        else:
            if len(parts) > 1:
                return parts[1].strip()
    return ''

# Apply the function to the DataFrame
df1['company_state'] = df1['company_location'].apply(extract_state)
     

def extract_zip(loc):
    if pd.notna(loc):
        parts = loc.split(',')
        if loc.endswith(tuple('0123456789')):
            return parts[-1].strip().split()[1]
    return ''

# Apply the function to the DataFrame
df1['company_zip'] = df1['company_location'].apply(extract_zip)
     

df1.head(5)
     
company_name	job_title	company_location	company_rating	salary	job_type	job_desc	apply_link	company_city	company_state	company_zip
0	Columbia University	Data Analyst	New York, NY	4.1 out of 5	
64,000 a year	Full time	Position Summary A Data Analyst position is a...	https://www.indeed.com/cmp/Columbia-University...	New York	NY	
1	Saint Francis Health System	Financial Data Analyst (Entry Level)- Tulsa, O...	6600 South Yale Avenue, Tulsa, OK 74136	3.7 out of 5	NaN	Full time	NaN	https://www.indeed.com/cmp/Saint-Francis-Healt...	Tulsa	OK	74136
2	City of Baltimore, MD	Data Analyst - Baltimore City Information Tech...	3800 East Biddle Street, Baltimore, MD 21213	3.7 out of 5	
119,684 a year	Full time	NaN	https://www.indeed.com/cmp/City-of-Baltimore?c...	Baltimore	MD	21213
3	The University of Iowa	Graduate Student Data Analyst	Iowa City, IA	4.1 out of 5	$22 an hour	Part time	The graduate student data analyst will be an i...	https://www.indeed.com/cmp/The-University-of-I...	Iowa City	IA	
4	Cass Information Systems Inc.	Data Analyst Associate (Remote)	Columbus, OH 43231	3.2 out of 5	NaN	Full time	Performs duties associated with our address c...	https://www.indeed.com/cmp/Cass-Information-Sy...	Columbus	OH	43231

import re
# Print cities that contain 'in' as a separate word
pattern = r'\bin\b'  # \b is a word boundary

# Define the function to process each city
def fixCompanyCity(city):
    if re.search(pattern, city, re.IGNORECASE):  # Ignore case for matching
        return city.split('in', 1)[1].strip()  # Split and take the second part, remove leading/trailing spaces
    return city

df1['company_city'] = df1['company_city'].apply(fixCompanyCity)
     

df1['company_city'].unique()
     
array(['New York', 'Tulsa', 'Baltimore', 'Iowa City', 'Columbus',
       'San Francisco', '', 'Chicago', 'Stanford', 'Norfolk', 'Concord',
       'Frisco', 'Hinds County', 'Phoenix', 'Albany', 'United States',
       'Boston', 'Fairfax', 'Chapel Hill', 'Denver', 'El Segundo',
       'Washington', 'Wilmington', 'Glen Allen', 'Green Hall',
       'Louisville', 'Montana', 'Georgia', 'Perrysburg', 'Atlanta',
       'East Windsor', 'Dublin', 'Brevard County', 'Kenosha',
       'Albuquerque', 'Kansas City', 'Kennesaw', 'Worcester', 'Manhattan',
       'Los Angeles', 'Minneapolis', 'Alexandria', 'Iselin', 'Seattle',
       'Duluth', 'Arlington', 'Ada', 'Irving', 'Memphis', 'Montgomery',
       'Miami', 'Richmond', 'Beaverton', 'Austin', 'Chicago Heights',
       'Richardson', 'Tyler', 'Tampa', 'Parsippany', 'Plantation',
       'Beavercreek', 'Norwalk', 'Quincy', 'Virginia', 'Richfield',
       'Newport Beach', 'Cincinnati', 'Bellevue', 'Charlotte',
       'Princeton', 'Dallas', 'One Microsoft Way', 'Ann Arbor',
       'East Berlin', 'San Jose', 'Salisbury', 'Vienna', 'Lansing',
       'Windsor', 'Sulphur', 'Palatine', 'Staples', 'Westfield Center',
       'Harrisburg', 'Suwanee', 'Carlisle', 'Springfield', 'Puerto Rico',
       'Plymouth', 'Patchogue', 'Everett', 'East Providence', 'Deerfield',
       'Dahlgren', 'Clifton', 'Riverside', 'San Diego', 'Huntington',
       'Aurora', 'Westlake', 'Pittsburgh', 'Philadelphia', 'Aldie',
       'Shawnee County', 'Morrisville', 'Fremont', 'Bronx', 'Rochester',
       'One Shields Avenue', 'Oakland', 'McLean', 'Lacey', 'Missouri',
       'Reston', 'Santa Monica', 'Hartford', 'Ridgefield', 'Renton',
       'Fort Lauderdale', 'Boca Raton', 'Honolulu', 'Milwaukee',
       'Las Vegas', 'Reno', 'Berrien Springs', 'Lancaster', 'Raleigh',
       'Cordova', "St. Mary's City", 'Township of Hamilton',
       'Oahu Island', 'New Port Richey', 'Herndon', 'Waltham',
       'California', 'Grapevine', 'Asheboro', 'Cleveland', 'Trenton',
       'Detroit', 'Rialto', 'Tallahassee', 'Perkasie', 'Fort Myers',
       'Nashville', 'Newtown', 'Gaithersburg', 'Menands', 'Saginaw',
       'Piscataway', 'San Fernando', 'Laurel', 'Valley', 'San Juan',
       'Gwinnett County', 'New Orleans', 'San Antonio', 'Alpharetta',
       'Omaha', 'Pleasanton', 'Daly City', 'New Jersey', 'Ashford',
       'Dimondale', 'Woodland Hills', 'Bridgeton', 'Greeley',
       'Marlborough', 'Flint', 'West Palm Beach', 'Westminster',
       'Richland', 'Basking Ridge', 'Madison', 'Salt Lake City',
       'Seagoville', 'Plano', 'Newport News', 'Edina', 'West Orange',
       'New Castle', 'Queens', 'Macdill AFB', 'Watervliet',
       'Kirtland AFB', 'Chadds Ford', 'Huntsville', 'Napa', 'Houston',
       'Arnold', 'Farmington Hills', 'Tysons Corner', 'Newton',
       'South Plainfield', 'Columbia', 'New Haven', 'Northbrook', 'Bend',
       'Orlando', 'Baton Rouge', 'Park Hills', 'Miami Gardens',
       'Frankfort', 'Topeka', 'Bakersfield', 'Lakeland', 'Auburn Hills',
       'San Luis Obispo', 'Portsmouth', 'Dover', 'Tennessee', 'Ashburn',
       'Bridgewater', 'West Lafayette', 'Lake Mary', 'Miramar',
       'Bowling Green', 'Brooklyn', 'Oklahoma City', 'Northfield',
       'Brandon', 'Portland', 'Erlanger', 'Plattsmouth', 'Urbana',
       'Salem', 'Cedar Rapids', 'Fort Wayne', 'Olympia', 'Tempe',
       'Urbandale', 'Birmingham', 'Hawthorne', 'San Bernardino',
       'Pewaukee', 'Wood Dale', 'Naples', 'Chantilly', 'New Brunswick',
       'Hershey', 'Nebraska', 'Jackson', 'Roy', 'Long Beach', 'Longview',
       'Honesdale', 'Menlo Park', 'Houghton', 'Salinas', 'New York State',
       'McKinney', 'Newark', 'Little Rock', 'Fort Mill', 'Somerset',
       'Hendersonville', 'Michigan', 'Washington State', 'Little Ferry',
       'Colorado Springs', 'Monterey', 'Sarasota County', 'China Lake',
       'Elmhurst', 'Greenville', 'Westford', 'Sacramento County',
       'King of Prussia', 'Patrick Afb', 'Santa Ana', 'Edmond',
       'St. Louis', 'Wyoming', 'Saint Petersburg', 'Eden Prairie',
       'Aliso Viejo', 'Pascagoula', 'Fresno County', 'Warren', 'Rosemont',
       'Bolingbrook', 'Edwards AFB', 'Boise', 'Linthicum Heights',
       'Kanawha County', 'Cranbury', 'ROOM 201', 'Edinburg', 'Rosslyn',
       'Charleston', 'Pasadena', 'Bentonville', 'Clearwater', 'Annapolis',
       'Norcross', 'Marietta', 'g in Boston', 'Mountain View',
       'Brentwood', 'El Paso', 'South Jordan', 'Medford', 'York',
       'Paterson', 'Nevada', 'Wilkes-Barre', 'Overland Park', 'Goldsboro',
       'Cheshire', 'Sacramento', 'Whiteland', 'Cambridge', 'Ontario',
       'Hemet', 'Modesto', 'Chandler', 'Gainesville', 'Osterville',
       'Maple Grove', 'Tigard', 'Towson', 'Brighton', 'Stafford',
       'Des Moines', 'Conyers', 'Mesa', 'Olathe', 'Anaheim', 'Waldorf',
       'Redstone Arsenal', 'Dania', 'Scottsdale', 'Fort Worth', 'Troy',
       'ment Retail Enterprises in Apopka', 'Middletown',
       'West Lake Hills', 'Bannockburn', 'Calexico', 'Durham',
       's Consulting in Chicago', 'Jacksonville', 'Largo', 'East Lansing',
       'Rapid City', 'Orange', 'West Des Moines', 'Englewood Cliffs',
       'Wendell', 'Hanover', 'Naperville', 'Arizona City', 'Santa Cruz',
       'Foxborough', 'Pontiac', 'Pleasant Grove', 'Peekskill',
       'Knoxville', 'Sutter Creek', 'Norco', 'University', 'Pennsylvania',
       'Milford', 'Ozark', 'South Elgin', 'Maywood', 'Dania Beach',
       'Livingston', 'Miamisburg', 'Huntersville', 'Zanesville',
       'Warner Robins', 'Fort Belvoir', 'Oak Ridge', 'Dauphin County',
       'Fall River', 'Fraser', 'Grand Rapids', 'Cary', 'Cumming',
       'Lexington', 'Hollywood', 'Syracuse', 'Arkansas City'],
      dtype=object)

df1['company_state'].unique()
     
array(['NY', 'OK', 'MD', 'IA', 'OH', 'CA', '', 'IL', 'VA', 'NC', 'TX',
       'MS', 'AZ', 'MA', 'CO', 'DC', 'DE', '35', 'KY', 'GA', 'NJ', 'FL',
       'WI', 'NM', 'MO', 'PA', 'MN', 'WA', 'TN', 'AL', 'OR', 'KS',
       'Redmond', 'MI', 'CT', 'LA', 'RI', 'WV', 'Davis', 'HI', 'NV', 'AR',
       'PR', 'NE', 'ID', 'UT', 'NH', 'IN', 'SC', 'Salt', 'Texas', 'SD'],
      dtype=object)

df1['company_state'] = df1['company_state'].replace('Texas', 'TX')
     

df1[df1['company_state'].isin(['35', 'Redmond','Davis','Salt'])]
     
company_name	job_title	company_location	company_rating	salary	job_type	job_desc	apply_link	company_city	company_state	company_zip
28	University of Rhode Island	Research Associate/Data Analyst I - (2 Positions)	Green Hall, 35 Campus Avenue, Kingston, RI 02881	4.2 out of 5	
70,000 a year	Full time		https://www.indeed.com/cmp/The-University-of-R...	Green Hall	35	02881
126	Microsoft	Security Analyst	One Microsoft Way, Redmond, WA 98052	4.2 out of 5	
208,800 a year	Full time	NaN	https://www.indeed.com/cmp/Microsoft?campaigni...	Windsor	Redmond	98052
198	University of California, Davis	Data Systems Analyst 2 (DATA SYS ANL 2)	One Shields Avenue, Davis, CA 95616	4.3 out of 5	
57.71 an hour	Full time	This position is in the Department of Neurolog...	https://www.indeed.com/cmp/Uc-Davis?campaignid...	Bellevue	Davis	95616
614	University of Rhode Island	Financial Analyst, Financial Strategy & Planning	Green Hall, 35 Campus Avenue, Kingston, RI 02881	4.2 out of 5	
100,000 a year	Full time		https://www.indeed.com/cmp/The-University-of-R...	Piscataway	35	02881
686	University of Utah	Research Assistant/Analyst	201 Presidents Circle, ROOM 201, Salt Lake Cit...	4.2 out of 5	
15.00 an hour	Full time	The University is a participating employer w...	https://www.indeed.com/cmp/University-of-Utah?...	York	Salt	84112

df1['company_state'] = df1['company_state'].replace('35', 'RI')
df1['company_state'] = df1['company_state'].replace('Redmond', 'WA')
df1['company_state'] = df1['company_state'].replace('Salt', 'UT')
df1['company_state'] = df1['company_state'].replace('Davis', 'CA')
df1['company_state'] = df1['company_state'].replace('', 'Unknown')
     

df1 = df1.drop('company_location', axis=1)
     
Standardizing "company_rating"

df1['company_rating']
     
0      4.1 out of 5
1      3.7 out of 5
2      3.7 out of 5
3      4.1 out of 5
4      3.2 out of 5
           ...     
877             NaN
883             NaN
889             NaN
891             NaN
892             NaN
Name: company_rating, Length: 992, dtype: object

df1['company_rating'] = df1['company_rating'].apply(lambda x: str(x).split(' ')[0] if pd.notna(x) else x)
     

df1['company_rating'] = df1['company_rating'].astype(float)
     

df1['company_rating'].dtype
     
dtype('float64')
Standardizing 'salary'

print(df1['salary'].unique())
     
['$60,000 - $64,000 a year' nan '$74,803 - $119,684 a year' '$22 an hour'
 '$67,000 - $94,200 a year' '$73,500 - $195,000 a year' '$58,000 a year'
 'From $147,150 a year' '$53,000 - $79,000 a year' '$36,624 a year'
 '$65,001 - $82,656 a year' '$75,000 - $100,000 a year'
 '$68,448 - $82,139 a year' '$57,800 - $84,000 a year'
 '$59,100 - $81,500 a year' '$80,000 - $90,000 a year'
 '$69,957 - $104,936 a year' '$55,000 - $70,000 a year'
 '$26.73 - $27.57 an hour' '$85,000 - $120,000 a year'
 '$45,000 - $73,000 a year' '$65,000 - $75,000 a year'
 '$62,000 - $81,375 a year' '$41.73 an hour' '$16 - $17 an hour'
 '$69,000 - $85,000 a year' '$82,506 - $103,548 a year'
 '$65,260 - $94,640 a year' '$117,962 - $153,354 a year'
 '$62,000 - $82,500 a year' '$75,000 - $97,000 a year'
 '$44,419 - $62,186 a year' '$48,000 - $60,000 a year'
 'From $55,000 a year' '$30.32 - $45.49 an hour'
 '$61,300 - $110,000 a year' '$51,900 - $82,900 a year'
 '$70,000 - $135,000 a year' 'From $52,465 a year'
 '$39,900 - $88,800 a year' '$84,156 - $106,454 a year'
 '$43,900 - $97,700 a year' '$4,000.00 - $4,583.34 a month'
 '$76.94 an hour' '$6,073.83 - $8,173.02 a month' '$125,000 a year'
 '$69,760 - $83,000 a year' '$70,000 - $115,000 a year'
 '$50,000 - $60,000 a year' '$50,200 - $107,400 a year'
 '$110,000 - $175,000 a year' '$40,059 - $46,406 a year' '$35 an hour'
 '$60,400 - $137,000 a year' '$56,509.18 - $69,437.17 a year'
 '$98,300 - $208,800 a year' '$62,100 - $120,000 a year'
 '$90,000 - $100,000 a year' '$70,000 - $85,000 a year'
 '$35 - $43 an hour' '$43,888 - $85,068 a year' '$55,000 - $60,000 a year'
 '$26.40 - $40.47 an hour' '$6,688 - $9,745 a month' '$20.92 an hour'
 '$70,000 - $90,000 a year' '$54,200 - $77,259 a year'
 '$87,131 - $90,000 a year' '$39.84 an hour' '$70,087 - $84,805 a year'
 '$60,000 - $82,500 a year' '$57,700 - $79,300 a year' '$90,000 a year'
 '$21 - $28 an hour' '$50,000 - $55,000 a year' '$39,500 - $51,400 a year'
 '$70,000 - $120,000 a year' '$76,332 - $114,929 a year'
 '$65,775 - $99,115 a year' '$23.31 - $26.29 an hour'
 '$60,600 - $96,800 a year' '$53,125 - $71,875 a year'
 '$59,116 - $91,768 a year' '$69,383 - $99,911 a year'
 '$32.42 - $57.71 an hour' '$46,925 - $70,408 a year'
 '$50,000 - $130,000 a year' '$67,424.90 - $112,377.41 a year'
 '$52.72 - $80.83 an hour' '$65,000 - $85,000 a year'
 '$63,091 - $98,305 a year' '$85,000 - $115,000 a year'
 '$45,000 - $50,000 a year' '$63,501 - $107,968 a year'
 '$40,098 - $55,000 a year' '$101,899.20 - $125,798.40 a year'
 '$50,000 - $80,000 a year' '$60,889 - $94,521 a year'
 '$38.87 - $54.64 an hour' '$35.47 - $48.85 an hour'
 '$3,640 - $7,114 a month' '$57,553.60 - $84,115.20 a year'
 '$63,790 - $72,156 a year' '$54,955 - $87,328 a year'
 '$79,154 - $134,561 a year' '$59,000 - $116,000 a year'
 '$57,700 - $106,600 a year' '$80,000 - $100,000 a year'
 '$63,030 - $105,050 a year' '$4,858 a month' '$77,158 - $95,000 a year'
 '$95,682 - $122,829 a year' '$53,363 - $80,044 a year'
 '$118,800 - $153,670 a year' '$112,513 - $191,273 a year' '$40 a day'
 '$109,330 - $110,000 a year' '$69,659.20 - $116,084.80 a year'
 '$49,148 - $83,552 a year' '$70,338 - $112,807 a year'
 '$65,484 - $81,855 a year' '$120,000 - $130,000 a year'
 '$120,000 - $180,000 a year' '$3,961.56 a month' '$66,560 a year'
 '$50,000 - $52,500 a year' '$55,000 a year' '$37.72 - $49.03 an hour'
 '$4,450 - $6,658 a month' '$63,935.04 - $83,200.00 a year'
 '$78,000 - $88,000 a year' '$3,694 - $7,131 a month'
 '$77,828.39 - $96,938.75 a year' '$65,000 - $96,000 a year'
 '$75,000 - $160,000 a year' '$78,687 - $108,195 a year'
 '$69,600 - $104,400 a year' '$58,851 - $84,257 a year'
 '$108,056 - $153,928 a year' '$65,871 - $83,275 a year' '$19.33 an hour'
 '$75,291 - $101,865 a year' '$67,000 - $80,000 a year'
 '$70,200 - $137,800 a year' '$135,200 - $142,554 a year'
 '$60,000 - $75,000 a year' '$28 an hour' '$22.49 - $41.27 an hour'
 '$31 an hour' '$61,500 - $73,545 a year' '$66,500 - $83,100 a year'
 '$60,000 a year' '$66,900 - $83,600 a year' '$55,000 - $75,500 a year'
 '$66,066 - $104,500 a year' '$96,800 - $125,290 a year'
 '$19 - $20 an hour' '$28.16 - $42.24 an hour' '$61,044 - $75,195 a year'
 '$53,310.72 - $70,677.24 a year' '$59,000 a year'
 '$55,150 - $58,508 a year' '$30.90 an hour'
 '$60,107.42 - $70,560.88 a year' '$76,000 a year'
 '$89,550 - $108,356 a year' '$115,900 - $152,100 a year'
 '$70,000 - $75,000 a year' '$3,958 - $5,950 a month'
 '$43,000 - $50,000 a year' '$65,000 - $70,000 a year'
 '$93,288 - $107,281 a year' '$83,685 - $122,506 a year'
 '$71,255 - $81,943 a year' '$59,116 - $67,983 a year'
 '$88,545.60 - $106,601.60 a year' '$92,894 - $124,013 a year'
 '$65,100 a year' '$77,158 - $114,887 a year' '$78,900 - $102,500 a year'
 '$29.13 - $31.90 an hour' '$33.52 - $38.31 an hour'
 '$72,774 - $83,690 a year' '$56,800 - $96,600 a year' '$48,056.98 a year'
 '$54,540 - $87,480 a year' '$71,958 - $122,328 a year'
 '$55,955 - $78,336 a year' 'From $55,901 a year'
 '$54,000 - $86,000 a year' '$3,733.60 - $5,169.46 a month'
 '$31 - $36 an hour' '$73,000 - $110,000 a year'
 '$57,000 - $70,000 a year' '$70,087 a year' '$67,800 - $91,500 a year'
 '$50,000 - $65,000 a year' '$70,000 - $87,000 a year'
 '$66,900 - $143,100 a year' '$70,615 - $169,806 a year' '$55,150 a year'
 '$55,000 - $65,000 a year' '$62,240 - $115,000 a year'
 '$71,000 - $88,000 a year' '$4,755 - $7,296 a month'
 '$44,680 - $75,956 a year' '$55,790 - $87,230 a year'
 '$51,874.00 - $62,248.80 a year' '$29.00 - $36.40 an hour'
 '$4,741 - $7,170 a month' '$86,712 - $108,252 a year'
 '$52,000 - $70,545 a year' '$82,506 a year' '$31.86 an hour'
 '$75,000 - $115,000 a year' '$86,070 - $109,958 a year'
 '$56,000 - $104,000 a year' '$12.02 - $21.63 an hour'
 '$56,316.95 - $84,477.05 a year' '$38.03 - $44.48 an hour'
 '$82,506 - $94,882 a year' '$73,100 - $117,300 a year'
 '$65,509.60 a year' '$62,268.18 - $89,143.08 a year'
 '$80,800 - $137,400 a year' '$35.08 an hour' '$69,107 - $118,069 a year'
 '$62,240 - $93,400 a year' '$63,750 - $84,000 a year'
 '$23.15 - $37.05 an hour' 'From $57,000 a year'
 '$109,120 - $163,680 a year' '$52,100 - $65,200 a year'
 '$8,040 - $10,975 a month' '$5,747 - $8,831 a month'
 '$100,000 - $120,000 a year' '$3,075.30 - $6,783.30 a month'
 '$58,035 - $88,235 a year' '$58,836 - $70,467 a year'
 '$26.25 - $43.75 an hour' '$82,000 - $100,000 a year'
 '$52,360.41 - $72,793.09 a year' '$85,000 - $110,000 a year'
 '$85,756 - $115,340 a year' '$9,328.89 - $11,339.32 a month'
 '$85,000 - $160,000 a year' '$55,577.60 - $62,000.00 a year'
 '$65,832 a year' '$45,000 - $60,000 a year' '$3,640 - $5,916 a month'
 '$31.84 - $47.40 an hour' '$70,000 - $110,000 a year'
 '$69,894 - $97,075 a year' '$160 a day' '$40,000 - $50,000 a year'
 '$70,000 - $87,110 a year' '$65,000 - $87,000 a year' '$22.41 an hour'
 '$65,338 - $99,372 a year' '$65,004 a year' '$73,537 - $101,144 a year'
 '$5,208 - $5,417 a month' '$65,000 - $72,500 a year' '$67,997 a year'
 '$40,000 a year' '$110,000 - $115,000 a year' '$42,898 - $79,358 a year'
 '$12.02 - $15.00 an hour' '$62,608 - $75,129 a year' '$25 - $28 an hour'
 '$25 - $30 an hour' '$60,000 - $65,000 a year' '$60,000 - $70,000 a year'
 '$75,000 - $85,000 a year' '$65,000 - $80,000 a year'
 '$8,000 - $18,000 a month' '$25 - $29 an hour'
 '$89,228 - $119,566 a year' '$30 an hour' '$75,000 - $80,000 a year'
 '$60,008 - $74,088 a year' '$25 - $35 an hour'
 '$69,273.53 - $102,000.00 a year' 'From $40,000 a year'
 '$65,000 - $72,000 a year' '$62,000 - $68,000 a year'
 '$110,000 - $300,000 a year' '$70,082 - $74,262 a year'
 '$52,500 - $80,000 a year' '$70 - $72 an hour' '$41,500 - $59,300 a year'
 'From $31.25 an hour' '$50,000 - $63,000 a year' '$20 - $25 an hour'
 '$58,300 - $80,000 a year' 'From $24 an hour' '$35.86 an hour'
 '$18 an hour' '$52.50 an hour' '$85,000 - $100,000 a year'
 '$52,000 - $62,000 a year' '$68,000 - $85,000 a year'
 '$85,000 - $90,000 a year' '$28.85 - $33.65 an hour'
 '$45,000 - $80,000 a year' '$24 - $28 an hour' '$65 - $70 an hour'
 '$70 - $75 an hour' '$43,245.35 - $50,000.00 a year'
 '$60,000 - $115,000 a year' '$62,400 - $68,000 a year'
 '$45,000 - $55,000 a year' '$25,000 - $35,000 a year'
 '$130,000 - $140,000 a year' '$18 - $20 an hour' 'From $80,598 a year'
 '$19 - $25 an hour' '$28 - $35 an hour' '$28 - $34 an hour'
 '$30 - $50 an hour' '$22 - $28 an hour' '$30 - $35 an hour'
 '$45,500 - $48,500 a year' '$29.24 an hour' '$58,000 - $90,000 a year'
 '$76,837 - $83,679 a year' '$22.21 an hour'
 '$52,028.39 - $59,832.65 a year' '$80,428 - $120,642 a year'
 '$65,000 - $73,000 a year' '$125,000 - $150,000 a year'
 'From $63,913 a year' '$92,492 - $138,738 a year' 'From $60,000 a year'
 '$60 - $65 an hour' '$70,750 - $98,600 a year' '$60,000 - $90,000 a year'
 '$36 - $42 an hour' '$50,000 a year' '$58,656 - $60,000 a year'
 '$102,900 - $125,900 a year' '$70 an hour' '$50 - $55 an hour'
 '$55,701.50 - $80,000.00 a year' '$50,000 - $67,000 a year'
 '$63,000 - $65,000 a year' '$41.49 - $49.96 an hour'
 '$80,000 - $130,000 a year' '$35,000 - $45,000 a year'
 '$90,000 - $115,000 a year' '$45,000 - $49,961 a year'
 '$60,000 - $100,000 a year' '$66,300 - $111,000 a year'
 '$60,000 - $88,000 a year' 'From $35 an hour'
 '$56,010.68 - $88,745.00 a year' '$21.50 - $24.50 an hour'
 '$67,760 - $76,569 a year' '$75,000 a year' 'From $16 an hour'
 'Up to $66 an hour' '$52,000 - $65,000 a year' '$47,000 - $57,000 a year'
 '$136,214 - $165,594 a year' '$48,484.80 - $54,683.20 a year'
 '$39 - $40 an hour' '$70 - $71 an hour' '$18.98 - $28.47 an hour'
 '$20 - $24 an hour' '$28 - $30 an hour' '$82,000 - $95,000 a year'
 '$35,000 - $40,000 a year' '$60,000 - $73,000 a year'
 'From $45,000 a year' '$55,000 - $75,000 a year'
 '$81,242 - $94,781 a year' '$55 - $60 an hour'
 '$67,333 - $101,001 a year' '$68,940 - $97,000 a year'
 '$18 - $26 an hour' '$49,000 - $74,000 a year' '$85,000 - $95,000 a year'
 'From $90,000 a year' '$77,000 a year' '$70,000 - $80,000 a year'
 '$66,950 - $92,700 a year' '$28.45 - $34.58 an hour' '$26.23 an hour'
 '$83,400 - $103,035 a year' '$87,890.51 - $90,000.00 a year'
 '$30 - $40 an hour' '$79,664 - $131,456 a year'
 '$52,000 - $72,000 a year']

df1[df1['salary'].str.endswith('a year', na=False)]
     
company_name	job_title	company_rating	salary	job_type	job_desc	apply_link	company_city	company_state	company_zip
0	Columbia University	Data Analyst	4.1	
64,000 a year	Full time	Position Summary A Data Analyst position is a...	https://www.indeed.com/cmp/Columbia-University...	New York	NY	
2	City of Baltimore, MD	Data Analyst - Baltimore City Information Tech...	3.7	
119,684 a year	Full time	NaN	https://www.indeed.com/cmp/City-of-Baltimore?c...	Baltimore	MD	21213
5	University of California San Francisco	DATA ANALYST	4.1	
94,200 a year	Full time	The final salary and offer components are sub...	https://www.indeed.com/cmp/University-of-Calif...	San Francisco	CA	94143
6	GitHub, Inc.	Data Analyst	4.0	
195,000 a year	Full time	GitHub is the place where over 83 million deve...	https://www.indeed.com/cmp/Github?campaignid=m...		Unknown	
7	Chicago Public Schools	Data Analyst	3.8	$58,000 a year	Full time	Chicago Public Schools (CPS) is one of the lar...	https://www.indeed.com/cmp/Chicago-Public-Scho...	Chicago	IL	60602
...	...	...	...	...	...	...	...	...	...	...
994	GeekSI	Business Analyst	5.0	
90,000 a year	Full time	GeekSI is seeking candidates matching our corp...	https://www.indeed.com/cmp/Geeksi-1?campaignid...		FL	
995	KS Management Services, LLC	Clinical Operation Analyst	3.6	
103,035 a year	Full time	Responsibilities The Clinical Operation Analys...	https://www.indeed.com/cmp/Kelsey--seybold-Cli...		TX	
999	NLB Technology Services	SAP Data Analyst	NaN	
90,000.00 a year	Full time	SAP Data Analyst Location:- Arkansas City, KS,...	https://www.indeed.com/cmp/Nlb-Technology-Serv...		KS	67005
1002	ECU Health	Business Intelligence Analyst III	3.7	
131,456 a year	Full time	ECU Health About ECU Health Medical Center ECU...	https://www.indeed.com/cmp/Ecu-Health?campaign...		NC	27835
1003	ERG	Occupational Safety and Health Coding Analyst	4.4	
72,000 a year	Full time	NaN	https://www.indeed.com/cmp/Eastern-Research-Gr...		Unknown	
374 rows × 10 columns


df1[df1['salary'].str.endswith('an hour', na=False)]
     
company_name	job_title	company_rating	salary	job_type	job_desc	apply_link	company_city	company_state	company_zip
3	The University of Iowa	Graduate Student Data Analyst	4.1	$22 an hour	Part time	The graduate student data analyst will be an i...	https://www.indeed.com/cmp/The-University-of-I...	Iowa City	IA	
30	State of Montana	Research Analyst 1	3.4	
27.57 an hour	Full time	Note: Employees for the State of Montana must...	https://www.indeed.com/cmp/State-of-Montana?ca...	Montana	Unknown	
40	State of Maryland	Data Analyst (ADMINISTRATOR III)	3.6	$41.73 an hour	Full time	When you join the Maryland Department of Human...	https://www.indeed.com/cmp/State-of-Maryland?c...	Baltimore	MD	21201
47	University of New Mexico	Data Analyst	4.0	
17 an hour	NaN	The University of New Mexico’s Institute Cente...	https://www.indeed.com/cmp/University-of-New-M...	Albuquerque	NM	87106
78	Seattle Theatre Group	Data Specialist	4.5	
45.49 an hour	Full time	STG is seeking a highly skilled data speciali...	https://www.indeed.com/cmp/Seattle-Theatre-Gro...	Phoenix	WA	98101
...	...	...	...	...	...	...	...	...	...	...
986	InfoLogitech	IT Business Analyst	NaN	
35 an hour	Full time, Contract	Job Position : Business AnalystJob Location : ...	https://www.indeed.com/cmp/Infologitech?campai...		NV	89169
992	Amador County	Staff Service Analyst I	NaN	
34.58 an hour	Full time	To Apply: https://www.governmentjobs.com/caree...	https://www.indeed.com/cmp/Amador-County-1?cam...		CA	95685
993	NaN	Corporate BA I	NaN	$26.23 an hour	Full time	NaN	NaN		AL	36116
996	Kros-Wise	Business Data Analyst	3.9	
25 an hour	Full time	NaN	https://www.indeed.com/cmp/Kros--wise?campaign...		CA	92860
1001	HIGH BRIDGE CONSULTING LLC	BI Analyst - Birst	NaN	
40 an hour	Full time	Flexible work from home options available.	https://www.indeed.com/cmp/High-Bridge-Consult...		NJ	07054
90 rows × 10 columns


import numpy as np

def extractSalary(sal):
    if pd.notna(sal):
        sal = str(sal)  # Ensure the salary is treated as a string
        if sal.endswith('a year') and '-' in sal:
            try:
                sal_lower = float(sal.split('-')[0].strip('$').replace(',', ''))
                sal_upper = float(sal.split('-')[1].split(' ')[1].strip('$').replace(',', ''))
                return (sal_lower + sal_upper) / 2
            except ValueError as e:
                print(f"Error parsing yearly salary range: {sal} - {e}")
                return np.nan

        elif sal.endswith('a year') and sal.lower().startswith('from'):
            try:
                return float(sal.split(' ')[1].strip('$').replace(',', ''))
            except ValueError as e:
                print(f"Error parsing yearly salary from 'From': {sal} - {e}")
                return np.nan

        elif sal.endswith('a year') and '-' not in sal:
            try:
                return float(sal.split(' ')[0].strip('$').replace(',', ''))
            except ValueError as e:
                print(f"Error parsing yearly salary: {sal} - {e}")
                return np.nan

        elif sal.endswith('an hour') and '-' in sal:
            try:
                hourly_lower = float(sal.split('-')[0].strip('$').replace(',', ''))
                hourly_upper = float(sal.split('-')[1].split(' ')[1].strip('$').replace(',', ''))
                return ((hourly_lower + hourly_upper) / 2) * 40 * 50
            except ValueError as e:
                print(f"Error parsing hourly salary range: {sal} - {e}")
                return np.nan

        elif sal.endswith('an hour') and sal.lower().startswith('from'):
            try:
                return float(sal.split(' ')[1].strip('$').replace(',', '')) * 40 * 50
            except ValueError as e:
                print(f"Error parsing hourly salary from 'From': {sal} - {e}")
                return np.nan

        elif sal.endswith('an hour') and '-' not in sal and 'Up' not in sal:
            try:
                return float(sal.split(' ')[0].strip('$').replace(',', '')) * 40 * 50
            except ValueError as e:
                print(f"Error parsing hourly salary: {sal} - {e}")
                return np.nan

        elif sal.endswith('a month') and '-' in sal:
            try:
                monthly_lower = float(sal.split('-')[0].strip('$').replace(',', ''))
                monthly_upper = float(sal.split('-')[1].split(' ')[1].strip('$').replace(',', ''))
                return (monthly_lower + monthly_upper) / 2 * 12
            except ValueError as e:
                print(f"Error parsing monthly salary range: {sal} - {e}")
                return np.nan

        elif sal.endswith('a month') and '-' not in sal:
            try:
                return float(sal.split(' ')[0].strip('$').replace(',', '')) * 12
            except ValueError as e:
                print(f"Error parsing monthly salary: {sal} - {e}")
                return np.nan

        elif sal.startswith('Up') and sal.endswith('an hour'):
            try:
              return float(sal.split(' ')[2].strip('$')) * 40 * 50
            except ValueError as e:
              print(f'Error parsing "Up To XXX An Hour": {sal} - {e}')
              return np.nan



    return np.nan  # Return NaN if none of the conditions match

# Apply the function to the 'company_rating' column
df1['salary_clean'] = df1['salary'].apply(extractSalary)
     

df1['salary_clean'].dtype
     
dtype('float64')

df1 = df1.drop('salary', axis=1)
     

df1.columns
     
Index(['company_name', 'job_title', 'company_rating', 'job_type', 'job_desc',
       'apply_link', 'company_city', 'company_state', 'company_zip',
       'salary_clean'],
      dtype='object')
Exploratory Data Analysis (EDA)
Job Counts Per State

import plotly.express as px
import plotly.graph_objects as go
import matplotlib.pyplot as plt

jobs_per_state = df1.groupby('company_state').size().reset_index(name='job_count').sort_values('job_count', ascending=False)

jobs_per_state = jobs_per_state[jobs_per_state['company_state'] != 'Unknown']

# Create a choropleth map
fig = px.choropleth(jobs_per_state,
                    locations='company_state',
                    locationmode="USA-states",
                    color='job_count',
                    color_continuous_scale='Viridis',
                    scope="usa",
                    labels={'job_count':'Job Count'},
                    title='Job Count By State')

# Update layout for better readability
fig.update_layout(
    title_font_size=20,
    title_font_color='teal',
    autosize=True,
    paper_bgcolor='lightgray', width = 1100, height = 650,
    font=dict(
        family='Arial',
        color='blue',
        size=10
    )
)

fig.show()
     
Key Takeaways:

California: This state has the highest job count, indicated by the bright yellow color. California is a hub for tech companies, especially in Silicon Valley, which explains the high number of data analyst job postings.

Texas: With a significant number of job postings, Texas is shown in green. Cities like Austin, Dallas, and Houston are becoming tech and business hubs, leading to increased demand for data analysts.

New York: Also depicted in green, New York is a major financial and business center, driving demand for data analysts to manage and interpret large datasets.

Some other notable states that have moderate job postings are: FL, VA, IL, MA, WA.

Company Ratings Overall And By State

df1['company_rating'].mean()
     
3.6861236802413275

rating_per_state = df1.groupby('company_state')[['company_rating']].mean().sort_values('company_rating', ascending=False).reset_index()

rating_per_state = rating_per_state[rating_per_state['company_state'] != 'Unknown']

fig = px.bar(rating_per_state,
              x = 'company_state',
              y = 'company_rating',
              color = 'company_rating',
              color_continuous_scale = 'viridis')



fig.update_layout(title_text = ' Average Rating By State ', title_font_size = 20, title_font_color = 'teal', autosize=True,
                  xaxis_title = 'State', yaxis_title = 'Count', width = 1100, height = 650, xaxis=dict(tickangle=45), paper_bgcolor = 'light gray',
                  font=dict(family='Arial',
                             color='green',
                             size=10
                             ))

fig.show()
     
Key Takeaways:

Consistency Across States: There is a noticeable consistency in average ratings across many states, with most states falling within the 3.5 to 4.0 range. This suggests that, on average, companies across the U.S. maintain a relatively similar level of employee satisfaction.

Variability in Ratings: The variation in ratings between the top and bottom states highlights differences in workplace environments and employee experiences. This variability can be crucial for job seekers who prioritize company culture and employee satisfaction when considering job opportunities.

Salary For Different Technical Skills

python_req = df1[df1['job_desc'].str.contains('python', case=False, na=False)][

    ['company_name','job_title','company_state','salary_clean']].sort_values('salary_clean', ascending=False)
     

sql_req = df1[df1['job_desc'].str.contains('sql', case=False, na=False)][

    ['company_name','job_title','company_state','salary_clean']].sort_values('salary_clean', ascending=False)
     

data_viz_req = df1[df1['job_desc'].str.contains('visualization', case=False, na=False)][

    ['company_name','job_title','company_state','salary_clean']].sort_values('salary_clean', ascending=False)
     

excel_req = df1[df1['job_desc'].str.contains('excel', case=False, na=False)][

    ['company_name','job_title','company_state','salary_clean']].sort_values('salary_clean', ascending=False)
     

import plotly.express as px

skills_list = [python_req, sql_req, data_viz_req, excel_req]

titles_list = ['Python-required jobs', 'SQL-required jobs', 'Data Visualization-required jobs', 'Excel-required jobs']


for skill, title in zip(skills_list, titles_list):
  fig = px.histogram(x = skill['salary_clean'], title = f'Distribution of Salary for {title}', labels = {'x':'Salary Amount'},
                    color_discrete_sequence=['teal'])

  fig.update_layout(
      plot_bgcolor = 'light gray',
      title_font_color = 'yellowgreen',
      title_font_family = 'Arial',
      title_font = dict(size=28))

  fig.update_xaxes(title_font = dict(size=22), title_font_family = 'Arial', title_font_color = 'darkcyan')

  fig.update_yaxes(title_font = dict(size=22), title_font_family = 'Arial', title_font_color = 'darkcyan')

  fig.show()
     
Key Takeaways:

Python-required jobs have a significant number of postings in the salary range of USD 80k - 99k.

SQL-required jobs show a wider distribution, with many postings around the USD 50k - 100k range and some higher salary positions.

Data Visualization-required jobs (likely including tools like Tableau and Power BI) show a concentration around the USD 50k - 100k range.

Excel-required jobs have a similar distribution to SQL, with a notable number of positions in the USD 40k - 80k range.

Important In-Demand Skills

import re
from sklearn.feature_extraction.text import CountVectorizer

# Function to preprocess text
def preprocess(text):
    if pd.notna(text):
        # Convert to lowercase
        text = text.lower()
        # Remove punctuation
        text = re.sub(r'[^\w\s]', '', text)
        return text
    return ''

# Apply preprocessing and remove NA values
df1['cleaned_job_desc'] = df1['job_desc'].apply(preprocess)

# Define the skills to look for

skills = [
    'python', 'sql', 'excel', 'r', 'tableau', 'machine learning',
    'power bi', 'sas', 'hadoop', 'pandas', 'scikit-learn', 'data visualization'
    'aws', 'google cloud platform', 'microsoft azure',
    'regression analysis', 'hypothesis testing', 'time series analysis',
    'critical thinking', 'communication skills', 'problem-solving', 'attention to detail'
]


# Function to count skill occurrences
def count_skills(text, skills):
    skill_counts = {skill: 0 for skill in skills}
    for skill in skills:
        # Use word boundaries to ensure 'r' is identified as a standalone word
        pattern = r'\b' + re.escape(skill) + r'\b'
        matches = re.findall(pattern, text)
        skill_counts[skill] = len(matches)
    return skill_counts

# Apply the skill counting function
skill_counts = df1['cleaned_job_desc'].apply(lambda x: count_skills(x, skills))

# Convert the results to a DataFrame
skill_counts_df = pd.DataFrame(list(skill_counts))

# Sum up the counts for each skill
total_skill_counts = skill_counts_df.sum().sort_values(ascending=False)

# Plot the skill frequencies using Plotly
fig = px.bar(
    x=total_skill_counts.index,
    y=total_skill_counts.values,
    title='Skill Frequency in Job Descriptions',
    labels={'x': 'Skill', 'y': 'Frequency'},
    color=total_skill_counts.values,
    color_continuous_scale='emrld'
)

# Update the layout for better readability
fig.update_layout(
    font_family='Arial',
    font_color='darkcyan',
    title_font=dict(size=28, color='yellowgreen'),
    xaxis_title='Skill',
    yaxis_title='Frequency',
    plot_bgcolor='light gray',
    paper_bgcolor='light gray',
    xaxis = dict(tickangle=45)
)

fig.show()
     
Key Takeaways:

Technical Skills: A successful data analyst should be proficient in SQL, Excel, data visualization tools (Tableau, Power BI), and programming languages (Python and/or R).

Soft Skills: Effective communication and attention to detail are vital for presenting findings and ensuring data accuracy.

Advanced Knowledge: Familiarity with machine learning, cloud platforms, and advanced statistical methods can enhance an analyst's capability and marketability.

Note: Some other advanced tools/skills such as: Hadoop, Cloud, Hypothesis Testing, Time Series Analysis, etc. are less likely to be included in an entry-level job posting. To my knowledge, these skills are more likely to be required at a Junior/Senior level in the data career tracks.

Thus, in order to stand out as a prospective candidate, acquiring these advanced skills mentioned above will serve as a huge advantage for anyone.

Identify Outliers In Salary

import plotly.express as px

# Create a box plot for salary distribution
fig = px.box(df1, y='salary_clean', title='Salary Distribution For Entry-Level Data Analysts', labels={'salary_clean': 'Average Salary'}, color_discrete_sequence = ['teal'])

# Update layout
fig.update_layout(
    font_family='Arial',
    font_color='darkcyan',
    title_font=dict(size=30, color='yellowgreen')
)

# Update y-axis title font
fig.update_yaxes(title_font=dict(size=20, family='Arial', color='darkcyan'))

fig.show()
     

# Create a histogram for salary distribution
fig = px.histogram(df1, x='salary_clean', title='Salary Frequency For Entry-Level Data Analysts', labels={'salary_clean': 'Salary Amount'}, color_discrete_sequence=['teal'])

# Update layout
fig.update_layout(
    font_family='Arial',
    font_color='darkcyan',
    title_font=dict(size=30, color='yellowgreen'),
)

# Update x-axis title font
fig.update_xaxes(title_font=dict(size=20, family='Arial', color='darkcyan'))

# Show plot
fig.show()
     
We can see it is right-skewed


import plotly.express as px

# Calculating quartiles, inter-quartile range, and identifying outliers
q1 = df1['salary_clean'].quantile(0.25)
q3 = df1['salary_clean'].quantile(0.75)
iqr = q3 - q1
lower_bound = q1 - 1.5 * iqr
upper_bound = q3 + 1.5 * iqr

salary_outliers = df1[(df1['salary_clean'] < lower_bound) | (df1['salary_clean'] > upper_bound)].groupby('company_state')['salary_clean'].mean().sort_values(ascending=False).reset_index()

salary_outliers = salary_outliers[salary_outliers['company_state'] != 'Unknown']

# Create the bar plot using Plotly
fig = px.bar(salary_outliers,
             x='company_state',
             y='salary_clean',
             color='salary_clean',
             labels={'company_state': 'State', 'salary_clean': 'Average Salary'},
             title='Average Salary by State (Outliers)',
             color_continuous_scale='emrld')

# Update layout for better readability
fig.update_layout(
    font_family='Arial',
    font_color='darkcyan',
    title_font=dict(size=26, color='teal'),
    xaxis=dict(tickangle=45, title_font=dict(size=20, family='Arial', color='darkcyan')),
    yaxis=dict(title_font=dict(size=20, family='Arial', color='darkcyan'))
)

# Show the plot
fig.show()
     

df1['company_state'] = df1['company_state'].apply(lambda x: x.strip())
     

# Calculating mean and median salary by state
avg_sal_state = df1.groupby('company_state')['salary_clean'].agg(['mean', 'median']).sort_values('mean', ascending=False)
avg_sal_state = avg_sal_state[avg_sal_state.index != 'Unknown']

median_sal_state = df1.groupby('company_state')['salary_clean'].agg(['mean', 'median']).sort_values('median', ascending=False)
median_sal_state = median_sal_state[median_sal_state.index != 'Unknown']

# Create bar plot for mean salary
fig_mean = px.bar(avg_sal_state,
             x=avg_sal_state.index,
             y='mean',
             color='mean',
             title='Average Salary by State',
             color_continuous_scale='teal')

# Update layout for mean salary plot
fig_mean.update_layout(
    font_family='Arial',
    font_color='darkcyan',
    xaxis_title='State', yaxis_title='Average Salary', title='Average Salary by State',
    title_font=dict(size=30, color='cornflower blue'),
    xaxis=dict(tickangle=45, title_font=dict(size=20, family='Arial', color='darkcyan')),
    yaxis=dict(title_font=dict(size=20, family='Arial', color='darkcyan'))
)

# Show mean salary plot
fig_mean.show()

# Create bar plot for median salary
fig_median = px.bar(median_sal_state,
             x=median_sal_state.index,
             y='median',
            color='median',
             title='Median Salary by State',
             color_continuous_scale='teal')

# Update layout for median salary plot
fig_median.update_layout(
    font_family='Arial',
    font_color='darkcyan',
    xaxis_title='State', yaxis_title='Median Salary',
    title_font=dict(size=30, color='cornflower blue'),
    xaxis=dict(tickangle=45, title_font=dict(size=20, family='Arial', color='darkcyan')),
    yaxis=dict(title_font=dict(size=20, family='Arial', color='darkcyan'))
)

# Show median salary plot
fig_median.show()
     
Average salary for New York jobs is roughly USD 81,000/year while the Median salary is about USD 78,000/year

Correlation Analysis - Rating & Salary

correlation = df1.corr(method = 'pearson', numeric_only=True)
     

fig = px.imshow(correlation,
                labels=dict(color="Correlation"),
                x=correlation.columns,
                y=correlation.columns,
                title='Correlation Heatmap')

# Update layout for better readability and styling
fig.update_layout(
    title_text='Correlation Analysis Between Salary & Rating ',
    title_font=dict(size=30, color='teal', family='Arial'),
    font=dict(family='Arial', color='darkcyan', size=14),
    plot_bgcolor ='lightgray'
)

# Show the heatmap
fig.show()
     
This heatmap shows the correlation analysis between company ratings and salaries. The colors indicate the strength and direction of the correlation, where yellow represents a strong positive correlation and blue represents a strong negative correlation. The correlation coefficient values range from -1 to 1, with values closer to 1 indicating a strong positive correlation and values closer to -1 indicating a strong negative correlation.

In this analysis, the heatmap reveals that there is no significant correlation between company ratings and salaries, as indicated by the darker blue and yellow squares showing minimal correlation. This means that higher salaries do not necessarily correspond to higher company ratings and vice versa.

Natural Language Processing - Job Description
Preprocess, Clean & Tokenize Text
Remove punctuation and convert the text to lowercase for consistency, and tokenize the documents into individual tokens or words.
Utilize pre-trained models from spaCy (https://spacy.io/models) to tag words with their Part-of-Speech (POS) labels.
Filter for words with the most relevant POS tags such as nouns (NOUN), verbs (VERB), adjectives (ADJ), and adverbs (ADV).
Remove stop words, which are commonly occurring words that do not carry significant meaning.
Apply lemmatization, a process that reduces words to their base or root form, using libraries such as nltk.

!pip install nltk
     
Requirement already satisfied: nltk in /usr/local/lib/python3.10/dist-packages (3.8.1)
Requirement already satisfied: click in /usr/local/lib/python3.10/dist-packages (from nltk) (8.1.7)
Requirement already satisfied: joblib in /usr/local/lib/python3.10/dist-packages (from nltk) (1.4.2)
Requirement already satisfied: regex>=2021.8.3 in /usr/local/lib/python3.10/dist-packages (from nltk) (2024.5.15)
Requirement already satisfied: tqdm in /usr/local/lib/python3.10/dist-packages (from nltk) (4.66.4)

import nltk
nltk.download('stopwords')
nltk.download('punkt')
import re
from nltk.corpus import stopwords
from nltk.tokenize import word_tokenize
from nltk.stem import WordNetLemmatizer
from sklearn.feature_extraction.text import TfidfVectorizer
import spacy
     
[nltk_data] Downloading package stopwords to /root/nltk_data...
[nltk_data]   Unzipping corpora/stopwords.zip.
[nltk_data] Downloading package punkt to /root/nltk_data...
[nltk_data]   Unzipping tokenizers/punkt.zip.

!python -m spacy download en_core_web_md
import en_core_web_md
nlp = en_core_web_md.load()
     
Collecting en-core-web-md==3.7.1
  Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_md-3.7.1/en_core_web_md-3.7.1-py3-none-any.whl (42.8 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 42.8/42.8 MB 7.2 MB/s eta 0:00:00
Requirement already satisfied: spacy<3.8.0,>=3.7.2 in /usr/local/lib/python3.10/dist-packages (from en-core-web-md==3.7.1) (3.7.5)
Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.11 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.0.12)
Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.0.5)
Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.0.10)
Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.0.8)
Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.0.9)
Requirement already satisfied: thinc<8.3.0,>=8.2.2 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (8.2.5)
Requirement already satisfied: wasabi<1.2.0,>=0.9.1 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.1.3)
Requirement already satisfied: srsly<3.0.0,>=2.4.3 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.4.8)
Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.0.10)
Requirement already satisfied: weasel<0.5.0,>=0.1.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.4.1)
Requirement already satisfied: typer<1.0.0,>=0.3.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.12.3)
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (4.66.4)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.31.0)
Requirement already satisfied: pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.8.2)
Requirement already satisfied: jinja2 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.1.4)
Requirement already satisfied: setuptools in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (67.7.2)
Requirement already satisfied: packaging>=20.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (24.1)
Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.4.0)
Requirement already satisfied: numpy>=1.19.0 in /usr/local/lib/python3.10/dist-packages (from spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.25.2)
Requirement already satisfied: language-data>=1.2 in /usr/local/lib/python3.10/dist-packages (from langcodes<4.0.0,>=3.2.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.2.0)
Requirement already satisfied: annotated-types>=0.4.0 in /usr/local/lib/python3.10/dist-packages (from pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.7.0)
Requirement already satisfied: pydantic-core==2.20.1 in /usr/local/lib/python3.10/dist-packages (from pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.20.1)
Requirement already satisfied: typing-extensions>=4.6.1 in /usr/local/lib/python3.10/dist-packages (from pydantic!=1.8,!=1.8.1,<3.0.0,>=1.7.4->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (4.12.2)
Requirement already satisfied: charset-normalizer<4,>=2 in /usr/local/lib/python3.10/dist-packages (from requests<3.0.0,>=2.13.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.3.2)
Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests<3.0.0,>=2.13.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.7)
Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.10/dist-packages (from requests<3.0.0,>=2.13.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.0.7)
Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.10/dist-packages (from requests<3.0.0,>=2.13.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2024.7.4)
Requirement already satisfied: blis<0.8.0,>=0.7.8 in /usr/local/lib/python3.10/dist-packages (from thinc<8.3.0,>=8.2.2->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.7.11)
Requirement already satisfied: confection<1.0.0,>=0.0.1 in /usr/local/lib/python3.10/dist-packages (from thinc<8.3.0,>=8.2.2->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.1.5)
Requirement already satisfied: click>=8.0.0 in /usr/local/lib/python3.10/dist-packages (from typer<1.0.0,>=0.3.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (8.1.7)
Requirement already satisfied: shellingham>=1.3.0 in /usr/local/lib/python3.10/dist-packages (from typer<1.0.0,>=0.3.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.5.4)
Requirement already satisfied: rich>=10.11.0 in /usr/local/lib/python3.10/dist-packages (from typer<1.0.0,>=0.3.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (13.7.1)
Requirement already satisfied: cloudpathlib<1.0.0,>=0.7.0 in /usr/local/lib/python3.10/dist-packages (from weasel<0.5.0,>=0.1.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.18.1)
Requirement already satisfied: smart-open<8.0.0,>=5.2.1 in /usr/local/lib/python3.10/dist-packages (from weasel<0.5.0,>=0.1.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (7.0.4)
Requirement already satisfied: MarkupSafe>=2.0 in /usr/local/lib/python3.10/dist-packages (from jinja2->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.1.5)
Requirement already satisfied: marisa-trie>=0.7.7 in /usr/local/lib/python3.10/dist-packages (from language-data>=1.2->langcodes<4.0.0,>=3.2.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.2.0)
Requirement already satisfied: markdown-it-py>=2.2.0 in /usr/local/lib/python3.10/dist-packages (from rich>=10.11.0->typer<1.0.0,>=0.3.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (3.0.0)
Requirement already satisfied: pygments<3.0.0,>=2.13.0 in /usr/local/lib/python3.10/dist-packages (from rich>=10.11.0->typer<1.0.0,>=0.3.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (2.16.1)
Requirement already satisfied: wrapt in /usr/local/lib/python3.10/dist-packages (from smart-open<8.0.0,>=5.2.1->weasel<0.5.0,>=0.1.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (1.14.1)
Requirement already satisfied: mdurl~=0.1 in /usr/local/lib/python3.10/dist-packages (from markdown-it-py>=2.2.0->rich>=10.11.0->typer<1.0.0,>=0.3.0->spacy<3.8.0,>=3.7.2->en-core-web-md==3.7.1) (0.1.2)
Installing collected packages: en-core-web-md
Successfully installed en-core-web-md-3.7.1
✔ Download and installation successful
You can now load the package via spacy.load('en_core_web_md')
⚠ Restart to reload dependencies
If you are in a Jupyter or Colab notebook, you may need to restart Python in
order to load all the package's dependencies. You can do this by selecting the
'Restart kernel' or 'Restart runtime' option.

nlp = en_core_web_md.load()
     

# Define a custom stopwords list
custom_stop_words = set(stopwords.words('english')).union(set([
    'datum', 'work', 'experience', 'year', 'job', 'business', 'require',
    'position', 'include', 'support', 'provide', 'opportunity',
    'status', 'employee', 'role', 'applicant', 'company', 'candidate',
    'process', 'project', 'information', 'responsibility',
    'service', 'system', 'use', 'skill', 'requirement', 'ability', 'client',
    'location', 'level', 'education', 'benefit', 'qualification',
    'application', 'need', 'program', 'offer', 'employment',
    'duty'
]))

good_pos = ['NOUN','VERB','ADJ','ADV']

def cleanTextAndLemmatize(s):
    if isinstance(s, str):
        s = s.lower()
        s = re.sub(r'[^\w\s]', '', s)
        tokens = word_tokenize(s)

        # lemmatize
        doc = nlp(' '.join(tokens))

        return ' '.join([w.lemma_ for w in doc if w.pos_ in good_pos and w.text not in custom_stop_words])
    return ''  # Return empty string for non-string values

df1['cleaned_job_desc'] = df1['job_desc'].apply(cleanTextAndLemmatize)
     

df1['cleaned_job_desc']
     
0      summary data analyst available department medi...
1                                                       
2                                                       
3      graduate student datum analyst integral member...
4      perform duty associate address change create v...
                             ...                        
877                                                     
883                                                     
889                                                     
891                                                     
892                                                     
Name: cleaned_job_desc, Length: 992, dtype: object
Convert Text Data to TF-IDF matrix

vec = TfidfVectorizer()

matrix = vec.fit_transform(df1['cleaned_job_desc'])
     

# Get the feature names (words) and their TF-IDF scores
feature_names = vec.get_feature_names_out()

tfidf_scores = matrix.sum(axis=0).A1

# Create a dictionary of words and their TF-IDF scores
word_scores = {word: score for word, score in zip(feature_names, tfidf_scores)}

# Sort the dictionary by scores in descending order
sorted_word_scores = dict(sorted(word_scores.items(), key=lambda item: item[1], reverse=True))
     

import matplotlib.pyplot as plt
from wordcloud import WordCloud

wordcloud = WordCloud(width=800, height=400, background_color='white').generate_from_frequencies(sorted_word_scores)

# Display the word cloud
plt.figure(figsize=(10, 5))
plt.imshow(wordcloud, interpolation='bilinear')
plt.axis('off')
plt.show()
     

Unsupervised Learning with Latent Dirichlet Allocation (LDA)
What is LDA?
Latent Dirichlet Allocation (LDA) is a generative probabilistic model used for topic modeling. It assumes that each document is a mixture of topics and that each topic is a mixture of words. The goal of LDA is to infer the hidden topic structure from the observed words in the documents.

What is the model doing in the background?
Imagine we have a bunch of job descriptions, but they contain some common, unimportant words like "the," "and," or "company." The first step is to remove these words to focus on the more important ones.

After cleaning, each job description is broken down into individual words.

We create a list where each unique word gets a unique ID number. This is like making a dictionary where each word has a number next to it.

We tell the model how many categories (topics) we want to find. The model then tries to group the words into these topics. It does this by looking at the words in all the job descriptions and figuring out which words often appear together.

The model goes through the text multiple times to refine these groupings until it stabilizes and is satisfied with the results.

After training, the model provides a list of topics. Each topic is represented by a group of words that frequently appear together in the job descriptions. For example, one topic might be characterized by words like "analysis," "report," and "data," indicating it's related to data analysis tasks.


from gensim.test.utils import common_texts
from gensim.corpora.dictionary import Dictionary
from gensim.models import LdaModel

# Define stop words to exclude
stop_words = set(stopwords.words('english')).union(set([
    'datum', 'work', 'experience', 'year', 'job', 'business', 'require',
    'position', 'include', 'support', 'provide', 'opportunity',
    'status', 'employee', 'role', 'applicant', 'company', 'candidate',
    'process', 'project', 'information', 'responsibility',
    'service', 'system', 'use', 'skill', 'requirement', 'ability', 'client',
    'location', 'level', 'education', 'benefit', 'qualification',
    'application', 'need', 'program', 'offer', 'employment',
    'duty', 'pay', 'range'
]))

# Preprocess the text to remove stop words
def preprocess(text):
    return [word for word in text if word not in stop_words]

common_texts = df1['cleaned_job_desc'].map(str).str.split().apply(preprocess).tolist()

common_dictionary = Dictionary(common_texts)
common_corpus = [common_dictionary.doc2bow(text) for text in common_texts]

num_topics= 15

lda = LdaModel(common_corpus, num_topics = num_topics, id2word=common_dictionary, passes=50)
     
Topic Results

# Display the topics
for idx, topic in lda.print_topics(-1):
    print(f"Topic: {idx} \nWords: {topic}\n")

# Visualize the topics using word clouds
for t in range(lda.num_topics):
    plt.figure()
    plt.imshow(WordCloud().fit_words(dict(lda.show_topic(t, 50))))
    plt.axis("off")
    plt.title(f"Topic #{t}")
    plt.show()
     
Topic: 0 
Words: 0.011*"team" + 0.007*"compensation" + 0.006*"employer" + 0.006*"analyst" + 0.006*"disability" + 0.005*"technology" + 0.005*"product" + 0.005*"part" + 0.005*"equal" + 0.005*"make"

Topic: 1 
Words: 0.012*"report" + 0.010*"analysis" + 0.009*"perform" + 0.009*"management" + 0.008*"analyst" + 0.008*"knowledge" + 0.006*"office" + 0.005*"analyze" + 0.005*"assist" + 0.005*"state"

Topic: 2 
Words: 0.020*"college" + 0.019*"degree" + 0.019*"accredit" + 0.018*"field" + 0.017*"computer" + 0.017*"science" + 0.013*"protect" + 0.013*"title" + 0.013*"fulltime" + 0.012*"university"

Topic: 3 
Words: 0.016*"federal" + 0.014*"document" + 0.013*"apply" + 0.012*"complete" + 0.011*"base" + 0.010*"resume" + 0.010*"meet" + 0.009*"accredit" + 0.009*"receive" + 0.009*"submit"

Topic: 4 
Words: 0.019*"state" + 0.009*"reporting" + 0.009*"federal" + 0.007*"product" + 0.007*"customer" + 0.006*"base" + 0.006*"team" + 0.006*"ensure" + 0.005*"functional" + 0.005*"well"

Topic: 5 
Words: 0.015*"examination" + 0.011*"department" + 0.009*"county" + 0.008*"list" + 0.008*"minimum" + 0.006*"receive" + 0.006*"degree" + 0.006*"resource" + 0.006*"state" + 0.006*"eligible"

Topic: 6 
Words: 0.019*"state" + 0.012*"disability" + 0.010*"accommodation" + 0.008*"medical" + 0.007*"reasonable" + 0.007*"also" + 0.007*"individual" + 0.007*"equal" + 0.007*"gender" + 0.007*"law"

Topic: 7 
Words: 0.012*"analyst" + 0.012*"management" + 0.010*"capital" + 0.008*"team" + 0.007*"financial" + 0.006*"office" + 0.006*"cost" + 0.005*"least" + 0.005*"make" + 0.005*"analysis"

Topic: 8 
Words: 0.011*"disability" + 0.010*"team" + 0.010*"analyst" + 0.009*"gender" + 0.008*"equal" + 0.008*"protect" + 0.007*"employer" + 0.007*"race" + 0.007*"orientation" + 0.007*"religion"

Topic: 9 
Words: 0.015*"salary" + 0.012*"type" + 0.012*"fulltime" + 0.009*"compensation" + 0.009*"schedule" + 0.009*"shift" + 0.008*"remote" + 0.008*"environmental" + 0.007*"bargaining" + 0.006*"description"

Topic: 10 
Words: 0.014*"management" + 0.012*"analyst" + 0.010*"report" + 0.010*"shelter" + 0.009*"maintain" + 0.008*"data" + 0.008*"month" + 0.008*"quality" + 0.007*"analysis" + 0.007*"type"

Topic: 11 
Words: 0.024*"submit" + 0.020*"resume" + 0.016*"date" + 0.015*"veteran" + 0.015*"preference" + 0.014*"document" + 0.011*"claim" + 0.011*"federal" + 0.009*"active" + 0.009*"copy"

Topic: 12 
Words: 0.012*"energy" + 0.009*"eversource" + 0.006*"appointment" + 0.006*"renewable" + 0.005*"safety" + 0.005*"national" + 0.005*"sponsorship" + 0.004*"class" + 0.004*"eligibility" + 0.004*"emergency"

Topic: 13 
Words: 0.019*"team" + 0.014*"analyst" + 0.008*"analysis" + 0.007*"technology" + 0.007*"solution" + 0.006*"analytic" + 0.006*"development" + 0.006*"customer" + 0.006*"environment" + 0.006*"join"

Topic: 14 
Words: 0.025*"health" + 0.015*"care" + 0.010*"research" + 0.009*"clinical" + 0.007*"team" + 0.007*"analyst" + 0.007*"community" + 0.007*"patient" + 0.007*"healthcare" + 0.005*"member"
















Key Takeaways - Most Important Topics:

-- Topic #1: "report, analysis, perform, management, analyst, knowledge, office, analyze, assist, state"

This topic clearly aligns with the typical responsibilities of a data analyst, including generating reports, performing data analysis, managing data-related tasks, and assisting with analytical needs.
-- Topic #10: "management, analyst, report, shelter, maintain, data, month, quality, analysis, type"

This topic is highly relevant to data analysts, focusing on management, reporting, data maintenance, and quality analysis.
Additionally, Topics #7 & #13 highlight important aspects like financial analysis, team collaboration, and technological solutions, which are also crucial for data analysts.
