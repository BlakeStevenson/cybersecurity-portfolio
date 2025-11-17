Apply filters to SQL queries
============================

### Project description  
In this project, I investigated potential security issues in an organization’s systems using SQL queries. I worked with two tables, log_in_attempts and employees, to filter and retrieve specific records related to failed logins, suspicious dates, locations, and employee departments. By applying filters with AND, OR, NOT, LIKE, and by filtering on dates and times, I was able to narrow large datasets down to only the rows relevant to security investigations.

---

### Retrieve after hours failed login attempts  
To investigate after-hours activity, I needed to find all failed login attempts that occurred after 18:00 (6:00 PM). The log_in_attempts table stores the time in the login_time column and whether the attempt succeeded in the success column. In this query, I filtered for rows where login_time is later than 18:00:00 and success is FALSE (or 0), which indicates failed login attempts after normal business hours.

Query:
```sql
SELECT *
FROM log_in_attempts
WHERE login_time > 18:00:00
  AND success = FALSE;
```
---

### Retrieve login attempts on specific dates  
To investigate a suspicious event on 2022-05-09, I needed to retrieve all login attempts on that date and the day before. The login_date column stores the date of each login attempt. I used an OR filter on login_date so that the query returns any login attempts that happened on either 2022-05-08 or 2022-05-09. This shows all relevant activity around the time of the incident.

Query:
```sql
SELECT *
FROM log_in_attempts
WHERE login_date = 2022-05-08
  OR login_date = 2022-05-09;
```

---

### Retrieve login attempts outside of Mexico  
The security team determined that suspicious activity did not originate from Mexico, so I needed to focus on login attempts from all other countries. The country column can contain both MEX and MEXICO to represent Mexico. To handle these variations, I used the LIKE keyword with a wildcard and combined it with NOT to exclude any country values that start with MEX. This keeps only login attempts that occurred outside of Mexico.

Query:
```sql
SELECT *
FROM log_in_attempts
WHERE country NOT LIKE MEX%;
```

---

### Retrieve employees in Marketing  
For security updates on Marketing department machines in the East building, I needed to filter the employees table. The department column contains values that include the word Marketing, and the office column includes office locations such as East-170, East-320, etc. I used LIKE %Marketing% to match any department value containing the word “Marketing”, and LIKE East-% to match any office in the East building. The AND operator ensures both conditions are true.

Query:
```sql
SELECT *
FROM employees
WHERE department LIKE %Marketing%
  AND office LIKE East-%;
```

---

### Retrieve employees in Finance or Sales  
Next, I needed to identify employees whose devices require a different security update for the Finance and Sales departments. The department column contains values that include Finance and Sales. I used two LIKE conditions combined with OR so that the query returns rows where the department contains either “Finance” or “Sales”.

Query:
```sql
SELECT *
FROM employees
WHERE department LIKE %Finance%
    OR department LIKE %Sales%;
```
---

### Retrieve all employees not in IT  
Finally, the Information Technology department had already received a security update, so I needed to find all employees in other departments. The department column contains values that include Information Technology. I used NOT with LIKE to exclude any rows where the department contains that phrase. This returns all employees who are not in IT and still need the update.

Query:
```sql
SELECT *
FROM employees
WHERE department NOT LIKE %Information Technology%;
```

---

### Summary  
In this project, I used SQL to filter and investigate security-related data in the log_in_attempts and employees tables. I retrieved failed login attempts after business hours, login attempts on specific dates, and login attempts outside of a particular country by filtering on dates, times, and country codes with AND, OR, and NOT. I also identified employees in certain departments and locations using pattern matching with LIKE to support targeted security updates for their machines. Together, these queries demonstrate how SQL filtering can be applied to real-world security investigations and incident response.
