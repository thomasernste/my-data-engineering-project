# Bitcoin/Reddit Data Engineering Project

### Introduction

Data scientists, their companies, and the general public as a whole are -- for a variety of reasons -- all interested  in trends in the price of Bitcoin over time, frequency of Bitcoin transactions, public sentiments about Bitcoin, and so on. Indeed, although Bitcoin's market valuation has fluctuated over time and declined over the last year or so, the Bitcoin total market capitalization is currently in the tens of billions of dollars.

However, although standard single node data science can find some basic insights from relatively small datasets, single node data science faces inherent challenges processing the kinds of massive data sets that contain much more complete informationn that can provide the greatest analytic value and insights about the issue. Having access to a data pipeline that enables efficient calculations on massive amounts of historical data about Bitcoin could be useful toward informing efforts by data scientists and others to better understand patterns over time in the price of Bitcoin, the frequency of exchanges, public sentiments about Bitcoin, and so on.

The data requirements for performing powerful analytics on trends in bitcoin price, public sentiment, and on other potential metrics requires the ability to ingest, process, and load massive datasets for analysis. Specifically, for this project, these data requirements can be met by a data engineering pipeline that facilitates access by data scientists to data from [**a massive publically available Bitcoin dataset**](https://www.kaggle.com/bigquery/crypto-bitcoin-cash) along with [**a massive publically available dataset containing all Reddit comments over time**](https://files.pushshift.io/reddit/).


### Project:

This data engineering project proposes to build such a pipeline that would enable front end users -- particularly data scientists -- to perform the calculations needed to search for trends and potential patterns in these massive datasets. The patterns they look for could be very simple -- for example, they could search the Reddit dataset for the frequency over time of relevant words like “Bitcoin” and “cryptocurrency” and “Blockchain” and perhaps other cryptocurrencies like Ethereum and, in a visualization, they could compare those frequencies to trends in the price of Bitcoin over time. Or, in a more advanced use for this project, a data scientist could use this data pipeline to perform a sentiment analysis on Reddit discussions of bitcoin and check for correlations between the status of public sentiments about Bitcoin (taken from the Reddit data) and Bitcoin price fluctuations over time (taken from the Bitcoin data). And so on.



### Data Pipeline:

This data is massive historical data in existing datasets (and not streaming data). For this reason, and because I have access to the AWS architecture, the appropriate ingestion tool for me would be Amazon Kinesis. In addition, although Amazon EMR could be used for the batch processing phase of my pipeline, it seems that the best tool for my batch processing purposes is Apache Spark (specifically, I would use PySpark because the code will be in Python). I would use Spark, for one, because it is better than Amazon EMR for performing the MapReduce process on very large datasets. Second, And further, the data cleaning that will be needed on these datasets can also be done in Spark. Data cleaning tasks will include, at the minimum, transforming the date columns into datetime values, removing usernames from the Reddit data, and stripping problem characters such as commas within Reddit comments that might cause problems within a csv file. Further, Spark is also better than Amazon EMR for facilitating analytical work by data scientists. For example, [as this discussion demonstrates](https://towardsdatascience.com/sentiment-analysis-with-pyspark-bc8e83f80c35), a data scientist could perform a sentiment analysis on the data within the Spark tool. 

To store the data within the Amazon AWS stack, I will run an SQL script on the data to store it in a star schema in Amazon Redshift (not in MySQL or PostgreSQL, since I want to take advantage of my access to the Amazon AWS stack).

