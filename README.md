# Data Portfolio: Excel to Power BI

## Table of Contents
- [Objectives](#objective)
- [Data Source](#data-source)
- [Stages](#stages)
- [Design](#design)
  - [Tools](#tools)
- [Development](#development)
  - [Pseudocode](#pseudocode)
  - [Data Exploration](#data-exploration)
  - [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)
  - [Create the SQL View](#create-the-sql-view)
- [Data Quality Test](#testing)
- [Visualization](#visualization)
- [Analysis](#analysis)
- [Validation](#validation)  


## Objectives
The Head of Marketing wants to find out who the top YouTubers are in 2024 to determine which YouTubers are most suitable for marketing campaigns for the remainder of the year.

### Key Notes from Marketing Department
- Channels with most subscribers: 
Campaign idea = product placement
Campaign cost (one-time fee) = $50,000

- Channels with most videos uploaded:
Campaign idea = sponsored video series
Campaign cost (11-videos @ $5,000 each) = $55,000

- Channels with most views:
  Campaign idea = Influencer marketing
  Campaign cost (3-month contract) = $130,000
  
### Ideal Solution
To create a dashboard that provides insights into the top UK YouTubers in 2024 that includes the following:
- Subscriber count
- Total views
- Total videos
- Engagement metrics

This will help the marketing team make informed decisions regarding which YouTubers to collaborate with for their marketing campaigns.

## Data Source
### What data is needed to achieve our objective?
We need data on the top UK YouTubers in 2024 that includes:
- Channel names
- Total subscribers
- Total views
- Total videos uploaded

### Where is the data coming from?
The data is sourced from Kaggle (an Excel extract), which can be found [here](https://www.kaggle.com/datasets/bhavyadhingra00020/top-100-social-media-influencers-2024-countrywise?resource=download).

## Stages
- Design
- Development
- Testing
- Analysis

## Design
### Dashboard components requirement
To understand what it should contain, we need to figure out what questions we need the dashboard to answer:
1. Who are the top 10 YouTubers with the most subscribers?
2. Which 3 channels have uploaded the most videos?
3. Which 3 channels have the most views?
4. Which 3 channels have the highest average views per video?
5. Which 3 channels have the highest views per subscriber ratio?
6. Which 3 channels have the highest subscriber engagement rate per video uploaded?

### Tools

| Tool | Purpose
 --- | ---
| Excel | Exploring Data |
|  SQL Server | Cleaning, testing, and analyzing the data |
| Power BI | Visualizing the data via interactive dashboards |
| GitHub | Hosting the project documentation and version control |

## Development

### Pseudocode
- What is the general approach in creating this solution from start to finish?
1. Get the data
2. Explore the data in Excel
3. Load the data into SQL Server
4. Clean the data with SQL
5. Visualize the data in Power BI
6. Generate the findings based on the insights
7. Write the documentation + commentary
8. Publish the data to GitHub Pages

### Data Exploration Notes
1. There are at least 4 columns that contain the data we need for this analysis, which signals we have everything we need from the file without needing to contact the client for any more data.
2. The first column contains the channel ID with what appears to be channel IDS, which are separated by a @ symbol - we need to extract the channel names from this.
3. Some of the cells and header names are in a different language - we need to confirm if these columns are needed, and if so, we need to address them.
4. We have more data than we need, so some of these columns would need to be remove

### Data Cleaning
The cleaned data should meet the following criteria and constraints:
  - Only relevant columns should be retained.
  - All data types should be appropriate for the contents of each column.
  - No column should contain null values, indicating complete data for all records.
Below is a table outlining the constraints on our cleaned dataset:

| Property | Description |
 --- | ---
| Number of Rows | 100 | 
| Number of Columns | 4 |

And here is a tabular representation of the expected schema for the clean data:

| Column Name	| Data Type	| Nullable |
---|---|---
| channel_name | VARCHAR | NO |
| total_subscribers	| INTEGER	| NO |
| total_views	| INTEGER	| NO |
| total_videos |	INTEGER |	NO |

- What steps are needed to clean and shape the data into the desired format?
1. Remove unnecessary columns by only selecting the ones you need
2. Extract Youtube channel names from the first column
3. Rename columns using aliases

## Transform the Data
The following SQL query is used to transform the data to extract YouTuber names (before the '@' character) along with their total subscribers, views, and videos uploaded:

```sql 
SELECT 
	cast(SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) - 1) as varchar(100)) AS YtName
	,[total_subscribers]
    ,[total_views]
     ,[total_videos]
   FROM Top_UK_YTubers;

```
## Create the SQL View
``` sql
create view uk_youtubers_2024 as
SELECT 
	cast(SUBSTRING(NOMBRE, 1, CHARINDEX('@', NOMBRE) - 1) as varchar(100)) AS YtName
	,[total_subscribers]
    ,[total_views]
     ,[total_videos]
   FROM [Yt_database].[dbo].[Top_UK_YTubers];

```


## Data Quality Test
Here are the data quality tests conducted:

### Row and Column Check
![Row and Column Count](asset/Images/Row_and_Column.png)

### Data Types and Duplicate Check

![Data Type and Duplicates](asset/Images/Data_Type.png)


##  Visualization
### Results
- What does the visualization look like?

    ![Visual](asset/Images/viz.gif)
  

## Analysis
- What did we find out?
  Here are the key questions we need to answer for our marketing client:
1. Who are the top 10 YouTubers with the most subscribers?
2. Which 3 channels have uploaded the most videos?
3. Which 3 channels have the most views?
4. Which 3 channels have the highest average views per video?
5. Which 3 channels have the highest views per subscriber ratio?
6. Which 3 channels have the highest subscriber engagement rate per video uploaded?

### 1. Who are the top 10 YouTubers with the most subscribers?

| Rank	| Channel Name	| Subscribers (M) |
--- | --- | --- 
| 1 | NoCopyrightSounds | 33.60 |
| 2 | DanTDM | 28.60 |
| 3 | Dan Rhodes | 26.50|
| 4 | Miss Katy | 33.60 |
| 5 | Mister Max| 24.50 |
| 6 | KSI | 24.10 |
| 7 | Jelly| 23.50 |
| 8 | Dua Lipa | 23.30 |
| 9 | Sidemen | 21.00 |
| 10 | Ali-A | 18.90 |

### 2. Which 3 channels have uploaded the most videos (excluding news channels)?

| Rank	| Channel Name	| Vidoes |
--- | --- | --- 
| 1 | GRM Daily	| 14,696 |
| 2 | Manchester City | 8,248|
| 3 | Yogscast	 | 6,435 |

### 3. Which 3 channels have the most views?

| Rank	| Channel Name	|Views (M) |
--- | --- | --- 
| 1 | DanTDM | 19,776 |
| 2 | Dan Rhodes | 18,559|
| 3 | Mister Max| 15,974 |

### 4. Which 3 channels have the highest average views per video?

| Rank | Channel Name | Averge Views per Video (M) |
--- | --- | --- 
| 1 | Mark Ronson | 32.27 |
| 2 | Jessie J | 5.97 |
| 3 | Dua Lipa	| 5.76 |

### 5. Which 3 channels have the highest views per subscriber ratio?

| Rank | Channel Name | Views per Subscriber (M) |
--- | --- | --- 
| 1 | GRM Daily | 1,186 |
| 2 | Nicolodeon UK | 1,061 |
| 3 | Disney Junior UK	| 1,032 |

### 6. Which 3 channels have the highest subscriber engagement rate per video uploaded?

| Rank | Channel Name    | Subscriber Engagement Rate  |
|------|-----------------|---------------------------- |
| 1    | Mark Ronson     | 343,000                     |
| 2    | Jessie J        | 110,416.67                  |
| 3    | Dua Lipa        | 104,954.95                  |

### Notes
For this analysis, we’ll prioritize analysing the metrics that are important in generating the expected ROI for our marketing client, which are the YouTube channels wuth the most

- subscribers
- total views
- videos uploaded

## Validation
### 1. Youtubers with the most subscribers 

#### Calculation breakdown:
1. NoCopyrightSounds 
- Average views per video = 6.92 million
- Product cost = $5
- Potential units sold per video = 6.92 million x 2% conversion rate = 138,400 units sold
- Potential revenue per video = 138,400 x $5 = $692,000
- Campaign cost (one-time fee) = $50,000
- **Net profit = $692,000 - $50,000 = $642,000**

b. DanTDM

- Average views per video = 5.34 million
- Product cost = $5
- Potential units sold per video = 5.34 million x 2% conversion rate = 106,800 units sold
- Potential revenue per video = 106,800 x $5 = $534,000
- Campaign cost (one-time fee) = $50,000
- **Net profit = $534,000 - $50,000 = $484,000**

c. Dan Rhodes

- Average views per video = 11.15 million
- Product cost = $5
- Potential units sold per video = 11.15 million x 2% conversion rate = 223,000 units sold
- Potential revenue per video = 223,000 x $5 = $1,115,000
- Campaign cost (one-time fee) = $50,000
- **Net profit = $1,115,000 - $50,000 = $1,065,000**


Best option from category: Dan Rhodes

### SQL Query

![SQL Query](asset/Images/KPI_1.png)


### 2. Youtubers with the most videos uploaded

### Calculation breakdown 

Campaign idea = sponsored video series  

a. GRM Daily
- Average views per video = 510,000
- Product cost = $5
- Potential units sold per video = 510,000 x 2% conversion rate = 10,200 units sold
- Potential revenue per video = 10,200 x $5= $51,000
- Campaign cost (11-videos @ $5,000 each) = $55,000
- **Net profit = $51,000 - $55,000 = -$4,000 (potential loss)**

b. **Manchester City**

- Average views per video = 240,000
- Product cost = $5
- Potential units sold per video = 240,000 x 2% conversion rate = 4,800 units sold
- Potential revenue per video = 4,800 x $5= $24,000
- Campaign cost (11-videos @ $5,000 each) = $55,000
- **Net profit = $24,000 - $55,000 = -$31,000 (potential loss)**

b. **Yogscast**

- Average views per video = 710,000
- Product cost = $5
- Potential units sold per video = 710,000 x 2% conversion rate = 14,200 units sold
- Potential revenue per video = 14,200 x $5= $71,000
- Campaign cost (11-videos @ $5,000 each) = $55,000
- **Net profit = $71,000 - $55,000 = $16,000 (profit)**


Best option from category: Yogscast

### SQL Query

![SQL Query](asset/Images/KP1.png)


### 3.  Youtubers with the most views 

#### Calculation breakdown

Campaign idea = Influencer marketing 

a. DanTDM

- Average views per video = 5.34 million
- Product cost = $5
- Potential units sold per video = 5.34 million x 2% conversion rate = 106,800 units sold
- Potential revenue per video = 106,800 x $5 = $534,000
- Campaign cost (3-month contract) = $130,000
- **Net profit = $534,000 - $130,000 = $404,000**

b. Dan Rhodes

- Average views per video = 11.15 million
- Product cost = $5
- Potential units sold per video = 11.15 million x 2% conversion rate = 223,000 units sold
- Potential revenue per video = 223,000 x $5 = $1,115,000
- Campaign cost (3-month contract) = $130,000
- **Net profit = $1,115,000 - $130,000 = $985,000**

c. Mister Max

- Average views per video = 14.06 million
- Product cost = $5
- Potential units sold per video = 14.06 million x 2% conversion rate = 281,200 units sold
- Potential revenue per video = 281,200 x $5 = $1,406,000
- Campaign cost (3-month contract) = $130,000
- **Net profit = $1,406,000 - $130,000 = $1,276,000**

Best option from category: Mister Max

### SQL Query

![SQL Query](asset/Images/kpi2.png)


## Discovery
- What did we learn?
We discovered that

1. NoCopyrightSOunds, Dan Rhodes and DanTDM are the channnels with the most subscribers in the UK
2. GRM Daily, Man City and Yogscast are the channels with the most videos uploaded
3. DanTDM, Dan RHodes and Mister Max are the channels with the most views


## Recommendation
Based on the potential revenue and net profit estimates, the top three channels to prioritize for your YouTube campaign are:

1. Dan Rhodes (Most Subscribers & Most Views Categories)
- Net Profit: $1,065,000 (Subscribers) & $985,000 (Views)
- Reason: Dan Rhodes offers an outstanding reach with an average of 11.15 million views per video. His channel shows high engagement, making it a profitable choice with a strong net profit margin from both the subscribers and views perspectives. The low campaign cost relative to revenue potential further enhances the ROI, positioning him as the top pick.

2. Mister Max (Most Views Category)
- Net Profit: $1,276,000
- Reason: Mister Max delivers the highest average views per video (14.06 million) and correspondingly the highest potential net profit among all channels. If maximizing exposure and revenue is your key objective, this channel provides an excellent opportunity. The campaign investment yields impressive returns with a 2% conversion rate assumption.

3. NoCopyrightSounds (Most Subscribers Category)
- Net Profit: $642,000
- Reason: NoCopyrightSounds is ideal for tapping into a highly loyal and engaged subscriber base, with significant viewership (6.92 million views per video) and a net profit of $642,000. This channel offers a cost-effective option for strong audience engagement, ensuring consistent brand exposure.

### Conclusion:
Dan Rhodes, Mister Max, and NoCopyrightSounds should be your top choices. These channels not only promise substantial reach but also ensure profitable campaign outcomes, making them ideal for driving conversions and revenue growth for your product.


  




