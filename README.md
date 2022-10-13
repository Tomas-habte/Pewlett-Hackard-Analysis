# Pewlett-Hackard-Analysis-
## Overview
The purpose of this analysis is to use SQL to determine the number of retiring employees per title and identify employees who are eligible to participate in a mentorship program. This will allow the manager to prepare for the “silver tsunami” as many current employees reach retirement age.

## Results
The analysis has revealed the following:
- There are 72,458 employees that are nearing retirement. 
- The vast majority (70%) of employees nearing retirement have senior titles.  
- Employees with "manager" as their title are the smallest minority with only 2. 

![retiring_titles](https://user-images.githubusercontent.com/111667387/195479315-9e77d39b-520d-4b0b-a6eb-001023dfddc6.jpg)
- According to the mentorship_eligbility table, there are 1,549 employees who are eligible for the Mentorship Program.

## Summary
There are 72,458 employees that are nearing retirement and only 1,549 employees are eligible for the Mentorship Program. Therefore, there are not enough qualified, retirement-ready employees to mentor the next generation of employees as they would each need to have many mentees which is not feasible. 

We can use the two additional queries below to provide more insight into the upcoming "silver tsunami":
- Employees eligible for the Mentorship program by department. 
```
SELECT DISTINCT ON (me.emp_no)	
					me.emp_no,
					me.first_name,
					me.last_name,
					me.birth_date,
					de.from_date,
					de.to_date,
					d.dept_no
INTO retiring_department
FROM mentorship_eligibility AS me
INNER JOIN dept_emp as de
ON (me.emp_no = de.emp_no)
INNER JOIN departments as d
ON (de.dept_no = d.dept_no)
WHERE (de.to_date = '9999-01-01')
AND (birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY emp_no;
