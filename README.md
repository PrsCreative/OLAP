SELECT WORKDEPT, EMPNO, SALARY
FROM EMP
ORDER BY WORKDEPT, EMPNO;


SELECT WORKDEPT, EMPNO, SUM(SALARY) SAL
FROM EMP
GROUP BY ROLLUP (WORKDEPT, EMPNO)
ORDER BY WORKDEPT, EMPNO;



SELECT WORKDEPT, SEX, SUM(SALARY) SAL
FROM EMP
GROUP BY CUBE (WORKDEPT, SEX);



SELECT 
		WORKDEPT, 
		SUM (CASE SEX WHEN 'F' 		THEN CNT ELSE 0 END) "Female",
		SUM (CASE SEX WHEN 'M' 		THEN CNT ELSE 0 END) "Male",
		SUM (CASE WHEN SEX IS NULL 	THEN CNT ELSE 0 END) "ALL"		
FROM 
	(SELECT WORKDEPT, SEX, COUNT(*) CNT
	FROM EMP
	GROUP BY WORKDEPT
	);
	
	

SELECT WORKDEPT, DEPTNAME, EMPNO, FIRSTNAM, SUM(SALARY) SAL
FROM EMP JOIN DEPT ON WORKDEPT = DEPTNO
GROUP BY ROLLUP ((WORKDEPT, DEPTNAME), (EMPNO, FIRSTNAME)); 


UPDATE EMP SET JOB = NULL WHERE JOB='PRES';

SELECT JOB, SEX, AVG(SALARY) SAL
FROM EMP
GROUP BY JOB, SEX;

SELECT JOB, SEX, AVG(SALARY) SAL
FROM EMP
GROUP BY ROLLUP (JOB, SEX);



SELECT 	CASE WHEN GROUPING(WORKDEPT) = 1 	THEN 'All Department' 	ELSE WORKDEPT END,
		CASE WHEN GROUPING(EMPNO)=1			THEN 'All Employee'		ELSE EMPNO END
FROM EMP
GROUP BY ROLLUP (WORKDEPT, EMPNO)
ORDER BY GROUPING(WORKDEPT) DESC, WORKDEPT, GROUPING(EMPNO) DESC, EMPNO;
		



	
