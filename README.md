# IBM Capstone Project: Job Market Analysis & Salary Insights

---

## Project by: Arihant Bhuyan

---

### Overview

This project analyzes the demand for job skills and technologies in the US job market by utilizing datasets from IBM. The data includes key job market indicators, programming languages, and databases that respondents wish to learn. The project uses various data extraction methods (API calls and web scraping) and Python data processing techniques to perform exploratory data analysis (EDA) and visualize insights. The analysis primarily focuses on job availability, compensation, and demographic breakdowns across multiple dimensions.

---

### Table of Contents

1. Dataset Overview
2. Technologies and Skills in Demand
3. Web Scraping Insights
4. Survey Data Exploration Lab
5. Outliers Detection and Cleaned Data
6. Visualizations
7. Conclusions

---

### Dataset Overview

This project makes use of multiple datasets related to job skills and compensation. The data is retrieved via an API and web scraping, covering job roles, key skills, location, compensation frequency, and additional demographic details like gender and age.

Key attributes include:

- **Key Skills**: Programming languages and technologies.
- **Location**: Where the job postings are from.
- **Compensation Frequency**: Yearly, Monthly, Weekly.
- **Compensation**: The normalized annual compensation of respondents.

---

# Technologies and Skills in Demand

## API Data Retrieval

An API call was made to retrieve job data. The function `get_number_of_jobs_T(technology)` was used to filter job postings based on specific technologies (e.g., Python).

## API Usage and Data Processing

The API call fetches data in **JSON** format, which is common for web APIs returning structured data. The process checks if the API request is successful before attempting to extract the data, ensuring error-free execution. **JSON** is then parsed into Python data structures (like dictionaries and lists) for easy manipulation.

### Counting Jobs by Technology

- **Technology Search Logic**:
  - The function `get_number_of_jobs_T()` uses `lower()` to make the technology search case-insensitive. This ensures that technologies like "Python" and "python" are counted regardless of how they are written in the job postings.
  - It counts only the jobs where the technology keyword appears in the "Key Skills" field.

- **Python-Specific Outcome**:
  - The function returns that there are **1,173 job postings** that specifically mention Python as a key skill. This can help someone assessing demand for specific technologies like Python in the job market.

### Counting Jobs by Location

- **Location Search Logic**:
  - Similar to the technology search, the function `get_number_of_jobs_L()` checks for a match in the "Location" field. It’s case-insensitive and iterates through each job posting to find the number of times the given location appears.

- **Los Angeles-Specific Outcome**:
  - The analysis shows that there are **640 jobs available in Los Angeles**. This data can be useful for job market analysis in specific regions.

## Insights and Use Cases

- **Job Market Demand for Python**: With **1,173 job postings** requiring Python skills, it's evident that Python is a highly demanded skill in the job market, particularly in the technology and software sectors.
  
- **Location-Based Job Distribution**: Knowing there are **640 jobs** available in Los Angeles provides insights into how opportunities are distributed geographically. Similar analysis can be done for other regions.

This code can be expanded to analyze trends across different locations, technologies, and even time frames if the dataset contains temporal data.

---

## Web Scraping Insights

This portion of the code involves scraping data from an HTML table containing salary information for various programming languages. The following components are analyzed:

### Web Scraping Process:
- **URL Extraction**: The `requests` library is used to pull the raw HTML data from a specified URL.
- **BeautifulSoup**: The data is parsed using BeautifulSoup's `html.parser` to navigate and extract the relevant portions from the HTML structure.
- **Table Extraction**: The code locates the first `<table>` tag, extracts its rows (`<tr>`), and then iterates through each row to extract language names and their corresponding salaries.

### Outcome:
- **Languages and Average Salaries**:
  - The scraped data reveals the following average annual salaries for different programming languages:
    - Python: $114,383
    - Java: $101,013
    - R: $92,037
    - Javascript: $110,981
    - Swift: $130,801
    - C++: $113,865
    - PHP: $84,793
    - SQL: $94,082

  This data gives a rough idea of how these programming languages compare in terms of average annual salary.

### Analysis:
- **Salary Insights**:
  - Swift developers appear to have the highest average salary in the dataset, while PHP developers earn the lowest.
  - Python and Java are on the higher end, reflecting their popularity and broad use in both web development and data science.

- **Real-World Application**:
  - This scraped salary data can be useful for job seekers and companies to benchmark salaries based on language specialization, helping guide decisions about skill development or hiring.

### Limitations of Web Scraping:
- **Outdated Data**: Since this is a static HTML page, the data may not reflect the latest trends. Using dynamic, real-time sources might offer more accurate insights.
- **Table Structure Dependence**: If the HTML structure of the page changes, the scraping code will need to be adjusted to continue working effectively.

---

# Survey Dataset Exploration Lab

## 1. Dataset Overview
- The dataset contains **11,552 rows and 85 columns**, representing data collected from a global survey of software developers. Key columns include age, country, employment status, and opinions on open-source contributions, among others.

### 2. Geographical Diversity
- There are **135 unique countries** represented, highlighting the global scale of this survey. This opens up opportunities for regional analysis, allowing us to observe trends in employment, education, and compensation across different geographic areas.

### 3. Data Structure
- The dataset features numerical columns such as age (`float64`), which can be analyzed for statistical insights like mean, median, and distribution. The presence of both categorical and numerical data means that we can explore a wide range of developer demographics and experiences.
- **Missing Data**: Before further analysis, it is essential to handle missing values, which can be done by dropping or imputing where necessary to ensure data integrity.

---

## Data Wrangling Process

### 1. Loading the Dataset into a DataFrame:
- The dataset is loaded from a URL using `pd.read_csv()`, which brings in the data for wrangling and analysis.

### 2. Displaying Columns:
- The command `df.columns.tolist()` is used to list all the column names for a better understanding of the structure of the dataset.

**Summary**: It's essential to understand the structure of the dataset before cleaning it, ensuring we know what data is available and if there are any columns that may be redundant or that we want to focus on.

### 3. Checking for Duplicate Rows:
- Duplicates are checked using the `duplicated()` method.
  - This reveals that **154 duplicate entries** exist in the column "Respondent." You then display these duplicates.

**Summary**: Handling duplicates is important for data integrity. These duplicates could skew results, especially when analyzing survey data where each respondent should ideally be unique.

### 4. Missing Values:
- The code checks for missing values in each column using `isnull().sum()`.
  - The data shows significant missing values in some columns like **Sexuality (542)**, **Ethnicity (675)**, **Dependents (140)**, and **SurveyEase (14)**.

**Summary**: Missing data can be critical. In this case, columns such as Sexuality and Ethnicity are missing a large proportion of their values, which could affect any demographic analysis.

### 5. Work Location Analysis:
- The `WorkLoc` column contains categorical data about work locations. Missing values are filled with the most frequent value, which in this case is "Office".

**Summary**: Filling missing values with the most frequent category (mode imputation) is a common technique. In this case, "Office" being the most frequent work location aligns with expectations for a survey about professional developers.

### 6. Normalizing Annual Compensation:
- The dataset includes information about compensation, with the compensation frequency varying between **Yearly**, **Monthly**, and **Weekly**. The normalization is performed to standardize all compensation data into a yearly figure.

**Summary**: This normalization allows for consistent analysis of compensation. After normalization, the **median annual compensation** was calculated to be **$100,000**.

---

### Key Takeaways from the Data Wrangling Process:
- **Duplicates**: There are **154 duplicate rows** in the dataset that need to be addressed. Removing or handling duplicates ensures that our analysis isn't skewed by repeated data.
- **Missing Values**: Several columns have substantial missing data, notably in demographic fields like Sexuality and Ethnicity, which could limit certain types of demographic insights.
- **Compensation Normalization**: Converting all compensation data to a yearly frequency allows for standardized analysis, which is critical when dealing with financial information. The **median annual compensation** of **$100,000** gives a good overview of what respondents in this survey earn on average.

This overall approach ensures that the data is clean, consistent, and ready for meaningful analysis, improving the accuracy of any conclusions drawn from it.

---

## Exploratory Data Analysis

### Distribution of Converted Compensation
The first chart represents the distribution of **converted compensation** (i.e., salary). It reveals that the majority of respondents have a compensation in the lower range. The histogram shows a **right-skewed distribution**, meaning that most people earn on the lower side, with a few outliers who earn substantially more.

- The peak of the distribution is near the left, suggesting that most compensations fall below **$100,000**.
- There are outliers with compensations going up to **$2 million**, which we would analyze further.

# Five-Number Summary for Age

---

The next analysis focuses on a five-number summary of age for respondents who identified as men. The key statistics include:
- **Minimum Age**: 16 years
- **1st Quartile (Q1)**: 25 years (25% of respondents are younger than 25)
- **Median Age**: 29 years (half of the respondents are younger than 29)
- **3rd Quartile (Q3)**: 35 years (75% are younger than 35)

The statistics show a relatively young population, with the majority of respondents in the tech field between **25 to 35 years old**.

---

## Median Converted Compensation by Gender

We also analyzed the **median compensation** for men and women. The results:
- **Men**: Median compensation is **$57,745.0**
- **Women**: Median compensation is **$57,788.0**

Interestingly, both genders have nearly identical median compensations, highlighting potential parity in pay in this dataset, though further insights into the sample size would be necessary for more accuracy.

---

## Outliers in Compensation

Next, we removed outliers in compensation using the **Interquartile Range (IQR)** method. Outliers were defined as compensations outside **1.5 times the IQR**. There were **879 outliers identified**, which were then removed to create a cleaned dataset.

After removing outliers, the dataset now contains **9,783 rows** compared to the original **11,552 rows**. This shows that a significant number of rows were excluded due to extremely high compensations.

---

## Correlation Analysis

Finally, we examined the correlation between various numeric features and age. The most notable correlations are:
- **Converted Compensation**: 0.105 (a weak positive correlation with age)
- **WorkWeekHrs**: 0.036 (little to no correlation with age)
- **CodeRevHrs**: -0.020 (a slight negative correlation with age)

This indicates that **age** has a slight positive correlation with **compensation**, meaning older respondents tend to earn more, but the effect is minimal.

---

## Summary of Insights

- **Compensation Distribution**: Most respondents earn less than **$100,000**, but there are outliers earning up to **$2 million**.
- **Age Statistics**: The tech workforce is primarily young, with the **median age being 29**.
- **Gender Compensation**: Both men and women have almost the same median compensation, indicating little difference in pay based on gender.
- **Outliers**: Outliers were identified and removed from the dataset to improve analysis reliability.
- **Correlations**: There is a weak correlation between age and compensation, with age having minimal influence on working hours or code review hours.

---

# Visualizations

---

## 1. Compensation Distribution:
The following histogram illustrates the distribution of compensation across respondents:
- The majority of respondents have an annual compensation between **$0 - $250,000**.

---

## 2. Age Distribution:
A boxplot was used to visualize the age distribution of respondents:
- The **median age is 29 years**, with most respondents falling between **25 and 35 years**. There are a few outliers aged above **50 years**.

---

## 3. Scatter Plot - Work Week vs Code Review Hours:
A scatter plot was created to show the correlation between weekly work hours and code review hours:
- Most respondents spend **0 to 50 hours** on code reviews and work **0 to 40 hours** per week.

---

## 4. Pie Chart - Top 5 Databases Respondents Wish to Learn:
The pie chart below shows the top databases respondents wish to learn next year, with **PostgreSQL** leading at **24.8%**.

---

## Conclusions

---

This project provides valuable insights into the job market demand for programming languages, compensation patterns, and the technologies professionals want to learn. Key takeaways include:

- **Python** is a highly sought-after skill with **1,173 job postings** and an average salary of **$114,383**.
- **PostgreSQL** is the most desired database for respondents to learn, with **24.8%** of them showing interest.
- **Median compensation** across the dataset was **$100,000**, with a noticeable right-skew in the income distribution.
- **Outliers in compensation data** were effectively identified and removed, ensuring a more accurate analysis.
- **Age and Work Week Hours** show that most professionals are younger than 30 and work less than 40 hours per week on average.

This analysis helps professionals and employers understand trends in skills, compensation, and job demand across different regions and demographics.

