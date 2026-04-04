# Day 18 - Web Scraping to DataFrame

## Resources
Video Link: https://www.youtube.com/watch?v=8NOdgjC1988

---

## Notebook: day18.ipynb

### Lesson Overview
Extract structured data from websites using BeautifulSoup HTML parsing and create organized DataFrames.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import pandas as pd, requests, numpy as np`
- `from bs4 import BeautifulSoup` - HTML parsing library

**Cell 2: Fetch webpage**
- `webpage = requests.get('https://www.ambitionbox.com/list-of-companies?page=1').text`
- Get raw HTML content from website

**Cell 3: Parse HTML**
- `soup = BeautifulSoup(webpage, 'lxml')` - Create parsed HTML object using lxml parser

**Cell 4: Pretty print HTML**
- `soup.prettify()` - Format and display HTML structure for analysis

**Cell 5: Find specific element**
- `soup.find_all('h1')[0].text` - Extract text from first H1 heading
- `find_all()` - Returns list of all matching elements
- `.text` - Extract text content

**Cell 6: Extract company names**
- Loop through H2 tags: `for i in soup.find_all('h2'): print(i.text.strip())`
- `.strip()` - Remove whitespace

**Cell 7: Extract paragraphs**
- Loop through P tags extracting text content

**Cell 8: Count ratings**
- `len(soup.find_all('p', class_='rating'))` - Find elements with specific class

**Cell 9: Count reviews**
- `len(soup.find_all('a', class_='review-count'))` - Target specific HTML elements by class

**Cell 10-12: Extract data from containers**
- `soup.find_all('div', class_='company-content-wrapper')` - Find parent containers
- Extract nested data for each company:
  - Name: `i.find('h2').text.strip()`
  - Rating: `i.find('p', class_='rating').text.strip()`
  - Reviews: `i.find('a', class_='review-count').text.strip()`
  - Details: `i.find_all('p', class_='infoEntity')[index].text.strip()`

**Cell 13-18: Error handling**
- Try-except blocks for robust extraction
- Use `np.nan` for missing values
- Handle missing HTML elements gracefully

**Cell 19: Create DataFrame**
- Combine lists into DataFrame with columns:
  - name, rating, reviews, company_type, headquarters, company_age, employees

**Cell 20-25: Pagination loop**
- `for j in range(1, 1001)` - Loop through 1000 pages
- Repeat extraction for each page
- `final = final.append(df, ignore_index=True)` - Accumulate results

### Key Methods:
- `requests.get()` - Fetch webpage HTML
- `BeautifulSoup()` - Parse HTML
- `find()` / `find_all()` - Element selection
- `.text.strip()` - Extract clean text
- Try-except - Error handling
- `np.nan` - Handle missing data

### Important Concepts:
- CSS class and tag selection for targeted extraction
- Nested element navigation
- Error handling for missing HTML elements
- Try-except patterns for web scraping robustness
