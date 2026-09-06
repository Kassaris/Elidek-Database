# ELIDEK Research Funding Database

Full-stack relational database application for managing **research projects, researchers, organizations, funding programs, evaluations and deliverables**.

Developed as a semester project for the **Databases** course at **NTUA ECE**, combining relational database design, advanced SQL querying and a Flask-based web application.

## Overview

The project models a research funding management system inspired by **ELIDEK**, providing structured storage and querying of research-related information.

The system supports entities such as:

* Research projects
* Researchers
* Organizations
* Research fields
* Funding programs
* Project evaluations
* Deliverables
* Administrative personnel

A **MySQL relational database** forms the core of the application, while a **Python Flask** web application provides an interface for interacting with the stored data.

## Tech Stack

* **Python**
* **Flask**
* **MySQL**
* **Flask-MySQLdb**
* **Flask-WTF**
* **SQL**
* **HTML / CSS**

## 📄 Technical Report

The complete database design, implementation decisions and project analysis are documented in the accompanying technical report.

>  **[Read the full Technical Report (PDF)](03119144_03119188.pdf)**

The report complements the source code and SQL scripts with detailed documentation of the database design and implementation.

## Architecture

```text
           Web Browser
                │
                ▼
        Flask Application
       ┌─────────────────┐
       │ Routes / Forms  │
       │ Controllers     │
       └────────┬────────┘
                │
                ▼
          Flask-MySQLdb
                │
                ▼
        ┌───────────────┐
        │     MySQL     │
        │   Database    │
        └───────────────┘
```

The Flask backend executes SQL queries directly against MySQL using database cursors and exposes the results through server-rendered web pages.

## Database Design

The relational schema models the relationships between research projects, researchers, organizations and funding entities.

Core entities include:

```text
Program
Research_Field
Admins
Organization
Researcher
Project
Evaluation
Deliverables
```

Relationship tables include:

```text
Project_Field
Works_in
Evaluate
Phone_Numbers
```

The schema makes use of:

* Primary keys
* Composite primary keys
* Foreign keys
* Referential integrity constraints
* Indexes
* Generated attributes
* One-to-many relationships
* Many-to-many relationships

For example, researchers are associated with organizations, projects reference their funding program and evaluation, and many-to-many relationships connect projects with research fields and participating researchers.

## SQL Queries

The project includes a collection of analytical and operational SQL queries in:

```text
queries.sql
```

The queries demonstrate:

* `INNER JOIN`
* `LEFT JOIN`
* Nested queries
* Aggregations
* `GROUP BY`
* `HAVING`
* SQL Views
* Date calculations
* Filtering
* Sorting
* Top-N queries

### Example Analytics

Implemented queries include analyses such as:

* Filtering projects by duration, date and administrator
* Retrieving researchers participating in projects
* Combining project and evaluation information
* Identifying organizations with consistent project activity
* Finding frequently occurring pairs of research fields
* Ranking active researchers under a specified age
* Aggregating project funding
* Identifying researchers working on projects without deliverables

This demonstrates both **relational database design** and practical SQL analytics over interconnected entities.

## Web Application

A Flask application provides a browser-based interface on top of the database.

The application is structured around:

```text
dbdemo/
├── __init__.py     # Flask & database configuration
├── routes.py       # Application routes and database operations
├── forms.py        # Flask-WTF forms
├── templates/      # HTML templates
└── static/
    └── css/        # Application styling
```

### Backend

`routes.py` contains the application endpoints and controllers responsible for:

```text
HTTP Request
     │
     ▼
Flask Route
     │
     ▼
SQL Query
     │
     ▼
MySQL
     │
     ▼
Query Result
     │
     ▼
HTML Template
```

Database communication is performed through **Flask-MySQLdb** using SQL queries and cursor operations.

## Project Structure

```text
Elidek-Database/
│
├── dbdemo/
│   ├── static/
│   │   └── css/
│   ├── templates/
│   ├── __init__.py
│   ├── forms.py
│   └── routes.py
│
├── ddl.sql                    # Database schema
├── dml.sql                    # Initial dataset
├── queries.sql                # SQL queries & analytics
├── requirements.txt           # Python dependencies
├── run.py                     # Application entry point
├── 03119144_03119188.pdf      # Technical report
└── README.md
```

## Requirements

### Software

* Python 3
* MySQL
* `pip`
* Python `venv` (recommended)

Python dependencies are provided in:

```text
requirements.txt
```

The application primarily uses:

* Flask
* Flask-MySQLdb
* Flask-WTF

## Installation

Clone the repository:

```bash
git clone https://github.com/Kassaris/Elidek-Database.git
cd Elidek-Database
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

or Linux/macOS:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Database Setup

Start your local MySQL server.

Create and initialize the database using the provided SQL scripts.

First execute:

```text
ddl.sql
```

to create the relational schema.

Then execute:

```text
dml.sql
```

to populate the database with the initial dataset.

The resulting database is named:

```text
ELIDEK
```

Additional queries used by the application and project requirements are available in:

```text
queries.sql
```

## Configuration

Database credentials and Flask configuration can be stored in:

```text
dbdemo/config.json
```

Example:

```json
{
    "MYSQL_USER": "root",
    "MYSQL_PASSWORD": "",
    "MYSQL_DB": "elidek",
    "MYSQL_HOST": "localhost",
    "SECRET_KEY": "key",
    "WTF_CSRF_SECRET_KEY": "key"
}
```

Load the configuration in `dbdemo/__init__.py`:

```python
import json

# ...

app.config.from_file("config.json", load=json.load)
```

> **Security Note:** Database credentials and secret keys should not be committed to version control. `config.json` should normally be included in `.gitignore`, with production secrets provided through environment variables or another secure configuration mechanism.

## Running the Application

After initializing MySQL and installing the dependencies, run:

```bash
python run.py
```

Alternatively, configure Flask:

```bash
export FLASK_APP=run.py
flask run
```

On Windows:

```bash
set FLASK_APP=run.py
flask run
```

The application will then start using Flask's built-in development server.

## Engineering Focus

This project provided hands-on experience with:

* Relational database design
* Entity relationships
* Database normalization
* MySQL
* SQL
* Primary & foreign keys
* Referential integrity
* Composite keys
* Database indexing
* Complex joins
* Nested queries
* SQL views
* Aggregations
* Flask backend development
* Database-backed web applications
* Form handling and validation
* Database configuration and credential management

The project combines **database modeling and SQL implementation with an application layer**, demonstrating how a relational database can serve as the persistence and query engine behind a web application.

## Academic Context

Developed as a semester project for the **Databases** course at the **National Technical University of Athens — School of Electrical and Computer Engineering**.

The project covers the complete workflow from **relational schema design and SQL implementation to application-level database integration**.

## Disclaimer

This repository is an academic project intended for educational purposes.

The application uses Flask's development server and local database configuration. Production deployment would require appropriate secret management, server configuration and additional security hardening.

---

### [Read the Technical Report](03119144_03119188.pdf)

**Python · Flask · MySQL · SQL · Relational Databases · Database Design**

*Database Systems Semester Project — NTUA ECE*
