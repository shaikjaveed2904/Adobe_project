# 🚀 Search Keyword Performance Analyzer  
### Data Engineer Applicant Assessment – Adobe Analytics

---

## 📌 Problem Statement

The objective of this exercise is to determine:

> How much revenue is generated from external search engines (Google, Yahoo, MSN, Bing), and which search keywords are performing the best based on revenue?

The input is a tab-delimited Adobe Analytics hit-level dataset, where each row represents a single visitor interaction (“hit”) on the website.

### Final Output Requirements

The final output must:

- Aggregate revenue by:
  - **Search Engine Domain**
  - **Search Keyword**
- Include only revenue from **purchase events (event ID 1)**
- Be sorted by **Revenue (Descending)**
- Be generated in the required naming format:

---

## 🏗 Solution Overview

This Python application:

- Reads the input file **line by line** (memory-efficient approach).
- Filters records where:
  - The `referrer` contains a supported search engine.
  - The `event_list` contains purchase event ID `1`.
- Parses the `product_list` column:
  - Extracts revenue from the 4th field of each product entry.
  - Revenue is counted only when a purchase event occurs.
- Extracts:
  - Search engine domain (e.g., `google.com`)
  - Search keyword (`q=` or `p=` parameter from the referrer URL)
- Aggregates total revenue by search engine and keyword.
- Sorts the results by revenue in descending order.
- Writes the final tab-delimited output file with a header row.

---

## 📂 Project Structure
Adobe_project/
│
├── search_keyword_performance.py # Main Python application
├── sample_data.tsv # Sample input dataset
├── output_example.tsv # Example output file
├── README.md


---

## ▶ How to Run

### 🔹 Prerequisites

- Python 3.7 or later

(Optional virtual environment)

```bash
python3 -m venv venv
source venv/bin/activate

🔹 Execute
python search_keyword_performance.py path/to/input_file.tsv

Example:
python search_keyword_performance.py sample_data.tsv

🔹 Output

The script generates:
YYYY-mm-dd_SearchKeywordPerformance.tab
☁ AWS Deployment

The application is deployed on AWS (EC2 instance) and accessible at:

http://52.66.30.106:8501/

📈 Scalability Considerations
Current Design

Processes input file line by line

Avoids loading the entire dataset into memory

Suitable for moderately large files

For Very Large Files (10GB+)

Improvements would include:

Using AWS Glue or EMR (Spark) for distributed processing

Storing data in Amazon S3 with partitioning

Writing results to Redshift or querying via Athena

Automating workflows using Step Functions

🛡 Assumptions & Error Handling

Only purchase events (event_list contains 1) generate revenue.

Revenue is extracted from the 4th field in product_list.

Malformed or incomplete rows are safely skipped.

Required columns exist (event_list, product_list, referrer).

🔮 Future Enhancements

Add unit tests (pytest)

Add structured logging

Dockerize the application

Implement CI/CD pipeline

Automate S3-triggered processing

📌 Summary

This project demonstrates:

Python-based data processing

File parsing and transformation

Revenue aggregation logic

AWS deployment

Scalability planning

Clean coding practices
