# 🦺 OSHA Workplace Safety Risk Analysis (2024–2025)

## Overview
SQL-based workplace safety risk analysis using OSHA incident data, scoring and ranking companies by injury rates, fatality rates, severity load, and statistical risk deviation from industry averages. The output classifies establishments into risk categories to identify the most dangerous workplaces in the U.S.

## Tools & Platform
- **SQL** (BigQuery)
- **Dataset:** OSHA Data 2024–2025
- **Rows:** ~398,158 | 20 columns

## Key Questions Answered
- Which companies and establishments have the highest injury and fatality rates?
- How does each company's risk compare to its industry average?
- Which establishments are statistical outliers ("Critical Outliers") vs. normal?
- What industries carry the highest cumulative risk burden?

## SQL Techniques Used
| Technique | Purpose |
|---|---|
| `WITH` / CTEs | Company-level aggregation → risk scoring → normalization → classification |
| `SUM()` / `AVG()` | Total injuries, deaths, DAFW/DJTR cases per company |
| `ROUND()` | Clean score presentation |
| Risk scoring formula | Composite score from injury rate, fatality rate, severity load, lost-time index |
| `AVG() OVER(PARTITION BY naics_code)` | Industry-average risk benchmark |
| Z-score calculation | Measuring deviation from industry norm |
| `CASE WHEN` risk classification | Tiered risk labels (LOW / MEDIUM / HIGH / CRITICAL OUTLIER) |
| `ORDER BY normalized_risk DESC` | Ranking by severity |

## Risk Metrics Explained
| Metric | Definition |
|---|---|
| `injury_rate` | Injuries per 100 employees |
| `fatality_rate` | Deaths per 100 employees |
| `severity_load` | Weighted combination of DAFW and DJTR cases |
| `lost_time_index` | Total days away from work / total DJTR days |
| `risk_z_score` | How many standard deviations above industry average |
| `risk_category` | LOW / MEDIUM / HIGH / CRITICAL OUTLIER |

## Key Findings
- Several establishments classified as **CRITICAL OUTLIER** with risk z-scores exceeding 25×
- Industries like structural steel fabrication and refrigerated warehousing showed disproportionate injury burdens relative to employee count
- Fatality rates and lost-time indexes together expose establishments that OSHA aggregate statistics alone miss

## Files
| File | Description |
|---|---|
| `osha_analysis.csv` | Full risk-scored and classified establishment dataset |
| `screenshots/` | BigQuery SQL query screenshots |

## Data Source
[OSHA Data Initiative](https://www.osha.gov/data) — 2024–2025 injury and illness records

---
*Project by Stephanie Sambo | Data Analyst | Operations & Safety Analytics | SQL • BigQuery*
