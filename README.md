# B2B Lead Scoring Engine

An end-to-end pipeline for scoring B2B SaaS leads in the mid-market manufacturing sector: from raw data ingestion through Snowflake, feature engineering and modeling in Python, dashboarding in Power BI, to daily automated hot-lead alerts via n8n.

---

## 🔧 Tech Stack

- **Data Warehouse**: Snowflake (DDL + CSV ingestion)  
- **Feature Engineering & Modeling**: Python (pandas, scikit-learn) in Jupyter Notebook  
- **Visualization**: Power BI (.pbix)  
- **Automation**: n8n (workflow JSON & SMTP)  

---

## 🚀 Getting Started

1. **Clone the repo**  
   ```bash
   git clone https://github.com/yourorg/project-origins-lead-scoring.git
   cd project-origins-lead-scoring
  
2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   
3. **Provision Snowflake**
   - Run DDLs in sql/ to create leads, company_firmographics, marketing_engagements.
   - Load data/*.csv via COPY INTO.
     
4. **Run the Notebook**
   - Launch Jupyter: jupyter lab → open notebooks/lead_scoring.ipynb.
   - Update credentials & paths, then:
       1. Ingest data from Snowflake
       2. Engineer features (lead_age, total_engagements, unique_actions, days_since_nonconv, industry dummies)
       3. Train & tune Random Forest (final AUC ≈ 0.95)
       4. Export model_input.csv, lead_scores.csv & enriched_lead_scores.csv
          
5. **Power BI Dashboard**
   - Open powerbi/LeadScoring.pbix.
   - Point to lead_scores.csv (or a Snowflake view).
   - Explore KPI cards, tiered bars, funnel, scatter, slicers.
     
6. **n8n Automation**
   - Import n8n/hot_lead_alert.workflow.json.
   - Configure your SMTP credentials.
   - Schedule daily: read lead_scores.csv, filter lead_score ≥ 0.8, send email.

## 🎯 Pipeline Overview

1. Snowflake: create tables & ingest raw CSVs
2. Python Notebook:
   - Read from Snowflake
   - Feature engineering
   - Train/tune Random Forest
   - Save lead_scores.csv
3. Power BI: visualize scores & insights
4. n8n: daily hot-lead email alerts

## 🔍 Key Features & Model

1. Features: firmographics, engagement counts, recency, industry dummies
2. Model: RandomForestClassifier (300 trees, balanced)
3. Validation: 5-fold CV AUC ≈ 0.99; time-split AUC ≈ 0.95
4. Output: probability lead_score ∈ [0, 1]

## 🔮 Future Scope

1. Real-time scoring & drift monitoring (Kinesis/Kafka + dashboard)
2. Third-party enrichment (Clearbit, intent data)
3. REST API for on-demand scoring & CRM integration




