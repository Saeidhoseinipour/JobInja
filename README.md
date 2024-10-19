# 🧰 Jobinja Web Scraper 🧑‍💻🔍

## Overview

This project is a 🐍 Python-based web scraper designed to systematically extract 📝 job listings from the Jobinja 🌐 website. The scraper 🗃️ collects, 🔄 preprocesses, and 🧽 cleanses data, saves it in multiple 📁 formats, and performs elementary 📊 descriptive statistics. The following sections provide an in-depth 📋 description of the core components of the class, along with illustrative examples of the results.

The purpose of this scraper is to facilitate efficient data extraction from the Jobinja 🌐 website, thereby automating the traditionally labor-intensive ⛏️ task of gathering job-related 📝 data. The scraper not only extracts raw information but also transforms it into structured, machine-readable formats 🖥️ for further analysis. By enabling customization of output formats, users can derive insights specific to their needs, supporting data-driven 📈 decision-making in the employment domain. Ultimately, this project aims to automate data collection and offer robust access to high-quality 🔍 data that supports the analytical process.

The web scraper’s modularity enables it to adapt to different sections of the 🌐 website, allowing for a targeted 🎯 approach based on job categories, employment types, or other user-specific criteria. By leveraging automation, this tool alleviates the repetitive 🔁 nature of manual job searching. It can aggregate information on job titles, companies, locations, required qualifications, and additional metadata, thereby empowering users to make well-informed career 💼 decisions. By structuring the data efficiently, users can conduct trend analysis, compare opportunities, and even create predictive models 📊 for emerging job market trends.

The data extracted by the scraper can further be used to build analytical dashboards 📊, generate comprehensive reports 📑, or be utilized in machine learning 🤖 models to identify optimal employment opportunities. This makes the scraper a valuable tool for data scientists 🧠, job market analysts 📊, and individuals interested in automating their job search processes.

## 📦 Class Overview

The `Jobinja` class offers functionalities to scrape, preprocess, and manage data extracted from the Jobinja platform 🌐. The class design ensures effective and efficient extraction of all key components associated with job listings. Additionally, the modular structure allows for extension and adaptation, facilitating scraping of other similar platforms or the integration of new features.

### `Jobinja` Class Methods

The `Jobinja` class comprises several key methods, each of which plays a pivotal role in the data extraction pipeline:

- **`__init__()`**: 🏗️ Initializes the scraper, sets HTTP headers 📨 to simulate browser requests, creates necessary directories 📂 for data storage, and configures logging 📜 for capturing errors. This setup guarantees that all prerequisites are in place for seamless scraper operation.
  
- **`get_links()`**: Gathers unique 🔗 hyperlinks from the main page, which serve as entry points for crawling 🕷️ job listings. This method sends an initial GET request to the Jobinja website 🌐 and parses the HTML to identify subpages containing job information. The use of a queue 📥 facilitates efficient link management, supporting breadth-first crawling.

- **`clean_persian_text(text)`**: Cleanses Persian 📝 text by removing extraneous whitespace and non-Persian characters. This preprocessing step ensures data quality, consistency, and standardization, which are vital for subsequent analytical procedures.

- **`extract_job_features(subpage_soup)`**: Extracts job-specific features such as job title 📛, description 📄, category 📂, location 📍, employment type 👨‍💼, and more. This method identifies relevant HTML elements where job information resides and processes the text to generate a structured output. This approach ensures that all relevant attributes are accurately captured and standardized.

- **`scrape_jobs()`**: Iterates 🔄 over collected hyperlinks to visit each job listing, invokes the `extract_job_features` method to gather relevant data, and subsequently saves the cleaned data into text files 📝 for further processing or analysis. This method also incorporates error handling 🛠️ to log any issues that arise during requests and retries.

- **`save_dataset()`**: Saves the collected dataset into both `.mat` and `.json` formats 📁. The `.mat` format is tailored for MATLAB integration, while `.json` offers a versatile format suitable for web-based applications and advanced analytics.

- **`display_dataset()`**: Converts the dataset into a pandas DataFrame 📊, making it easy to visualize 👀, explore, and manipulate the data in a tabular format. This method is highly beneficial for conducting preliminary data analysis.

- **`descriptive_statistics()`**: Generates descriptive 📈 statistics for the dataset, providing an overview of features such as job title frequencies, distribution across job categories, and other key attributes. These statistics offer valuable initial insights that inform subsequent analysis.

### Method Details

1. **Initialization (`__init__`)**:
   - Configures HTTP headers to prevent request blocking 🚫 by mimicking a legitimate user agent.
   - Creates a designated save directory 🗂️ for data files.
   - Sets up a rotating file handler for logging 🔄 to ensure that log files do not grow indefinitely and overwhelm the system.

2. **Collecting Links (`get_links`)**:
   - Sends an HTTP GET request to the main page of the Jobinja platform 🌐.
   - Parses the HTML using BeautifulSoup 🍲 to locate all anchor (`<a>`) tags.
   - Uses a queue 📥 to maintain the order of links for breadth-first crawling, ensuring systematic coverage of the job listings.

3. **Cleaning Text (`clean_persian_text`)**:
   - Employs regular expressions 🔍 to remove non-Persian characters and extraneous whitespace.
   - Ensures that text data is consistent across the dataset, which is crucial for effective analysis and machine learning modeling 🤖.

4. **Extracting Job Features (`extract_job_features`)**:
   - Extracts features such as job title 📛, job description 📄, category 📂, and location 📍 from a subpage.
   - Stores the cleaned information in a structured dictionary 📑.
   - Handles missing fields by assigning default values to maintain dataset integrity and avoid potential issues during analysis.

5. **Scraping Jobs (`scrape_jobs`)**:
   - Iterates through each subpage link collected via `get_links()` 🔗.
   - Issues GET requests to each link and invokes `extract_job_features()` to collect and process relevant data.
   - Implements a delay ⏱️ between requests to prevent overwhelming the server and risking IP blocks.
   - Saves data in `.txt` files 📄, providing a straightforward and accessible format for users.

## ⚙️ Installation and Usage

To deploy the `Jobinja` scraper, follow these steps:

1. **Clone the Repository** 🐙
   ```bash
   git clone <repository-url>
   cd jobinja_scraper
   ```

2. **Install Dependencies** 📦
   Ensure you have the necessary Python libraries installed:
   ```bash
   pip install requests beautifulsoup4 scipy pandas
   ```

3. **Run the Script** 🚀
   To scrape job listings and save the dataset (saved in the `JobInja` directory 📁):
   ```bash
   python jobinja_scraper.py
   ```

4. **Customize the Scraper**:
   - Modify the `base_url` 🌐 to target different parts of the Jobinja website as required.
   - Adjust logging levels 📜 to capture more or less detail, depending on debugging needs.
   - Change the delay ⏱️ in the `scrape_jobs()` method to accommodate different server request limits.
   - Update `extract_job_features()` to capture additional fields or features relevant to the analysis.

## 📝 Example Output

### Extracted Job Features

An example of the output from a scraped job listing is shown below:

```
🔗 URL: https://jobinja.ir/companies/world-ocean-oil-company/jobs/A4VV/...
📝 Job_title: استخدام خانم
📄 Job_description: همین حالا رزومه خود را در کمتر از ۱۰ دقیقه بسازید...
📂 Job_category: فروش و بازاریابی
📍 Job_location: تهران
👨‍💼 Employment_type: تمام‌وقت
📆 Min_experience: 1 سال
💰 Salary: توافقی
🚻 Gender: خانم
🛡️ Military_status: معافیت دائم
🎓 Education_level: کارشناسی
🏢 Company_intro: شرکت اقیانوس جهانی نفت فعالیت خود را...
🛠️ Skills_required: تسلط به نرم‌افزارهای مایکروسافت آفیس
🔎 Content_snippet: همین حالا رزومه خود را در کمتر از ۱۰ دقیقه بسازید...
```

### Descriptive Statistics

Upon scraping job listings, the script can generate descriptive 📈 statistics for the dataset:

```
          job_title job_category job_location employment_type ...
count           50            50           50             50 ...
unique          30             8            6              3 ...
top     استخدام خانم     فروش و بازاریابی        تهران      تمام‌وقت ...
freq            10            20           18             25 ...
```

These descriptive statistics provide an overall view of the dataset, allowing users to understand the diversity of job listings and their respective distributions. By highlighting key trends—such as in-demand job categories or common employment types—the analysis can yield valuable insights for both job seekers and researchers.

## 🚀 Features to Improve

- **Adaptive Rate-Limiting**: Currently, a fixed delay of 1 second ⏱️ is added between requests to avoid overwhelming the server. This could be enhanced by implementing adaptive rate limiting that dynamically adjusts based on server response times, thus improving efficiency ⚡.
- **Error Logging Enhancements**: The logging mechanism 📜 employs a rotating file handler 🔄 to prevent log files from growing unchecked. More granular and detailed error messages would further facilitate debugging and improve the scraper's robustness.
- **Retry Mechanism**: Introducing a retry mechanism 🔁 for failed HTTP requests would significantly enhance the reliability of the scraper, particularly when scraping a large number of job listings, where transient network failures are common. This would improve the scraper's fault tolerance, ensuring more comprehensive data collection 📊.

## 📜 License

This project is licensed under the MIT License ⚖️, ensuring it is freely available for use, modification, and distribution. Contributions are welcomed 🤝, with the aim to foster collaboration and knowledge-sharing among those interested in web scraping, data analysis, and automation 🤖.

---

We invite contributions 🤲, suggestions for improvements 💡, and the use of this scraper for educational 🎓 or research purposes. Whether you aim to enhance your web scraping skills, automate job searches 🔍, or conduct research on labor market trends, this project offers a robust starting point 🚀. We welcome any improvements that can make the scraper more efficient, reliable, and useful. As a community, we look forward to evolving this tool to address emerging challenges and opportunities in data scraping and analysis 🧠.

