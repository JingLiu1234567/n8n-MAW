# 🌟 n8n Marketing Automation Workflow (n8n-MAW)

**CMW (Campaign Marketing Automation Workflow)** is an **end-to-end AI-powered analysis system** built with **n8n, Google Sheets, and OpenAI**.

It transforms a *raw natural-language marketing case* into structured analytical metrics, loads selected datasets, and automatically generates **MySQL-ready SQL queries**.

---

## 🚀 Overview
CMAW automates the entire analytics pipeline:

- **User inputs one natural-language case**（中文 / English）
- **AI extracts analytical question + required metrics**
- **Result is saved to Google Sheets**
- **Analyst selects relevant databases**
- **Workflow loads all selected datasets**
- **AI generates MySQL-compatible SQL queries**
- **Formatted SQL is emailed as a file attachment**

---

# 🧩 Workflow Architecture
<img width="3840" height="1732" alt="46cf12916a48001dd14f79003df683c7" src="https://github.com/user-attachments/assets/6c8ca9c1-ff26-4039-b494-37592c9d97f2" />

The system consists of **six major components**:

---

## 1️⃣ Natural-Language Case Input (Trigger Form)

The user submits *one* free-text case:

Examples:

- “分析客户 A 在 2022 年的季节性销售”
- “What are seasonal demand trends for Client A?”
- “Analyze sessions → conversion performance for Campaign B”

This triggers the workflow.

---

## 2️⃣ Automatic Question & Metrics Extraction (AI Agent)

- Understanding of case intent (中文 or English)
- Inference of essential metrics like a senior analyst
- Field validation to ensure metrics exist in uploaded databases
- JSON structuring for downstream processing

---

## 3️⃣ Automatic Saving to Google Sheets

The workflow logs:

- Extracted question
- Identified metrics
- Timestamp

into a Google Sheet for versioning and collaboration.

---

## 4️⃣ Analyst Chooses Relevant Databases (Google Sheets)

You may upload **any number of datasets**.

### Common sheets:

| Sheet Name       | Content                                      |
|------------------|----------------------------------------------|
| `site_data`      | date, sessions, orders, sales, category      |
| `keyword_data`   | keyword, search_volume, date                 |
| *(optional)* more | campaign, SKU views, ads data, etc.          |

---

### 🔄 Replacing / Adding Databases

You may freely:

- Replace sheet contents  
- Point a **Read Sheet** node to a new sheet  
- Add additional sheet nodes  

**No code change is needed.**  
`Code2` automatically detects available fields and sends them to the SQL Agent.

---

## 5️⃣ Automatic SQL Generation (SQL Agent)

The SQL Agent uses:

- Extracted question  
- Extracted metrics  
- Uploaded database fields  
- Auto-detected date ranges  
- MySQL-compatible time grain rules  

It outputs multi-level seasonal analysis SQL, for example:

```sql
SELECT date_format(date, '%Y-%m') AS month,
       SUM(sales) AS total_sales
FROM site_data
GROUP BY 1;
```

---

## 6️⃣ SQL Formatting & Gmail Delivery (Code3)

Code3 formats the SQL:

- Adds question at the top  
- Labels each metric & time grain  
- Cleans and formats SQL  
- Generates a downloadable `.sql` file  
- Emails it to your inbox  

---

# 🔥 End-to-End Summary

✔ User inputs **one natural-language case**  
✔ AI identifies **the question & metrics**  
✔ Google Sheets stores **the results**  
✔ Workflow loads **chosen datasets**  
✔ AI generates **clean MySQL SQL**  
✔ SQL is **emailed automatically**  

A complete intelligent analytics pipeline, ideal for:

- E-commerce analysis  
- Campaign insights  
- Traffic → conversion analysis  
- Seasonal performance analysis  
- Automated BI reporting  

---

# 📁 Repository Structure
/Campaign Marketing Analysis.json   → n8n workflow export  
/README.md                         → Documentation  
/screenshots/                      → Workflow images  

---

# 🛠 Setup Guide

1. Import workflow JSON into n8n  
2. Connect Google Sheets credentials  
3. Upload or link your datasets  
4. Connect Gmail  
5. Trigger workflow  
6. Receive formatted SQL  

---

# 🧱 Database Maintenance Guide

### Replace a dataset:

- Replace the content inside the same Google Sheet  
- **OR** modify the **Read Sheet** node to point to a new sheet  
- No code changes needed  

### Add a dataset:

- Create a new Google Sheet  
- Duplicate a **Read Sheet** node  
- Connect it to **Merge → Code2**  
- `Code2` will automatically detect fields  
