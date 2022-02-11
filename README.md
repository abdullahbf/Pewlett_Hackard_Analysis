# Pewlett_Hackard_Analysis

## Purpose/Objective:

The purpose of this repository was to analyze the employee data at "Pewlett Hackard" and gain insights about the employees retiring using PostgresSQL. "queries.sql" contains the initial queries used to create the tables and establish primary and foreign keys using "EmployeeDB.png" as reference. "EmployeeDB.png" is an Entity Relationship Diagram created using "QuickDBD". "Employee_Database_Challenge.sql" contains the queries that were used to obtain the following data:

1) Number of retirement age employees by most recent job title (excluding the people who have already left the company).

2) Create a table of employees eligible for mentorship.

For the purpose of this readme, the focus will be on "Employee_Database_Challenge.sql".

## Results:

### Retirement age employees with job titles 

<img width="491" alt="Screen Shot 2022-02-11 at 11 32 10 AM" src="https://user-images.githubusercontent.com/92544151/153630470-5bb3a34a-b44c-44c5-b1c4-20ecebd519a2.png">

<img width="99" alt="Screen Shot 2022-02-11 at 11 43 43 AM" src="https://user-images.githubusercontent.com/92544151/153632325-0719199a-e1a2-4743-8a76-4b7555ae8fbd.png">

The employees and titles tables were joined using an inner join and the results were filtered to only get the retiring employees. The resulting table, retirement_titles.csv, had 133,776 entries. Looking at the csv file, it was clear that there were a lot of duplicate employee entries. 

<img width="327" alt="Screen Shot 2022-02-11 at 11 35 04 AM" src="https://user-images.githubusercontent.com/92544151/153630982-b3275c56-2b07-4d38-b757-f02a74542435.png">

<img width="99" alt="Screen Shot 2022-02-11 at 11 45 13 AM" src="https://user-images.githubusercontent.com/92544151/153632613-7a66792e-ea2d-4393-befc-7cfec6cfc4cd.png">

Next, to eliminate the duplicate entries, we used 'DISTINCT ON' command as part of the query to create unique_titles table. The table was also filtered on to_date to exclude people who had already left the company. This left us with 72458 people. 

<img width="475" alt="Screen Shot 2022-02-11 at 11 37 37 AM" src="https://user-images.githubusercontent.com/92544151/153631355-2d4e486e-a06b-4e2c-93c7-69f529e6973b.png">

Then, the unique_titles table was used to give us the number of retiring employees grouped by their most recent job title. We got the following results: 

<img width="171" alt="Screen Shot 2022-02-11 at 11 39 17 AM" src="https://user-images.githubusercontent.com/92544151/153631615-0ca47730-723d-4578-bec7-efe90ea85cd4.png">

As the data shows, most of the people retiring are currently working as senior engineers, followed by senior staff. Only 2 managers are up for retirement. 

### Employees eligible for mentorship program 

Moving on, I determined the amount of retiring employeees eligible to participate in a mentorship program.

<img width="667" alt="Screen Shot 2022-02-11 at 11 48 09 AM" src="https://user-images.githubusercontent.com/92544151/153633124-7305240f-63fe-4453-9578-ad7c7f3dd39b.png">

Columns from three tables, employees, dept_emp and titles, were joined (this time using left join). The results were then filtered by to_date (employees currently working) and birth_date (ones up for retirement soon). 

<img width="99" alt="Screen Shot 2022-02-11 at 11 53 50 AM" src="https://user-images.githubusercontent.com/92544151/153634067-13ccf471-cc4b-47fe-9942-b29da26be530.png">

Only 1549 employees were eligible for the program. 

## Summary

### Number of people retiring

<img width="188" alt="Screen Shot 2022-02-11 at 12 29 32 PM" src="https://user-images.githubusercontent.com/92544151/153639822-371ca54f-1369-474f-bd80-398af22ccd8b.png">
<img width="99" alt="Screen Shot 2022-02-11 at 12 29 27 PM" src="https://user-images.githubusercontent.com/92544151/153639837-b5b6dd79-d41e-43f6-8411-23f38f9b1bc2.png">

The query and the result shows that the company will have to replace 72,458 employees current employees in the near future. This is assuming that each employee retires as soon as they are eligible. 

### Mentorship program 

<img width="311" alt="Screen Shot 2022-02-11 at 12 00 49 PM" src="https://user-images.githubusercontent.com/92544151/153636128-359c2eb8-7e88-465b-8a3e-b0774b6cbdcf.png">
<img width="235" alt="Screen Shot 2022-02-11 at 12 01 06 PM" src="https://user-images.githubusercontent.com/92544151/153636138-fd8a55f6-16b7-4ad7-9654-f301e4e847ee.png">

As the query and the results show, most of the employees eligible for the program are senior staff. Now, assuming that all the people in retirement_titles.csv retire, we can get the following ratios of "new hires : possible mentors"   

Senior Engineers   - 25916 : 169  - 153.3 new hires per mentor

Engineers          - 9285  : 501  - 18.5 new hires per mentor

Senior Staff       - 24926 : 569  - 43.8 new hires per mentor

Staff              - 7636  : 155  - 49.3 new hires per mentor 

Assistant Engineer - 1090  : 78   - 14 new hires per mentor

Technique Leader   - 3603  : 77   - 46.8 new hires per mentor 

Manager            -    2  : 0    - No managers eligible for mentoring

The ratios show that there are clearly not enough senior engineers eligible for mentoring. The ratios are also high for senior staff, staff and technique leaders. 





