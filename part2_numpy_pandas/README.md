# Part 2 — NumPy & Pandas Data Wrangling

## Project Overview

This project analyzes YouTube trending video data from India, USA and UK using NumPy and Pandas.

It covers array operations, engagement scoring, data cleaning, filtering, merging, aggregation and trending lifespan analysis.

## Task 1 — NumPy Arrays

I loaded views, likes, dislikes and comment counts into NumPy arrays.

Each array initially contained 46,230 values with the `float64` data type.

I used NumPy sorting and slicing to display the top 10 views, every 100th value and a subset of the array.

## Task 2 — Engagement Score

I calculated an engagement score using NumPy without explicit loops.

Weights:
- Views: 20%
- Likes: 50%
- Comments: 30%

I used min-max normalization, `np.log1p()` for log-scaled views and the 90th percentile to identify top-engagement records.

Zero denominators were handled using `np.where()`.

## Task 3 — Reshape and Broadcasting

I created a daily trending-count matrix with dates as rows and countries as columns.

I used `flatten()` and `reshape()` to transform the array.

Broadcasting was used to calculate each country's daily share and compare daily counts against country averages.

## Task 4 — Loading and Inspection

I loaded and combined country CSV files using Pandas.

I inspected shapes, sample rows, descriptive statistics, data types, missing values, duplicates, negative counts and invalid date order.

I converted dates into datetime values and numeric fields using `pd.to_numeric()`.

## Task 5 — Filtering

I used `loc`, `iloc` and Boolean conditions to filter records.

The analysis included:
- Videos with at least 1,000,000 views and more than 50,000 likes.
- Top 20 videos by engagement score.
- Music or Gaming videos above median views.

Music category ID is 10 and Gaming category ID is 20.

## Task 6 — Missing Values and Duplicates

I reported missing-value counts and percentages.

I filled missing optional text fields with suitable defaults and removed records missing essential fields.

I also removed duplicate country, video ID and trending-date combinations.

**Records after cleaning: 46,182**

## Task 7 — Joining Category Names

I loaded `categories.csv` and used a left merge to attach category names to trending records.

The merge used `category_id` with `validate="many_to_one"`.

- Records before merge: 46,182
- Records after merge: 46,182
- Unmatched categories: 0

The left merge preserved all cleaned trending records.

## Task 8 — Aggregation

I used `groupby()` and `agg()` to calculate record counts, average views, average likes and average engagement by category and country.

I calculated category distribution percentages and compared publishing weekdays and UTC hours.

**Highest average-view publishing weekday: Monday**, according to the notebook output.

## Task 9 — Time to Trend and Trending Lifespan

I calculated the number of days between publication and trending.

Negative delays were checked and replaced with missing values when applicable.

I counted distinct trending days for each country/video combination, displayed the 10 longest-lasting videos and calculated average lifespan by category.

## Task 10 — Combining Data

I combined country datasets using `pd.concat()`.

**Combined dataset shape:** 46,230 rows × 17 columns.

I created video-level and channel-level summaries using `groupby()`.

The summaries were merged to compare trending-video counts and total views by channel.

## Tools Used

- Python
- Google Colab
- NumPy
- Pandas

## Dataset Files

- `INvideos.csv` — India
- `USvideos.csv` — USA
- `GBvideos.csv` — UK
- `categories.csv` — Category ID and name mapping

## How to Run

1. Open the Part 2 notebook in Google Colab.
2. Run the first cell and upload the dataset files.
3. The notebook stores uploaded files in `/content/part2_numpy_pandas/data/`.
4. Run the remaining cells in order.
5. Review the array, cleaning, aggregation and lifespan outputs.
6. Restart the runtime and run all cells to check reproducibility.

## Conclusion

Part 2 demonstrates NumPy vectorization, Pandas filtering, data cleaning, joins, aggregation and time-based analysis using YouTube trending data from three countries.
