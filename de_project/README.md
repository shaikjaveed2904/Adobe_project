# 🚀 Search Keyword Performance Analyzer  
**Data Engineer Applicant Assessment – Adobe Analytics**
---
## 📌 Problem Statement
The objective of this exercise is to determine:
> How much revenue is generated from external search engines (Google, Yahoo, MSN, Bing), and which search keywords are performing the best based on revenue?
The input is a tab-delimited Adobe Analytics hit-level dataset, where each row represents a single visitor interaction (“hit”).
---
## 🎯 Expected Output
The final output:
- Aggregates revenue by:
  - Search Engine Domain  
  - Search Keyword  
- Includes only revenue from **purchase events (event ID 1)**  
- Is sorted by **Revenue (Descending)**  
- Is generated in the required naming format:
YYYY-mm-dd_SearchKeywordPerformance.tab
---
# 🏗 Solution Overview
The Python application performs the following steps:
1. Reads the input file line-by-line (memory-efficient approach).
2. Filters records where:
   - The referrer contains a supported search engine.
   - The `event_list` contains purchase event ID 1.
3. Parses the `product_list` column:
   - Extracts revenue from the 4th field of each product entry.
4. Extracts:
   - Search engine domain (e.g., google.com)
   - Search keyword (`q=` or `p=` parameter from referrer URL)
5. Aggregates total revenue by:
   - Search Engine Domain
   - Search Keyword
6. Sorts results by revenue in descending order.
7. Writes the final tab-delimited output file with a header row.
---
# 📂 Project Structure
DE_PROJECT/
│
├── de_project/
│ ├── search_keyword_performance.py
│ ├── sample_data.tsv
│ ├── output_example.tsv
│ │
│ └── terraform/
│ ├── main.tf
│ ├── provider.tf
│ ├── variables.tf
│ └── outputs.tf
│
└── README.md

---
# 🧠 Technical Implementation

## ✔ Application Requirements Met


- Implemented in Python 3
- Contains at least one class
- Accepts a single command-line argument (input file path)
- Generates required tab-delimited output file
- Includes header row
- Sorted by revenue (descending)
---
## ✔ Revenue Calculation Logic
Revenue is extracted from the `product_list` column.
Format example:
Category;ProductName;Quantity;Revenue;Events
Revenue is counted only if:
- `event_list` contains event ID 1 (Purchase)
Multiple products in a single row are comma-separated and processed individually.
---
## ✔ Supported Search Engines
The script identifies traffic from:
- google.*
- yahoo.*
- bing.*
- msn.*
Keyword extraction logic:
- `q=` parameter (Google, Bing, MSN)
- `p=` parameter (Yahoo)
---
# ▶ How to Run Locally
## 1️⃣ Prerequisites
- Python 3.7+
(Optional virtual environment setup)
python3 -m venv venv
source venv/bin/activate

## 2️⃣ Execute the Script
python search_keyword_performance.py sample_data.tsv
## 3️⃣ Output
The script generates a file in the current directory:
YYYY-mm-dd_SearchKeywordPerformance.tab
Output columns:
Search Engine Domain Search Keyword Revenue
✔ Tab-delimited  
✔ Includes header  
✔ Sorted by Revenue (Descending)
---
# ☁ AWS Deployment
The application is deployed on AWS EC2:
http://52.66.30.106:8501/

### EC2 Configuration
- Region: ap-south-1
- Instance Type: t3.micro
- AMI: Amazon Linux 2023
- Security Group: Ports 22 and 8501 open
---
# 🏗 Infrastructure as Code (Terraform)
Infrastructure is provisioned using Terraform.
Resources created:
- EC2 Instance (t3.micro)
- Security Group (SSH + Port 8501)
- Public IP association

## ▶ To Provision Infrastructure
Navigate to the terraform folder:
cd de_project/terraform
terraform init
terraform plan
terraform apply

After apply:
terraform output
Terraform will output the public IP and DNS of the instance.
---
# 📈 Scalability Considerations
## Current Design
- Line-by-line file processing
- Avoids loading entire dataset into memory
- Suitable for moderately large files


## For Very Large Files (10GB+)
Recommended production architecture:
- Store raw data in Amazon S3
- Use AWS Glue (Apache Spark) or EMR for distributed processing
- Partition data in S3
- Perform parallel aggregation
- Store processed results in:
  - S3
  - Redshift
  - Athena
Optional workflow orchestration:
- AWS Step Functions
- EventBridge scheduling


---


# 🛡 Error Handling & Assumptions


- Skips malformed rows safely
- Skips records without purchase events
- Ignores invalid or missing revenue values
Assumes:
- Required columns exist (`event_list`, `product_list`, `referrer`)
- Revenue field is numeric
- Referrer URL contains valid query parameters
---

# 🧪 Testing with Sample Data
Run:
python search_keyword_performance.py sample_data.tsv
Compare generated output with:
output_example.tsv
---
# 🔮 Future Enhancements
- Add unit tests (pytest)
- Add structured logging (CloudWatch integration)
- Dockerize the application
- Add CI/CD pipeline (GitHub Actions)
- Implement S3-triggered Lambda processing
- Store output in a data warehouse for reporting
---
# 📌 Summary
This project demonstrates:
- Python-based data processing
- Revenue aggregation logic
- Search keyword analytics
- AWS EC2 deployment
- Infrastructure as Code (Terraform)
- Scalability planning
- Clean and maintainable code structure


The solution successfully answers the business question by identifying which search engines and keywords generate the highest revenue.

