# Employee Survey Responses: Analysis of Pierce County WA Engagement Survey

Capstone project for the Digitaley Drive Data Analyst Bootcamp.

## Overview

This project analyses a voluntary employee engagement survey completed by Pierce County WA government employees. It answers three questions: what employees agree and disagree with most, what patterns appear by department and role, and what an employer should do about it.

**Main finding:** employees know what is expected of them, but recognition, learning opportunities and the Sheriff's Department stand out as problem areas.

## Dataset

`Employee_Survey.xlsx` has two sheets: `HR Survey Reponses` (14,725 rows, 10 fields) and `Data Dictionary`. Each row is one answer to one question. Responses use a scale from 1 (Strongly Disagree) to 4 (Strongly Agree), with 0 meaning Not Applicable.

**Cleaning steps**
- Removed 15 exact duplicate rows.
- Excluded 135 incomplete answers and 394 "Not Applicable" answers from averages.
- Merged question wording variants into 10 questions.
- Result: 14,181 usable answers.

**Limits:** there is no respondent ID, and 72% of answers have no role flag, so role results cover only about 28% of the data.

## Tools

Excel and Power BI. Power Query was used to clean and shape the data, a data model and DAX measures to calculate the results, and Power BI for the dashboard.

## Findings

| Question | Result |
|---|---|
| Most agreed | I know what is expected of me (92.6% agree) |
| Most disagreed | I have a best friend at work (47.6% disagree) and recent recognition (34.8% disagree) |
| Overall | 77% positive, average 3.07 out of 4 |
| Department outlier | Sheriff's Department, average 2.46 (rest of county 3.15) |
| Role pattern | Director 3.41, Manager 3.27, Supervisor 3.20, Staff 2.97 |
| Biggest role gaps | Recognition (director 3.43 vs staff 2.66) and learning (3.73 vs 2.95) |

## Recommendations

1. Start a recognition programme and track question 3 each quarter.
2. Run listening sessions, then a pulse survey, in the Sheriff's Department.
3. Give staff training budgets, mentoring and career ladders.
4. Encourage team connection through cross-team projects and mentoring pairs.
5. Add respondent IDs and a role field for every answer in future surveys.

## How the analysis was done

1. **Clean in Power Query.** Load the `HR Survey Reponses` sheet and then:
   - Remove duplicate rows.
   - Trim the Question text and replace "learn & grow" and "&" with "learn and grow" and "and", so each question has one wording.
   - Add a Question Number column by extracting the digits at the start of the Question text.
   - Add a Role column with a conditional column: Director, Manager, Supervisor or Staff from the four flag columns, otherwise "Unassigned".
   - Filter Status to Complete and Response to greater than 0, which removes incomplete and Not Applicable answers.
2. **Create DAX measures** (the main table is called `Survey` here).

```DAX
Avg Score = AVERAGE(Survey[Response])
Agree % = DIVIDE(CALCULATE(COUNTROWS(Survey), Survey[Response] >= 3), COUNTROWS(Survey))
Disagree % = DIVIDE(CALCULATE(COUNTROWS(Survey), Survey[Response] <= 2), COUNTROWS(Survey))
Answers = COUNTROWS(Survey)
```

3. **Build visuals and answer each question.**

| Question | How it was answered |
|---|---|
| Q1 | Bar chart of Agree % and Disagree % by Question Number, sorted. A 100% stacked bar shows the full mix of answers |
| Q2 department | Bar chart of Avg Score by Department, sorted lowest first, with Answers shown to flag small departments |
| Q2 role | Avg Score by Role, and a matrix of Question Number by Role (with conditional-format colours) to show the role gaps |
| Q3 | Recommendations based on the lowest-scoring questions and the departments and roles that fall furthest behind |

Excel pivot tables can be used to cross-check the same averages.

## Project files

| File | Description |
|---|---|
| `Employee_Survey.xlsx` | Source data |
| `[your file name].pbix` | Power BI report with the data model, measures and dashboard |
| Dashboard screenshot | Picture of the dashboard (also posted on LinkedIn) |
| Presentation deck | Slides summarising the findings |

## Links

## Author

[GIFTY ALORZUKE]

# Employee-survey
Employee survey Analysis
