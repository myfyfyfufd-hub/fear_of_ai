# AI Use & Student Outcomes: Data Analysis

End-to-end analysis of how generative-AI use relates to GPA, skill retention, exam anxiety, AI dependency and burnout, using a dataset of 50,000 students.

## Contents

| File | Description |
|---|---|
| `AI_Student_Impact_Dashboard.xlsx` | Interactive Excel dashboard (filters, KPIs, 8 charts), Summary Report, Data_Quality log, Cleaned_Data and untouched Original_Data |
| `ai_student_impact_analysis.py` | Pandas script: load, clean, validate, EDA, KPIs, export |
| `ai_student_impact_analysis.sql` | PostgreSQL-style SQL: staging table, validation (PASS/WARN/FAIL), cleaned view, KPIs, segments, reconciliation |
| `requirements.txt` | Python dependencies |

## Key findings

- Average GPA rose from 3.146 to 3.349 (+0.203); 87.5% of students improved.
- Students using GenAI 20+ hours/week (10% of the sample): 74% high burnout risk (vs 9% at 0-2 h), skill retention 70.3 (vs 75.8 overall), smallest GPA gain (+0.156).
- Traditional study time is the strongest correlate of GPA gain (r = 0.38); GenAI hours barely correlate with it (r = -0.05).
- Use case matters: debugging users gain most (+0.249), direct-answer users least (+0.133).
- Advanced prompt skill and more tools go with higher skill retention (82.1 vs 71.1; 79.8 with 5 tools vs 72.6 with 1).
- Strict-ban students report higher exam anxiety (4.89 vs about 4.12) with similar usage.

**Caveat:** the data is observational with no real non-user comparison group, so these are associations, not causal effects.

## Data quality

No missing values, duplicates or impossible values; no rows removed. 4,804 students sit at the 4.0 GPA ceiling and 448 at the 40 h/week maximum. These are flagged, not deleted.

## How to run

### Python
```bash
pip install -r requirements.txt
python ai_student_impact_analysis.py path/to/ai_student_impact_dataset.csv analysis_output
```

### SQL (PostgreSQL)
1. Run the `CREATE TABLE` section to create `stg_ai_student_impact`.
2. Load the CSV: `\copy stg_ai_student_impact FROM 'ai_student_impact_dataset.csv' CSV HEADER`
3. Run the rest of `ai_student_impact_analysis.sql`.

### Excel
Open the workbook, go to the **Dashboard** sheet and use the yellow dropdowns (Major, Year, Policy, Prompt skill) to filter every KPI, chart and table.

## Data

Source: `ai_student_impact_dataset.csv` (50,000 rows, 16 columns). Not included in this repo by default; place it in the project folder to run the scripts.
