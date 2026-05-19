# Project 02 - Streaming and Query Finance Data

## Project Overview
Our final Project 2 builds a real-time stock data pipeline using AWS cloud services. 
Historical daily stock price data was collected for 66 randomly selected S&P 500 
companies using the Alpha Vantage API. The data was streamed through AWS Kinesis, 
stored in Amazon S3, cataloged using AWS Glue, and queried using AWS Athena. 
Finally, the query results were visualized using Python in a Jupyter Notebook.

## Technology Stack
- **AWS Lambda** — collects stock data from Alpha Vantage API and streams it to Kinesis
- **AWS Kinesis Data Stream** — receives individual stock records from Lambda
- **AWS Kinesis Firehose** — delivers streamed data to S3
- **Amazon S3** — stores raw JSON stock data files
- **AWS Glue** — crawls and catalogs S3 data for querying
- **AWS Athena** — queries the cataloged data using SQL
- **Python/Jupyter Notebook** — visualizes query results

## Data
- 66 randomly selected S&P 500 companies
- 100 trading days of historical daily data per company
- 6,600 total records
- Fields: name, ts, open_stock, close_stock, difference

## Dataset Statistics
- Total Records: 396 (66 companies × 6 months)
- Mean % Change: -0.019% (overall market slightly negative)
- Std Deviation: 0.598 (moderate volatility)
- Min: -2.68% (ANET, May 2026)
- Max: +4.11% (SNDK, May 2026)
- Median: 0.018% (most companies near flat performance)

## Visualization Questions

### Visualization 1 — Heatmap of Monthly % Changes Across Companies and Time
The heatmap reveals several key patterns across the 66 companies 
over the 6-month period from December 2025 to May 2026:

- **May 2026 shows the most extreme movements** in both directions, 
  suggesting a market-wide event that caused significant volatility 
  across multiple sectors simultaneously.
- **SNDK had the strongest positive movement** at +4.11% in May 2026, 
  followed by WDC (+2.60%) and STX (+2.54%), suggesting strength 
  in the storage/semiconductor sector.
- **ANET had the biggest negative movement** at -2.68% in May 2026, 
  followed by WFC (-1.75%) and PODD (-1.75%).
- **January and February 2026** show mostly positive values (green) 
  across companies, indicating a broadly positive market period.
- **March 2026** shows a mixed picture with some companies turning 
  negative, suggesting early market uncertainty.
- Companies like **SNDK, WDC, STX and MPWR** consistently showed 
  positive performance, while **PODD, COO and BSX** were consistently 
  negative throughout the period.

### Visualization 2 — Companies Ranked by Average Daily % Change
The bar chart ranks all 66 companies by their average monthly 
percentage change over the full period:

#### Top 5 Performers
| Rank | Company | Avg Monthly % Change |
|---|---|---|
| 1 | SNDK | +1.44% |
| 2 | WDC | +0.86% |
| 3 | STX | +0.73% |
| 4 | VRT | +0.44% |
| 5 | BIIB | +0.33% |

#### Bottom 5 Performers
| Rank | Company | Avg Monthly % Change |
|---|---|---|
| 62 | TYL | -0.37% |
| 63 | COO | -0.37% |
| 64 | BSX | -0.40% |
| 65 | ANET | -0.42% |
| 66 | PODD | -0.71% |

#### Key Insights
- **Storage/Tech sector** (SNDK, WDC, STX) dominates the top 3 
  performers, suggesting strong sector momentum during this period.
- **Healthcare/Tech sector** (PODD, ANET, BSX) dominates the 
  bottom performers, indicating sector-wide weakness.
- The spread between best (+1.44%) and worst (-0.71%) is 
  approximately **2.15%**, reflecting moderate cross-sectional 
  dispersion in performance.
- The majority of companies cluster near zero, consistent with 
  the dataset mean of -0.019%, indicating most companies had 
  relatively flat performance over the period.
- **Green bars** (positive performers) and **red bars** (negative 
  performers) are roughly balanced, reflecting the near-zero 
  overall market average.

## How to Reproduce
1. Create AWS infrastructure (S3, Kinesis, Firehose, Lambda, Glue, Athena)
2. Run Lambda function to collect 6,600 stock records
3. Run Glue crawler to catalog S3 data
4. Run Athena query to compute monthly average percentage changes
5. Open Analysis.ipynb and run all cells to generate visualizations
