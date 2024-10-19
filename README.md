# 🧰 Jobinja Web Scraper 🧑‍💻🔍

## Overview

This project is a Python-based web scraper designed to extract job listings from the Jobinja website. It collects and cleans data, then saves it in various formats and performs basic descriptive statistics. The following sections describe the main components of the class, along with example snippets of the results.

The web scraper makes it easy for users to extract useful job information, automating the process of gathering employment opportunities from Jobinja. The scraper not only extracts information but also processes it to generate structured data that can be analyzed further. Users can customize the output data format, perform analysis, and derive insights from the data. The goal of this project is to facilitate data-driven decision-making in job hunting by automating data collection and providing efficient access to relevant information.

The scraper is versatile and can be adapted to scrape different parts of the website, allowing users to focus on specific types of jobs or categories. With this scraper, users can automate what would otherwise be a very time-consuming process of manually searching for jobs. It can gather information about job titles, company names, locations, required qualifications, and much more, helping job seekers make informed decisions. By having structured data readily available, users can analyze trends, compare opportunities, and even predict market changes.

The data extracted by the scraper can be used for building dashboards, generating reports, or feeding into machine learning models to predict the best job opportunities. This makes it a powerful tool for anyone interested in data science, job market analysis, or automating their job search.

## 📦 Class Overview

The `Jobinja` class provides functionalities to scrape, process, and manage data from the Jobinja website. It ensures that all key components of the job listings are extracted effectively. The class is modular, making it easy to extend and customize for other websites or additional features.

### `Jobinja` Class Methods

The `Jobinja` class contains several methods that play a crucial role in the data extraction process:

- **`__init__()`**: Initializes the scraper, sets up headers for requests to mimic a browser, creates the save directory for output data, and configures logging to capture errors effectively. This ensures that all necessary directories and configurations are in place before the scraper starts running.
  
- **`get_links()`**: Collects unique links from the main page for crawling. This method makes an initial request to the website and parses all the links to identify potential subpages containing job listings. It uses a queue system to manage the links efficiently, allowing for breadth-first crawling.

- **`clean_persian_text(text)`**: Cleans Persian text by removing extra spaces and non-Persian characters. This function is critical for maintaining data quality and ensuring that the extracted text is consistent and ready for analysis.

- **`extract_job_features(subpage_soup)`**: Extracts job-related information such as job title, job description, job category, location, employment type, etc., from a job listing page. It parses specific HTML elements where this information is typically located, ensuring that all important attributes of a job listing are captured accurately.

- **`scrape_jobs()`**: Scrapes job listings and saves the extracted data into text files. This method loops through the list of links collected, visits each link, and uses the `extract_job_features` method to gather relevant data. It also saves the data in a format that can be used for further analysis.

- **`save_dataset()`**: Saves the scraped dataset into `.mat` and `.json` files. The `.mat` format is useful for integration with MATLAB, while the `.json` format is versatile for web-based and data analysis applications.

- **`display_dataset()`**: Converts the dataset into a DataFrame for viewing. Using pandas, this method makes it easy to explore the dataset in a tabular form, which is ideal for initial data exploration.

- **`descriptive_statistics()`**: Generates descriptive statistics for the scraped dataset, providing quick insights such as the number of unique job titles, the distribution of job locations, and other categorical information.

### Method Details

1. **Initialization (`__init__`)**:
   - Configures headers to avoid getting blocked by the website.
   - Creates a save directory to ensure that output files are saved properly.
   - Sets up a rotating file handler for logging to prevent log files from growing indefinitely.

2. **Collecting Links (`get_links`)**:
   - Sends a GET request to the main page of the Jobinja website.
   - Parses the HTML using BeautifulSoup to find all links (`<a>` tags).
   - Uses a queue to maintain the order of links to be crawled, avoiding duplicates by using a set.

3. **Cleaning Text (`clean_persian_text`)**:
   - Uses regular expressions to remove unwanted characters, ensuring that only Persian text is retained.
   - Maintains consistency across the dataset, which is important for generating insights or applying machine learning models.

4. **Extracting Job Features (`extract_job_features`)**:
   - Extracts job-related features such as job title, description, category, and location.
   - Stores the cleaned Persian text in a dictionary for further analysis.
   - Handles missing fields by assigning default values to maintain data integrity.

5. **Scraping Jobs (`scrape_jobs`)**:
   - Iterates through each subpage link obtained from `get_links()`.
   - Sends GET requests and calls `extract_job_features()` to collect the required data.
   - Adds a delay between requests to avoid overwhelming the server.
   - Saves the scraped data in `.txt` files for easy access.

## ⚙️ Installation and Usage

To use the `Jobinja` scraper, follow these steps:

1. **Clone the Repository**
   ```bash
   git clone <repository-url>
   cd jobinja_scraper
   ```

2. **Install Dependencies**
   Ensure you have the following Python libraries installed:
   ```bash
   pip install requests beautifulsoup4 scipy pandas
   ```

3. **Run the Script**
   To scrape job listings and save the dataset (which will be saved in the `JobInja` directory):
   ```bash
   python jobinja_scraper.py
   ```

4. **Customize the Scraper**:
   - Modify the `base_url` parameter to target different parts of the Jobinja website.
   - Adjust logging settings to capture different levels of information.
   - Change the delay between requests in the `scrape_jobs()` method to accommodate website restrictions.
   - Update the `extract_job_features()` method to include new fields of interest.

## 📝 Example Output

### Extracted Job Features

An example of the output from a scraped job listing:

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

After collecting job listings, the script generates basic descriptive statistics for the dataset:

```
          job_title job_category job_location employment_type ...
count           50            50           50             50 ...
unique          30             8            6              3 ...
top     استخدام خانم     فروش و بازاریابی        تهران      تمام‌وقت ...
freq            10            20           18             25 ...
```

The descriptive statistics provide an overview of the dataset, helping users understand the variety of job listings and their distribution. This summary can highlight trends such as the most in-demand job categories or common employment types, providing valuable insights for job seekers and analysts.

## 🚀 Features to Improve

- **Rate-Limiting**: To avoid overwhelming the server, the scraper currently adds a delay of 1 second between requests. This could be improved by implementing adaptive rate limiting based on the server's response time.
- **Error Logging**: Errors are logged to a rotating file to prevent log files from growing indefinitely. Adding more detailed error messages could help in debugging specific issues.
- **Retry Mechanism**: Adding a retry mechanism for failed requests would improve reliability, especially for transient network issues. This would be particularly useful when scraping a large number of job listings, where occasional network failures are likely.

## 📜 License

This project is licensed under the MIT License, which means it is open-source and available for anyone to use, modify, and distribute. Contributions are welcome, and the goal is to foster collaboration and learning by making this tool accessible to anyone interested in web scraping or data analysis.

---

Feel free to contribute, suggest improvements, or use this scraper for educational purposes. Whether you are looking to improve your scraping skills, automate job searches, or conduct research on job market trends, this project provides a solid foundation to get started. Contributions are encouraged, and the project welcomes any enhancements that could make it more efficient, robust, and useful for the community. We look forward to seeing how the community can enhance and adapt this tool to meet new challenges and opportunities in data scraping and analysis.

