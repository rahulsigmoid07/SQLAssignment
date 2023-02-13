#### Ques1: Given a table of employees, find the number of male and female employees in each department

```sql

CREATE TABLE employee (
  EmpID INT NOT NULL AUTO_INCREMENT,
  Name VARCHAR(20),
  Gender VARCHAR(10),
  Department VARCHAR(20),
  PRIMARY KEY (EMPID)
);

INSERT INTO employee (Name, Gender, Department)
VALUES
  ('X', 'Female', 'Finance'),
  ('Y', 'Male', 'IT'),
  ('Z', 'Male', 'HR'),
  ('W', 'Female', 'IT');
  
 SELECT Department,
        SUM(Gender = 'Female') AS "Num of Female",
        SUM(Gender = 'Male') AS "Num of Male"
 FROM employee
 GROUP BY Department;
 

```

