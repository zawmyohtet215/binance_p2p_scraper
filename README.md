# binance_p2p_scraper
Extract Binance P2P USDT Price Data using Selenium

# Binance P2P Data Scraper

This script scrapes data from the Binance P2P exchange platform, extracts buy and sell price information, processes the data, and inserts it into a PostgreSQL database. It uses Selenium for web automation, pandas for data handling, and SQLAlchemy for database operations.

## Requirements

- Python 3.x
- `selenium` for web scraping
- `pandas` for data manipulation
- `sqlalchemy` for database operations
- `Firefox` with geckodriver for Selenium (or any compatible browser driver)

### Install dependencies

```bash
pip install selenium pandas sqlalchemy
```

Ensure that you have the required web driver installed for Selenium to interact with your chosen browser (e.g., geckodriver for Firefox).

## Script Overview

1. **Webdriver Initialization**: Initializes a Firefox WebDriver (headless mode can be enabled by uncommenting the `options.add_argument("-headless")` line).
2. **Cookies Acceptance**: Accepts the cookies pop-up if present.
3. **Refresh Interval Selection**: Selects a predefined refresh interval for scraping data.
4. **Data Extraction**: Extracts buy and sell data from the Binance P2P trade page, including:
   - Name
   - Price
   - USDT price
   - Minimum and Maximum MMK
5. **Data Processing**:
   - Stores the extracted data into a pandas DataFrame.
   - Calculates the best price and volume, along with the average price and total volume of the top 4 entries.
6. **Database Insertion**: Inserts the processed data into a PostgreSQL database.

## Functions

### `init_webdriver()`
Initializes the Selenium WebDriver for Firefox.

### `accept_cookies(driver)`
Handles accepting cookies if the popup appears.

### `select_refresh_interval(driver)`
Selects the refresh interval dropdown and sets it to 5 seconds.

### `extract_data(driver, formatted_time, adv_list_name="AdvTableList", data_type="buy")`
Extracts the buy or sell data from the webpage and returns it as a pandas DataFrame. It collects various fields such as name, price, USDT, minimum and maximum MMK.

### `switch_tab(driver, tab_index)`
Switches between the tabs on the Binance page (buy/sell).

### `insert_dataframe_to_postgres(df, db_config)`
Inserts the data into a PostgreSQL database.

### `main()`
Runs the main scraping loop, where data is continuously extracted every hour and stored in the database.

## Configuration

- **Database Configuration**: 
  - Replace `yourhost`, `yourdatabase`, `youruser`, and `yourpassword` with your PostgreSQL connection details in the `db_config` dictionary.
  
## Usage

1. **Set up WebDriver**: Ensure that you have Firefox and geckodriver installed. 
2. **Configure Database**: Set up PostgreSQL and provide the connection details in the `db_config` dictionary.
3. **Run the Script**: Simply run the script:

```bash
python binance_scraper.py
```

The script will continuously scrape the Binance P2P exchange page, extract buy and sell data, process it, and store it in the configured PostgreSQL database every hour.

## Logging

The script uses Python's built-in logging module to track the progress and errors. Logs are printed to the console with timestamps.

## Notes

- The script assumes that the webpage structure of Binance's P2P platform does not change. If the structure changes, the XPaths used in the script may need to be updated.
- This script is intended for educational purposes and should be used responsibly with respect to Binance's terms of service.

