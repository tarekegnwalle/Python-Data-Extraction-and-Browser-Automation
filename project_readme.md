# Python Data Extraction and Browser Automation Project

## Overview
This project demonstrates an end-to-end data extraction and browser automation workflow using Python. It utilizes **Selenium** to launch and control an automated Google Chrome browser session, navigates to a target webpage, extracts specific data fields (quotes and authors), structures the raw data using **Pandas**, and exports the final dataset into a clean CSV file.

## Features
- **Browser Automation:** Automated launch and navigation of Google Chrome via Selenium WebDriver and `webdriver-manager`.
- **Web Scraping:** Dynamic extraction of web elements using CSS selectors.
- **Data Manipulation:** Cleaning and structuring raw text data into a Pandas DataFrame.
- **Data Export:** Persisting the structured dataset into a comma-separated values (`.csv`) file format.

## Technology Stack
- **Python** (Core programming language)
- **Selenium** (Browser automation and element location)
- **WebDriver Manager** (Automated ChromeDriver management)
- **Pandas** (Data manipulation, analysis, and CSV export)
- **Jupyter Notebook** (Interactive development environment)

## Project Workflow & Implementation Steps

### 1. Environment Setup & Dependencies Installation
First, install the required third-party Python packages inside your environment:
```bash
pip install selenium webdriver-manager pandas
```

### 2. Importing Libraries
```python
import time
import pandas as pd
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
```

### 3. Initializing the Browser Driver
```python
service = Service(ChromeDriverManager().install())
driver = webdriver.Chrome(service=service)
```

### 4. Navigating to the Target Page and Extracting Data
```python
url = "https://quotes.toscrape.com/"
driver.get(url)
time.sleep(2) # Allow page content to render

quote_elements = driver.find_elements(By.CSS_SELECTOR, ".quote")
extracted_data = []

for el in quote_elements:
    try:
        text = el.find_element(By.CSS_SELECTOR, ".text").text
        author = el.find_element(By.CSS_SELECTOR, ".author").text
        extracted_data.append({
            "Quote": text,
            "Author": author
        })
    except Exception as e:
        continue

driver.quit()
```

### 5. Structuring and Exporting Data with Pandas
```python
df = pd.DataFrame(extracted_data)
display(df)

df.to_csv("extracted_quotes.csv", index=False)
print("Data successfully saved to 'extracted_quotes.csv'!")
```

## Author
**Tarekegn Walle**  
*Data Analyst, Information Systems Professional, and University Lecturer*