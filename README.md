# Extracting and Visualizing Stock Data

## Description
Extracting essential data from a dataset and displaying it is a critical part of data science, enabling stakeholders and individuals to make informed, data-driven decisions. In this project/assignment, historical stock prices and revenue data for **Tesla (TSLA)** and **GameStop (GME)** are extracted using two different methodologies, processed into clean data structures, and visualized on a synchronized financial dashboard.

## Table of Contents
- [Project Overview](#project-overview)
- [Technologies & Libraries Used](#technologies--libraries-used)
- [Features & Pipeline Steps](#features--pipeline-steps)
- [The Graphing Function](#the-graphing-function)
- [How to Run the Project](#how-to-run-the-project)
- [Author & Credits](#author--credits)

## Project Overview
The workflow is divided into six logical questions/tasks designed to practice different data science extraction mechanisms:
1. **Question 1:** Use `yfinance` to extract historical stock data for Tesla (`TSLA`).
2. **Question 2:** Use Webscraping (`BeautifulSoup`) to extract Tesla's quarterly revenue data.
3. **Question 3:** Use `yfinance` to extract historical stock data for GameStop (`GME`).
4. **Question 4:** Use Webscraping (`BeautifulSoup`) to extract GameStop's quarterly revenue data.
5. **Question 5:** Clean, merge, and plot Tesla's historical stock graph and revenue dashboard.
6. **Question 6:** Clean, merge, and plot GameStop's historical stock graph and revenue dashboard.

Estimated Time Needed to complete or run through the codebase: **30 minutes**.

## Technologies & Libraries Used
The project is built entirely in Python and requires the following libraries:
- **`yfinance`**: For programmatically downloading historical market data from Yahoo Finance.
- **`pandas`**: For data manipulation, cleaning, index resetting, and structuring into dataframes.
- **`requests`**: For fetching HTML web pages containing corporate revenue tables.
- **`beautifulsoup4` (bs4)**: For parsing and scraping HTML trees to extract text data from tables.
- **`matplotlib`**: For rendering static, dual-axis dashboards containing historical share prices and revenue distributions over time.

## Features & Pipeline Steps

### 1. Financial API Data Extraction
Utilizes the `yf.Ticker` object to reference stock symbols (`TSLA` and `GME`). Extracts maximum available historical data via the `.history(period="max")` function and normalizes the format by performing a `reset_index(inplace=True)` to make `Date` a queryable column.

### 2. Web Scraping for Revenue Data
Fetches specialized financial history pages using `requests.get()`. Parses table rows (`<tr>`) and cells (`<td>`) via `BeautifulSoup` to find historical figures, subsequently stripping out non-numeric characters (like commas `,` and dollar signs `$`) and dropping null/empty rows to ensure pristine data types.

### 3. Dashboard Visualization
An automated charting system links both datasets together onto unified visual timelines.

## The Graphing Function
The codebase includes a pre-defined modular plotting function called `make_graph`. It filters and matches timelines seamlessly to prevent data misalignment.

```python
def make_graph(stock_data, revenue_data, stock):
    """
    Takes a dataframe with stock data (must contain 'Date' and 'Close' columns),
    a dataframe with revenue data (must contain 'Date' and 'Revenue' columns),
    and the string name of the stock to generate a 2-row synchronized dashboard.
    """
    # Function filters dates internally and renders beautiful Matplotlib subplots
