## Building the data foundation 
Data sources are the oil fields, the water springs or raw materials depending on which analogy you prefer. There are increasingly many ways in which data is generated often referred to as the 3 V's of data which are volume, variety, velocity and sometimes a fourth veracity. These are used to describe the ways in which the data landscape has evolved over the years as the term big data has come along. To built the data foundation of an organization requires a serious data acquisition strategy which should be driven by a fifth "V" *value*, something that is ensures with a good requirements gathering strategy as discussed in previous sections. There are many considerations that companies face in building a data acquisition strategy and a key question that Anderson tries to answer in his chapter 3 on data collection is "how do we value a data source?" something that organizations seems to struggle with. There are some interesting economics about data, something which Bill Schmarzo is debating in his work. For example in the book *The the Economics of Data, Analytics, and Digital Transformation*. 

In the beginning of this book i discussed in-depth the value proposition of data. The key insight from that discussion is that data has value proportional to how well it closes the gap between prior and complete information in a way that increases utility in excess of the cost of collecting the data. We also saw how giving systems access to information builds feedback loops which can improve the overall performance. Putting these lofty ideas in to practice organizations and data profesionals aim to unlock this value through data lifecycle and by practicing foundational activities. Driven by the fifth *v* data should be fit for purpose is because a good cook can only do so much with poor ingredients. 

Having data fit for purpose creates demand to use language from economic theory where the concept of supply and demand describes how the price or value of any good in the market given by the intersection of supply and demand. When it comes to data goods there is a key difference where increases in supply of data do not necessarily reduce the price or value that the market will converge towards. Schmarzo calls it the economic multiplier effect something that Anderson also brings up and it's this idea of building an entire contextual view by puzzling pieces of data together. Schmarzo relies on this when creating his entity propensity models in his more recent work. When we are able to collect more data at increasingly granular levels it allows for ever more nuanced and situational awareness which we can reuse across multiple use-cases. This means data value increases with supply and a call for us to become more innovative and creative about how we can generate data, here Matthew Benham is a great inspiration. Figure 3.8 show some entities in the middle which may be customers, employees, athletes, stores, machines and so on and how we by collecting all things and connecting the dots can create rich context about these which can lead to more valuable analytics. 

![](Connecting%20the%20dots%20with%20data%20and%20context.png)
Figure 3.8 connecting the dots with data collection in context

A related theory is that of law of diminishing returns which describe how firms produce by combining inputs labor and capital until at some point adding an extra employee or piece of equipment no longer adds excess profits. Schmarzo proposes the idea that data can essentially shifts the production or economic value curve upwards by "doing more with less" which has been the general gains from technological advancement and innovation. This happens when data is "Increasing operational uptime while reducing maintenance costs while improving customer satisfaction while reducing carbon footprint and emissions while increasing employee job satisfaction." (p. 43-44).  Value of data sources therefore lies within it's quality and fit for purpose towards creating real business value and the more high quality data we have the greater the economic multiplier effet we gain.

When it comes to choosing how to build the data foundation there are many considerations. What data sources should we acquire? How should we acquire them? What data sources can we create ourselves? These are complex questions which requires organizations to think strategically, prioritize resources and understand technical limits and possibilities. In general we might think that more data is better given that we might be able to puzzle more pieces together as a result. However we have to remember that ETL comes at a cost and there are often limited resources available to businesses. Anderson discusses the tasks of prioritizing data collection and how to think in terms ROI on data sources. Making estimations of the ROI is a difficult exercise in calculating and comparing the expected value of their decisions with and without the data. Some data might be obviously urgent, critical and have hard deadline to which it should be prioritized first. More often each department will have conflicting views on what is most important and so the estimation of ROI might be the most scientific way of building the data foundation. 
The crux is to estimate the real economic impact of the data including how it might optimize operational efficiency, increasing revenue, reducing costs, making new innovations and better offers. That corresponds to the upwards shift in the production curve that Schmarzo speaks about which make it clear how data is an asset like any other. Below here are some example questions to consider when evaluating a new data source as a part of a well-thought-out data acquisition strategy. 

* What is the price of acquiring the data and the systems that produces it?
* What is the quality of the data?
* How much innovation and competitive edge does this data source provide? How does it align with business initiatives and goals?
* How frequently is the data changing and updated? When is the data becoming stale?
* What ways are there to extract data from the source? Flat files, API, database connection, web scraping?
* Does it pose any security risks?
* What is the format that the data source is producing and what is the volume of data generated? 
* How granular is the data capable of producing?
* How does the data piece together with other?
* How well document it the data source? 

There is often a decision to be made on the frequency of which ingestion should occur. For example it's sometimes possible and valuable to make real-time copies of data. In some cases slower intervals such as daily batches are more appropriate or the only choice. The method we use for ingestion and so only largely depends on what the data source allows, but it may also be a matter of other things. The volume of the data is also a consideration as it helps us understand the burden that is put on the tasks we create to ingest data but also on the storage system. For example transactional or event data will often be quite large in size and so it's not master data such as customer and vendor data have less instances and change less often. The structure of the data is also relevant. Unstructured data may be text, video and sound. It could also be more traditional data but come in forms such as JSON or XML. 

## Practical example of ingesting data
To manufacture a knowledge product we need the raw materials and the data warehouse where we can puzzle and shape those materials in the ways we desire, without disturbing the systems that generate it. For personal projects the "data warehouse" might be your C drive where you store local files but for organizational data volumes and for many other reasons we want to have a dedicated database server either on-premise or cloud. Ingestion can be done using in different ways, perhaps the most simple being typing data manually into a spreadsheet. This can be very effective, fast and cost-efficient. However the downside is that the process is manual and whenever we require manual labor and insertions we are jeopardizing the data quality. With that said these types of systems serves their own right and I've seen them being used in a very good way. The more standard ingestion work involves extracting data from databases, the dedicated systems which we analyzed in previous chapters. Here data can be stored in large amounts and in efficient ways such as the relational model that Edgar Codd suggested in his famous paper in 1970. To extract data from a database typically requires authorization which can be different of different forms. For example a database connection string along with a user name and password. It's also possible to access data in databases with application programming interfaces or APIs which establish connection with *HTTP* protocols to request data over the network. The URL will specify the *endpoint* that corresponds to the specific data objects you want and again you will need to authorize yourself. If a valid endpoint is requested it will return an object with the data sometimes as a JSON object, XML or another data structure. 

I will first here show a few simple personal projects that go through the entire end-to-end analytics while avoiding heavy infrastructure investment. These are some projects anyone can try out or work with without incurring large costs or use a large setup. While the familiar cloud-providers are generally sharing the market at the enterprise level there exists a broad suite of tools that can be fun to play around with for personal projects and also provide a lot of experience that can be transferred into any environment.At the end i will show how a real data platform might look like using microsoft fabric.  

## Database connections 
The most common form of data ingestion in any organization involves extracting data from a database. Whether that database lives on-premise or in the cloud, the mechanics follow the same principle: establish a **connection**, send a **query**, receives a result set, and close the connection. The specific technology behind the database — Microsoft SQL Server, PostgreSQL, Snowflake — changes the connection string and other details for example like the driver you import, but the SQL language and the code remains almost identical.

For this example we will use **SQLite**, which is a fully capable relational database that ships with Python's standard library. This means you need nothing installed beyond Python itself. SQLite creates a light database as a single file on your filesystem, which makes it excellent for learning, prototyping, and small-to-medium analytical workloads. We will first create a small database with two tables — one for companies and one for their dividend history — and then extract that data in the same way a production pipeline would pull from a much larger enterprise system.

### Setting up the database
The code below creates a local SQLite database, defines two tables with a relationship between them, and inserts some sample records. If you are already working with an existing database you would skip this step and go straight to the extraction.

code example 2.1: creating a local SQLite database with company and dividend tables
```
import sqlite3
import pandas as pd

# sqlite3 is part of Python's standard library — no install needed
# The connect() call creates the file if it does not already exist

conn = sqlite3.connect('company_data.db')
cursor = conn.cursor()

# Create a companies reference table

cursor.execute('''
    CREATE TABLE IF NOT EXISTS companies (
        ticker      TEXT PRIMARY KEY,
        name        TEXT NOT NULL,
        sector      TEXT
    )
''')

# Create a dividends fact table with a foreign key to companies

cursor.execute('''
    CREATE TABLE IF NOT EXISTS dividends (
        id              INTEGER PRIMARY KEY AUTOINCREMENT,
        ticker          TEXT NOT NULL,
        pay_date        TEXT NOT NULL,
        cash_amount     REAL NOT NULL,
        currency        TEXT DEFAULT 'USD',
        FOREIGN KEY (ticker) REFERENCES companies(ticker)
    )
''')

# Insert sample company records
companies = [
    ('MRK', 'Merck & Co., Inc.',       'Healthcare'),
    ('JNJ', 'Johnson & Johnson',        'Healthcare'),
    ('MSFT','Microsoft Corporation',    'Technology'),
]

cursor.executemany(
    'INSERT OR IGNORE INTO companies VALUES (?,?,?)', companies
)

# Insert sample dividend records

dividends = [
    ('MRK', '2025-04-07', 0.81, 'USD'),
    ('MRK', '2025-01-08', 0.81, 'USD'),
    ('MRK', '2024-10-07', 0.77, 'USD'),
    ('JNJ', '2025-03-04', 1.24, 'USD'),
    ('JNJ', '2024-12-03', 1.24, 'USD'),
    ('MSFT','2025-03-13', 0.83, 'USD'),
]

cursor.executemany(
    'INSERT INTO dividends (ticker, pay_date, cash_amount, currency) VALUES (?,?,?,?)',
    dividends
)

conn.commit()
conn.close()
print('Database created successfully.')
```
### Extracting data with a SQL query
With the database in place we can now connect to it and extract data using a SQL query. Notice that we join the two tables to enrich the dividend records with the company name — exactly the kind of transformation that would otherwise happen in a downstream step if the data arrived separately.

code example 2.2: connecting to the database and extracting data into a pandas DataFrame
```
# The connection string for SQLite is simply the path to the .db file
# For other databases this would look like:
#   PostgreSQL:  'postgresql://user:password@host:5432/dbname'
#   SQL Server:  'mssql+pyodbc://user:password@server/dbname?driver=...'
#   Snowflake:   'snowflake://user:password@account/dbname'

conn = sqlite3.connect('company_data.db')
query = '''
    SELECT
        d.pay_date,
        d.cash_amount,
        d.currency,
        d.ticker,
        c.name        AS company_name,
        c.sector
    FROM dividends d
    JOIN companies c ON d.ticker = c.ticker
    ORDER BY d.pay_date DESC
'''
# pandas read_sql() executes the query and returns a DataFrame directly

df = pd.read_sql(query, conn)
conn.close()
print(df)
```

output: resulting DataFrame printed to console
```
     pay_date  cash_amount currency ticker           company_name      sector
0  2025-04-07         0.81      USD    MRK      Merck & Co., Inc.  Healthcare
1  2025-03-13         0.83      USD   MSFT  Microsoft Corporation  Technology
2  2025-03-04         1.24      USD    JNJ      Johnson & Johnson  Healthcare
3  2025-01-08         0.81      USD    MRK      Merck & Co., Inc.  Healthcare
4  2024-12-03         1.24      USD    JNJ      Johnson & Johnson  Healthcare
5  2024-10-07         0.77      USD    MRK      Merck & Co., Inc.  Healthcare
```

**What changes in production**
In a production environment the only lines that would meaningfully change are the import statement and the connection string. Instead of sqlite3 you would import the appropriate driver for your database — for example psycopg2 for PostgreSQL or pyodbc for SQL Server — and pass the corresponding connection string. The pd.read_sql() call and the SQL query itself remain the same. This is by design: the abstraction that SQL provides means your analytical logic is portable across virtually any relational system. In enterprise platforms such as Databricks or Microsoft Fabric the connection is typically handled by a cluster-level configuration or a secret scope, meaning credentials never appear directly in notebook code. The pattern is otherwise identical.
## Ingesting data with a REST API
As discussed earlier, a great deal of data today is made available through APIs. Rather than giving you direct access to a database, the provider exposes one or more **endpoints** — specific URLs you can call to request particular data objects. The response typically comes back as a **JSON** object, which is a structured text format that Python can easily parse. To keep this example fully reproducible we will use **Open-Meteo**, a free weather API that requires no registration, no API key, and no account. Despite being free it is a well-designed API with a clear endpoint structure and is used in real production applications. We will request historical daily temperature data for a city — a type of time-series that is structurally very similar to financial or operational data you might encounter in an organizational context.

code example 2.3: installing the requests library and calling the Open-Meteo API
```
# requests is not in the standard library — install once with:
pip install requests pandas
import requests
import pandas as pd
import json
# Build the request URL
# The base URL identifies the API, the path identifies the endpoint,
# and the query string carries our parameters

base_url = 'https://archive-api.open-meteo.com/v1/archive'
params = {'latitude': 52.52, 
		  'longitude': 13.41, 
		  'start_date': '2024-01-01',
		  'end_date':   '2024-03-31',
		  'daily': 'temperature_2m_max,temperature_2m_min',    
		  'timezone': 'Europe/Berlin'}

# Send the HTTP GET request

response = requests.get(base_url, params=params)

# Inspect the status code before proceeding
# 200 means the request was accepted and data was returned

print('Status code:', response.status_code)

# Parse the response body as JSON

json_data = response.json()
```

code example 2.4: transforming the JSON response into a structured DataFrame
```
# The JSON response has a nested structure.
# We navigate to the 'daily' key which contains our time-series data.

daily = json_data['daily']
df = pd.DataFrame({'date': daily['time'], 
				   'temp_max': daily['temperature_2m_max'],   
				   'temp_min': daily['temperature_2m_min'],})
df['date'] = pd.to_datetime(df['date'])
print(df.head())
```

output: first five rows of the resulting DataFrame
```
        date  temp_max  temp_min
0 2024-01-01       7.3       3.4
1 2024-01-02       7.2       2.5
2 2024-01-03      10.6       7.2
3 2024-01-04       7.2      -2.2
4 2024-01-05       0.9      -0.7
```

**What changes in production**
Most organizational APIs require authentication. The most common mechanisms are an API key (passed as a query parameter or in a request header) or an OAuth 2.0 bearer token. In either case you would add it to the params dictionary or to a headers dictionary passed to requests.get(). The rest of the code is unchanged. When working with large volumes of API data, production pipelines typically loop through paginated responses, writing each page to storage before requesting the next. Pagination details vary by provider but the pattern — request, parse, store, advance — is consistent.
## Ingesting data from flat files
Not all data arrives through a live connection. A significant and often underestimated share of organizational data exists in flat files: CSVs emailed between departments, Excel workbooks maintained by individual analysts, extracts downloaded from systems that offer no API. Dismissing this as informal or low quality misses the point — in many organizations flat files carry security mappings, reference data, or enrichment tables that simply do not exist anywhere else. In this example we continue from where we left off in example one. We will export our extracted data to a CSV file — simulating a scenario where an analyst has taken a database extract and passed it on — and then re-ingest that file into a new DataFrame, as would happen if a downstream team received it.

Code example 2.5: exporting a DataFrame to CSV and reading it back


**Code example 2.6: reading an Excel file — the pattern is nearly identical**
```
# pip install openpyxl  (required for .xlsx support)<br><br>import pandas as pd<br><br># Writing to Excel<br><br>df.to_excel('dividend_extract.xlsx', index=False, sheet_name='Dividends')<br><br># Reading from Excel — note the sheet_name parameter<br><br>df_excel = pd.read_excel('dividend_extract.xlsx', sheet_name='Dividends')<br><br>print(df_excel.head())
```

**What changes in production**
In enterprise data platforms like Microsoft Fabric or Databricks, reading a flat file follows the same logical pattern but targets cloud storage rather than a local path. In Databricks you might read from an ADLS Gen2 path such as *abfss://container@storageaccount.dfs.core.windows.net/folder/file.csv* using the same *pd.read_csv()* call or Spark's *spark.read.csv()*. In Microsoft Fabric the file would live in a Lakehouse and be accessible directly from a notebook. The principle — locate the file, parse its contents, load into a DataFrame — does not change.

A practical point worth noting: when ingesting files from other people or systems, always validate the shape of the data before processing it. Column names change, delimiters vary between regions, and date formats differ between systems. Building lightweight validation into the ingestion step saves considerable debugging time later.
## Comparing the three ingestion methods
Having worked through all three examples it is worth pausing to observe what they have in common. In each case we ended up with a **pandas DataFrame** containing structured, queryable data. The ingestion method determined how we obtained that data, but not what we could do with it afterwards. This is a useful mental model: ingestion is about the route, not the destination.

Table 16. Summary comparison of the three ingestion methods

| Method                | Require credentials  | Data freshness         | Best suited for                    |
| --------------------- | -------------------- | ---------------------- | ---------------------------------- |
| Database connector    | Yes (usually)        | Live or near-live      | Transactional & operational data   |
| REST API              | Often (key or token) | Live                   | External & operational data        |
| Flat file (CSV/Excel) | No                   | Point-in-time snapshop | Reference, enrichment, ad-hoc data |

### Data transformation
We have now seen three ways of collecting data and like technologies for ingestion and storage there exists a broad range of data transformation options. Current options include utilizing programmatic capabilities of high-level programming languages like Python or Java. Another classic tool which many people are comfortable using is SQL, a dedicated language to write expressions that transform data. Knowledge factories embed these tools into them for example including interactive developer environment that supports all of the above languages. There also exists many low-code options such as the very accessible options from Microsoft PowerQuery tool in Excel and Power BI. The choice of transformation tool again comes down to picking the most appropriate tool for the job. A low-code solution like PowerQuery generally lacks the ability to version control and productionalize which means it's difficult to maintain and collaborate on. Most enterprises uses a blend of tools. They make the most of their transformations using professional tools that support multi developer environments, version control enabling seamless deployment of code and other artifacts across environments. For some smaller use cases they may use the low-code options for example to ingest local files that closes some gaps in the data that resides in the systems that make up the IT-infrastructure. To make data fit for purpose and puzzling together dimensional models typically require some transformations that implement business logic. I will show a few common operations as i go through some worked examples here.

Let's return to the example of the financial data that has been ingested and continue with the raw data coming from the API. When you look at the raw data ingested it may for the trained eye allow you to catch the information, but for the most part it will be much better to have a table structure such as that in table 14. To solve this we need to transform the data. The important information to extract is the pay date and cash amount. To transform the raw data, we may inspect it a little further such as running the type() command on the JSON object. This command reveals that the data structure is a dictionary or json object a complex data structure which often is the output of an API call. 
code example 1.3: showing the type of the JSON data output
```
type(json_data)
dict
```
Listing 3.2 Python code to show the data type of the json_data object

Dictionaries are storing data in key-value pairs and in this case the data is nested through multiple levels. That it's nested can be seen that the first key 'result' contains a list data structure and inside that list the information about each dividend payment is held as a dictionary. To access for example the most recent dividend payment one can write the code shown in code example 1.4

code example 1.4: Python code to access the latest dividend amount from the json data structure
```
json_data['results'][0]['cash_amount'] # returns the latest dividend cash amount
0.81
```

We’re going to need to loop through each of the list items in the result key and extract the keys “cash_amount” and “pay_date”. First I store the list of dividend recordings in a new variable dividend_list. Then I create an empty dictionary that will hold the pairs of dates and cash amounts. Finally a loop over the dividend list is initiated and the keys are used to extract the right values of the individual dividends. 

code example 1.5: Python code to extract the history of dividends and store it in a dictionary data structure
```
# list of dividends
dividend_list = json_data['results']

# data structure to store dividend payments and key-value pairs {'PayDate': {cash_amount}}

dividends = {}

for dividend in dividend_list:
  pay_date = dividend['pay_date']
  cash_amount = dividend['cash_amount']
  dividends[pay_date] = cash_amount
```
The data stored in the dividends dictionary after end runtime is shown in code example 1.6.

code example 1.6: Output from displaying the dividend_list dictionary
```
{'2025-04-07': 0.81,
 '2025-01-08': 0.81,
 '2024-10-07': 0.77,
 '2024-07-08': 0.77,
 '2024-04-05': 0.77,
 '2024-01-08': 0.77,
 '2023-10-06': 0.73,
 '2023-07-10': 0.73,
 '2023-04-10': 0.73,
 '2023-01-09': 0.73}
```

That is what we want. Now the thing is just to turn this into a tabular format with the headers: pay date and cash amount. The library pandas can help one transform dictionaries into a dataframes, a temporary table. In order to obtain the desired result I use the *from_dict()* function and add an index column such that the pay date and cash amount columns can be created. Finally the result is printed out and is shown in code example 1.7. It has the desired table format we can begin to analyze. This table shows a descending order of dividend payments and from that we can see that dividends have been paid out in regular quarterly intervals with increases both from 2023 to 2024 and from 2024 to 2025. 

code example 1.7: Dictionary output to dataframe using python and the pandas library
```
dividend_table = pd.DataFrame.from_dict(dividends, orient='index')
dividend_table = dividend_table.reset_index()
dividend_table = dividend_table.rename(columns={0: 'Cash Amount'})
dividend_table = dividend_table.rename(columns={'index': 'Pay date'})

dividend_table
	Pay date	Cash Amount
0	2025-04-07	0.81
1	2025-01-08	0.81
2	2024-10-07	0.77
3	2024-07-08	0.77
4	2024-04-05	0.77
5	2024-01-08	0.77
6	2023-10-06	0.73
7	2023-07-10	0.73
8	2023-04-10	0.73
9	2023-01-09	0.73
```
### Core data transformations
The example above showed how raw data can be transformed into a finished good in form of a table. There are an almost unimaginable number of ways data can be transformed, but in this section some common operations to manipulate and reshape data are presented. 

**Filtering and creating new columns**
To fit analytic or application needs some of the key operations include filtering and mapping new values. Code example 1.8 shows an example of a filtering operation and column transformation.

code example 1.8: Common filtering and column transformations
```
df = read_table(‘users’)
# Filter to only active users
df = df["status"] == "active"
# Map: create a full_name column
df = df.withcolumn(‘full_name’, col(‘first_name’) + ‘ ‘ + col(‘last_name’)
```
This operation filters on a status field with the line (status == "active") and a mapping (concatenate first/last name). Most processing frameworks (Pandas, Spark, SQL) support these operations. In SQL expression language the WHERE clause can be used to filter a table. 

**Combining data with joins**
Data in databases are often related in some way and when we create dimensional models we rely on our ability to join and combine data. Typically facts and dimensions are combined into *star schemas* and to do that we're going to join the tables using foreign keys. What we need to make sure is that the fact table contains the columns needed, the primary keys that make up a unique row in the dimensions. In code example 1.9 there is examples of two common join types, the inner and the left join. In addtion there exists also, full outer joins, right joins, anti joins and cross joins all serving some particular purpose. 

code example 1.9: Common join operations using pandas
```
orders = read_table(‘orders’)
users  = read_table(‘users’)
# Inner join on user_id: keep only orders with matching user
df_inner = orders.join(users, on="user_id", how="inner")
# Left join: all orders, fill nulls where no user match
df_left  = orders.join(users, on="user_id", how="left")
```
An inner join retains only records present in both tables, whereas a left join keeps all rows from the left table, filling with nulls when the right table has no match. These operations correspond to SQL JOIN clauses. For example, SQL’s  `SELECT * FROM A INNER JOIN B ON A.id=B.id` yields the intersection of A and B, while LEFT JOIN retains all rows from A, and FULL JOIN combines all rows from both sides. 

**Summarizing and aggregating data**
Aggregating or summarizing data is something that is done typically at the analytical level such as in a dashboard or using SQL tools. It can however be useful to do it in the engineering stage, if there are billions or millions of historical records which no longer need the granularity it originally was recorded in. For that reason it may be grouped by months or a set of columns which reduced the overall size of the dataset. Code example 1.10 shows a common aggregation operation on some sales data.

code example 1.10: Common aggregation operation
```
df_sales = read_table(‘sales’)
sales_by_user = group_by(df_sales, by="user_id").agg(‘amount’)
```

In SQL:`SELECT user_id, SUM(amount) FROM sales GROUP BY user_id;. 

Python comes with several aggregation functions like sum(), count(), avg(), etc. It's also possible to use window functions or rolling aggregations to compute things like rolling totals over time.

**Pivoting data from wide to narrow formats**
In some cases it can be really useful to pivot the data. That could for example be when the raw data is very wide in it's format. That's possible when data is not coming from relational databases and so data is not necessarily normalized. An example could be survey data. Survey data may come as flat files and contain one column for each question, thus resulting often in very wide tables. In that case it could make sense to pivot the data such that each question and result of the question becomes a row. The result is that we can transform this single table into perhaps a fact table containing results in rows and then have a dimension that holds each question as a row. 

**Handling complex data structures**
When the raw data is in a complex data structure like the JSON data I ingested from the API, then the data really needs to be "unpacked" or flattened. This can be done with the method is used, looping over the nested data structure and extracting the information. It could also be done using functions that unpack these complex nested data structures.  

**Splitting, casting, removing data**
The final set of operations i will highlight here are all operations that related to for example casting data types to ensure consistent types across systems such as (dates, numbers, categories). We also may want to clean data values by using operations to trim whitespace, standardize values, or drop duplicates (`df.drop_duplicates()`). 

Following good software design principles, each of these transformations should be accompanied by clear documentation (e.g. docstrings or comments) and tests to verify correctness. For example, testing that a filter returns only valid rows, or that joins produce the expected row count.

## Serving and activating data
Finally we are ready to produce finished goods. This is where curated, transformed data is made available for use for some productive purpose be it analytical dashboards, data scientist projects, machine learning models, business intelligence or automation. The form of the final data product depends on the use case—whether human-centric (exploration, visualization, reporting) or machine-driven (inference, model training). The data may be structured and served as a dimensional model with fact and dimension tables that support slice-and-dice analytics. Alternatively, data may be structured in wide tables that are easier to consume for models expecting flattened datasets. 

From a data engineering perspective, the emphasis at this stage is on accessibility, performance, and trust. This means ensuring the following:
- Data is available in formats suited to its consumers
- Metadata and lineage are well maintained,
- Tables or views follow naming and modeling conventions (e.g., star schema),
- Security and privacy rules are enforced 

What may we imagine doing with our financial data of historical dividend payments? We may consider plotting it visually, something that often is very generous to the human eye. The following code example 1.12 produces a plot using python code and two excellent libraries matplotlib and seaborn. Figure 3.2 shows the subsequent plot. 

code example 1.12: Python code to plot dividend history data
```
from matplotlib import pyplot as plt
import seaborn as sns
def _plot_series(series, series_name, series_index=0):
  palette = list(sns.palettes.mpl_palette('Dark2'))
  xs = series['Pay date']
  ys = series['Cash Amount']
  
  plt.plot(xs, ys, label=series_name, color=palette[series_index % len(palette)])

fig, ax = plt.subplots(figsize=(10, 5.2), layout='constrained')
df_sorted = dividend_table.sort_values('Pay date', ascending=True)
_plot_series(df_sorted, '')
sns.despine(fig=fig, ax=ax)
plt.xlabel('Pay date')
_ = plt.ylabel('Cash Amount')
```

![](Plot%20of%20dividend%20history%20using%20python.png)
Figure 3.2 plot of dividend history data made using python

To increase the information value one may combine this with other types of financial information and extract it to a spreadsheet or the like to create other types of graphics and visuals. In recent years, the idea of data activation has emerged, particularly within reverse ETL workflows. Here, curated data is not only analyzed but also sent back into operational systems (like CRMs or marketing platforms) to directly influence business processes in real time. This closes the loop between insight and action, turning data into a truly operational asset.
## More data on the menu
The journey to wisdom can take many forms. What follows are additional small examples that can be made without incurring large costs of setting up entire enterprise scale manufacturing infrastructure. To practice developing knowledge products we may start from personal world. We may have our own goals and ambitions, such as eating healthy foods. To our luck we can find raw data on this. As an example i found a downloadable file from official authorities here in Denmark on the nutritional values of different types of food. I ingested it simply by downloading it to my local desktop computer. Yes ingestion can look that simple. The raw data was formattet as a normal spreadsheet structure and contained data about different foods, including the name, food group and the nutritional values. There were multiple sheets and figure 3.3 shows a snapshot of first sheet and the data in that.
![](Raw%20nutritional%20data%20data%20sheet.png)
Figure 3.3 Screenshot of raw nutritional data extract

To begin with i considered what kind of questions or use-cases that may actually be important or relevant. It could be to ask question such as, what foods contains high amounts of vitamins and minerals? Or which foods have good balance of protein, carbs and fat. Such questions revolves around the central measure of nutritional values, that is the KPI underlying these questions. The questions introduce some dimensional perspectives such as which *foods* and *nutritional parameter*, thus we may begin to see the data model that describe this reality. Figure 3.4 shows a conceptual design of this practical example. It shows how the nutrition values as the center of the model and how it relates to the two entities food and nutrition parameter.
![](Nutrition%20value%20conceptual%20model.png)
Figure 3.4 Conceptual data model for nutritional solution

Kimball and his idea of the dimensional model seems fitting here. Inspecting the raw data reveals that the data is not readily normalized, like it typically is in relational databases. That means we cannot skip the transformation stage and we need to build the dimensions and fact. The food dimension needs to have one row for each food recorded in the dataset and the nutrition parameter dimension needs to have one row for each parameter such as vitamin A, vitamin K and so on.

The first thing i noticed was that the data was not very structured, at least not normalized like it would be in a relational database. I considered how i could transform this data such that it would be easier to work with and make some meaningful insights. I decided to follow  This dimension would hold the name of the food and a unique ID that funciton as a primary key. The second dimension was a food group dimension, a much smaller table with only around 200 food groups, again an ID and a name. The third dimension is a nutrition parameter dimension, one row for each nutritional parameter in which there are around 220 different values such as vitamin K, vitamin A and so on. To complete the dimensional model there needs to be some central table we want to view from the constituent dimensions. It makes sense that the actual values of nutrition parameters is held in the central fact table of this dimensional model. Figure 3.5 shows how the food dimension ended up looking like. A very slim table given the simplicity of the data here containing the name of the food, the food group and the generated surrogate key. 

![](food%20dimension.png)
Figure 3.5 Food dimension

The nutrition parameter dimension shown in figure 3.6 is also quite slim containing the parameter name, unit of measure, parameter group name and the surrogate key i generated with a simple index column. 
![](Nutrition%20parameter%20dimension.png)
Figure 3.6 Nutrition parameter dimension 

These transformations were done with low-code tools again in this case because the transformations are quite trivial and cheap. Low-code options typically work well for scenarios such as smaller personal projects. It's also a very common tool used among business people that want quick results. The actual operations behind creating the star schema in this case were quite simple. It involved referencing the base table a few times, deleting some columns, dropping duplicates, creating index column for the surrogate key and complete the model with relationships between the tables. 

Now that the analytical model is finished, what can we use it for? One of the ways is to inspect which types of foods have great amounts of a particular type of vitamin such as K. Leafy greens and herbs top the list according to this data set and i am fairly sure I've heard this before and so it confirms that. Figure 3.7 shows the matrix visualization i built. 

![](Matrix%20visual.png)
Figure 3.7 Matrix visualization of vitamin K, K1 and K2 content in different foods in descending order

There are many ways to extend our analysis here. We can include custom measures that compare values against recommended daily intakes, standardize values if they are in micro and milligrams and we could look for additional data to enrich the analytical model. 

This quick setup served as a good prototype and practical exercise. If valuable it may be transformed into a more production ready solution, something that runs in a knowledge factory. This could look like the following: 

1) Get access to a API use programmatic tools to ingest data into a scalable cloud database or data lake. 
2) Transform using programmatic tools reading and writing from and to different layers of curation 
3) Design a dimensional model or analytical table for data science 
4) Import those dimensional model into visualization software or build the first statistical learning model. 
5) Setup automatic orchestration that ingest, transform and update the final product with new data points at regular intervals.

This version would be more scalable and it does not rely on a single persons computer running. Keeping data in medallion architecture would allow the data to be shareable for different purposes. Use cases could be extended to building meal plan based on getting certain nutritional values in and so on. To be data literate is to try and fail with these projects and imitate those around you that succeed, that is the only way to acquire the language of data. There will be opportunities that come and go but being prepared to take these is what we built these solutions for. It's time to practice and built for a smarter, better and informed tomorrow. 

## From prototypes and personal projects to enterprise data platforms
Now that we have seen some prototype and personal projects i think it's suitable to show how those differ from larger enterprise sized solutions. There are alot of similarities and the big picture ingest -> transform -> serve remains intakt. One of the main differences is that many data systems in current technology have become high-code environments because of the benefits it provide. That also means building these systems entails a considerable amount of software engineering. We might say that data engineers is a type of software engineer that specializes in developing systems that creates these big data pipelines that creates knowledge and data centric products. Therefore many data engineers come with a software engineering background. 

**Metadata driven pipelines**
In large software projects some task or series of tasks have to be executed again and again, but perhaps with some minor modifications depending on the state of the program. Raw materials are moved through the system that ingest data from source system A, B, C and D. That activity looks very similar but need modifications. As an example all of the raw data may be ingested with APIs which means the URL needs to be change as well as other details such as authentication variables and method. It may also be moved using standard database connections, here the connection string, user name and password needes to change. The foldes and schemas which data lands in needs also needs to reflect these changes. To handle this software engineers write modules that execute general tasks and they use *metadata* files to define parameter details that controls specific details of the general task. Large scale production of data struggles without adopting this structure. We have general activities such as load to bronze, load to silver, copy data from database, clean and vacuum folders, ingest API data and so on. These are the templates the generic tasks which have a set of parameters such as database, server, table that is passed to the activity and looked up in metadata repositories. Instead of creating hundreds of ingestion jobs, we define a list of hundred tables which can be done much more compact and loop the general task over this list.  
In code example 3.11 there is an example structure of a data class that could represent a single data source. It's then possible to create instances of this class that includes the details of that specific table.

code example 3.11: Creating a metadata Python class for defining details of a single source 
```
class Metadata:
    def __init__(self, source_name: str, file_format: str, delimiter: str = ',', 
                 schema: Dict[str, str] = None, 
                 transformations: List[Dict[str, Any]] = None, 
                 load_strategy: str = "append", 
                 partition_keys: List[str] = None):
        self.source_name = source_name
        self.file_format = file_format
        self.delimiter = delimiter
        self.schema = schema if schema else {}
        self.transformations = transformations if transformations else []
        self.load_strategy = load_strategy
        self.partition_keys = partition_keys if partition_keys else []     
``` 

The conceptual class above captures the idea. What follows is a walk-through of a real data platform built on Microsoft Fabric that implements the medallion architecture end to end. The same ingest-transform-serve pattern from the prototypes applies, but the code is structured for production: reusable libraries, metadata-driven pipelines, incremental loads and star schema dimensional models written to Delta tables. The examples shown are adapted from a production platform. Sensitive details such as workspace identifiers, credentials and business data have been anonymized but the patterns and code are representative of real enterprise implementations.

### Platform architecture
The platform follows the medallion architecture with a star schema in the Gold layer. Source systems expose data through REST APIs. Raw JSON responses land in a Raw lakehouse, are flattened into Bronze Delta tables, cleansed into Silver and finally shaped into dimensional Gold tables that feed Power BI semantic models.

```
┌──────────────────────────────────────────────────────────────────┐
│                       SOURCE SYSTEMS                             │
│   ┌────────────┐    ┌────────────┐    ┌───────────────────────┐  │
│   │  ERP API   │    │  HRMS API  │    │  Dataflow / Files     │  │
│   └─────┬──────┘    └──────┬─────┘    └──────────┬────────────┘  │
│         │                  │                      │               │
│   ┌─────▼──────────────────▼──────────────────────▼───────────┐  │
│   │                  BRONZE (Raw JSON → Delta)                 │  │
│   └────────────────────────┬──────────────────────────────────┘  │
│                            │                                     │
│   ┌────────────────────────▼──────────────────────────────────┐  │
│   │                  SILVER (Cleansed Delta)                   │  │
│   └────────────────────────┬──────────────────────────────────┘  │
│                            │                                     │
│   ┌────────────────────────▼──────────────────────────────────┐  │
│   │            GOLD (Star Schema — Data Warehouse)             │  │
│   │                                                            │  │
│   │  ┌────────────┐  ┌─────────────┐  ┌───────────────────┐  │  │
│   │  │ Sales      │  │ Finance     │  │ Time Registration │  │  │
│   │  │ Model      │  │ Model       │  │ Model             │  │  │
│   │  └────────────┘  └─────────────┘  └───────────────────┘  │  │
│   └────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

A shared utility library provides four classes that all notebooks import. This keeps the codebase DRY as each notebook focuses on its specific transformation rather than re-implementing I/O or path logic.

code example 3.12: Centralized lakehouse configuration class
```python
@dataclass
class WorkspaceOneLakePaths:
    """Centralized configuration for OneLake lakehouse identifiers.
    Provides consistent access to workspace and lakehouse IDs across the
    medallion architecture (Raw, Bronze, Silver, Gold, Metadata).
    """
    metadata_lakehouse = 'Metadata'
    raw_lakehouse = 'Raw'
    bronze_lakehouse = 'Bronze'
    silver_lakehouse = 'Silver'
    gold_lakehouse = 'Gold'

    def get_workspace(self):
        return config.get_variable('StorageWorkspace')

    def get_bronze_lakehouse(self):
        return config.get_variable('BronzeLakehouse')

    def get_silver_lakehouse(self):
        return config.get_variable('SilverLakehouse')

    def get_gold_lakehouse(self):
        return config.get_variable('GoldLakehouse')
```

Every notebook begins with the same three lines that instantiate the shared classes. This means that a developer working on a new dimension table or fact table never needs to figure out how to connect to storage — the library handles it.

```python
path = WorkspaceOneLakePaths()
dwr  = DataWriteReader()
nt   = DataTransformer()
```

### Bronze layer — metadata-driven API ingestion
Earlier we saw the conceptual `Metadata` class. In production the metadata configuration is richer. Each API source is described as a dictionary containing authentication details, endpoint URLs, query parameters, pagination rules and incremental loading specifications. A default dictionary holds settings shared across all endpoints of the same source system and individual table configs extend it.

code example 3.13: Production API metadata configuration (anonymized)
```python
default_dict = {    
    "ApiName": "ERP",
    "ApiVersion": "v1",
    "ApiCall": "GET",
    "ApiHeader": {
        "Accept": "*/*",
        "Content-Type": "application/json"
    },
    "AuthParam": {
        "AuthType": "HeaderSecrets",
        "KeyVaultName": "[company-keyvault]",
        "HeaderSecrets": {
            "X-GrantToken": "API-ERP-Grant-Token",
            "X-AppSecret":  "API-ERP-App-Secret"
        },
    "Pagination": {
        "NextPageKey": "pagination",
        "NextPageSelect": "nextPage"
    }},
    "SourceSystem": "ERP",
    "FileOptions": {"cloudFiles_format": "json", "multiLine": "true"},
    "ApiLoadDays": {
        "DaysOffset": 0, 
        "DaysInterval": 1, 
        "FullLoadDaysOffset": 365
    },
}

Meta_Tables_Config = [
    {   **default_dict,
        "ObjectName": "Customers",
        "ApiUrl": "https://api.erp-system.com/customers",
        "ApiQueryParams": {
            "AlwaysApply": {"pagesize": "1000", "skippages": "0"}
        },
        "ApiLoadDays": None,
    },
    {   **default_dict,
        "ObjectName": "Invoices",
        "ApiUrl": "https://api.erp-system.com/invoices/booked",
        "ApiQueryParams": {
            "AlwaysApply": {"pagesize": "1000", "skippages": "0"},
            "IncrementalApply": {"filter": "date$gte:{start_date}"}
        },
        "ApiLoadDays": {
            "DaysOffset": 120, 
            "DaysInterval": None, 
            "FullLoadDaysOffset": None
        },
    },
    {   **default_dict,
        "ObjectName": "InvoiceDetails",
        "ApiUrl": "https://api.erp-system.com/invoices/booked/{invoiceNumber}",
        "ApiUrlParam": {"invoiceNumber": "bookedInvoiceNumber"},
        "BaseParamTable": {
            "TableZone": "bronze",
            "TableName": "ERP_v1/Invoices",
            "SelectColumns": ["collection__bookedInvoiceNumber"], 
            "TransformColumns": {
                "bookedInvoiceNumber": "collection__bookedInvoiceNumber"
            }
        },
        "ApiLoadDays": None,
    },
]
```

Notice the `InvoiceDetails` entry: it uses a `BaseParamTable` to look up invoice numbers from a previously loaded Bronze table and loops over them, substituting each into the URL. This is a common pattern when an API requires you to call a detail endpoint once per parent record.

The generic ingestion notebook reads this configuration and executes the extraction. The core loop handles pagination, incremental date ranges and writes raw payloads to OneLake before transforming them into Bronze Delta tables.

code example 3.14: Core API ingestion loop with pagination (simplified)
```python
# Parameters passed from pipeline
ApiName  = 'ERP'
ApiTable = 'Invoices'
LoadType = 'Daily'

# Load configuration from metadata lakehouse
ls_config = api.get_table_config(df_metadata, ApiName, ApiVersion, ApiTable)
api_access = api.set_access(ls_config.get('AuthParam'))

# Resolve date intervals for incremental loading
df_intervals = api.resolve_load_intervals(
    load_days_config=ls_config.get('ApiLoadDays'),
    load_type=LoadType
)

# Resolve parameter combinations (base table × date intervals)
param_rows = api.resolve_base_params(ls_config.get("BaseParamTable"), 
                                      df_intervals, dwr, ws, raw_lh, bronze_lh, LoadType)

for param_row in param_rows:
    url = ls_config.get("ApiUrl")
    params = api.resolve_query_params(query_params_config, LoadType, param_row)
    page_number = 1

    # Substitute URL placeholders from metadata
    if api_url_param_map:
        for placeholder, field_name in api_url_param_map.items():
            url = url.replace(placeholder, str(param_row[field_name]))

    # Paginated extraction
    while True:
        response = api.get_request(url=url, headers=api_access.get("headers"),
                                   params=params, auth=api_access.get("auth"))
        
        # Write raw payload to OneLake Files (Raw layer)
        dwr.write_file_to_onelake(
            folder_path=raw_folder, data=response.text,
            page_number=page_number, file_format='json'
        )
        
        # Check for next page
        next_url = api.get_next_url(response, ls_config, pagination_key, 'json')
        if not next_url:
            break
        page_number += 1
        url = next_url
```

After extraction, raw files are read with Spark, flattened from nested JSON, enriched with metadata columns and written to Bronze as Delta tables.

code example 3.15: Raw to Bronze transformation
```python
# Read all raw JSON files from the extraction run
df_raw = (spark.read
    .option("recursiveFileLookup", "true")
    .option("multiLine", multi_line)
    .json(raw_source))

# Flatten nested structures and sanitize column names
df_raw_clean = nt.flatten_dataframe(df_raw)
df_raw_clean = nt.fix_header(df_raw_clean)

# Add engineering metadata columns
bronze_df = (df_raw_clean
    .withColumn("DW_source_file", col("_metadata.file_name"))
    .withColumn("DW_source_file_added", col("_metadata.file_modification_time"))
    .withColumn("DW_processing_time", current_timestamp())
    .withColumn("DW_RunID", lit(DWRunID))
    .withColumn("SourceSystem", lit(ls_config.get("SourceSystem"))))

# Write to Bronze lakehouse as Delta table
dwr.write_data_frame_to_onelake(
    df=bronze_df, workspace=ws, lakehouse=bronze_lh,
    table_name=bronze_table, write_mode="overwrite")
```

### Silver layer — generic cleansing
The Silver notebook is entirely metadata-driven. A configuration table in the metadata lakehouse defines for each Silver table which Bronze table to read, which columns to select, how to rename and cast them and which columns form the primary key for deduplication.

code example 3.16: Metadata-driven Silver ETL
```python
# Parameters passed from pipeline
SilverSystemName = 'erp'
SilverTableName  = 'invoicedetails'
LoadType = 'Daily'

# Load silver metadata configuration
silver_config = df_silver_metadata.filter(
    (col("SilverSystemName") == SilverSystemName) & 
    (col("SilverTableName") == SilverTableName)
).first().asDict()

# Extract configuration
bronze_table_path = silver_config.get("BronzeTablePath")
silver_columns    = silver_config.get("SilverColumns", [])
pk_cols           = silver_config.get("PK", [])
order_by          = silver_config.get("OrderBy", ["DW_source_file_added"])

# Load Bronze source
bronze_df = dwr.load_delta_from_lakehouse(
    workspace=ws, lakehouse=bronze_lh, table_name=bronze_table_path)

# Apply column selections, renames and type casts from metadata
silver_df = nt.select_silver_columns(bronze_df, silver_columns)

# Deduplicate: keep latest record per primary key
if pk_cols:
    order_cols = [col(c).desc() for c in order_by]
    w = Window.partitionBy(*pk_cols).orderBy(*order_cols)
    silver_df = (silver_df
        .withColumn("_rn", row_number().over(w))
        .filter(col("_rn") == 1)
        .drop("_rn"))

# Write to Silver lakehouse
write_mode = 'overwrite' if LoadType == 'Full' else 'merge'
dwr.write_data_frame_to_onelake(
    df=silver_df, workspace=ws, lakehouse=silver_lh,
    table_name=silver_table, write_mode=write_mode)
```

The beauty of this pattern is that adding a new source table to the Silver layer requires no new code. You add a row to the metadata configuration table and the existing notebook handles the rest. This is what metadata-driven development looks like in practice.

### Gold layer — building the star schema in code
The Gold layer is where the dimensional model comes to life. Each dimension and fact table has its own notebook that reads from Silver, applies business logic and writes to Gold. Here the patterns from earlier in this chapter — surrogate keys, star schemas, joins — are implemented in PySpark.

**Building a dimension with SCD Type 2**

Slowly changing dimensions (SCD Type 2) track historical changes. When a customer changes address, we don't overwrite the old record — we close it and insert a new version. This allows analysts to see what the customer looked like at the time of any given transaction.

code example 3.17: Customer dimension with SCD Type 2 and surrogate keys
```python
# Load Silver source
silver_customer = dwr.load_delta_from_lakehouse(
    workspace=ws, lakehouse=silver_lh, table_name='erp/customers')

# Build dimension with SCD columns
dim_customer = (silver_customer
    .withColumn('Customer_SK', lit(0))
    .withColumn('Customer_PK', 
        nt.hash_key_sha2(['CustomerNumber_BK', 'SourceSystem']))
    .withColumn('DW_DateStart', to_timestamp(lit('1900-01-01 00:00:00')))
    .withColumn('DW_DateEnd',   to_timestamp(lit('9999-12-31 23:59:59')))
    .withColumn('DW_IsCurrent', lit(1))
    .withColumn('row_sha2_scd2', 
        sha2(concat_ws('||', *[col(c).cast('string') for c in type2_columns]), 256))
    .select(
        'Customer_SK', 'Customer_PK', 'CustomerNumber_BK',
        'Currency', 'Address', 'City', 'CountryName', 'Name', 'ZipCode',
        'SourceSystem', 'DW_DateStart', 'DW_DateEnd', 
        'DW_IsCurrent', 'row_sha2_scd2'
    ))

# Create unknown row (SK = -1) for referential integrity
unknown_row = nt.create_surrogate_unknown_row(dim_customer)

# Preserve existing surrogate keys for incremental loads
existing_dim = dwr.load_delta_from_lakehouse(
    workspace=ws, lakehouse=gold_lh, table_name='dbo/Dim_Customer')

dim_customer_final = nt.add_surrogate_key_incremental(
    df=dim_customer, existing_df=existing_dim,
    pk_columns=['Customer_PK'], sk_column='Customer_SK')

dim_customer_union = dim_customer_final.unionByName(unknown_row)

# Validate primary key uniqueness
nt.check_primary_key_unique(
    df=dim_customer_union, pk_columns=['Customer_PK'])

# Write with SCD Type 2 merge logic
dwr.write_delta_with_scd2_to_onelake(
    source_df=dim_customer_union, workspace=ws, lakehouse=gold_lh,
    table_name='dbo/Dim_Customer', business_keys=['Customer_PK'],
    type2_columns=type2_columns, sk_column='Customer_SK')
```

The SCD2 write method matches incoming rows to existing ones by business key. If the hash of tracked columns has changed, it closes the old version (`DW_IsCurrent = 0`, `DW_DateEnd = yesterday`) and inserts a new version with a new surrogate key. If the hash matches, it updates in place.

**Building a date dimension**

The date dimension is generated rather than sourced. It creates a continuous date spine spanning 30 years with temporal attributes that allow analysts to slice by year, quarter, month, week and day.

code example 3.18: Generating the date dimension
```python
start_date = date(2010, 1, 1)
end_date   = date(2040, 12, 31)
span_days  = (end_date - start_date).days

# Build continuous date spine
date_df = (spark.range(0, span_days + 1)
    .withColumn('Date', expr(f"date_add('{start_date}', CAST(id AS INT))"))
    .drop('id')
    .withColumn('Date_SK', date_format(col('Date'), 'yyyyMMdd').cast('int')))

# Enrich with temporal attributes
date_enriched = (date_df
    .withColumn('Year',       year(col('Date')))
    .withColumn('Quarter',    quarter(col('Date')))
    .withColumn('Month',      month(col('Date')))
    .withColumn('Day',        dayofmonth(col('Date')))
    .withColumn('WeekOfYear', weekofyear(col('Date')))
    .withColumn('DayOfWeek',  dayofweek(col('Date')))
    .withColumn('MonthName',  date_format(col('Date'), 'MMMM'))
    .withColumn('DayName',    date_format(col('Date'), 'EEEE'))
    .withColumn('YearMonth',  date_format(col('Date'), 'yyyy-MM'))
    .withColumn('IsWeekend',  col('DayOfWeek').isin(1, 7)))
```

**Building a fact table with dimension lookups**

The fact table reads from Silver, creates composite keys, calculates derived measures and joins to dimensions to pick up surrogate keys. Missing references default to the unknown row (`SK = -1`) using `coalesce` — ensuring referential integrity is never broken.

code example 3.19: Invoice fact table with dimension lookups
```python
# Load Silver source
silver_invoices = dwr.load_delta_from_lakehouse(
    workspace=ws, lakehouse=silver_lh, table_name='erp/invoicedetails')

# Create composite keys and calculated measures
fact_invoice = (silver_invoices.alias('i')
    .withColumn('Invoice_PK', 
        nt.hash_key_sha2(['InvoiceNumber_BK', 'LineNumber', 'SourceSystem']))
    .withColumn('Date_SK', 
        date_format(col('InvoiceDate'), 'yyyyMMdd').cast('int'))
    .withColumn('ExchangeRate', 
        coalesce(col('ExchangeRate'), lit(1.0)))
    .withColumn('M_Amount_DKK', 
        coalesce(col('NetAmountInBaseCurrency'), 
                 col('AmountExclusiveVAT') * col('ExchangeRate')))
    .withColumn('M_Amount_VAT_DKK', 
        coalesce(col('AmountVAT'), lit(0)) * col('ExchangeRate'))
    .select(
        'Invoice_PK', 'InvoiceNumber_BK', 'LineNumber',
        'CustomerNumber_BK', 'ProductNumber_BK',
        'InvoiceDate', 'Date_SK', 'ExchangeRate',
        'M_Amount_DKK', 'M_Amount_VAT_DKK',
        'LineQuantity', 'LineUnitNetPrice',
        'SourceSystem'))

# Load dimensions and lookup surrogate keys
dim_customer = dwr.load_delta_from_lakehouse(
    workspace=ws, lakehouse=gold_lh, table_name='dbo/Dim_Customer'
).select('Customer_SK', 'CustomerNumber_BK', 'SourceSystem')

dim_product = dwr.load_delta_from_lakehouse(
    workspace=ws, lakehouse=gold_lh, table_name='dbo/Dim_Product'
).select('Product_SK', 'ProductNumber_BK', 'SourceSystem')

# Join and default missing references to unknown row (SK = -1)
fact_final = (fact_invoice
    .join(dim_customer, ['CustomerNumber_BK', 'SourceSystem'], 'left')
    .join(dim_product,  ['ProductNumber_BK', 'SourceSystem'], 'left')
    .withColumn('Customer_SK', coalesce('Customer_SK', lit(-1)))
    .withColumn('Product_SK',  coalesce('Product_SK',  lit(-1))))

dwr.write_data_frame_to_onelake(
    df=fact_final, workspace=ws, lakehouse=gold_lh,
    table_name='dbo/Fact_Invoices', write_mode='overwrite')
```

### Pipeline orchestration
Individual notebooks are orchestrated by pipelines that chain the medallion layers in sequence. The orchestration pipeline invokes Bronze first, waits for completion, then Silver and finally Gold. Each layer can contain sub-pipelines that run multiple source systems in parallel.

code example 3.20: Pipeline orchestration definition (simplified)
```json
{
  "activities": [
    {
      "name": "Bronze 1-0",
      "type": "InvokePipeline",
      "dependsOn": []
    },
    {
      "name": "Silver 2-0",
      "type": "InvokePipeline",
      "dependsOn": [
        { "activity": "Bronze 1-0", 
          "dependencyConditions": ["Completed"] }
      ]
    },
    {
      "name": "Gold 3-0",
      "type": "InvokePipeline",
      "dependsOn": [
        { "activity": "Silver 2-0", 
          "dependencyConditions": ["Completed"] }
      ]
    }
  ]
}
```

In tools like Microsoft Fabric Data Factory or Azure Data Factory this JSON translates to a visual pipeline where you can see the dependency chain, monitor run history and set up scheduled triggers. I created a pipeline called *full_orchestration* which invokes three children pipelines. Figure 3.9 shows the full orchestration pipeline which chains the three medallion layers sequentially.

![Full orchestration pipeline](full-orchestration-pipeline.png)
Figure 3.9 Full orchestration pipeline chaining Bronze, Silver and Gold layers

Opening the bronze pipeline reveals that there are three different APIs that is ingested into the data platform with the framework used above. Figure 3.10 shows the bronze sub-pipeline.

![Bronze pipeline](bronze-pipeline.png)
Figure 3.10 Bronze pipeline invoking three API ingestion pipelines

After that run completes, the silver pipeline is invoked which runs a loop over all the tables having been defined in a dedicated silver metadata notebook. Figure 3.11 shows the silver pipeline with its metadata lookup and ForEach loop.

![Silver pipeline](silver-pipeline.png)
Figure 3.11 Silver pipeline with metadata-driven ForEach loop

Finally we have the gold pipeline that runs dimensions first to generate surrogate keys and on completion the fact tables are created. Figure 3.12 shows the gold pipeline.

![Gold pipeline](gold-pipeline.png)
Figure 3.12 Gold pipeline loading dimensions before facts

This is how data pipelines might be orchestrated and designed in a enterprise level environment.

### Semantic models and serving finished goods
The star schema in the Gold layer feeds Power BI semantic models. These models define relationships between facts and dimensions, and contain DAX measures that calculate business KPIs. The dimensional model we built in code becomes directly queryable through visualizations.

code example 3.21: DAX measures for a finance report
```dax
-- Base measure: sum of financial entries in base currency
Amount = SUM(Fact_FinancialEntries[M_Amount_DKK])

-- Revenue: filter to revenue accounts only
Revenue = CALCULATE([Amount], Dim_Account[Accounting Group] = "Revenue")

-- Costs: filter to cost accounts
Costs = CALCULATE([Amount], Dim_Account[Accounting Group] = "Costs")

-- Profit and margin
Profit = [Revenue] + [Costs]
Profit Margin % = [Profit] / [Revenue]
```

More sophisticated measures can build an entire income statement dynamically using `SWITCH` to calculate subtotals like gross profit and EBITDA.

code example 3.22: Dynamic income statement measure
```dax
Income Statement Amount = 
    VAR CurrentCalcType = SELECTEDVALUE(ChartOfAccountsLayout[CalcType])
    VAR Revenue = 
        CALCULATE(SUM(Fact_FinancialEntries[M_Amount_DKK]),
            Dim_Account[Accounting Group] = "Revenue")
    VAR CostOfSales = 
        CALCULATE(SUM(Fact_FinancialEntries[M_Amount_DKK]),
            Dim_Account[Accounting Sub Group] = "Direct costs")
    VAR GrossProfit = Revenue + CostOfSales
    VAR EBITDA = GrossProfit + 
        CALCULATE(SUM(Fact_FinancialEntries[M_Amount_DKK]),
            Dim_Account[Accounting Group] = "Costs",
            Dim_Account[Accounting Sub Group] IN {"Operating Expenses", "Payroll"})
    RETURN
    SWITCH(CurrentCalcType,
        "Accounts", CALCULATE(SUM(Fact_FinancialEntries[M_Amount_DKK]),
            Dim_Account[Accounting Sub Group] = 
                SELECTEDVALUE(ChartOfAccountsLayout[SubGroup])),
        "RevenueTotal", Revenue,
        "GrossProfit", GrossProfit,
        "EBITDA", EBITDA)
```

Similarly a sales report model might define year-over-year comparisons and month-to-date calculations using time intelligence functions. These DAX measures are the final layer of transformation turning the star schema into the specific KPIs and views that business users consume. Figure 3.13 shows a customer analytics dashboard built on a dimensional model. The report segments customers by spend tier and order frequency and visualizes revenue distribution and average order value — the kind of insight that becomes possible once data flows through the full lifecycle from ingestion to a well-modeled star schema.

![Customer analytics dashboard](customer-analytics-dashboard.png)
Figure 3.13 Customer analytics dashboard showing spend tiers, order frequency, revenue distribution and average order value

### What this platform demonstrates
Walking through this platform end to end, we can see the same lifecycle that began with a local SQLite database and a weather API in the earlier sections. The difference is not in the logic but in the infrastructure and engineering practices that surround it.

| Concept | Prototype | Production |
| --- | --- | --- |
| Ingestion | `requests.get()` to a free API | Metadata-driven API loop with auth, pagination, watermarks |
| Storage | Local `.db` file or CSV | OneLake lakehouses with Delta tables |
| Transformation | Pandas DataFrame operations | PySpark with metadata-driven column maps and deduplication |
| Dimensional model | PowerQuery star schema | PySpark with SCD2, surrogate keys, unknown rows |
| Serving | Matplotlib plot | Power BI semantic models with DAX measures |
| Orchestration | Manual script execution | Pipeline chains with dependency management |

The skills are the same. Python, SQL, Spark, dimensional modeling, data quality validation — these transfer directly from personal projects to enterprise scale. What changes is the wrapper: version control, automated pipelines, shared libraries and cloud infrastructure.

To sum it up we might have the following check list questions whenever we stand in front of a new data project.
* Does this data serve productive use cases? 
* Have we modeled the data to design the solution? 
* What are the security risks if any with this data? 
* Who are going to be responsible for the solution from the technical and business side? 
* Is the data already generated? If so, where is it located? or do we need to generate it ourselves?
* What quality is or should the data be in? 
* Can we do things at the source to increase the data quality? 
* What methods of extraction are we allowed to use?
* How often can the data be copied from the source database and what is most appropriate frequency? 
* Should we copy the entire data and overwrite existing or can we copy the rows that have been inserted and updated since last time? 
* What is the volume and format of the data? also known as the *payload* of the data.
* Where should the data land?
* Is the analytical model for data visualizations based on dimensional modeling or data scientific use?
* How can we extend the analytical model with custom measures?

  

