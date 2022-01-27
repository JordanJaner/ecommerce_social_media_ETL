# ecommerce_social_media_ETL

## Project Purpose

This project aims to create a PostgresSQL database that can examine the influence of social media 
on ecommerce.

### Research Questions
* What changes in ecommerce have arisen due to the influence of social media?
* Is there a correlation between social media usage and ecommerce profit?
* How does usage between platforms/devices change overtime?
* What predictions can we make going forward?

### Data Sources
For this project, we used two data sources. The first was, monthly Social Media Market Share data in the United States by platform and device type from the Stat Counter website.
https://gs.statcounter.com/social-media-stats/all/united-states-of-america/#monthly-201901-202112-bar

<img src="/images/social_media_raw.png" alt="Raw Social Media Data"/>

The second was US Census Data of monthly retail sales by retail type. Specifically, the dataset was called Estimated Food and Services Sales by Kind of Business (US Census 1992-2021).
https://view.officeapps.live.com/op/view.aspx?src=https%3A%2F%2Fwww.census.gov%2Fretail%2Fmrts%2Fwww%2Fmrtssales92-present.xls&wdOrigin=BROWSELINK

<img src="/images/retail_raw.png" alt="Raw Retail Sales Data"/>


### Data Extraction
Social Media Data was available from 2009 to 2021 so we used the entire timeframe. That said, one of the device types that we were interested in started gaining traction in 2012. So, for the retail data, although we had data ranging from 1992-2021 in the original data source, we decided to focus on data from 2021-2021. The social media data was clean. The retail data however, needed to be transposed and have rows removed to be usable. Transposing and the removing of rows was done in Excel. The rest of the cleaning was conducted in Jupyter Notebook.

### Data Transformation
Next the data had to be cleaned and appended in Jupyter notebook to be usable by PostgresSQL. First dependencies were added, and csv files were stored in DataFrames. 
<img src="/images/store_platform.png" alt="Store Platform"/>

DataFrames were reduced to the relevant columns. 
<img src="/images/reduce_df.png" alt="Reduce Platform"/>
<img src="/images/reduce_retail.png" alt="Reduce Retail"/>

A device type column was added to the platform DataFrames to be used to identify data later when the platform DataFrames were appended. 
<img src="/images/add_column.png" alt="Add Column"/>

The DataFrames were appended since they had all of the same columns across years. 
<img src="/images/append_platform.png" alt="Append Platform"/>
<img src="/images/append_retail.png" alt="Append Retail"/>

To make retail and platform data comparable, we changed the date format of the retail data so that it matched the platform data.
<img src="/images/date_change.png" alt="Date Change"/>
<img src="/images/datetime.png" alt="Date Time"/> 

Finally, we converted the appended DataFrames into csv files that could be imported into pgAdmin4
<img src="/images/new_csv.png" alt="Create New CSV Files"/>

### Data Loading
This next section was conducted using pgAdmin4. Tables were created and the csv file data were added to them. Then the created database was connected back to Jupyter Notebook. 

### Conclusions and Limitations
First, we'll discuss the conclusions. As popular social media sites increase in market share, so does retail sales. This finding can be broken up further by device type. From 2009-2021, US desktop usage gradually decreased while mobile usage gradually increased until each device stabilized around the same number of time being used. People in the US could be online purchasing more from their mobile devices. This is especially relevant information for marketing departments because they can tailor their organization's content to be more mobile-friendly or create company apps for mobile devices. 

The limitations were the following:
We were not able to find affordable Social Media Ad Data. The data that we found was out of our price range and meant for brands to track their own ads' market penetration as opposed to tracking the market. Similarly, social media platform APIs no longer offer open access to their APIs, what is available to users is now much more limited in scope. Social media usage is based on page views only. 

Specific to our study, we limited it to a select amount of social media platforms. The size of sample data reflects a total of 2.7 billion page views for United States. Some alternative ways we could have formed the database for analysis would be to collect the full 1992-2021 Census Sales Data to pre-post analysis of Retail Sales and Social Media to then compare retail sales before social media versus after the appearance of particular platforms.



