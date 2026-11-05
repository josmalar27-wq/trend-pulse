# Part 3 — Visualization, EDA & Business Thinking

## Project Overview

This project analyzes YouTube trending videos from India (IN), USA (US), and Great Britain (GB) using Python, Pandas and Plotly.

The objective is to clean the data, explore video performance and visualize engagement trends.

## Task 1 — Data Profiling

I combined multiple country CSV files using Pandas.

I checked:
- Number of rows and columns
- Data types
- Missing-value percentages
- Duplicate records

I used `pd.concat()` to combine datasets and `df.isna()` to identify missing values.

## Task 2 — Data Cleaning

I removed duplicate records using `drop_duplicates()`.

I loaded `categories.csv` and merged category names into the main dataset using `category_id`.

I used a left join to preserve the original video records.

I also removed unavailable videos using the `video_error_or_removed` column.

## Task 3 — Interactive Scatter Plot

I created an interactive Plotly scatter chart to compare video views and likes.

**Chart:** Views vs Likes by Category

- X-axis: Views
- Y-axis: Likes
- Colour: Category Name
- Hover information: Video Title

This chart helps identify relationships between video popularity and engagement.

## Task 4 — Chart Interpretation

The scatter plot shows a positive relationship between views and likes.

Most videos have relatively low views and likes, while a smaller number achieve very high engagement.

A scatter plot is suitable because both variables are numeric.

## Task 5 — Average Views by Category and Country

I calculated average views using:

`df.groupby(["category_name", "country"])["views"].mean()`

I created an interactive grouped bar chart using Plotly.

- X-axis: Category Name
- Y-axis: Average Views
- Colour: Country

This chart compares category performance across countries.

## Task 6 — Business Insights

According to the notebook interpretation:

- Music has the highest average views across the three countries.
- GB Music averages approximately 3.7 million views.
- US Music averages approximately 2.9 million views.
- IN Music averages approximately 2.4 million views.
- India leads in several other categories, including Comedy and Entertainment.

These observations can help content creators understand differences in category performance across countries.

## Tools Used

- Python
- Google Colab
- Pandas
- Plotly

## Dataset Files

- `INvideos.csv` — India
- `USvideos.csv` — USA
- `GBvideos.csv` — Great Britain
- `categories.csv` — Category mapping

## How to Run

1. Open the Part 3 notebook in Google Colab.
2. Upload the country CSV files and `categories.csv`.
3. Run the data-loading cells.
4. Check data types, missing values and duplicates.
5. Merge category names and remove unavailable videos.
6. Run the Plotly visualization cells.
7. Review the charts and interpretations.

## Limitations

The notebook currently includes two Plotly charts. Additional Matplotlib charts, statistical analysis, correlation, funnel, retention and cohort analysis are not yet included.

## Conclusion

This project demonstrates exploratory data analysis, data cleaning and interactive visualization of YouTube trending videos.

The analysis highlights differences in video engagement across countries and categories.
