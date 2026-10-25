# HealthConnect Rwanda Healthcare Analytics

**A Healthcare Data Analytics Project | AnalystLab Africa Experience Lab Internship | Week 6**

**Prepared by:** Adeyemo Taiwo Aminat (Meenah)
**Track:** Data Analytics
**Project:** HealthConnect Rwanda Healthcare Analytics
**Tools:** PostgreSQL 18, pgAdmin 4, Python, Jupyter Notebook, Power BI, Microsoft Word, Microsoft PowerPoint

---

## 1. Project Overview

HealthConnect Rwanda is a healthcare analytics project focused on understanding hospital performance, patient demographics, clinical activity, revenue collection, insurance claims, operational efficiency and patient satisfaction.

As part of the AnalystLab Africa Experience Lab internship, I worked with healthcare datasets to build a database, perform data quality checks, write SQL queries and develop an interactive Power BI dashboard.

The goal was to turn raw healthcare data into useful information that can help healthcare managers identify performance gaps, improve patient experience, monitor finances and make better operational decisions.

This project also highlights the importance of data quality and the need to interpret healthcare data carefully before making decisions.

## 2. Business Objectives

The project set out to answer ten business questions:

1. Which hospitals serve the highest number of patients?
2. Which departments experience the greatest workload?
3. Which diseases are becoming more common?
4. Are medical staff distributed efficiently?
5. Which insurance companies generate the largest revenue?
6. Which facilities have the highest patient satisfaction?
7. Which hospitals require expansion?
8. How can operational costs be reduced?
9. Which services contribute most to revenue?
10. Which regions require additional healthcare investment?

The project also looked at how much revenue was generated, collected and left outstanding, and at which data quality issues could affect the reliability of business decisions.

## 3. Dataset Overview

The project used 26 CSV files covering different areas of healthcare operations.

| Dataset / Entity | Record Count |
|---|---:|
| Healthcare facilities | 20 |
| Patients | 20,000 |
| Appointments | 5,000 |
| Bills | 60,000 |
| Diagnoses | 60,000 |
| Insurance claims | 42,036 |
| Patient feedback records | 21,064 |
| Staff | 1,250 |
| Beds | 2,000 |
| Medical equipment items | 200 |

**Important:** These counts describe the supplied datasets. They should not be interpreted as proof that every record represents a unique patient visit or a unique real-world event.

The data covers 2026. The project uses the Rwandan franc (RWF) as the assumed currency for financial reporting, shown as RF in the findings. The dataset itself does not state a currency.

## 4. Tools and Technologies

### PostgreSQL 18 and pgAdmin 4
Used to create the relational database, store the 26 datasets, run SQL queries, create cleaned views and prepare data for analysis.

### Python and Jupyter Notebook
Used to load the CSV files into PostgreSQL through the `psycopg2` library.

### SQL
Used to explore healthcare data, investigate business questions, check data quality and prepare reporting datasets. A collection of 40 SQL queries was developed and run.

### Power BI
Used to build an interactive dashboard with six main report pages, a facility drill-through page, a hidden tooltip page, bookmarks and about 30 DAX measures.

### Microsoft Word and PowerPoint
Used to prepare the business insights report and an 11-slide presentation summarising the findings.

## 5. Project Workflow

1. **Data preparation:** Reviewed the supplied CSV files and prepared the database tables.
2. **Database development:** Created the PostgreSQL tables using `01_create_tables.sql`.
3. **Data loading:** Loaded the 26 CSV files into the `healthconnect` database using Python and `psycopg2`.
4. **Data quality assessment:** Created a data quality log and investigated missing links, inconsistent information and other limitations.
5. **SQL analysis:** Developed and ran 40 SQL queries to answer healthcare business questions.
6. **Data preparation for reporting:** Created cleaned views and Power BI reporting views.
7. **Data modelling:** Connected the reporting tables in Power BI and created a DateTable and 23 relationships.
8. **Dashboard development:** Built interactive report pages, DAX measures, drill-through, bookmarks and a tooltip page.
9. **Business reporting:** Prepared a written insights report and an 11-slide presentation.
10. **Recommendations:** Identified areas that need management attention and further data investigation.

## 6. Database Design and SQL Work

The PostgreSQL database is named `healthconnect`.

The project includes these database objects:

- `data_quality_log`: records the data quality issues found during the project.
- `health_facilities`: a list of the 20 facility IDs (HF001 to HF020), created from the departments table, because the data had no facility names.
- `v_patients`: cleaned patient data, with real dates, age groups and province, district and sector names.
- `v_appointments`: cleaned appointment data with proper dates.
- `v_billing_full`: billing view with appointment, department and payment details.
- `v_diagnoses_full`: diagnosis view with appointment details.
- `v_feedback_full`: patient feedback view with appointment details.
- `v_staff_all`: all six staff tables combined into one view.

The SQL work covers patients, appointments, clinical activity, financial performance, insurance claims and data quality. Three queries use stand-ins because the data has no referral, admission or service-level records: Q15 (visit type by hospital, for referral patterns), Q29 (emergency rate by diagnosis, for admission rate) and Q33 (revenue by visit type, for revenue by service). Six queries (Q22, Q23, Q24, Q26, Q27 and Q28) could not be answered because laboratory, prescription, admission and referral data were not provided.

The database was backed up as `healthconnect_backup.backup`.

**Note:** The backup is a PostgreSQL custom-format backup and needs PostgreSQL tools (`pg_restore`) to restore.

## 7. Power BI Dashboard

The dashboard gives an overview of healthcare performance and lets users explore each area in more detail.

### Page 1: Executive Dashboard
High-level KPIs (patients, appointments, revenue, facilities, doctors and satisfaction), month and hospital slicers, a revenue trend and a chart and table bookmark toggle.

### Page 2: Patient Analytics
Patient demographics, age pyramid, chronic conditions, province map and insurance distribution.

### Page 3: Clinical Analytics
Diagnoses, severity, monthly diagnosis trend and emergency appointments.

### Page 4: Financial Dashboard
Revenue, collections, outstanding balances, claim approval, revenue by facility and department, payment methods and month over month growth.

### Page 5: Operational Dashboard
Staff distribution, beds, medical equipment, patients per staff member and a facility comparison matrix.

### Page 6: Patient Experience
Satisfaction scores, rating distribution, feedback analysis, poor rating trend, hospital and department rankings and a decomposition tree.

### Additional Features

- Facility Details drill-through page
- Hidden tooltip page
- Bookmarks for switching between views
- About 30 DAX measures for KPIs
- DateTable for time analysis, with month over month growth
- 23 relationships between reporting tables

Month over month growth is used instead of year over year because the data covers only 2026.

## 8. Key Findings

### Financial Performance

- Billed revenue was approximately **RF9.31 billion**.
- Revenue collection was approximately **90.1%**.
- Outstanding revenue was approximately **RF920 million**.

Most revenue was collected, but a substantial balance remains and needs follow-up.

### Insurance Claims

- Approximately **50% of insurance claims were approved**, and the rate was almost the same for each of the four insurers.

This suggests the cause may sit in the claims process itself, such as documentation or submission, and not with one insurer.

### Patient Experience

- The average patient satisfaction score was approximately **2.99** out of 5.
- Approximately **40.4% of feedback records received poor ratings**.
- Facility HF014 had an average satisfaction score of approximately **2.77** and was also among the busier facilities.

Patient experience deserves attention, particularly at facilities that combine high activity with lower satisfaction.

### Patient Demographics and Clinical Activity

- The average patient age was approximately **45 years**.
- Approximately **74.6% of patients had a recorded chronic condition**.
- Emergency visits accounted for approximately **33% of appointments**.

### Facility Performance

HF013, HF014 and HF010 were the busiest facilities in the supplied data. These facilities may need closer monitoring of demand, patient experience and resources.

### Operational Data

All 2,000 beds were marked as available, so bed utilisation shows 0%. This should not be read as proof that no beds were occupied. It shows that the supplied bed status data cannot establish actual utilisation.

## 9. Data Quality Issues and Limitations

### Incomplete Relationships Between Datasets

Only 5,000 of 60,000 bills and 5,000 of 60,000 diagnoses link to an appointment record, and 19,308 of 21,064 feedback records are unlinked. Results by hospital, department or month use only the linked records, while overall totals use all records.

### Damaged Phone Numbers

All 20,000 phone numbers were damaged by Excel formatting (scientific notation such as 2.50788E+11), leaving only a handful of distinct values. Phone numbers were not used in the analysis.

### Limited Healthcare Data

The supplied datasets did not include laboratory results, prescription records, admission data or referral information, so the analysis could not cover the full patient care journey.

### Bed Utilisation Data

All beds were marked as available. Without reliable occupancy information, actual bed utilisation could not be calculated.

### Feedback and Rating Inconsistencies

Written comments did not match their ratings (for example, "Poor" comments appeared with 5 star ratings), so ratings were used to measure satisfaction.

### Missing Facility Names

Facilities were represented by IDs (HF001 to HF020) and not by names, which limited the readability of some visuals and ruled out regional analysis by facility.

### Limited Time Coverage

The data covers only 2026, so month over month comparisons should not be treated as evidence of long-term growth or seasonal trends.

### Interpretation of Findings

The findings describe the supplied data and its limitations. They should not be generalised to every healthcare facility in Rwanda.

## 10. Business Recommendations

1. **Improve revenue collection:** Investigate outstanding balances, monitor collection performance and set up a process for following up on unpaid bills.
2. **Review insurance claims:** Examine rejected and pending claims to find common causes and improve claim submission and processing.
3. **Improve patient satisfaction:** Investigate low ratings and feedback patterns, especially at busy facilities such as HF014.
4. **Match staffing to demand:** Staffing is roughly even while demand ranges from 217 to 278 appointments per hospital, so review whether staff and resources follow patient demand.
5. **Monitor emergency demand:** Review emergency volumes and whether follow-up and primary care could reduce them.
6. **Strengthen chronic disease management:** Explore the needs of patients with recorded chronic conditions and improve follow-up and continuity of care.
7. **Improve data quality:** Introduce validation rules, keep phone numbers as text and check for missing or inconsistent records.
8. **Fix data relationships:** Make sure bills, diagnoses and feedback link to appointments, so reports give a more complete view of patient activity.
9. **Improve bed reporting:** Record occupied, available and out-of-service beds before calculating utilisation.
10. **Add descriptive facility information:** Include facility names and locations to support clearer comparisons.
11. **Expand future analysis:** Add more periods and datasets, such as laboratory results, prescriptions, admissions and referrals.

These recommendations are based on the available data and should be validated with the relevant healthcare teams before action.

## 11. Project Deliverables

- PostgreSQL table creation script: `01_create_tables.sql`
- Healthcare analytics SQL queries (40): `Healthconnect_queries.sql`
- Power BI views: `PoweBI_Views.sql`, the cleaned views that feed the dashboard
- PostgreSQL database backup: `healthconnect_backup.backup`
- Data quality log: `data_quality_log.csv`
- Power BI dashboard: `.pbix` file
- Power BI dashboard export: PDF report
- Business insights report: Word document
- Project presentation: 11-slide PowerPoint
- Project documentation: `README.md`

## 12. Repository Contents

| File | Description |
|---|---|
| `README.md` | Project documentation |
| `01_create_tables.sql` | Creates the 26 empty tables |
| `Healthconnect_queries.sql` | The 40 SQL queries |
| `PoweBI_Views.sql` | Cleaned views used by Power BI |
| `healthconnect_backup.backup` | Full PostgreSQL backup |
| `data_quality_log.csv` | Data cleaning and validation log |
| Power BI dashboard (`.pbix`) | Interactive dashboard |
| Dashboard PDF | Executive dashboard export |
| Business insights report | Written findings and recommendations |
| Presentation (`.pptx`) | 11-slide executive presentation |

## 13. How to Use the Project

1. Clone or download the repository.
2. Install PostgreSQL and pgAdmin 4.
3. Create an empty database named `healthconnect`.
4. Restore the backup:
   `pg_restore -U postgres -d healthconnect healthconnect_backup.backup`
5. Open `Healthconnect_queries.sql` in pgAdmin and run the queries one at a time.
6. Open the Power BI file in Power BI Desktop. If asked, connect to server `localhost` and database `healthconnect`, then refresh.

The source CSV files are not included in this repository.

## 14. Privacy and Data Handling

The datasets were supplied by AnalystLab Africa as part of the internship. This repository contains no database passwords or credentials.

## 15. Skills Demonstrated

- SQL querying and data exploration
- PostgreSQL database development
- Data loading with Python
- Data quality assessment and cleaning
- Relational data modelling
- Power BI dashboard development
- DAX measures and KPI reporting
- Data visualisation and business storytelling
- Identifying data limitations
- Turning findings into business recommendations
- Technical documentation and project presentation

## 16. Conclusion

The HealthConnect Rwanda Healthcare Analytics project shows how data analytics tools can be used to explore healthcare performance, financial collection, insurance claims, patient demographics, facility activity and patient satisfaction.

The analysis identified important areas for further investigation, including outstanding revenue, insurance claim approvals, patient feedback, incomplete data relationships and unreliable bed availability records.

Beyond building a dashboard, this project reinforced the importance of data quality, careful interpretation and practical recommendations when using data to support business decisions.

This project was completed as part of my Data Analytics track in the AnalystLab Africa Experience Lab internship.

---

**Author:** Adeyemo Taiwo Aminat (Meenah)
**Program:** AnalystLab Africa Experience Lab
**Track:** Data Analytics
**Project:** HealthConnect Rwanda Healthcare Analytics

#AnalystLabAfrica #DataAnalytics #HealthcareAnalytics #SQL #PostgreSQL #PowerBI #Python #BusinessIntelligence
