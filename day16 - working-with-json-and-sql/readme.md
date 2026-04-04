# Day 16 - Working with JSON and SQL

## Resources
Video link: https://www.youtube.com/watch?v=fFwRC-fapIU

Xampp download link: https://www.apachefriends.org/index.html
World dataset : https://www.kaggle.com/busielmorley/worldcities-pop-lang-rank-sql-create-tbls?select=world.sql
Pandas read_json documentation: https://pandas.pydata.org/docs/reference/api/pandas.read_json.html
Pandas read_sql_query documentation: https://pandas.pydata.org/docs/reference/api/pandas.read_sql_query.html#pandas.read_sql_query

---

## Notebook: day16.ipynb

### Lesson Overview
Learn to read JSON data and connect to SQL databases, combining multiple data sources in pandas.

### Code Cells Explanation:

**Cell 1: Import pandas**
- `import pandas as pd` - Core library for data manipulation

**Cell 2: Read JSON from file**
- `pd.read_json('train.json')` - Parse JSON file directly into DataFrame
- Automatically infers structure and creates appropriate columns

**Cell 3: Read JSON from API**
- `pd.read_json('https://api.exchangerate-api.com/v4/latest/INR')` - Fetch and parse JSON from REST API
- Returns DataFrame from nested JSON structure

**Cell 4: Install MySQL connector**
- `!pip install mysql.connector` - Install MySQL database driver package

**Cell 5: Import MySQL connector**
- `import mysql.connector` - Import database connection library

**Cell 6: Create database connection**
- `mysql.connector.connect(host='localhost', user='root', password='', database='world')`
- Establishes connection to MySQL server with authentication credentials

**Cell 7: Execute SQL query**
- `pd.read_sql_query('SELECT * FROM countrylanguage', conn)` - Execute SQL and return DataFrame
- Direct integration of SQL results into DataFrame for analysis

### Key Methods:
- `pd.read_json()` - Parse JSON into DataFrame
- `mysql.connector.connect()` - Establish database connection
- `pd.read_sql_query()` - Execute SQL queries with pandas
- `pd.read_sql_table()` - Read entire table from database

### Important Concepts:
- JSON structure determines column creation
- Database connections require proper credentials
- pandas seamlessly integrates with multiple data sources
- SQL queries return DataFrames for immediate analysis
