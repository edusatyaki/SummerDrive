# NYC Yellow Taxi Data Cleaning Logs

## Dataset

* Dataset: NYC Yellow Taxi Trip Records
* Year: 2025
* Format: Parquet
* Raw files: 12 monthly files from January to December

## Purpose

The purpose of cleaning is to remove invalid records and prepare the dataset for analysis, dashboard, and reporting.

## Cleaning Steps

1. Loaded all 12 monthly Parquet files.
2. Merged all files into one dataframe.
3. Selected useful columns only.
4. Converted pickup and drop-off time columns into datetime format.
5. Created a new column: `trip_duration_min`.
6. Removed invalid records:

   * zero or negative trip distance
   * negative or zero fare amount
   * zero passengers
   * invalid total amount
   * very short or very long trip duration
7. Removed duplicate rows.
8. Created new columns for analysis:

   * `pickup_hour`
   * `pickup_day`
   * `pickup_month`
9. Saved the cleaned dataset separately.

## Output

Raw data location:

```text
Data Cleaning/Raw Dataset/
```

Cleaned data location:

```text
Data Cleaning/Cleaned Dataset/yellow_taxi_cleaned_2025.parquet
```

Notebook:

```text
Data Cleaning/NYC_Taxi_Data_Cleaning.ipynb
```
