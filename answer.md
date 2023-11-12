1. add new employee record to employee table with id = 168, firstname = 'John', lastname = 'Doe', initials = 'JD', job = 'Programmer', hire_date = today's date.

today = datetime.now()

sql = "INSERT INTO EMPLOYEE (emp_num, emp_lname, emp_fname, emp_initial, emp_hiredate, job_code) VALUES(%s, %s, %s, %s, %s, %s)"
value= (168, "Doe", "John", "JD", today, 500)

cursor.execute(sql, value)

DB.commit()

print(cursor.rowcount, "Record Inserted.") 


2. query the new created employee (id=168) from employee table, with information of employee id, firstname, lastname, initials, job description (join with job), charge per hour (join with job) and hire_date.

sql = """
    SELECT 
        e.EMP_NUM, 
        e.EMP_FNAME, 
        e.EMP_LNAME, 
        e.EMP_INITIAL, 
        j.JOB_DESCRIPTION, 
        j.JOB_CHG_HOUR, 
        e.EMP_HIREDATE
    FROM 
        EMPLOYEE AS e
    JOIN 
        JOB AS j ON e.JOB_CODE = j.JOB_CODE 
    WHERE 
        e.EMP_NUM = 168;
"""
cursor.execute(sql)

result = cursor.fetchone()

print("Employee ID:", result[0],
      "\nFirst Name:", result[1], 
      "\nLast Name:", result[2], 
      "\nInitial:", result[3],
      "\nJob Description:", result[4],
      "\nCharge per Hour:", result[5],
      "\nHire Date:", result[6])


3. update the new created employee (id=168) job, from 'Programmer' to 'Database Designer'.

update_sql = """
    UPDATE EMPLOYEE
    SET job_code = (SELECT job_code FROM JOB WHERE job_description = 'Database Designer')
    WHERE emp_num = 168;
"""

cursor.execute(update_sql)

DB.commit()

print(cursor.rowcount, "Successfully Updated.") 


4. query all project that has "Programmer" assigned to, with information of project id, project name and program manager (join with employee).

sql = """
    SELECT
        p.PROJ_NUM,
        p.PROJ_NAME,
        e.EMP_FNAME,
        e.EMP_LNAME
    FROM
        PROJECT AS p
    JOIN
        ASSIGNMENT AS a ON p.PROJ_NUM = a.PROJ_NUM
    JOIN
        EMPLOYEE AS e ON a.EMP_NUM = e.EMP_NUM
    JOIN
        JOB AS j ON e.JOB_CODE = j.JOB_CODE
    WHERE
        j.JOB_DESCRIPTION = 'Programmer';
"""
cursor.execute(sql)

result = cursor.fetchall()

print(result)


5. delete the new created employee (id=168) from employee table.

delete_sql = """
    DELETE FROM EMPLOYEE 
    WHERE EMP_NUM = 168;
"""
cursor.execute(delete_sql)

DB.commit()

print(cursor.rowcount, "Successfully Deleted.")
