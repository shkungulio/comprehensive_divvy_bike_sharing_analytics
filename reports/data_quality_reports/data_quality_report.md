# Divvy Data Quality Report
**Run timestamp (UTC):** 2026-10-09T22:22:53+00:00  
**Rows assessed (fact_trip):** 16,440,836  
**Overall Quality Score:** 90.5 / 100 (Grade A)

## Table Row Counts
- `fact_trip`: 16,440,836 rows
- `dim_date`: 1,004 rows
- `dim_station`: 3,957 rows
- `dim_ride_type`: 3 rows
- `dim_member_type`: 2 rows

## Check Results

| # | Check | Key Metric | % Rows Affected | Verdict |
|---|---|---|---|---|
| 1 | Duplicate ride IDs | 0 duplicate rows | 0.0% | PASS |
| 2 | Missing stations | 6,736,498 null station refs | 31.572% | FAIL |
| 3 | Invalid timestamps | 0 invalid rows | 0.0% | PASS |
| 4 | Negative ride durations | 0 non-positive + 314 mismatched | 0.0019% | PASS |
| 5 | Impossible coordinates | 0 impossible + 0 (0,0) | 0.0% | PASS |
| 9 | Data consistency | 6,368,150 issues | 38.7337% | FAIL |

## Null Percentages (columns with any nulls)

| table     | column            |   n_rows |   n_null |   null_pct |
|:----------|:------------------|---------:|---------:|-----------:|
| fact_trip | is_round_trip     | 16440836 |  5190701 |     31.572 |
| fact_trip | end_station_key   | 16440836 |  3437205 |     20.907 |
| fact_trip | start_station_key | 16440836 |  3299293 |     20.068 |
| fact_trip | end_lat           | 16440836 |    17107 |      0.104 |
| fact_trip | end_lng           | 16440836 |    17107 |      0.104 |

## Cardinality (fact_trip)

|                   |       n_unique |      n_rows |   uniqueness_ratio |
|:------------------|---------------:|------------:|-------------------:|
| ride_id           |    1.64408e+07 | 1.64408e+07 |             1      |
| start_station_key | 3918           | 1.64408e+07 |             0.0002 |
| end_station_key   | 3953           | 1.64408e+07 |             0.0002 |
| ride_type_key     |    3           | 1.64408e+07 |             0      |
| member_type_key   |    2           | 1.64408e+07 |             0      |
| start_hour        |   24           | 1.64408e+07 |             0      |
| day_of_week       |    7           | 1.64408e+07 |             0      |
| month_partition   |   33           | 1.64408e+07 |             0      |

## Data Completeness

- Overall completeness score: **93.17%**
- Missing calendar days in `dim_date`: 0
- Days with zero recorded rides: 0
- Date range assessed: 2024-01-01 to 2026-09-30

## Data Quality Score Breakdown

| dimension    |   score |   weight |
|:-------------|--------:|---------:|
| Uniqueness   |  100    |     0.2  |
| Completeness |   93.17 |     0.2  |
| Validity     |  100    |     0.25 |
| Consistency  |   61.27 |     0.2  |
| Accuracy     |   97.43 |     0.15 |

**Overall: 90.5 / 100 — Grade A**