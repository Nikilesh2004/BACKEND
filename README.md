

# 📊 Vehicle Registration Dashboard – Backend Developer

---

## 🚀 Objective

Build an interactive dashboard focused on **vehicle registration data** from the **Vahan Dashboard**, with insights for investors.

---

## 📂 Features

* **YoY & QoQ growth** for:

  * Total vehicles by category (2W/3W/4W)
  * Manufacturer-wise registrations
* **Filters**: Date range, Vehicle category, Manufacturer
* **Visualizations**: Line charts, Bar graphs, % change
* **Investor-friendly UI** built with **Streamlit**

---

## 🛠 Tech Stack

* **Python 3.10+**
* **Streamlit** (dashboard UI)
* **Pandas** (data processing)
* **Matplotlib / Plotly** (charts)
* **SQL (optional)** for querying structured data

---

## 📑 Data Source

* Public Vahan Dashboard exports
* Preprocessed into `registrations.csv`

**Sample Format:**

```csv
date,category,manufacturer,registrations
2023-01-15,2W,Honda,1520
2023-01-15,4W,Maruti,1100
2023-02-01,3W,Bajaj,500
```

---

## 📊 Example SQL Queries

### Year-over-Year Growth

```sql
SELECT category,
       EXTRACT(YEAR FROM reg_date) AS year,
       SUM(registrations) AS total,
       (SUM(registrations) - LAG(SUM(registrations)) OVER (PARTITION BY category ORDER BY EXTRACT(YEAR FROM reg_date)))
       / LAG(SUM(registrations)) OVER (PARTITION BY category ORDER BY EXTRACT(YEAR FROM reg_date)) * 100 AS yoy_growth
FROM registrations
GROUP BY category, EXTRACT(YEAR FROM reg_date);
```

### Quarter-over-Quarter Growth

```sql
SELECT category,
       EXTRACT(YEAR FROM reg_date) AS year,
       EXTRACT(QUARTER FROM reg_date) AS quarter,
       SUM(registrations) AS total,
       (SUM(registrations) - LAG(SUM(registrations)) OVER (PARTITION BY category ORDER BY EXTRACT(YEAR FROM reg_date), EXTRACT(QUARTER FROM reg_date)))
       / LAG(SUM(registrations)) OVER (PARTITION BY category ORDER BY EXTRACT(YEAR FROM reg_date), EXTRACT(QUARTER FROM reg_date)) * 100 AS qoq_growth
FROM registrations
GROUP BY category, EXTRACT(YEAR FROM reg_date), EXTRACT(QUARTER FROM reg_date);
```

---

## 🖥 Setup Instructions

1. Clone the repo

   ```bash
   git clone https://github.com/yourusername/vehicle-dashboard.git
   cd vehicle-dashboard
   ```

2. Create virtual environment

   ```bash
   python -m venv venv
   source venv/bin/activate   # Linux/Mac
   venv\Scripts\activate      # Windows
   ```

3. Install dependencies

   ```bash
   pip install -r requirements.txt
   ```

4. Place dataset in `data/registrations.csv`

5. Run Streamlit app

   ```bash
   streamlit run app/main.py
   ```

---


## 📈 Investor Insights (Sample)

* **EV 3W segment** is the fastest growing
* Top 3 manufacturers hold **>60% market share**
* Seasonal sales dip in **Q2**, rebound in festive season

---

## 🗺 Roadmap

* Regional drilldowns (state/district)
* Auto data refresh
* Export PDF/Excel reports
* AI-powered investment insights

---


