# Scenario

You are a security professional at a large organization. Part of your job is to investigate security issues to help keep the system secure. You recently discovered some potential security issues that involve login attempts and employee machines.

Your task is to examine the organization’s data in their **employees** and **log\_in\_attempts** tables. You’ll need to use SQL filters to retrieve records from different datasets and investigate the potential security issues.

# Apply filters to SQL queries

## Project description

This project demonstrates how SQL filters are used to perform queries on a database.

## Retrieve after hours failed login attempts

**Filter Failed Login Attempts After Business Hours:** Executing `SELECT * FROM log_in_attempts WHERE login_time > '18:00' AND success = 0;` retrieves all record entries where an authentication attempt occurred after 18:00 (6:00 PM) and resulted in a failure (`success = 0` or false). Combining the range filter `login_time > '18:00'` with the boolean flag `success = 0` using the `AND` operator isolates after-hours security events, aiding in the identification of potential unauthorized access attempts or off-hours brute-force activity.   

## Retrieve login attempts on specific dates

Query Execution: To analyze login activity across multiple target dates, the following query was executed to filter for all login attempts that occurred on either May 8, 2022, or May 9, 2022:   
`SELECT *`  
`FROM log_in_attempts`  
`WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';`  
Query Breakdown & Description: Executing `SELECT * FROM log_in_attempts WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';` retrieves all record entries where an authentication attempt took place on either target date. Using the `OR` operator allows the query to evaluate multiple standalone equality conditions on the same column, returning all records matching either date to support multi-day security auditing and trend analysis.   

## Retrieve login attempts outside of Mexico

`SELECT *`  
`FROM log_in_attempts`  
`WHERE NOT country LIKE 'Mex%';`

**Description:**

Queries the `log_in_attempts` table using the `NOT` and `LIKE` operators alongside the `%` wildcard to filter out login records originating from Mexico. This pattern match accounts for standard country codes and full names (e.g., "MEX", "Mexico"). In security operations and threat hunting, this query isolates external or foreign login activity outside a baseline geographic region to identify anomalous access attempts.


## Retrieve employees in Marketing

`SELECT *`  
`FROM employees`  
`WHERE department = 'Marketing' AND office LIKE 'East%';`

**Description:**

Queries the `employees` table using the `WHERE` clause combined with the `AND` operator to enforce multiple filter criteria simultaneously. The query targets records strictly belonging to the `Marketing` department while applying the `LIKE` operator with a `%` wildcard to match any office location beginning with `East` (e.g., `East-170`, `East-195`). In cybersecurity operations and asset management, combining conditional logic with pattern matching isolates specific personnel, assets, or assigned hardware (`device_id`) within target departments or physical facility zones during access audits or incident investigations.


## Retrieve employees in Finance or Sales

`SELECT *`  
`FROM employees`  
`WHERE department = 'Sales' OR department = 'Finance';`

**Description:**

Queries the `employees` table using the `WHERE` clause combined with the `OR` logical operator to evaluate multiple non-mutually exclusive conditions. The query isolates all personnel belonging to either the `Sales` or `Finance` departments. In cybersecurity asset management and access auditing, using logical boolean operators allows security analysts to aggregate user accounts across specific target units to review department-wide access controls, audit assigned endpoint hardware (`device_id`), or identify unassigned device records (`NULL` values) across sensitive business divisions.


## Retrieve all employees not in IT

`SELECT *`  
`FROM employees`  
`WHERE NOT department = 'Information Technology';`

**Description:**

Queries the `employees` table using the `WHERE` clause alongside the `NOT` logical operator to exclude a specific condition—filtering out all user records where the `department` matches `'Information Technology'`. In security governance and identity asset audits, isolating non-IT personnel is key to evaluating baseline privilege levels, identifying unassigned corporate hardware (indicated by `NULL` values in the `device_id` column), and targeting security awareness outreach across operational business units.


## Summary

This project demonstrated the application of SQL filtering techniques to investigate potential security threats, perform access control audits, and support IT asset management within an organization. By utilizing conditional operators (`AND`, `OR`, `NOT`) and pattern matching (`LIKE` with `%` wildcards), structured queries were constructed to extract actionable intelligence from the `log_in_attempts` and `employees` database tables.

Key technical achievements and operational outcomes include:

* **Authentication & Anomaly Detection:** Identified potential brute-force and unauthorized access risks by filtering for failed login attempts outside standard business hours (`login_time > '18:00' AND success = 0`) and inspecting multi-day incident windows using conditional date logic (`OR`).  
* **Geographic Threat Isolation:** Screened out baseline domestic activity using pattern exclusion (`NOT country LIKE 'Mex%'`) to focus threat-hunting efforts on non-standard and foreign access attempts.  
* **Asset & Privilege Auditing:** Analyzed organizational privilege structures by isolating high-risk business divisions (`Sales` and `Finance`), mapping departmental physical locations (`East%`), and auditing non-technical personnel (`NOT department = 'Information Technology'`) to detect unassigned hardware assets (`NULL` device IDs) and enforce principle-of-least-privilege standards.

Overall, these database filtering methods establish a foundational capability for security analysts to query operational logs efficiently, identify policy violations, and strengthen identity and asset governance across an enterprise environment.

[View the Full Report Here:](Apply_filters_to_SQL_queries.pdf)
