Search Keyword Performance Analyzer
Data Engineer Applicant Assessment – Adobe Analytics
📌 Problem Statement
The objective of this exercise is to determine:
How much revenue is generated from external search engines (Google, Yahoo, MSN, Bing), and which search keywords are performing the best based on revenue?
The input is a tab-delimited Adobe Analytics hit-level dataset, where each row represents a single visitor interaction (“hit”) on the website.
Final Output Requirements
The final output must:
Aggregate revenue by:
Search Engine Domain
Search Keyword
Include only revenue from purchase events (event ID 1)
Be sorted by Revenue (Descending)
Be generated in the required naming format:
YYYY-mm-dd_SearchKeywordPerformance.tab
🏗 Solution Overview
This Python application performs the following steps:
Reads the input file line by line (memory-efficient approach).
Filters records where:
The referrer contains a supported search engine.
The event_list contains purchase event ID 1.
Parses the product_list column:
Extracts revenue from the 4th field of each product entry.
Revenue is counted only when a purchase event occurs.
Extracts:
Search engine domain (e.g., google.com)
Search keyword (q= or p= parameter from the referrer URL)
Aggregates total revenue by:
Search Engine Domain
Search Keyword
Sorts the results by revenue in descending order.
Writes the final tab-delimited output file with a header row.
📂 Project Structure
Adobe_project/
│
├── search_keyword_performance.py   # Main Python application
├── sample_data.tsv                 # Sample input dataset
├── output_example.tsv              # Example output file
├── README.md
🧠 Technical Implementation
✔ Application Requirements Met
Implemented in Python 3
Contains at least one class
Accepts a single command-line argument (input file path)
Generates required tab-delimited output file
Includes header row
Sorted by revenue (descending)
✔ Revenue Calculation Logic
Revenue is extracted from the product_list column.
Format example:
Category;ProductName;Quantity;Revenue;Events
Revenue is only counted if:
event_list contains event ID 1 (Purchase)
Multiple products in a single row are comma-separated and processed individually.
✔ Supported Search Engines
The script identifies traffic from:
google.*
yahoo.*
bing.*
msn.*
Keyword extraction logic:
q= parameter (Google, Bing, MSN)
p= parameter (Yahoo)
▶ How to Run
🔹 Prerequisites
Python 3.7 or later
(Optional virtual environment setup)
python3 -m venv venv
source venv/bin/activate
🔹 Execute the Script
python search_keyword_performance.py path/to/input_file.tsv
Example:
python search_keyword_performance.py sample_data.tsv
🔹 Output
The script generates a file in the current directory:
YYYY-mm-dd_SearchKeywordPerformance.tab
Output columns:
Search Engine Domain
Search Keyword
Revenue
✔ Tab-delimited
✔ Includes header
✔ Sorted by Revenue (Descending)
☁ AWS Deployment
The application has been deployed on AWS and is accessible at:
http://52.66.30.106:8501/
(Hosted on an AWS EC2 instance.)
🏗 Suggested Production Architecture
For large-scale production workloads:
Store raw data in Amazon S3
Trigger processing using AWS Lambda (for moderate file sizes)
For large files (10GB+):
Use AWS Glue (Apache Spark)
Or EMR for distributed processing
Store processed results in S3
Query results using Amazon Athena or Redshift
📈 Scalability Considerations
Current Design
Processes input file line by line
Avoids loading entire dataset into memory
Suitable for moderately large files
For Very Large Files (10GB+)
Improvements would include:
Distributed processing with Spark (AWS Glue / EMR)
Data partitioning in S3
Parallel aggregation
Writing output to a data warehouse
Automating workflows using Step Functions
This ensures horizontal scalability and fault tolerance.
🛡 Error Handling & Assumptions
Skips malformed rows safely
Skips records without purchase events
Ignores invalid or missing revenue values
Assumptions:
Required columns exist (event_list, product_list, referrer)
Revenue field is numeric
Referrer URL contains valid query parameters
🧪 Testing with Sample Data
Run:
python search_keyword_performance.py sample_data.tsv
Verify output:
cat $(date +%Y-%m-%d)_SearchKeywordPerformance.tab
Compare with output_example.tsv.
🔮 Future Enhancements
Add unit tests (pytest)
Add structured logging (CloudWatch integration)
Dockerize the application
Add CI/CD pipeline (GitHub Actions)
Implement S3-triggered Lambda processing
Store output in a data warehouse for reporting
📌 Summary
This project demonstrates:
Python-based data processing
File parsing and transformation
Revenue aggregation logic
AWS deployment
Scalability planning
Clean coding practices


