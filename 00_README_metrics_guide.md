# HR Analytics Dataset — Synthetic Company (1,500 employees, India)

Snapshot date: 30-Sep-2026 · Join key: `employee_id`

## Files
| # | File | Rows | What it holds |
|---|------|------|---------------|
| 01 | departments | 9 | Dept, HQ, budget, headcount target |
| 02 | employees | 1,500 | Master: demographics, role, level, CTC, work mode, status |
| 03 | attrition_exits | 263 | Exit date, type, reason, notice, regrettable, rehire |
| 04 | exit_reviews_raw | 185 | **Free-text reviews (no sentiment label)** + 1–5 ratings |
| 05 | performance | 3,700 | Yearly rating, goals %, promotion, hike %, training hrs |
| 06 | engagement_survey | 2,374 | Annual survey scores (1–5) + eNPS (0–10) |
| 07 | compliance_trainings | 7,422 | POSH, CoC, DPDP, InfoSec, Anti-Bribery, Fire — status/due |
| 08 | compliance_employee_records | 1,500 | BGV, PF/UAN, ESI, NDA, grievances, POSH complaints |
| 09 | attendance_leave | 13,891 | Monthly presence, leaves, absences, overtime (last 12 mo) |
| 10 | recruitment | 1,500 | Requisition → offer → join dates, applicants, cost |

## Metrics to calculate
**Attrition**
- Attrition rate = exits ÷ avg headcount × 100 (overall, by dept/level/location)
- Voluntary vs involuntary split
- Regrettable attrition % = regrettable exits ÷ total exits
- Early attrition = exits with tenure < 6 / 12 months
- Avg tenure at exit
- Retention rate = 1 − attrition rate

**Workforce**
- Headcount vs target (01 vs 02), gender ratio, avg age, span of control (manager_id)
- Avg CTC by level / dept, pay gap by gender

**Performance & engagement**
- Rating distribution, promotion rate, avg hike %
- eNPS = % promoters (9–10) − % detractors (0–6)
- Satisfaction vs attrition correlation

**Attendance**
- Absenteeism rate = (working_days − days_present) ÷ working_days
- Unplanned absence trend before exit (early-warning signal)

**Compliance**
- Training completion % by course/dept, overdue count
- BGV pending/discrepancy %, PF linkage %, NDA coverage

**Recruitment**
- Time-to-hire = join_date − req_open_date
- Offer-to-join days, cost-per-hire, source effectiveness (source vs early attrition)

## Sentiment exercise (file 04)
- Label `review_text` as Positive / Neutral / Negative (VADER, TextBlob, or transformer)
- Compare sentiment vs `stated_reason` and the rating columns
- Mixed reviews ("liked team but pay low") are intentional — watch for them

Built-in patterns: overtime, L1 level, Sales/Support, long commute and age < 28 raise exit risk; Remote lowers it.
