
# 🏫 NYC Schools PostgreSQL Exploration

This project connects to a hosted PostgreSQL database using Python (`psycopg2`) to explore key NYC school datasets through SQL queries and analysis in pandas.

---

## 🗂️ Datasets Queried

All tables are under the schema `nyc_schools`:

- `high_school_directory`
- `school_demographics`
- `school_safety_report`

---

## ⚙️ Technologies Used

- Python
- pandas
- psycopg2 (PostgreSQL driver)
- SQL (PostgreSQL syntax)

---

## 🔍 Key Analysis Performed

- **School Count per Borough**
  - Total and distinct school counts (`dbn`) by borough

- **English Language Learner (ELL) Insights**
  - Average ELL percentage by borough (joined `school_demographics` and `high_school_directory`)

- **Special Education Focus**
  - Top 3 schools per borough with highest `% of special education students` (`sped_percent`)

---

## 🧠 Sample SQL Used (in Python)

```python
query = """
SELECT borough, COUNT(*) AS school_count
FROM nyc_schools.high_school_directory
GROUP BY borough;
"""
df = pd.read_sql(query, conn)

🏁 How to Run

	1.	Set up PostgreSQL credentials (hardcoded for demo)
	2.	Run Python scripts or Jupyter Notebook
	3.	Explore dataframes or export results

📁 Folder Structure

nyc_schools_analysis/database_queries

├── queries.ipynb      # Python + SQL logic
├── README.md