-- Course Registration Management System

CREATE DATABASE CourseRegistrationSystem;
USE CourseRegistrationSystem;

-- Students Table
CREATE TABLE Students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    student_name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    department VARCHAR(50),
    year_of_study INT
);

-- Courses Table
CREATE TABLE Courses (
    course_id INT PRIMARY KEY AUTO_INCREMENT,
    course_name VARCHAR(100),
    credits INT,
    faculty_name VARCHAR(100)
);

-- Registration Table
CREATE TABLE Registrations (
    registration_id INT PRIMARY KEY AUTO_INCREMENT,
    student_id INT,
    course_id INT,
    semester VARCHAR(20),
    registration_date DATE,
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);

-- Faculty Table
CREATE TABLE Faculty (
    faculty_id INT PRIMARY KEY AUTO_INCREMENT,
    faculty_name VARCHAR(100),
    department VARCHAR(50)
);

-- Insert Students
INSERT INTO Students(student_name,email,department,year_of_study) VALUES
('Sravani','sravani@gmail.com','CSE',3),
('Rahul','rahul@gmail.com','ECE',2),
('Anjali','anjali@gmail.com','CSE',4);

-- Insert Courses
INSERT INTO Courses(course_name,credits,faculty_name) VALUES
('Database Management System',4,'Dr. Kumar'),
('Web Technologies',3,'Dr. Priya'),
('Operating Systems',4,'Dr. Ramesh');

-- Insert Faculty
INSERT INTO Faculty(faculty_name,department) VALUES
('Dr. Kumar','CSE'),
('Dr. Priya','CSE'),
('Dr. Ramesh','ECE');

-- Insert Registrations
INSERT INTO Registrations(student_id,course_id,semester,registration_date) VALUES
(1,1,'Semester 5','2025-08-10'),
(1,2,'Semester 5','2025-08-10'),
(2,3,'Semester 4','2025-08-11'),
(3,1,'Semester 7','2025-08-12');

-- 1. Display All Students
SELECT * FROM Students;

-- 2. Display All Courses
SELECT * FROM Courses;

-- 3. Student Course Registration Details
SELECT s.student_name, c.course_name, r.semester
FROM Registrations r
JOIN Students s ON r.student_id = s.student_id
JOIN Courses c ON r.course_id = c.course_id;

-- 4. Count Students Registered for Each Course
SELECT c.course_name, COUNT(r.student_id) AS total_students
FROM Courses c
JOIN Registrations r ON c.course_id = r.course_id
GROUP BY c.course_name;

-- 5. Students from CSE Department
SELECT student_name, department
FROM Students
WHERE department = 'CSE';

-- 6. Courses with More than 3 Credits
SELECT course_name, credits
FROM Courses
WHERE credits > 3;

-- 7. Update Student Year
UPDATE Students
SET year_of_study = 4
WHERE student_id = 1;

-- 8. Delete a Registration
DELETE FROM Registrations
WHERE registration_id = 3;

-- 9. Create View for Registered Students
CREATE VIEW Registered_Students AS
SELECT s.student_name, c.course_name, r.semester
FROM Registrations r
JOIN Students s ON r.student_id = s.student_id
JOIN Courses c ON r.course_id = c.course_id;

-- Display View
SELECT * FROM Registered_Students;
