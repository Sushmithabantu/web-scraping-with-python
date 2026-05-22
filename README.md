# Web Scraping Project using Python

## Project Overview
This project demonstrates how to scrape data from a real website using Python.  
The data was extracted from Wikipedia’s list of the largest companies in the United States by revenue using BeautifulSoup and Requests, then converted into a structured CSV file using Pandas.

---

## Technologies Used
- Python
- BeautifulSoup
- Requests
- Pandas
- Google Colab

---

## Features
- Extracts real-time data from a live website
- Parses HTML tables using BeautifulSoup
- Cleans and structures scraped data
- Stores data in a Pandas DataFrame
- Exports data into CSV format

---

## Website Used
Wikipedia – List of largest companies in the United States by revenue

---

## Project Workflow
1. Send request to the website using Requests
2. Parse HTML content using BeautifulSoup
3. Find and extract the required table
4. Extract table headers and rows
5. Store the data in a Pandas DataFrame
6. Export the final dataset as a CSV file

---

## Python Libraries

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd
```

---

## Complete Code

```python
from bs4 import BeautifulSoup
import requests
import pandas as pd

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'

headers = {
    'User-Agent': 'Mozilla/5.0'
}

page = requests.get(url, headers=headers)

soup = BeautifulSoup(page.text, 'html.parser')

table = soup.find_all('table')[1]

world_titles = table.find_all('th')

world_table_titles = [title.text.strip() for title in world_titles]

df = pd.DataFrame(columns=world_table_titles)

columns_data = table.find_all('tr')

for row in columns_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]

    if len(individual_row_data) == len(world_table_titles):
        df.loc[len(df)] = individual_row_data

print(df)

df.to_csv('companies.csv', index=False)

from google.colab import files
files.download('companies.csv')
```

---

## Output
The final output is a CSV file named:

```text
companies.csv
```

The dataset contains:
- Rank
- Company Name
- Industry
- Revenue
- Employees
- Headquarters

---

## Learning Outcomes
Through this project, I learned:
- Basics of web scraping
- Working with HTML tags
- Extracting tables from websites
- Data cleaning using Pandas
- Exporting datasets into CSV format

---

## Future Improvements
- Add error handling
- Scrape multiple tables automatically
- Visualize data using Matplotlib or Power BI
- Automate scraping using scheduled scripts

---
