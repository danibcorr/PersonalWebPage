# Ejercicios practicos SQL

# Ejercicios básicos
1. Get job details for BOTH 'Data Analyst' or 'Business Analyst' positions for 'Data Analyst', I want jobs only > $100k, and for 'Business Analyst', I only want jobs > $70k. Only include jobs located in EITHER 'Boston, MA' and 'Anywhere'.
    ```sql
    SELECT
        job_posting_fact.job_title_short,
        job_posting_fact.salary_year_avg,
        job_posting_fact.job_location

    FROM
        job_posting_fact

    WHERE
        job_location IN ('Boston, MA', 'Anywhere') AND
        (
            -- Utilizamos parentesis para encapsular condiciones una dentro de otra
            (job_title_short  = 'Data Analyst' AND salary_year_avg > 100000) OR
            (job_title_short = 'Business Analyst' AND salary_year_avg > 70000)
        )
    ```

2. Look for non-senior data analyst or business analyst roles. Get the job title, location, and average yearly salary.
    ```sql
    SELECT
        job_posting_fact.job_title,
        job_posting_fact.job_location,
        job_posting_fact.salary_year_avg
        
    FROM
        job_posting_fact

    WHERE
        job_title NOT LIKE '%Senior%' AND
        (job_title LIKE '%Data%' OR job_title LIKE '%Business%') AND
        job_title LIKE '%Analyst%'
    ```