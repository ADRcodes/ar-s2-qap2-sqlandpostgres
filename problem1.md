<!-- Problem 1: SQL code for a university enrollment system -->

CREATE TABLE students (
	student_id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
	school_enrollment_date DATE NOT NULL
);

CREATE TABLE professors (
	prof_id SERIAL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
	department VARCHAR(50)
);

CREATE TABLE courses (
	course_id SERIAL PRIMARY KEY,
	course_name VARCHAR(50) NOT NULL,
	course_description TEXT,
	prof_id INT,
	FOREIGN KEY (prof_id) REFERENCES professors(prof_id)
);

CREATE TABLE enrollments (
    student_id INTEGER,
    course_id INTEGER,
    enrollment_date DATE,
    FOREIGN KEY (student_id) REFERENCES students(student_id),
    FOREIGN KEY (course_id) REFERENCES courses(course_id),
	PRIMARY KEY (student_id, course_id)
);

INSERT INTO Students (first_name, last_name, email, school_enrollment_date)
VALUES ('Alex', 'Johnston', 'real@example.com', '2001-01-01'),
       ('Rob', 'Myth', 'Rob@example.com', '2021-01-02'),
  	   ('Cob', 'Sith', 'Cob@example.com', '2001-01-02'),
	     ('Dob', 'Byth', 'Dob@example.com', '1921-01-02'),
	     ('Gob', 'E', 'Gee@example.com', '3021-01-02');

INSERT INTO professors (first_name, last_name, department)
VALUES ('Ralex', 'Vohnston', 'Magic'),
       ('Hob', 'Pyth', 'Finance'),
       ('Fob', 'Key', 'Engineering'),
       ('Mob', 'Spawn', 'Muggle Affairs'),
       ('Job', 'Binsureance', 'Govermental Efficiency');

INSERT INTO courses (course_name, course_description, prof_id)
VALUES ('Defence against the darkish arts', 'Good luck', 1),
	     ('Atrology', 'Look up and think', 5),
		   ('Electromagnetism and optics', 'its harder than it sounds', 3);


INSERT INTO enrollments (student_id, course_id, enrollment_date)
VALUES (13, 1, '2000-01-01'),
       (14, 3, '2000-01-01'),
       (14, 2, '2000-01-01'),
       (15, 2, '2000-01-01'),
       (17, 1, '2000-01-01'),
       (16, 2, '2000-01-01');


SELECT students.first_name || ' ' || students.last_name AS full_name
FROM students
JOIN enrollments ON students.student_id = enrollments.student_id
JOIN courses ON enrollments.course_id = courses.course_id
WHERE courses.course_id = 1

SELECT courses.course_name, professors.first_name || ' ' || professors.last_name
FROM courses
JOIN professors ON courses.prof_id = professors.prof_id

UPDATE students
SET email = 'comeoncome@me.com'
WHERE first_name = 'Alex';

DELETE FROM enrollments
WHERE student_id = 15 AND course_id = 2;

