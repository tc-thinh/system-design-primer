## Designing a University Course Registration System
### Requirements
- The course registration system should allow **students** to register for **courses** and view their registered courses.
- Each course should have a course code, name, instructor, and maximum enrollment capacity.
- Students should be able to search for courses based on course code or name.
- The system should prevent students from registering for courses that have reached their maximum enrollment capacity.
- The system should handle concurrent registration requests from multiple students.
- The system should ensure data consistency and prevent race conditions.
- The system should be extensible to accommodate future enhancements and new features.

### Summary
- Register for class, no limit on the number of registration
- Search classes
- Handling concurrent registration

### High-level overview
- Presentation layer (frontend) - client
- Business logic layer (redirections and form validation)
- Service layer
    - Registration service
    - Search service
- Database layer
    - students
    - courses

### Database
- Students
    - studentId UUID PRIMARY KEY
    - name VARCHAR(128) -- can divide into first and last
    - email VARCHAR(128)
    - ... other information about students
- StudentCourses
    - studentId FOREIGN KEY to Students.studentId
    - courseId FOREIGN KEY to Courses.courseId
    - (studentId, courseId) - PRIMARY KEY
    - timeRegistered DATETIME
    - semesterId -- can be a foreign key to another table called semester
    - ... other information to record
- Courses
    - courseId UUID PRIMARY KEY
    - courseName VARCHAR(512)
    - instructorId FOREIGN KEY to instructor.instructorId -- 1-many relationship between instructor-course
    - capacity INT
- Instructor
    - instructorId UUID PRIMARY KEY
    - name VARCHAR(128)
    - email VARCHAR(128)
    - ... other information about students

### Search Service
- Students can look up their registered courses
- Students can find a list of available courses
- Search by [keyword]
#### APIs
- GET /courses?keyword={keyword}&page={page-number}?... - get all available courses, using query parameter bc this is a public information - for bookmarking and sharing purposes
- GET /students/{studentId}/courses?semester={semesterId} - get all the courses that the student registered

### Registration service
- A centralized job queue for registration handling, and after processing a job (in one writing thread/process), we can push to the **Notification Service** to notify the student whether or not their registration success.
- Follow strictly a producer-consumer problem/swe architecture
- Handling all logic about course registration, whether to check if the student has completed all the prerequisite or not
- POST /registration
    - INPUT: studentId, courseId
    - OUTPUT: boolean - put into job queue or not
