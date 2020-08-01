# ETL Project by Muskatweeters
Check it out @ https://sarahparzyck.github.io/ETL_Project/

# Executive Summary
The Six Muskatweeters were interested in exploring whether Elon Musk’s prolific Twitter presence had meaningful impacts on the stock price of his electric car company and brainchild, Tesla. To do this, we scraped Mr. Musk’s Twitter profile for Tesla-related tweets and Yahoo Finance for daily Tesla stock data. We combined our data in Jupyter notebooks and loaded it into PostgreSQL for further analysis.

![Image](Musk_Twitter_backgnd.jpg)

# Extract
The Six Muskatweeters extracted daily Tesla stock (NASDAQ: TSLA) data from Yahoo Finance and combined that data with tweets from Elon Musk’s Twitter profile (@elonmusk). Yahoo Finance and Twitter required custom BeautifulSoup/Splinter web scrapers. After extracting the stock and social media data for the past 5 years (7-28-2015 – 7-28-2020), we were able to begin our data transformation.

# Transform
After importing our stock and tweet data into Jupyter notebooks, we began analyzing and cleansing the data for eventual loading into PostgreSQL.
We began by loading the stock and tweet data into Pandas Dataframes and excluding extraneous columns from the data. For the project, we required only the Date, High, Low, Open, and Close prices from the Tesla stock data, together with the Date and Tweet fields from the Twitter data. We performed a str.contains(“esla”) to limit our dataset to Tweets specifically related to Tesla.
To calculate fluctuations in stock price, we had to strip out non-numeric characters (i.e. “,”). We then cast the High/Low/Open/Close columns as floats and created new columns to store the calculated values. Differences between open and close prices were stored in Open_Close, while differences in high and low prices were stored in High_Low.
To merge the stock and tweet DataFrames, we standardized the date field formats in each DataFrame by casting them each as datetime64[ns]. Upon merging the dataframes, we were ready to load our data into PostgreSQL.

# Load
Due to the highly structured nature of the data, we decided to load our data into a relational, PostgreSQL database. To prepare our DataFrame for loading, we first converted it to CSV using the Pandas to_csv command. After that, we connected to our local database, created a new database called tesla_final_db, and loaded the data into a new table called tesla using the Pandas to_sql command.
