# EPRP_Louise_Schindler

# Cot Analysis



### Directory Structure

* [RunInfinuxDb.bat](RunInfinuxDb.bat): Bash script to run InfluxDB locally.
* [preProcessing.R](preProcessing.R): Script to download and insert COT reports into InfluxDB.
* [Market_and_Exchange_Names.xlsx](Market_and_Exchange_Names.xlsx): All Market and Exchange Names
* [app.R](app.R): Shiny app script.
* [dataset/](dataset/): After preProcessing.R  COT report data will be downloaded in this Directory.
* [screenshots/](screenshots/): directory contains images used in this readme.md file to provide visual context.



### Prerequisites

* Local installation of [InfluxDB](https://docs.influxdata.com/influxdb/v2/install/).
* Execute [RunInfinuxDb.bat](RunInfinuxDb.bat) to start InfluxDB locally. This script automatically runs InfluxDB from the command line.
* Execute [preProcessing.R](preProcessing.R) to download COT (Commitment of Traders) future-only reports (from 1986 to 2023) and insert them into the local InfluxDB database.

### Running the Shiny App

Execute [app.R](app.R) to launch the Shiny app.


### Note

* The data is downloaded from the [CFTC website](https://www.cftc.gov/MarketReports/CommitmentsofTraders/HistoricalCompressed/index.htm) future only report in Excel format (from 1986 to 2023).
* Make sure to configure InfluxDB token in both scripts.

```R
  token <- "lvNsjbSNYpIyM50wy1U9tIhN3gzWD_yppZpHfqxKEEerlsy2cvAewUVpMJT8uog9n9NVMXT7eyhdLd9CC6ZqcA=="
```




### Dataset

The dataset contains COT report data from 1986 to 2023 with a total of 126 columns. For this app, the following 41 important columns have been selected:


|   .           | **Selected Columns**              | .              
| ---------------------------------- | ----------------------------------|  ---------------------------------- |
| Market_and_Exchange_Names         | Report_Date_as_MM_DD_YYYY          | CFTC_Contract_Market_Code          |
| Open_Interest_All                  | NonComm_Positions_Long_All         | NonComm_Positions_Short_All        |
| NonComm_Postions_Spread_All        | Comm_Positions_Long_All            | Comm_Positions_Short_All           |
| Tot_Rept_Positions_Long_All        | Tot_Rept_Positions_Short_All       | NonRept_Positions_Long_All         |
| NonRept_Positions_Short_All        | Change_in_Open_Interest_All        | Change_in_NonComm_Long_All         |
| Change_in_NonComm_Short_All        | Change_in_NonComm_Spead_All        | Change_in_Comm_Long_All            |
| Change_in_Comm_Short_All           | Change_in_Tot_Rept_Long_All        | Change_in_Tot_Rept_Short_All       |
| Change_in_NonRept_Long_All         | Change_in_NonRept_Short_All        | Pct_of_OI_NonComm_Long_All         |
| Pct_of_OI_NonComm_Short_All        | Pct_of_OI_NonComm_Spread_All       | Pct_of_OI_Comm_Long_All            |
| Pct_of_OI_Comm_Short_All           | Pct_of_OI_Tot_Rept_Long_All        | Pct_of_OI_Tot_Rept_Short_All       |
| Pct_of_OI_NonRept_Long_All         | Pct_of_OI_NonRept_Short_All        | Traders_Tot_All                    |
| Traders_NonComm_Long_All           | Traders_NonComm_Short_All          | Traders_NonComm_Spread_All         |
| Traders_Comm_Long_All               | Traders_Comm_Short_All              | Traders_Tot_Rept_Long_All          |
| Traders_Tot_Rept_Short_All          | Contract_Units                      |



### App OverView

There are thee Tabs in the shinyapp.




#### 1. User Guide

![userguide](screenshots/userguide.png)
In "Overview" section of the Shiny app have Reference tables that include information about the Commitments of Traders (COT) dataset and a comprehensive list of all markets and exchange names. This section serves as a valuable resource for accessing detailed information about the COT dataset and obtaining insights into various markets.
#### 2. Data Overview

![dataoverview](screenshots/overview.png)

The "Overview" section of the Shiny app provides a quick summary of key information:

- **Time Period Coverage**
  - From-To: 1986-2023
- **Total Number of Market and Exchange Names**
- **Top Contract Units Packed Bubble Chart**
    - Explore the most common contract units through an interactive packed bubble chart.
- **Comparison between two Markets**
  - Select two market and exchange names for comparison using scatter and bar plots.
  - Analyze and contrast Non-Commercial and Commercial positions for the chosen markets.
  - Display the average open interest for selected markets over the last 10 years.
#### 3. Analysis


The "Analysis" tab provides users with a powerful tool for dynamic market analysis. 

- The dropdown menu allows users to choose from a list of available markets. This feature enhances the flexibility of the analysis, enabling users to focus on specific assets.
- The date picker (dateInput) complements the market selection by enabling users to narrow down their analysis to a specific date.

**Market Overview/Table**

![analysisTable](screenshots/analysisTable.png)

Upon selecting a market and date, the analysis tab generates an overview Table of key metrics related to the chosen market. This includes open interest, changes in positions, and the distribution of traders among different categories (e.g., non-commercial, commercial) also includes details about market Position Changes, percentage of open interest held by different categories of traders, Trader Count etc


The true strength of the "Analysis" tab lies in its interactivity. Users can seamlessly switch between markets and dates, instantly observing how changes in parameters impact the displayed analysis. 

**Long vs Short (Bar Chart)**

![longVsShortBarChart](screenshots/longVsShortBarchart.png)


This bar chart provides a visual breakdown of long and short positions for different trader types, dynamically generated based on the selected market and date.This bar chart was chosen to complement the tabular data and provide a visual representation of the distribution of long and short positions across different trader categories.

While the table offers detailed numerical information, the bar chart provides a visual summary. Together, they offer a comprehensive view of market dynamics, catering to users who prefer both numerical details and visual insights.

All other plots will be filtered based solely on the market, without consideration for the date.

**Long and Short Correlation**

![Long vs Short Corealation](screenshots/longVsShortCorelation.png)

The correlation matrix, on Non-Commercial and Commercial Long/Short positions, reveals relationships between these variables. Positive correlations signal simultaneous movements, while negative correlations indicate opposing trends.

**Long and Short Positions Heatmap**

![Long and Short Positions Heatmap](screenshots/longAndShortHeatMap.png)


Heatmap visually represents how the different types of positions (long and short) in the COT data have changed over time. The color intensity indicates the magnitude of the values, providing insights into the trends and patterns of the COT data for the specified positions.


**Net Positions**

![Net Positions](screenshots/netPosition.png)


The net positions chart provides an overview of the overall market sentiment by summing up long and short positions. Positive values indicate a bullish market sentiment, while negative values suggest a bearish sentiment. It serves as a valuable tool for gauging the overall market direction.

**Positions: Long**

![Positions: Long](screenshots/positionLong.png)


This chart focuses specifically on long positions, offering insights into the prevailing sentiment among traders. Understanding the distribution of long positions helps users assess market optimism and potential upward trends.

**Positions: Short**

![Positions: Short](screenshots/positionShort.png)


Similarly, the short positions chart sheds light on market pessimism and potential downward trends. Analyzing the distribution of short positions provides valuable information about trader expectations for market declines.


These charts collectively offer a comprehensive toolkit for users to interpret market dynamics, catering to diverse preferences for both numerical details and visual representations.
