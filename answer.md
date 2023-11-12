'''
Insert new employee record, emp_num = 999, emp_lname = Doe, emp_fname = John, emp_initial = D, emp_hiredate = current date
'''
emp_num = 999
emp_lname = 'Doe'
emp_fname = 'John'
emp_initial = 'D'
emp_hiredate = datetime.now().strftime('%Y-%m-%d')  # current date

cursor.execute("""
    INSERT INTO employee (emp_num, emp_lname, emp_fname, emp_initial, emp_hiredate)
    VALUES (%s, %s, %s, %s, %s)
""", (emp_num, emp_lname, emp_fname, emp_initial, emp_hiredate))


'''
Update employee record, job_code = 510 where emp_num = 999
'''
emp_num = 999
job_code = 510

cursor.execute("""
    UPDATE employee 
    SET job_code = %s
    WHERE emp_num = %s
""", (job_code, emp_num))

'''
Delete employee record, emp_num = 999
'''
emp_num = 999

cursor.execute("""
    DELETE FROM employee 
    WHERE emp_num = %s
""", (emp_num,))


'''
Query assigment where assign_date is larger than 2010-01-01
'''
date = '2010-01-01'

cursor.execute("""
    SELECT * FROM assignment 
    WHERE assign_date > %s
""", (date,))

assignments = cursor.fetchall()

for assignment in assignments:
    print(assignment)