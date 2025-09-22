# 🏙️ NYC School Analysis – End-to-End Data Exploration, Integration & Visualization

This project performs a comprehensive analysis of various NYC school datasets, spanning data cleaning, SQL queries, exploratory visualizations, and database integration for reproducible insights.

---

## 🔄 Project Workflow

### 1. 🚨 School Incident Analysis
> *Dataset:* Incident reports by school and borough

- Cleaned column names (lowercase, underscores, no special chars)
- Linked dataset to [Google Sheets](https://docs.google.com/spreadsheets/d/1DIzcNSxlzB2cKDN7tTS8CgtEZqfhHjDEhnd593LALn4/edit?usp=sharing)
- Counted total incidents (6,310) and unique schools (1,890)
- Identified most frequent incident type: `no criminal`
- Calculated Bronx's incident share: **28.24%**
- Explored major violations, borough-level breakdowns, and anomaly cases

**🔍 Key Insights**
- Brooklyn and Bronx have the highest number of incidents
- Staten Island shows high rate of "no crime" reports
- `dbn` and `location_code` had ~16% missing values
- Building name was missing in 40%+ rows

---

### 2. 🏫 High School Directory Exploration
> *Dataset:* NYC DOE High School Directory

- Cleaned and standardized columns
- Converted start/end times to school day duration
- Filtered missing and unusable values
- Parsed nested lists and text fields

**📊 Visualizations Created**
- 🧭 Total & unique schools by borough
- 🎓 Grade span & student distribution
- 🚍 School accessibility and transport services
- ⏰ School day length distribution
- 📚 Course, language, AP offerings
- 🤝 Top 10 schools by partnership count
- 🎨 Word cloud of extracurriculars
- 🏀 Sports by gender (bar + donut chart)
- 🗺️ Interactive student-population bubble map (Folium)

> 📁 Output saved in: `school_directory_exploration/visuals/`

---

### 3. 🧮 PostgreSQL Database Queries (via Python)

- Connected to Neon PostgreSQL with `psycopg2`
- Queried key tables in schema `nyc_schools`:
  - `high_school_directory`
  - `school_demographics`
  - `school_safety_report`

**🔍 SQL-Based Analysis**
- Schools per borough (total & unique `dbn`)
- Average English Language Learner (ELL%) per borough
- Top 3 schools per borough by special education percentage (`sped_percent`)

> 📂 Notebook saved in: `nyc_schools_analysis/database_queries/queries.ipynb`

---

### 4. ✍️ SAT Scores Cleaning & Database Integration

> *Dataset:* NYC SAT performance dataset

- Normalized headers and cleaned formatting (e.g., removed `%` signs)
- Fixed SAT score typos and filtered invalid values outside 200–800
- Dropped irrelevant or duplicate columns (e.g., `contact_extension`)
- Converted to numeric types and handled missingness

**🧠 Key Fixes**
- Removed 15 exact duplicates
- Converted `"85%"` to `85.0` for `pct_students_tested`
- Handled partial missing SAT scores while preserving valuable rows

**📦 Integration Strategy**
- Uploaded cleaned table to PostgreSQL using `SQLAlchemy`
- Table name: `thofa_tazkia_sat_results` under schema `nyc_schools`
- Joined by `dbn` with other datasets

| Column Name                      | Type   | Description                        |
|----------------------------------|--------|------------------------------------|
| dbn                              | TEXT   | School identifier                  |
| school_name                      | TEXT   | School name                        |
| num_of_sat_test_takers          | FLOAT  | Count of test takers               |
| sat_critical_reading_avg_score  | FLOAT  | Avg. Reading SAT score             |
| sat_math_avg_score              | FLOAT  | Avg. Math SAT score                |
| sat_writing_avg_score           | FLOAT  | Avg. Writing SAT score             |
| pct_students_tested             | FLOAT  | Percentage tested (0–100)          |
| academic_tier_rating            | FLOAT  | Academic tier score (1–4 scale)    |

> 📂 Upload script: `sat_cleaning/sat_to_postgres.py`

---

## 🧰 Tools & Libraries Used

- **Python**: `pandas`, `matplotlib`, `seaborn`, `folium`, `wordcloud`, `psycopg2`, `sqlalchemy`
- **SQL**: PostgreSQL (Neon)
- **Data Sources**: NYC Open Data
- **IDE**: Visual Studio Code / Jupyter Notebook

---

## 📁 Final Folder Structure

nyc-school-analysis/
├── incident_analysis/                   # Incident insights + Google Sheets
├── school_directory_exploration/        # Directory data cleaning + visuals
│   ├── data/
│   ├── visuals/
├── nyc_schools_analysis/
│   ├── database_queries/                # psycopg2 SQL scripts + results
├── sat_cleaning/                        # SAT cleaning and upload to DB
├── README.md                            # This file

---

## ✅ Summary

This multi-stage project combines data wrangling, exploratory visualization, and SQL analytics to deliver comprehensive insights into NYC schools—covering everything from student performance to safety and enrichment offerings.