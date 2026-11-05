# Part 1 — Python Foundations & Data Structures

## Project Overview

This project analyzes YouTube trending videos from India, USA and UK using Python fundamentals. It covers CSV loading, data cleaning, data structures, variable scope, loops, functions and rule-based video classification.

## Task 1 — Setup

I used Python variables to configure file paths, countries and classification thresholds.

- Countries: India, USA, UK
- Data folder: `/content/`
- Libraries: Pandas and datetime
- Run start time displayed using f-strings

I organized the notebook with clear headings and sequential code cells. I followed a restart-and-run-all approach to avoid hidden state.

## Task 2 — Loading Function

I created `load_country(path, country, max_rows=None)` to read CSV files using Pandas.

The function checks required columns, adds the country field and returns a list of dictionaries using `to_dict("records")`.

### Records Loaded

| Country | Records |
|---|---:|
| India | 15,075 |
| USA | 16,080 |
| UK | 15,075 |
| **Total** | **46,230** |

I also created a `category_names` dictionary from `categories.csv` to map category IDs to category names.

## Task 3 — Type Conversion and Cleaning

I converted `views`, `likes`, `dislikes` and `comment_count` into non-negative integers.

I converted `comments_disabled`, `ratings_disabled` and `video_error_or_removed` into Boolean values.

Date conversion:
- `trending_date`: `%y.%d.%m`
- `publish_time`: ISO datetime format

I used `try/except` to handle invalid values. Invalid values were replaced with `None`, while the remaining record was kept because other fields could still be useful.

### Cleaning Failure Report

| Field | Failed Values |
|---|---:|
| views | 0 |
| likes | 12 |
| dislikes | 0 |
| comment_count | 36 |
| comments_disabled | 0 |
| ratings_disabled | 0 |
| video_error_or_removed | 0 |
| trending_date | 0 |
| publish_time | 0 |

## Task 4 — Core Data Structures

I used lists of dictionaries for cleaned records, tuples for fixed video information, sets for unique video IDs, dictionaries for channel counts and nested dictionaries for country/category summaries.

Lists, dictionaries and sets are mutable. Tuples are immutable.

### Unique Videos

| Country | Unique Videos |
|---|---:|
| India | 5,878 |
| USA | 5,068 |
| UK | 4,113 |

**Videos trending in more than one country:** 340

### Videos Unique to One Country

| Country | Unique to Country |
|---|---:|
| India | 5,652 |
| USA | 4,834 |
| UK | 3,873 |

I used set intersection and difference to compare countries.

I also counted trending appearances by channel and used slicing to display the top 15 channels.

The channel dictionary contained 438 channels. The highest recorded appearance count was 2,464 for `QuietChallenge75`.

A nested dictionary summarized record counts by country and category.

## Task 5 — Variable Scope

I demonstrated global and local variables using `show_scope()`.

- Global variable: `project_name = "YouTube Analysis"`
- Local variable: `message = "Hello from the function"`

The global variable was accessible inside and outside the function.

Accessing the local variable outside the function raised a `NameError`, which was handled using `try/except`.

## Task 6 — Loops Over Strings and Sequences

I created `title_features(title)` to count uppercase words, exclamation marks, question marks and word count.

Example title: `WOW! Is this REAL?`

| Feature | Result |
|---|---:|
| Uppercase words | 2 |
| Exclamation marks | 1 |
| Question marks | 1 |
| Word count | 4 |

I used `for` loops, `range()` with index access and a `while` loop with `continue` and `break`.

The while loop searched for the first record exceeding the viral view threshold.

## Task 7 — Rule-Based Classification

I used `classify_video()`, `classify_rated()` and `other_label()` to classify trending records.

### Thresholds

| Setting | Value |
|---|---:|
| Viral views | 1,000,000 |
| Steady views | 100,000 |
| Low views | 10,000 |
| High like ratio | 0.80 |
| Divisive like ratio | 0.60 |

Like ratio = `likes / (likes + dislikes)`.

### Classification Rules

Rules are checked in the following order:

1. **Unrated:** Missing required values, zero views, disabled ratings or zero total ratings.
2. **Viral Hit:** Views at least 1,000,000 and like ratio at least 0.80.
3. **Divisive:** Like ratio below 0.60.
4. **Low Engagement:** Views below 10,000.
5. **Steady Performer:** Views at least 100,000 after earlier checks.
6. **Unrated:** Records that do not match another rule.

A missing comments-disabled flag produces Unrated, but disabled comments alone do not change the label.

### Hand Trace Example

A video has 2,000,000 views, 900 likes and 100 dislikes, with ratings enabled.

Like ratio = 900 / (900 + 100) = 0.90.

The views exceed 1,000,000 and the ratio exceeds 0.80.

**Classification: Viral Hit**

### Classification Results

| Classification | Records |
|---|---:|
| Steady Performer | 27,271 |
| Unrated | 9,027 |
| Viral Hit | 9,497 |
| Divisive | 251 |
| Low Engagement | 184 |
| **Total** | **46,230** |

## Task 8 — Refactoring

I created a reusable `clean_number()` function for converting views, likes, dislikes and comment counts into integers.

This reduces repeated code and makes cleaning rules easier to maintain.

## Task 9 — Installation and Run Instructions

### Required Tools

- Python 3
- Google Colab
- Pandas

### Dataset Files

| File | Purpose |
|---|---|
| `INvideos.csv` | India trending videos |
| `USvideos.csv` | USA trending videos |
| `GBvideos.csv` | UK trending videos |
| `categories.csv` | Category ID and name mapping |

### How to Run

1. Open `part1_python_foundations.ipynb` in Google Colab.
2. Upload the four CSV files to `/content/`.
3. Install Pandas if necessary using `!pip install pandas`.
4. Run the setup and loading cells.
5. Execute cleaning, data structures and loop examples.
6. Run the classification functions.
7. Review failure counts and classification results.
8. Use **Runtime → Restart session and run all** to verify execution.

### Data Source

YouTube Trending Videos dataset supplied for the project, containing video metadata, trending dates, engagement statistics and category information.

## Conclusion

This project processed 46,230 trending records across three countries. It demonstrates Python fundamentals, data cleaning, data structures, loops, functions, scope and rule-based classification.

The analysis identified 9,497 Viral Hit records and 27,271 Steady Performer records.
