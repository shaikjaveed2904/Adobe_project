Search Keyword Performance Analyzer
Data Engineer Applicant Assessment – Adobe Analytics
📌 Problem Statement
This project analyzes Adobe Analytics hit-level data to determine:
How much revenue is generated from external search engines (Google, Yahoo, Bing, MSN), and which search keywords drive the highest revenue?
The input is a tab-delimited dataset where each row represents a visitor interaction (“hit”). The goal is to extract purchase-related revenue and attribute it to the originating search engine and keyword.
The final output:
Aggregates revenue by Search Engine Domain and Search Keyword
Includes only purchase events (event ID 1)
Is sorted by Revenue (descending)
Is generated in the format:
YYYY-mm-dd_SearchKeywordPerformance.tab
Approach
The application:
Reads the file line by line to ensure memory efficiency.
Filters rows where:
The referrer belongs to a supported search engine.
The event_list includes purchase event 1.
Parses the product_list column to extract revenue (4th field).
Extracts:
Search engine domain (e.g., google.com)
Search keyword (q= or p= parameter from the referrer URL)
Aggregates total revenue by search engine and keyword.
Outputs a tab-delimited file with a header, sorted by revenue (highest first).
📂 Project Structure
Adobe_project/
│
├── search_keyword_performance.py
├── sample_data.tsv
├── output_example.tsv
├── README.md

How to Run
Prerequisites
Python 3.7+
(Optional virtual environment)
python3 -m venv venv
source venv/bin/activate
Execute
python search_keyword_performance.py path/to/input_file.tsv
Example:
python search_keyword_performance.py sample_data.tsv
The script generates:
YYYY-mm-dd_SearchKeywordPerformance.tab
With columns:
Search Engine Domain
Search Keyword
Revenue
☁ AWS Deployment
The application is deployed on AWS (EC2 instance) and accessible at:
http://52.66.30.106:8501/
Scalability Considerations
The current implementation processes the file line by line, which avoids loading the entire dataset into memory.
For large-scale datasets (10GB+), improvements would include:
Using AWS Glue or EMR (Spark) for distributed processing
Storing data in Amazon S3 with partitioning
Writing results to Redshift or querying via Athena
Automating workflows using Step Functions
🛡 Assumptions & Error Handling
Only purchase events (event_list contains 1) generate revenue.
Revenue is extracted from the 4th field in product_list.
Malformed or incomplete rows are safely skipped.
Required columns exist in the dataset.
🔮 Future Improvements
Add unit tests (pytest)
Add structured logging
Dockerize the application
Implement CI/CD pipeline
Automate S3-triggered processing
📌 Summary
This solution demonstrates:
Efficient file processing in Python
Revenue aggregation logic
URL parsing and data transformation
AWS deployment
Scalability planning
The result provides clear visibility into which search engines and keywords generate the most revenue.


