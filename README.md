# School-Management Project

--CREATING TABLES
----------------------------------------------

 CREATE TABLE Students 
   (	Student_ID int PRIMARY KEY, 
	FIRST_NAME VARCHAR2(200) NOT NULL, 
	LAST_NAME VARCHAR2(200) NOT NULL , 
	DATE_OF_BIRTH DATE NOT NULL , 
	GENDER VARCHAR2(200) NOT NULL, 
	PHONE_NUMBER NUMBER NOT NULL, 
	STATE VARCHAR2(200) NOT NULL, 
	CITY VARCHAR2(200) NOT NULL, 
	 CONSTRAINT PH_NUM CHECK (length(phone_number)=10)
   );

CREATE TABLE TEACHERS 
   (	TEACHER_ID int PRIMARY KEY, 
	FIRST_NAME VARCHAR2(200) NOT NULL, 
	LAST_NAME VARCHAR2(200) NOT NULL , 
	DATE_OF_BIRTH DATE NOT NULL , 
	GENDER VARCHAR2(200) NOT NULL, 
	PHONE_NUMBER NUMBER NOT NULL, 
	STATE VARCHAR2(200) NOT NULL, 
	CITY VARCHAR2(200) NOT NULL, 
	 CONSTRAINT PH_NUMB CHECK (length(phone_number)=10)
   );
   
   CREATE TABLE COURSES
   (	COURSE_ID int PRIMARY KEY , 
	COURSE_NAME VARCHAR2(200) NOT NULL, 
	TEACHER_ID int NOT NULL, 
	 FOREIGN KEY (TEACHER_ID) REFERENCES TEACHERS (TEACHER_ID)
   );
   
   CREATE TABLE ENROLLMENTS
   (
    ENROLLMENT_ID INT PRIMARY KEY,
    STUDENT_ID INT NOT NULL,
    COURSE_ID INT,
     FOREIGN KEY (STUDENT_ID) REFERENCES Students (STUDENT_ID),
    ENROLLMENT_DATE DATE,
     FOREIGN KEY (COURSE_ID) REFERENCES COURSES (COURSE_ID)
   ); 
   
   --INSERTING DATA'S INTO TABLE:-
   ---------------------------------------------------------------------
   
   INSERT INTO STUDENTS (student_id,first_name,last_name,date_of_birth,gender,phone_number,State,City) 
   VALUES(1,'BHASKAR','SAHA','12-DEC-98','MALE',7894561289,'WEST BENGAL','CHAKDAHA');
   INSERT INTO STUDENTS (student_id,first_name,last_name,date_of_birth,gender,phone_number,State,City) 
   VALUES(2,'Sweta','Sinha','25-MAR-00','FEMALE',7892978142,'Punjab','Mohali');
   
    INSERT INTO TEACHERS (TEACHER_id,first_name,last_name,date_of_birth,gender,phone_number,State,City) 
   VALUES(101,'Jackey','Sinha','28-JUN-05','MALE',7849126532,'Jharkhand','Dhanbad');
   INSERT INTO TEACHERS (TEACHER_id,first_name,last_name,date_of_birth,gender,phone_number,State,City) 
   VALUES(102,'Puja','Bala','18-AUG-01','FEMALE',7792796241,'West Bengal','Chakdaha');
   

   INSERT INTO ENROLLMENTS (ENROLLMENT_ID,STUDENT_ID,ENROLLMENT_DATE,COURSE_ID)
   VALUES(10001,1,'12-JAN-15',1002);
    INSERT INTO ENROLLMENTS (ENROLLMENT_ID,STUDENT_ID,ENROLLMENT_DATE,COURSE_ID)
   VALUES(10002,2,'22-FEB-17');
    INSERT INTO ENROLLMENTS (ENROLLMENT_ID,STUDENT_ID,ENROLLMENT_DATE,COURSE_ID)
   VALUES(10003,1,'12-JUL-15',1003);
    INSERT INTO ENROLLMENTS (ENROLLMENT_ID,STUDENT_ID,ENROLLMENT_DATE,COURSE_ID)
   VALUES(10004,2,'21-JUL-17',1004);
   
  INSERT INTO COURSES (COURSE_ID,COURSE_NAME,TEACHER_id)
   VALUES(1001,'Mathematics',101);
   INSERT INTO COURSES (COURSE_ID,COURSE_NAME,TEACHER_id)
   VALUES(1002,'Physics',102);
   INSERT INTO COURSES (COURSE_ID,COURSE_NAME,TEACHER_id)
   VALUES(1003,'Bengali',101);
   INSERT INTO COURSES (COURSE_ID,COURSE_NAME,TEACHER_id)
   VALUES(1004,'English',102);


--PROCEDURES:-
------------------
   --WRITE THIS PROCEDURE FOR ENROLLING ANY STUDENT
   --------------------------------------------------------------
   create or replace PROCEDURE EnrollStudents (
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    enrollment_id int
)
as
begin
    INSERT INTO enrollments (student_id, course_id, enrollment_date,enrollment_id)
    VALUES (student_id, course_id, enrollment_date,enrollment_id);
END;

--CALL PROCEDURE:-
-----------------------------
CALL EnrollStudents(10005,2,'19-OCT-17',1003);

  --WRITE THIS PROCEDURE FOR ADD ANY STUDENT
  ----------------------------------------------------------------
  create or replace PROCEDURE AddStudent(
    student_id INT,
    first_name varchar,
    last_name varchar, 
    date_of_birth date,
    gender varchar, 
    phone_number int,
    State varchar,
    City varchar
)
as
BEGIN
    INSERT INTO students (student_id,first_name,last_name,date_of_birth,gender,phone_number,State,City)
    VALUES (student_id,first_name,last_name,date_of_birth,gender,phone_number,State,City);
END;

--CALL PROCEDURE:-
-----------------------------
CALL AddStudent(3,'Girish','Sharma','15-SEP-95','Male',7844651216,'West Bengal','Kolkata');

--WRITE VIEW QUERY TO FIND A PARTICULAR STUDENT COUSRSE DETAILS:-
------------------------------------------------------------------------------------

CREATE OR REPLACE VIEW STUDENT_COURSES
AS
SELECT S.FIRST_NAME|| ' ' || S.LAST_NAME  STUDENT_NAME ,c.course_name
FROM STUDENTS S, COURSES C, enrollments E
WHERE S.STUDENT_ID=e.student_id
AND E.COURSE_ID=c.course_id;
