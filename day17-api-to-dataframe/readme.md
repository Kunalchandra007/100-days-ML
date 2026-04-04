# Day 17 - API to DataFrame

## Resources
TMDB API : https://developers.themoviedb.org/
RapidAPI : https://rapidapi.com/collection/list-of-free-apis
JSON Viewer: http://jsonviewer.stack.hu/

---

## Notebook: day17.ipynb

### Lesson Overview
Fetch data from REST APIs, handle pagination, and build comprehensive DataFrames from multiple API requests.

### Code Cells Explanation:

**Cell 1: Import libraries**
- `import pandas as pd, requests` - HTTP requests and data manipulation

**Cell 2: Single API request**
- `response = requests.get('https://api.themoviedb.org/3/movie/top_rated?api_key=...&page=1')`
- Fetch JSON response from The Movie Database API

**Cell 3: Extract and transform data**
- `response.json()['results']` - Extract results from JSON response
- `pd.DataFrame(...)` - Convert list of dictionaries to DataFrame
- Select specific fields: `[['id','title','overview','release_date','popularity','vote_average','vote_count']]`

**Cell 4: View results**
- `df.head()` - Display first few rows of API data

**Cell 5: Initialize empty DataFrame**
- `df = pd.DataFrame()` - Create empty container for accumulating API results

**Cell 6: Pagination loop**
- `for i in range(1, 429)` - Loop through 428 pages of API results
- `requests.get(url.format(i))` - Fetch each page with pagination parameter
- `df = df.append(temp_df, ignore_index=True)` - Accumulate results

**Cell 7: DataFrame from multiple pages**
- `df.head()` - View complete dataset after pagination

**Cell 8: Dataset dimensions**
- `df.shape` - Returns (rows, columns) - verify complete dataset loaded

**Cell 9: Save to CSV**
- `df.to_csv('movies.csv')` - Export collected data to CSV file for future use

### Key Concepts:
- API pagination handles large result sets
- JSON structure parsing and transformation
- DataFrame accumulation across multiple requests
- Data export for offline analysis
- Handling API rate limits and response structure

### Methods:
- `requests.get()` - HTTP GET requests
- `response.json()` - Parse JSON responses
- `pd.DataFrame()` - Create/initialize DataFrames
- `df.append()` - Accumulate results
- `df.to_csv()` - Export data
