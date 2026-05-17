# 🏢 AmbitionBox Company Analysis

A data collection and Exploratory Data Analysis (EDA) project that scrapes, cleans, and analyzes company data from AmbitionBox to uncover patterns in employee satisfaction across industries, locations, and company sizes in India.

---

## 📌 Problem Statement

Job seekers and HR professionals lack a structured, data-driven understanding of what makes a company a great place to work in India. While platforms like AmbitionBox collect thousands of employee reviews, this data remains largely unexplored at scale. There is no clear analysis of which industries, locations, or company sizes consistently deliver better employee satisfaction across key factors.

---

## 🎯 Objectives

1. Identify which industries have the highest and lowest employee ratings
2. Understand how company size impacts overall employee satisfaction
3. Discover which sub-factors (work-life balance, career growth, etc.) drive overall ratings the most
4. Analyze geographic trends — which Indian states and cities have the best-rated companies
5. Examine how company age (founding year) correlates with ratings

---

## 📂 Dataset

- **Source:** Scraped from [AmbitionBox](https://www.ambitionbox.com) using `requests` + `BeautifulSoup`
- **Final File:** `Company_Data.csv` (merged from 6 scraping batches)
- **Key columns scraped:**

| Column | Description |
|---|---|
| `Company` | Company name |
| `Ratings` | Overall employee rating |
| `Founded` | Year of founding |
| `Industry` | Primary industry |
| `Indian_Employee_Count` | Headcount in India |
| `Global_Employee_Count` | Global headcount |
| `India_Hq_City / State` | Indian headquarter location |
| `Main_Hq_City / Country` | Global headquarter location |
| `Job_Security_Rating` | Sub-rating |
| `WorkLife_Rating` | Sub-rating |
| `Company_Culture_Rating` | Sub-rating |
| `Skill_Development_Rating` | Sub-rating |
| `Work_Satisfaction_Rating` | Sub-rating |
| `Compensation_Rating` | Sub-rating |
| `Career_Growth_Rating` | Sub-rating |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| Pandas | Data manipulation |
| NumPy | Numerical operations |
| Matplotlib | Visualizations |
| Seaborn | Statistical plots |
| Requests + BeautifulSoup | Web scraping |
| JSON | Parsing Next.js page data |
| Jupyter Notebook | Development environment |

---

## 📋 Project Structure

```
├── Ambition_Box_Analysis.ipynb    # Main notebook (scraping + EDA)
├── Company_Data.csv               # Final merged dataset
├── Batch_01.csv to Batch_06.csv   # Scraping batch files
└── README.md
```

---

## 🔄 Workflow

### Section 1 — Data Collection (Web Scraping)

- Scraped company names and ratings from listing pages (paginated)
- For each company, fetched the `__NEXT_DATA__` JSON embedded in the overview page to extract structured data
- Scraped 6 batches of 100 companies each and merged into a single CSV
- Fields extracted: founding year, HQ details, employee counts, industry, and all 7 sub-ratings

### Section 2 — Data Cleaning & Preparation

- **Null value handling** — Dropped rows with missing ratings, industry, or employee count
- **Duplicate removal** — Verified and removed duplicate company entries
- **HQ column splitting** — Parsed `"Bangalore/Bengaluru, Karnataka"` format into separate `City` and `State` columns for both India and global HQs
- **State name standardization** — Fixed inconsistent state entries (`"New Delhi"→"Delhi"`, `"Tamilnadu"→"Tamil Nadu"`, `"Harayana"→"Haryana"`, etc.)
- **Country name standardization** — Merged variants like `"US"`, `"USA"`, `"United States (USA)"` into `"United States"`
- **Dtype fixes** — Converted `Founded` and `Indian_Employee_Count` to integers; HQ columns to strings
- **Feature Engineering:**
  - `Ind_Emp_Size_Range` — Binned Indian employee count into 9 size ranges (1–50 to 100k+)
  - `Decade` — Derived from `Founded` year for trend analysis

---

## 📊 Key Insights

### 🏭 Industry Landscape

- **IT Services & Consulting dominates** with 214 companies — more than double the second place
- IT-related sectors combined (IT Services + Software + Internet) = **331 companies (~21% of dataset)**
- Auto Components (91) and Engineering & Construction (73) reflect India's strong manufacturing and infrastructure presence
- **BPO (55)** confirms India's outsourcing industry is still significant

### 🏙️ Geographic Distribution

- **Maharashtra leads** with 355 company HQs — driven by Mumbai, India's financial capital
- **Karnataka (165)** second — Bengaluru's IT ecosystem
- **Haryana (139)** third — Gurugram's corporate hub
- Top 5 states account for **875 companies (~54% of dataset)**
- South India combined (Karnataka + Tamil Nadu + Telangana + Kerala) = **357 companies**

### 📏 Company Size

- **1k–5k employee range dominates** with 914 companies — AmbitionBox skews toward mid-sized companies
- Very few small companies (1–50 employees: only 2 entries) — small businesses are underrepresented
- 100k+ companies: 38 entries covering India's largest employers

### ⭐ Ratings Overview

- Most companies rated between **3.5 and 4.2**, peak around **3.9–4.0**
- Very few companies below 3.0

### 🏆 Industry Ratings — Best vs Worst

| Rank | Top Industries | Bottom Industries |
|---|---|---|
| 1 | Sports & Recreation (~4.2) | Architecture & Interior Design (~3.3) |
| 2 | Non-Profit (~4.2) | Content Development (~3.3) |
| 3 | Fitness & Wellness (~4.1) | Accounting & Auditing |
| 4 | Defence & Aerospace | Analytics & KPO |
| 5 | Government | — |

### 📈 Sub-Rating Averages

| Sub-Rating | Average |
|---|---|
| Work-Life Balance | ~3.71 ✅ Highest |
| Company Culture | ~3.63 |
| Job Security | ~3.63 |
| Skill Development | ~3.61 |
| Compensation | ~3.56 |
| Work Satisfaction | ~3.54 |
| Career Growth | ~3.19 ❌ Lowest |

> Career growth is the biggest pain point for employees across industries.

### 🔗 Correlation with Overall Rating

| Sub-Rating | Correlation |
|---|---|
| Work Satisfaction | 0.97 — Highest |
| Company Culture | 0.94 |
| Career Growth | ~0.90 |
| Compensation | 0.81 — Lowest |

All sub-ratings show strong positive correlation with overall rating.

### 🗺️ State-wise Ratings

- **Kerala (~3.96)** — highest average company rating
- **Rajasthan (~3.94)** and **Delhi (~3.92)** — runner-ups
- Major corporate states (Maharashtra ~3.80, Karnataka ~3.72) score only moderate despite high company count
- **Madhya Pradesh (~3.55)** — lowest among major states

### 🌍 Global HQ Countries

- **India dominates** with 1,069 domestic HQs
- **United States (247)** — highest foreign contributor
- UK, Germany, France — moderate European presence

---

## 💡 Business Recommendations

- **Career growth is the #1 gap** — companies looking to improve retention should focus on structured growth paths and promotion pipelines
- **Work satisfaction drives overall rating the most (0.97 correlation)** — meaningful work and role clarity are critical
- **Sales/high-pressure industries consistently rate lower** — workload management programs can improve perception
- **Kerala and Rajasthan outperform** larger states — best practices from smaller-state companies should be studied
- **IT sector is oversaturated** in AmbitionBox listings — job seekers in non-IT fields may find less comparative data

---

## 🚀 How to Run

```bash
# Clone the repository
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# Install dependencies
pip install pandas numpy matplotlib seaborn requests beautifulsoup4 jupyter

# Launch the notebook
jupyter notebook Ambition_Box_Analysis.ipynb
```

> **Note:** The scraping section is commented out by default since the data has already been collected. Load `Company_Data.csv` directly to run the EDA.

---

## ⚠️ Scraping Note

The scraper uses rotating user-agents and randomized delays (`2–5s`) to be respectful to AmbitionBox's servers. Data was collected in 6 batches of 100 companies each. Always check the website's `robots.txt` and Terms of Service before scraping.

---

## 👨‍💻 Author

**Sourabh Patnaik**
Data Science Student | Innomatics Research Labs

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
