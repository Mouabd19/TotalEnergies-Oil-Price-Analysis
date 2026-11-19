# Data

All figures come from TotalEnergies' annual Factbooks (Excel versions, 2014 to 2025 editions), published on [totalenergies.com](https://totalenergies.com). Each Factbook covers the last five years; for each year, I kept the value from the most recent edition that contains it. Amounts are in millions of US dollars.

## Annual data

`totalenergies_annual_2011_2025.csv` has one row per year, from 2011 to 2025:

| Column | Meaning | Unit |
| --- | --- | --- |
| `year` | Year | |
| `brent_avg_usd_per_bbl` | Average Brent price over the year | $ per barrel |
| `sales_musd` | Sales (including excise taxes) | $ millions |
| `net_income_musd` | Net income, group share | $ millions |
| `adjusted_net_income_musd` | Adjusted net income, group share (excluding special items) | $ millions |
| `production_kboe_per_day` | Hydrocarbon production | thousand barrels of oil equivalent per day |

`sources_annual.csv` gives the Factbook edition and sheet for every figure.

## Results by segment

`segments_annual_2011_2025.csv` has one row per year and per segment:

| Column | Meaning |
| --- | --- |
| `year` | Year |
| `segment` | Segment as reported by TotalEnergies that year |
| `group` | `Upstream & Gas` (exploration and production, gas, power) or `Downstream` (refining, chemicals, marketing) |
| `adjusted_net_operating_income_musd` | Adjusted net operating income of the segment, in $ millions |
| `factbook_edition`, `sheet` | Source of the figure |

TotalEnergies reorganized its segments several times (Gas, Renewables & Power created in 2016, Integrated Gas, Renewables & Power in 2019, split into Integrated LNG and Integrated Power in 2023). Individual upstream segments are therefore not comparable from one period to another. The `Upstream & Gas` / `Downstream` grouping is comparable over the whole period: the downstream scope (Refining & Chemicals and Marketing & Services) has not changed since 2012.

For each year, all segments come from the same edition, and their sum equals the "Adjusted net operating income from business segments" total published in that edition.

## Quarterly data

`totalenergies_quarterly_2011_2025.csv` has one row per quarter, from 2011Q1 to 2025Q4 (60 rows):

| Column | Meaning | Unit |
| --- | --- | --- |
| `quarter` | Quarter (for example `2020Q2`) | |
| `quarter_end_date` | Last day of the quarter | date (YYYY-MM-DD) |
| `brent_avg_usd_per_bbl` | Average Brent price over the quarter | $ per barrel |
| `avg_liquids_price_usd_per_bbl` | Average price at which TotalEnergies sold its oil and liquids | $ per barrel |
| `net_income_musd` | Net income, group share | $ millions |
| `adjusted_net_income_musd` | Adjusted net income, group share | $ millions |

`segments_quarterly_2011_2025.csv` gives the adjusted net operating income by segment and by quarter, with the same `segment` and `group` columns as the annual file.

Sources: quarterly sheets of the Factbooks ("Fin. High. by quarter", "Op. High. by quarter", "Market envir. price", "Select. quarterly figures"). The 2025 Factbook does not report the Brent or the liquids price by quarter: for 2025, these two columns come from TotalEnergies' official press releases "Second Quarter 2025: Main Indicators" and "Fourth Quarter 2025: Main Indicators". `sources_quarterly.csv` gives the source of every figure.

## Checks

For each year, the sum of the four quarters (or their average, for prices) was compared with the published annual figure, and the sum of the segments with the published total for each quarter. These checks revealed three points:

- **An error in the 2019 Factbook**: the Q4 2015 Brent price is identical to Q3 (50.5 $). The value from the 2017 Factbook (43.8 $), consistent with the annual average, was kept.
- **2011 and 2012**: the sum of quarterly results differs slightly from the annual figure (up to 1.8% for 2011 net income), including in the Factbooks themselves. The quarters are kept as published; the gap probably comes from the conversion into dollars of figures originally reported in euros.
- **2015 segments by quarter**: no Excel Factbook contains them. They come from Total's quarterly results filed with the SEC: Q1 from the 1Q15 results, Q2 and Q3 from the 3Q15 results, and Q4 computed as the full year (2015 Form 20-F) minus the first nine months (3Q15 results). These sources match the Factbooks exactly for the 2014 quarters they also report. Their segment structure is the one in place in 2015 (Upstream, Refining & Chemicals, Marketing & Services), before the 2016 reorganization: their 2015 total by group therefore differs slightly from the restated figures in `segments_annual_2011_2025.csv` (Upstream & Gas: 4,774 vs 4,897 $M; Downstream: 6,588 vs 6,430 $M).
- **Missing values**: results by segment are not available by quarter for 2011 and 2012. These rows are present with an empty value (24 rows out of 236).

## Official sensitivity to oil prices

For 2025, TotalEnergies estimates that a ±10 $/b change in the average price of its liquids (with Brent between 70 and 80 $/b) changes its adjusted net operating income by about ±2.3 $ billion ([Fourth Quarter 2025: Main Indicators](https://www.businesswire.com/news/home/20260119985120/en/TotalEnergies-SE-Fourth-Quarter-2025-Main-Indicators)).
