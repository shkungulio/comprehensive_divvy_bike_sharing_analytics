# Divvy Data Quality Report
**Run timestamp (UTC):** 2026-10-01T18:02:43+00:00  
**Rows assessed (fact_trip):** 15,670,295  
**Overall Quality Score:** 90.51 / 100 (Grade A)

## Table Row Counts
- `fact_trip`: 15,670,295 rows
- `dim_date`: 974 rows
- `dim_station`: 3,943 rows
- `dim_ride_type`: 3 rows
- `dim_member_type`: 2 rows

## Check Results

| # | Check | Key Metric | % Rows Affected | Verdict |
|---|---|---|---|---|
| 1 | Duplicate ride IDs | 0 duplicate rows | 0.0% | PASS |
| 2 | Missing stations | 6,406,151 null station refs | 31.4451% | FAIL |
| 3 | Invalid timestamps | 0 invalid rows | 0.0% | PASS |
| 4 | Negative ride durations | 0 non-positive + 314 mismatched | 0.002% | PASS |
| 5 | Impossible coordinates | 0 impossible + 0 (0,0) | 0.0% | PASS |
| 9 | Data consistency | 6,062,767 issues | 38.6896% | FAIL |

## Null Percentages (columns with any nulls)

| table     | column            |   n_rows |   n_null |   null_pct |
|:----------|:------------------|---------:|---------:|-----------:|
| fact_trip | is_round_trip     | 15670295 |  4927540 |     31.445 |
| fact_trip | end_station_key   | 15670295 |  3267187 |     20.85  |
| fact_trip | start_station_key | 15670295 |  3138964 |     20.031 |
| fact_trip | end_lat           | 15670295 |    16463 |      0.105 |
| fact_trip | end_lng           | 15670295 |    16463 |      0.105 |

## Cardinality (fact_trip)

|                   |       n_unique |      n_rows |   uniqueness_ratio |
|:------------------|---------------:|------------:|-------------------:|
| ride_id           |    1.56703e+07 | 1.56703e+07 |             1      |
| start_station_key | 3900           | 1.56703e+07 |             0.0002 |
| end_station_key   | 3937           | 1.56703e+07 |             0.0003 |
| ride_type_key     |    3           | 1.56703e+07 |             0      |
| member_type_key   |    2           | 1.56703e+07 |             0      |
| start_hour        |   24           | 1.56703e+07 |             0      |
| day_of_week       |    7           | 1.56703e+07 |             0      |
| month_partition   |   32           | 1.56703e+07 |             0      |

## Data Completeness

- Overall completeness score: **93.19%**
- Missing calendar days in `dim_date`: 0
- Days with zero recorded rides: 0
- Date range assessed: 2024-01-01 to 2026-08-31

## Data Quality Score Breakdown

| dimension    |   score |   weight |
|:-------------|--------:|---------:|
| Uniqueness   |  100    |     0.2  |
| Completeness |   93.19 |     0.2  |
| Validity     |  100    |     0.25 |
| Consistency  |   61.31 |     0.2  |
| Accuracy     |   97.42 |     0.15 |

**Overall: 90.51 / 100 — Grade A**