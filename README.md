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

#### Ques2:Given a table with salaries of employees for different month, find the max amount from the rows with month name

```sql

CREATE TABLE salempdiffmon (
  Name VARCHAR(20),
  Jan INT,
  Feb INT,
  Mar INT
);

INSERT INTO salempdiffmon (Name, Jan, Feb, Mar)
VALUES
  ('X', 5200, 9093, 3832),
  ('Y', 9023, 8942, 4000),
  ('Z', 9834, 8197, 9903),
  ('W', 3244, 4321, 2093);



WITH data AS (
  SELECT Name, 'Jan' AS Month, Jan AS Salary FROM salempdiffmon
  UNION ALL
  SELECT Name, 'Feb' AS Month, Feb AS Salary FROM salempdiffmon
  UNION ALL
  SELECT Name, 'Mar' AS Month, Mar AS Salary FROM salempdiffmon
)

select d1.Name,d1.Salary,d1.Month from data as d1 where d1.Salary = (Select max(salary) from data as d2 where d1.name = d2.name group by d2.Name) order by d1.Name;

```

#### Ques3:Given the marks obtained by candidates in a test, rank them in proper order

```sql

Create table candidate( Candidate_ID int ,Marks Int);

INSERT INTO candidate (Candidate_ID, Marks)
VALUES
  (1, 98),
  (2, 78),
  (3, 87),
  (4, 98),
  (5, 78);
  
  select marks,dense_rank() over (order by marks desc) as `rank`,group_concat(candidate_id) as candidate_Id from candidate group by marks;

```

#### Ques4:If same value is repeated for different id, then keep the value that has smallest id and delete all the other rows having same value:

```sql

create candidemail(candidate_ID int,Email varchar(20));

INSERT INTO candidemail (Candidate_ID, Email)
VALUES
  (45, 'abc@gmail.com'),
  (23, 'def@yahoo.com'),
  (34, 'abc@gmail.com'),
  (21, 'bcf@gmail.com'),
  (94, 'def@yahoo.com');
  
  
WITH duplicateemails AS ( 
select * from candidemail
)
delete from candidemail where candidate_id not in (select min(candidate_id) from duplicateemails group by email);

select * from candidemail;


```
