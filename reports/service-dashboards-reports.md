# Reports: Service Dashboards Reports

Decoded from the org's report definitions on snapshot 20260929T163700Z, most recently run first.

### Cases Currently Open by Priority [00OKc000001YCujMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-17
filters: 1. OPEN equals "True"
date: Case.CreatedDate CUSTOM
standard: units=d
grouped by: Case.Priority
aggregates: Record count

### Cases by Type and Open Status [00OKc000001YCuoMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
date: CREATED_DATEONLY CUSTOM
standard: units=h
grouped by: Case.Type, OPEN
aggregates: Record count

### Trend of Case Resolution Time [00OKc000001YCurMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_AND_LAST_YEAR:2 (2025-01-01 to 2026-12-31)
standard: units=d
grouped by: Case.ClosedDate (Month)
aggregates: Average Age, Goal, Record count
formulas: Goal: 25

### Trend of Cases Created [00OKc000001YCutMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
date: Case.CreatedDate THIS_AND_LAST_YEAR:2 (2025-01-01 to 2026-12-31)
standard: units=h
grouped by: Case.CreatedDate (Month)
aggregates: Record count

### Trend of Cases Closed [00OKc000001YCusMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. STATUS equals "Closed"
date: CLOSED_DATEONLY THIS_AND_LAST_YEAR:2 (2025-01-01 to 2026-12-31)
standard: units=h
grouped by: Case.ClosedDate (Month)
aggregates: # of Cases Closed, Goal, Record count
formulas: # of Cases Closed: RowCount; Goal: 50

### Average Case Resolution Time MTD [00OKc000001YCuZMAW]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_MONTH (2026-09-01 to 2026-09-30)
standard: units=d
grouped by: Case.Priority
aggregates: Average Age, Record count

### Cases Closed MTD [00OKc000001YCucMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_MONTH (2026-09-01 to 2026-09-30)
standard: units=h
grouped by: Case.ClosedDate (Month)
aggregates: Record count

### Case Resolution Time MTD by Origin [00OKc000001YCubMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_MONTH (2026-09-01 to 2026-09-30)
standard: units=d
grouped by: Case.Origin
aggregates: Average Age, Record count

### Cases by Origin and Open Status [00OKc000001YCumMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
date: CREATED_DATEONLY CUSTOM
standard: units=h
grouped by: Case.Origin, OPEN
aggregates: Record count

### Cases by Priority [00OKc000001YCunMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
date: Case.CreatedDate CUSTOM
standard: units=d
grouped by: Case.Priority
aggregates: Record count

### Cases Currently Open by Agent [00OKc000001YCuhMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.Owner.Name, Case.Status
aggregates: Record count

### Cases Currently Open by Type [00OKc000001YCukMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.Type
aggregates: Record count

### High Priority Open Cases by Account [00OKc000001YCuqMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"; 2. Case.Priority equals "High"
date: CREATED_DATEONLY CUSTOM
standard: units=h
grouped by: Case.Account.Name
aggregates: # of Cases, Record count
formulas: # of Cases: RowCount

### Top 10 Cases by Age [00OKc000001YCupMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.CaseNumber, Case.Account.Name
aggregates: Average Age, Record count

### Avg Case Resolution Time MTD by Agen [00OKc000001YCuaMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_MONTH (2026-09-01 to 2026-09-30)
standard: units=d
grouped by: Case.Owner.Name
aggregates: Average Age, Record count

### Cases Closed MTD by Agent [00OKc000001YCudMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_MONTH (2026-09-01 to 2026-09-30)
standard: units=h
grouped by: Case.Owner.Name, Case.Priority
aggregates: Record count

### Cases Currently Open [00OKc000001YCufMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: Case.CreatedDate CUSTOM
standard: units=d
grouped by: Case.Status
aggregates: Record count

### Cases Currently Open by Account [00OKc000001YCugMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=h
grouped by: Case.Account.Name
aggregates: # of Cases, Record count
formulas: # of Cases: RowCount

### Cases Created MTD [00OKc000001YCueMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
date: CREATED_DATEONLY THIS_MONTH (2026-09-01 to 2026-09-30)
standard: units=d
grouped by: Case.Owner.Name
aggregates: Record count

### Aged Cases by Account [00OKc000001YCuWMAW]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.Account.Name
aggregates: Largest Age, Record count

### Aged Cases by Agent [00OKc000001YCuXMAW]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.Owner.Name
aggregates: Largest Age, Record count

### Average Case Resolution Time [00OKc000001YCuYMAW]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. Case.Status equals "Closed"
date: CLOSED_DATEONLY THIS_AND_LAST_YEAR:2 (2025-01-01 to 2026-12-31)
standard: units=d
grouped by: Case.Priority
aggregates: Average Age, Record count

### Age of Cases Currently Open by Type [00OKc000001YCuVMAW]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-07
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.Type
aggregates: Average Age, Record count

### Cases Currently Open by Origin [00OKc000001YCuiMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-03
filters: 1. OPEN equals "True"
date: CREATED_DATEONLY CUSTOM
standard: units=d
grouped by: Case.Origin
aggregates: Record count

### Cases by Origin [00OKc000001YCulMAG]
folder Service Dashboards Reports · type CaseList · Summary · last run 2015-08-03
date: CREATED_DATEONLY THIS_AND_LAST_YEAR:2 (2025-01-01 to 2026-12-31)
standard: units=h
grouped by: Case.Origin
aggregates: Record count
