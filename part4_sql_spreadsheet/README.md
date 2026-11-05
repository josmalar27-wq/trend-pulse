# Part 4 — SQL & Spreadsheet Analysis

## Project Overview

This project analyzes YouTube trending videos using SQL, Python, Pandas and Excel.

The analysis focuses on database design, data loading, SQL queries, aggregations, spreadsheet formulas and data validation.

**Dataset:** Great Britain (GB) YouTube Trending Videos

**Tools:** Google Colab, Python, Pandas, SQLite, MySQL DB Fiddle, OpenPyXL and Excel.

## Task 1 — Database Schema Design

I designed a relational database named `trendpulse` with three tables.

| Table | Primary Key | Purpose |
|---|---|---|
| categories | category_id | Stores video category names |
| videos | video_id | Stores unique video details |
| trending_records | record_id | Stores daily trending statistics |

### Foreign Keys

- `videos.category_id` references `categories.category_id`.
- `trending_records.video_id` references `videos.video_id`.

Separating categories, videos and trending records reduces repeated information and supports SQL joins.

The MySQL schema was prepared using DB Fiddle.

## Task 2 — Data Preparation and Loading

I prepared three datasets using Pandas:

- `categories` — Unique video categories.
- `videos` — Unique video information.
- `trending_records` — Daily video engagement statistics.

I standardized dates, prepared numeric columns and added a country code and unique record IDs.

I exported the tables as CSV files and loaded the data into SQLite using Pandas `to_sql()`.

### Database Row Counts

| Table | Rows |
|---|---:|
| categories | 14 |
| videos | 4,113 |
| trending_records | 15,075 |

These counts were verified using SQL `COUNT(*)` queries.

## Task 3 — Basic SQL Queries

I used SELECT, WHERE, ORDER BY, LIMIT, DISTINCT and aliases to retrieve information.

### Top 10 Trending Records by Views

```sql
SELECT video_id, views AS total_views
FROM trending_records
WHERE country = 'GB'
ORDER BY views DESC
LIMIT 10;
```

### Unique Countries

```sql
SELECT DISTINCT country
FROM trending_records;
```

### Unique Category IDs

```sql
SELECT DISTINCT category_id
FROM videos
ORDER BY category_id;
```

These queries help identify highly viewed records and explore the dataset.

## Task 4 — Grouping, Aggregation and JOINs

I used GROUP BY, AVG, COUNT DISTINCT and HAVING to analyze category performance and channel activity.

### Average Views by Category

```sql
SELECT v.category_id,
       ROUND(AVG(t.views), 2) AS avg_views
FROM videos v
JOIN trending_records t
ON v.video_id = t.video_id
GROUP BY v.category_id
HAVING AVG(t.views) > 100000;
```

### Channels With at Least Five Unique Videos

```sql
SELECT v.channel_title,
       COUNT(DISTINCT v.video_id) AS total_videos
FROM videos v
JOIN trending_records t
ON v.video_id = t.video_id
GROUP BY v.channel_title
HAVING COUNT(DISTINCT v.video_id) >= 5;
```

### JOIN Justification

I used an INNER JOIN between `videos` and `trending_records` because the analysis requires matching video IDs from both tables.

This ensures that only trending records with corresponding video information are included in the aggregation.

## Task 5 — Excel Workbook Export

I used Pandas to export the dataset into `trendpulse_final.xlsx`.

### Workbook Sheets

| Sheet | Purpose |
|---|---|
| Records | Trending video statistics |
| Videos | Unique video information |
| Lookup | Category ID and name mapping |
| Pivot Summary | Average views by category and country |

### Pivot Summary Layout

- Rows: Category Name
- Columns: Country
- Values: Views
- Calculation: Average

The summary was generated using Pandas rather than a native interactive Excel PivotTable.

## Task 6 — Excel Formulas

I used VLOOKUP to retrieve category names and spreadsheet formulas to calculate summary statistics.

**VLOOKUP**

`=VLOOKUP(I2,Lookup!$A$2:$B$15,2,FALSE)`

**COUNTIF**

`=COUNTIF(Records!H2:H15076,"GB")`

**SUM**

`=SUM(Records!D2:D15076)`

**AVERAGE**

`=AVERAGE(Records!D2:D15076)`

These formulas support category lookup, country record counts, total views and average views.

## Task 7 — Filters, Sorting and Conditional Formatting

I configured an AutoFilter on the Records sheet.

I added a descending sort condition for the Views column.

I applied conditional formatting to highlight the top 10% of view values in yellow.

**Range:** `Records!D2:D15076`

**Rule:** Top 10% of values.

## Task 8 — Named Range

I created a named range called `ViewsData`.

**Range:** `Records!$D$2:$D$15076`

**Formula:**

`=AVERAGE(ViewsData)`

The named range makes spreadsheet formulas easier to read and maintain.

## Task 9 — SQL and Excel Cross-check

I wrote a comparison between the SQLite database and the Excel workbook.

Two metrics were selected:

1. Total trending records.
2. Total views.

### SQL Query

```sql
SELECT COUNT(*) AS total_records,
       SUM(views) AS total_views
FROM trending_records;
```

### Excel Formulas

**Record count:** `=COUNT(Records!D2:D15076)`

**Total views:** `=SUM(Records!D2:D15076)`

### Cross-check Results

| Metric | SQL | Excel |
|---|---|---|
| Trending records | 15,075 | To be verified |
| Total views | To be verified | To be verified |

The Python comparison code prints both SQL and Excel results. The actual output values should be added after execution.

## Project Run Order

1. Open the Part 4 notebook in Google Colab.
2. Mount Google Drive.
3. Load and prepare the GB trending dataset.
4. Prepare the categories, videos and trending records tables.
5. Create the SQL schema.
6. Load the cleaned tables into SQLite.
7. Run the basic SQL and aggregation queries.
8. Export the Excel workbook.
9. Add spreadsheet formulas, filters and conditional formatting.
10. Create the named range.
11. Compare SQL and Excel results.
12. Download the workbook and save the project files.

## Project Files

```text
part4_sql_spreadsheet/
├── README.md
├── Part_4_SQL_Spreadsheet_Analysis.ipynb
├── trendpulse_final.xlsx
└── data/
    ├── categories.csv
    ├── videos.csv
    └── trending_records.csv
```

The workbook and CSV files should be uploaded to GitHub alongside the notebook.

## Limitations

- The analysis currently uses GB data only.
- Full MySQL data import has not been verified.
- The Pivot Summary is not a native Excel PivotTable.
- The notebook demonstrates INNER JOIN but does not include separate LEFT JOIN and RIGHT JOIN queries.
- The workbook's Summary sheet is referenced by the named-range code, but its creation is not shown in the export cell.
- Actual SQL and Excel cross-check outputs are not recorded in the notebook.

## Conclusion

Part 4 demonstrates relational database design, SQL queries, data aggregation, spreadsheet export, Excel formulas, conditional formatting and SQL-to-Excel validation using YouTube trending video data.
