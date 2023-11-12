


1

sql="INSERT INTO employee (emp_num, emp_lname, emp_fname, emp_initial, emp_hiredate, job_code) VALUES(%s, %s, %s, %s, %s, %s)"
current_date = datetime.now()
value= (168, "Doe", "John", "JD", current_date, 500)

cursor.execute(sql, value)

DB.commit()

print(cursor.rowcount, "Successfully added.") 

2

sql = """
    SELECT E.EMP_NUM, E.EMP_FNAME, E.EMP_LNAME, E.EMP_INITIAL, jb.JOB_DESCRIPTION, jb.JOB_CHG_HOUR, E.EMP_HIREDATE FROM EMPLOYEE AS E 
    JOIN JOB AS jb ON E.JOB_CODE = jb.JOB_CODE 
    WHERE E.EMP_NUM = 168;
"""
cursor.execute(sql)

result = cursor.fetchone()


3

update_sql = """
    UPDATE employee
    SET job_code = (SELECT JOB_CODE FROM JOB WHERE JOB_DESCRIPTION = 'Database Designer') WHERE emp_num = 168;
"""
cursor.execute(update_sql)

DB.commit()

print(cursor.rowcount, "Successfully updated.") 


4

sql = """
    SELECT P.PROJ_NUM, P.PROJ_NAME, E.EMP_FNAME,E.EMP_LNAME FROM PROJECT AS P
    JOIN `assignment` AS A ON P.PROJ_NUM = A.PROJ_NUM
    JOIN employee AS E ON A.EMP_NUM = E.EMP_NUM
    JOIN job AS J ON E.JOB_CODE = J.JOB_CODE
    WHERE J.JOB_DESCRIPTION = 'Programmer';
"""
cursor.execute(sql)

result = cursor.fetchall()

print(result)


5

delete_sql = "DELETE FROM employee WHERE EMP_NUM = 168;"

cursor.execute(delete_sql)

DB.commit()

print(cursor.rowcount, "Successfully deleted.")