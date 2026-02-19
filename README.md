IntelliSQL: Intelligent SQL Querying with LLMs Using Gemini Pro
Team ID : LTVIP2026TMIDS64421
Team Size: 4
Team Leader: Kommu Priya
Team member: Gandikota Prasanna Jyothi
Team member: Chappidi Nandini
Team member: Bolligarla Durga Parvathi
Project Overview
IntelliSQL is an AI-powered web application that enables users to interact with an SQL database using natural language. Built with Streamlit and integrated with Google's Gemini Pro large language model, IntelliSQL translates plain English questions into SQL queries, executes them on a student database, and displays the results. This empowers users—regardless of their SQL expertise—to explore and analyze data efficiently.
Introduction
Intelligent SQL Querying with LLMs using Gemini Pro
Modern organizations generate vast amounts of structured data stored in relational databases such as PostgreSQL and BigQuery. However, extracting meaningful insights from this data traditionally requires strong SQL expertise, limiting accessibility to technical users. Intelligent SQL querying powered by Large Language Models (LLMs) addresses this challenge by enabling users to interact with databases using natural language.
With the emergence of advanced LLMs such as Gemini Pro, it is now possible to automatically translate natural-language questions into accurate, executable SQL queries. By integrating Gemini Pro through the Gemini API or prototyping within Google AI Studio, organizations can build systems that generate, validate, optimize, and explain SQL queries intelligently.
Features
Intelligent SQL Querying with LLMs using Gemini Pro
Using Gemini Pro for intelligent SQL querying enables a powerful natural-language interface over structured databases. Below are the core features that make this approach effective for modern data systems.
•	Natural Language to SQL: Converts English questions into accurate SQL queries using Gemini Pro.
•	Instant Data Retrieval: Executes generated queries and displays results in real time.
•	User-Friendly Interface: Streamlit-based UI with clear navigation and modern styling.
•	Sample Student Database: Pre-populated SQLite database for demonstration.
•	Secure API Key Management: Uses .env files to keep credentials safe.
•	Extensible Design: Easily adaptable for other databases or additional features.
Installation & Setup
1.	Clone the Repository: git clone https://github.com/your-username/IntelliSQL.git cd IntelliSQL
2.	Create and Activate a Virtual Environment: python -m venv myenv
Windows:
myenv\Scripts\activate
macOS/Linux:
source myenv/bin/activate
3.	Install Dependencies: pip install -r requirements.txt
4.	Set Up Environment Variables:
o	Copy .env.example to .env and add your Gemini API key: API_KEY=your_gemini_api_key_here
5.	Initialize the Database: python 1.sql.py
6.	Run the Application: streamlit run app.py
o	Open the provided local URL in your browser.
Usage Instructions
1.	Home Page:
o	View project introduction and key features.
2.	About Page:
o	Learn about the project’s purpose and technology stack.
3.	Intelligent Query Assistance:
o	Enter a question in plain English (e.g., "Show all students in BTech").
o	Click Get Answer to see the generated SQL query and the database results.
Screenshots
Below are sample screenshots from the application placed in screenshots/ folder and referenced as shown.
Screenshot Descriptions
1.	Interactive NL→SQL App Interface
A simple app screen where users enter natural-language questions and get results back — typical of end-to-end text-to-SQL tools built with Gemini Pro.
2.	AI-Powered SQL Generator UI
Example of an LLM-based SQL generator showing natural language on the left and the generated SQL output on the right. Similar interfaces are used in AI SQL tools like AI2SQL.
3.	Query Flow Diagram
A conceptual visualization of how an LLM processes natural language into an SQL query and executes it — useful for documentation or architecture overview.
4.	Text → SQL Visualization Illustration
A high-level image representing the flow from user language through a model like Gemini into SQL output, common in Cloud tutorials on text-to-SQL pipelines.

Home Page:  
About Page:  
Query Assistance Page:  
Query Result Example:  
Demo Video
Placed in demo video in the demo/ folder and linked as shown below:
Click here to watch the demonstration video
Credits
Google Cloud Credits Can Be Used
If you have Google Cloud credits (for example, from the $300 Free Trial or other promotional credits), you can apply them toward Gemini API usage.
These credits are part of your Cloud Billing account and are deducted as you consume API tokens. 
✔ Your project balance will reduce as you make calls to the Gemini API (input + output tokens).
✔ Credits can cover usage until they are fully consumed.
✔ Once credits run out, usage starts getting charged to your actual payment method
•	Project Developer: Atmikha Narayan
•	LLM Integration: Google Gemini Pro
•	UI Framework: Streamlit
•	Version Control: GitHub
Executive Summary
This document describes how to build an intelligent SQL querying system using Gemini Pro, enabling users to query databases using natural language. Intelligent SQL Querying with LLMs using Gemini Pro
Organizations today generate vast amounts of structured data stored in relational databases such as PostgreSQL, MySQL, and BigQuery. However, accessing and analyzing this data typically requires specialized SQL expertise, creating a bottleneck between business users and actionable insights. Intelligent SQL querying powered by Large Language Models (LLMs) addresses this challenge by enabling natural-language interaction with structured databases.
This solution leverages Gemini Pro through the Gemini API to convert user questions into accurate, secure, and optimized SQL queries. By integrating schema context, validation mechanisms, and automated correction loops, the system allows users to retrieve data conversationally while maintaining enterprise-grade security and performance standards.
The system:
•	Converts natural language → SQL
•	Validates generated SQL
•	Executes queries safely
•	Auto-corrects failures
•	Explains results in plain English
•	Enforces enterprise-grade guardrails
This approach reduces dependency on SQL expertise while maintaining security and reliability.
Technology Stack
Layer	Technology
LLM	Gemini Pro
API Access	Gemini API
Interface	Google AI Studio (for prototyping)
Backend	Python (FastAPI / Flask)
Database	PostgreSQL / BigQuery
SQL Parser	sqlparse
Optional	Vector DB (for schema retrieval)
System Architecture
 

Core Components
 Natural Language to SQL Generation
Gemini Pro is prompted with:
•	Database schema
•	Table relationships
•	Data types
•	Query constraints
•	Example queries
Example Prompt Template
You are a senior PostgreSQL SQL generator.
STRICT RULES:
- Only generate SELECT queries.
- Never modify data.
- Use only provided schema.
- Always include LIMIT 100 unless aggregation.

DATABASE SCHEMA:
{schema}

USER QUESTION:
{question}

Return only SQL.
Schema Injection (Critical for Accuracy)
Provide structured schema:
Table: customers
- id (INTEGER, PRIMARY KEY)
- name (TEXT)
- email (TEXT)
- country (TEXT)
Table: orders
- id (INTEGER, PRIMARY KEY)
- customer_id (INTEGER, FK -> customers.id)
- order_date (DATE)
- total_amount (NUMERIC)
Providing:
•	Data types
•	Primary keys
•	Foreign keys
Significantly reduces hallucination.
SQL Validation Layer (Security Control)
Before execution:
Validation Steps
•	Parse SQL
•	Reject multi-statements
•	Block dangerous keywords:
o	DROP
o	DELETE
o	UPDATE
o	INSERT
o	ALTER
•	Enforce row limits
•	Use read-only DB user
Example Enforcement Logic (Conceptual)
If query is not SELECT → reject
If LIMIT missing → append LIMIT 100
If multiple statements → reject
Self-Healing SQL Loop
If query execution fails:
1.	Capture database error
2.	Send error + SQL back to Gemini
3.	Ask model to fix the query
4.	Retry (max 2–3 attempts)
This significantly improves reliability in production.
Retrieval-Augmented SQL (Large Schema Optimization)
For large databases (100+ tables):
Instead of passing full schema:
1.	Embed table definitions
2.	Store in vector database
3.	Retrieve relevant tables based on question
4.	Inject only relevant schema into prompt
Benefits:
•	Reduced token usage
•	Faster inference
•	Higher SQL accuracy
Enterprise Security Best Practices
•	Enforce read-only database roles
•	Apply query timeouts
•	Log all generated SQL
•	Track user → query mapping
•	Add row count limits
•	Monitor execution cost (BigQuery)
Never execute raw LLM output without validation
Advanced Capabilities
 SQL Explanation
Gemini can explain generated SQL in simple terms:
“Explain this query to a business user.”
Query Optimization
Provide slow query + execution time:
“Rewrite for better performance.”
Gemini may:
•	Replace subqueries with CTEs
•	Suggest indexing strategies
•	Simplify joins
 Insight Generation
After execution:
Pass results back to Gemini:
“Summarize key trends in this dataset.”
Enables AI-powered data storytelling.
8. BigQuery Considerations
When using BigQuery:
•	Require fully-qualified table names
•	Use backticks
•	Enforce cost limits
•	Monitor bytes billed
Add these rules to prompt explicitly.
9. Observability & Monitoring
Log:
•	User question
•	Generated SQL
•	Execution time
•	Rows returned
•	Errors
•	Correction attempts
Use logs to:
•	Improve prompts
•	Detect misuse
•	Optimize performance

 Common Failure Modes
Even when using advanced LLMs like Gemini Pro, certain failure modes can arise when building intelligent SQL querying systems. Understanding these helps in designing robust, production-ready pipelines.
Issue	Solution
Hallucinated columns	Provide stronger schema
Incorrect joins	Add FK relationships
Missing GROUP BY	Add few-shot examples
Slow queries	Add optimization step
Security risk	Enforce validation layer
 Recommended Production Stack
Intelligent SQL Querying with LLMs using Gemini Pro
For deploying a secure, scalable, and reliable intelligent SQL querying system using Gemini Pro, the following production stack is recommended. This setup ensures optimal performance, observability, and enterprise-grade security.
•	Frontend: Chat interface
•	Backend: FastAPI
•	LLM: Gemini Pro
•	Database: PostgreSQL / BigQuery
•	Validation: sqlparse + read-only role
•	Optional: Vector DB for schema retrieval
•	Monitoring: Logging + tracing

Conclusion
Using Gemini Pro for intelligent SQL querying enables:
•	Natural-language data access
•	Reduced reliance on SQL expertise
•	Faster analytics workflows
•	AI-powered insights
However, production deployment requires:
•	Strong schema context
•	Guardrails
•	Validation layer
•	Self-healing correction loop
•	Observability
When implemented correctly, this architecture can power internal analytics tools, BI assistants, customer support dashboards, and enterprise data copilots

