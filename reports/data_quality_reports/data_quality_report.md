# Divvy Data Quality Report
**Run timestamp (UTC):** 2026-09-11T20:19:41+00:00  
**Rows assessed (fact_trip):** 8,000,000  
**Overall Quality Score:** 90.8 / 100 (Grade A)

## Table Row Counts
- `fact_trip`: 8,000,000 rows
- `dim_date`: 974 rows
- `dim_station`: 3,943 rows
- `dim_ride_type`: 3 rows
- `dim_member_type`: 2 rows

## Check Results

| # | Check | Key Metric | % Rows Affected | Verdict |
|---|---|---|---|---|
| 1 | Duplicate ride IDs | 0 duplicate rows | 0.0% | PASS |
| 2 | Missing stations | 3,052,333 null station refs | 29.0692% | FAIL |
| 3 | Invalid timestamps | 0 invalid rows | 0.0% | PASS |
| 4 | Negative ride durations | 0 non-positive + 171 mismatched | 0.0021% | PASS |
| 5 | Impossible coordinates | 0 impossible + 0 (0,0) | 0.0% | PASS |
| 9 | Data consistency | 3,029,165 issues | 37.8646% | FAIL |

## Null Percentages (columns with any nulls)

| table     | column            |   n_rows |   n_null |   null_pct |
|:----------|:------------------|---------:|---------:|-----------:|
| fact_trip | is_round_trip     |  8000000 |  2325538 |     29.069 |
| fact_trip | end_station_key   |  8000000 |  1550226 |     19.378 |
| fact_trip | start_station_key |  8000000 |  1502107 |     18.776 |
| fact_trip | end_lat           |  8000000 |     9379 |      0.117 |
| fact_trip | end_lng           |  8000000 |     9379 |      0.117 |

## Cardinality (fact_trip)

|                   |   n_unique |   n_rows |   uniqueness_ratio |
|:------------------|-----------:|---------:|-------------------:|
| ride_id           |      8e+06 |    8e+06 |             1      |
| start_station_key |   3215     |    8e+06 |             0.0004 |
| end_station_key   |   3205     |    8e+06 |             0.0004 |
| ride_type_key     |      3     |    8e+06 |             0      |
| member_type_key   |      2     |    8e+06 |             0      |
| start_hour        |     24     |    8e+06 |             0      |
| day_of_week       |      7     |    8e+06 |             0      |
| month_partition   |     18     |    8e+06 |             0      |

## Data Completeness

- Overall completeness score: **93.64%**
- Missing calendar days in `dim_date`: 0
- Days with zero recorded rides: 426
- Date range assessed: 2024-01-01 to 2026-08-31

## Data Quality Score Breakdown

| dimension    |   score |   weight |
|:-------------|--------:|---------:|
| Uniqueness   |  100    |     0.2  |
| Completeness |   93.64 |     0.2  |
| Validity     |  100    |     0.25 |
| Consistency  |   62.14 |     0.2  |
| Accuracy     |   97.6  |     0.15 |

**Overall: 90.8 / 100 — Grade A**