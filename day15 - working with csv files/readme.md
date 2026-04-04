# Day 15 - Working with CSV Files

## Resources
Video link : https://www.youtube.com/watch?v=a_XrmKlaGTs

Books dataset link : http://www2.informatik.uni-freiburg.de/~cziegler/BX/

---

## Notebook: working-with-csv.ipynb

### Lesson Overview
Comprehensive guide to reading and parsing CSV files using pandas, exploring various parameters and configuration options.

### Code Cells Explanation:

**Cell 1: Import pandas**
- `import pandas as pd` - Imports pandas library for data manipulation

**Cell 2: Read local CSV**
- `pd.read_csv('aug_train.csv')` - Basic CSV reading using read_csv() method

**Cell 3: Read CSV from URL**
- `import requests; from io import StringIO`
- `requests.get(url, headers=headers)` - Fetch CSV from remote URL with user-agent header
- `pd.read_csv(StringIO(req.text))` - Parse remote CSV content
- Handles 403 Forbidden errors with proper User-Agent headers

**Cell 4: sep Parameter**
- `pd.read_csv('file.tsv', sep='\t', names=['col1','col2',...])` - Specify delimiter and column names
- Works with any delimiter: tabs, commas, pipes, etc.

**Cell 5: index_col Parameter**
- `pd.read_csv('file.csv', index_col='enrollee_id')` - Set specific column as DataFrame index

**Cell 6: header Parameter**
- `pd.read_csv('file.csv', header=1)` - Use row 1 as header instead of default row 0

**Cell 7: usecols Parameter**
- `pd.read_csv('file.csv', usecols=['col1','col2','col3'])` - Read only specific columns

**Cell 8: squeeze Parameter**
- `pd.read_csv('file.csv', usecols=['gender'], squeeze=True)` - Return Series instead of DataFrame for single column

**Cell 9: nrows Parameter**
- `pd.read_csv('file.csv', nrows=100)` - Load only first N rows (useful for large files)

**Cell 10: encoding Parameter**
- `pd.read_csv('file.csv', encoding='latin-1')` - Handle non-UTF8 encodings

**Cell 11: error_bad_lines Parameter**
- `pd.read_csv('file.csv', sep=';', encoding='latin-1', error_bad_lines=False)` - Skip malformed rows

**Cell 12: dtype Parameter**
- `pd.read_csv('file.csv', dtype={'target':int})` - Specify data types for columns

**Cell 13: parse_dates Parameter**
- `pd.read_csv('file.csv', parse_dates=['date'])` - Automatically parse columns as datetime

**Cell 14: converters Parameter**
- Define custom function for transformations: `def rename(name): ...`
- `pd.read_csv('file.csv', converters={'team1':rename})` - Apply custom transformation during read

**Cell 15: na_values Parameter**
- `pd.read_csv('file.csv', na_values=['Male'])` - Treat specific values as missing/NaN

**Cell 16: chunksize Parameter**
- `dfs = pd.read_csv('file.csv', chunksize=5000)` - Return iterator for memory-efficient processing
- Useful for extremely large files that don't fit in memory
- Process in batches: `for chunk in dfs: process(chunk)`

### Key Methods:
- `pd.read_csv()` - Primary function for CSV reading
- `requests.get()` - HTTP requests for remote files
- `StringIO()` - File-like object for string data

### Important Concepts:
- Parameter flexibility allows fine-grained control over data loading
- Chunking enables processing of very large datasets
- Data type specification prevents automatic type inference errors
- Encoding handling essential for international datasets
