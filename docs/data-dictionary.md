# Mobile App for Enhanced Parent-Teacher Communication in Baka-bakahan Elementary School Data Dictionary

## Table of Contents
1. [Core User Entities](#core-user-entities)
2. [Academic Structure](#academic-structure)
3. [Communication Entities](#communication-entities)
4. [Document Management](#document-management)
5. [Event Management](#event-management)
6. [Academic Records](#academic-records)
7. [System Configuration](#system-configuration)
8. [Relationship Tables](#relationship-tables)

---

## Core User Entities

### USER
**Purpose:** Stores basic information for all system users (parents, teachers, administrators)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| user_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each user |
| email | VARCHAR(255) | UNIQUE, NOT NULL | User's email address for login |
| password_hash | VARCHAR(255) | NOT NULL | Encrypted password for authentication |
| first_name | VARCHAR(100) | NOT NULL | User's first name |
| last_name | VARCHAR(100) | NOT NULL | User's last name |
| phone_number | VARCHAR(20) | NULL | User's contact phone number |
| profile_picture_url | VARCHAR(500) | NULL | URL to user's profile picture |
| created_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | Account creation timestamp |
| updated_at | DATETIME | DEFAULT CURRENT_TIMESTAMP ON UPDATE | Last profile update timestamp |
| last_login | DATETIME | NULL | Timestamp of last successful login |
| status | ENUM | DEFAULT 'active' | Account status: active, inactive, suspended |
| reset_token | VARCHAR(255) | NULL | Token for password reset functionality |
| reset_token_expires | DATETIME | NULL | Expiration time for reset token |

### PARENT
**Purpose:** Stores additional information specific to parent users

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| parent_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each parent |
| user_id | INT | FOREIGN KEY, NOT NULL | Reference to USER table |
| occupation | VARCHAR(100) | NULL | Parent's occupation |
| work_phone | VARCHAR(20) | NULL | Parent's work phone number |
| emergency_contact | VARCHAR(100) | NULL | Emergency contact information |
| address | TEXT | NULL | Parent's home address |
| city | VARCHAR(100) | NULL | City of residence |
| state | VARCHAR(100) | NULL | State of residence |
| zip_code | VARCHAR(20) | NULL | Postal code |
| is_primary_contact | BOOLEAN | DEFAULT FALSE | Whether this parent is the primary contact |
| preferred_communication_method | VARCHAR(50) | NULL | Preferred method of communication |

### TEACHER
**Purpose:** Stores additional information specific to teacher users

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| teacher_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each teacher |
| user_id | INT | FOREIGN KEY, NOT NULL | Reference to USER table |
| employee_id | VARCHAR(50) | UNIQUE, NOT NULL | School-assigned employee identifier |
| department | VARCHAR(100) | NULL | Department the teacher belongs to |
| qualification | VARCHAR(200) | NULL | Teacher's educational qualifications |
| years_experience | INT | DEFAULT 0 | Number of years of teaching experience |
| office_location | VARCHAR(100) | NULL | Teacher's office location |
| office_hours | VARCHAR(100) | NULL | Teacher's available office hours |
| is_class_teacher | BOOLEAN | DEFAULT FALSE | Whether teacher is assigned as a class teacher |
| hire_date | DATETIME | DEFAULT CURRENT_TIMESTAMP | Date when teacher was hired |

### STUDENT
**Purpose:** Stores information about students enrolled in the system

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| student_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each student |
| student_number | VARCHAR(50) | UNIQUE, NOT NULL | School-assigned student number |
| first_name | VARCHAR(100) | NOT NULL | Student's first name |
| last_name | VARCHAR(100) | NOT NULL | Student's last name |
| date_of_birth | DATE | NOT NULL | Student's date of birth |
| gender | ENUM | NOT NULL | Student's gender: male, female, other |
| grade_level | VARCHAR(20) | NOT NULL | Current grade level |
| address | TEXT | NULL | Student's home address |
| medical_info | TEXT | NULL | Important medical information |
| emergency_contact | VARCHAR(100) | NULL | Emergency contact details |
| enrollment_date | DATETIME | DEFAULT CURRENT_TIMESTAMP | Date of enrollment |
| status | ENUM | DEFAULT 'active' | Student status: active, inactive, graduated, transferred |

---

## Academic Structure

### SCHOOL
**Purpose:** Stores information about schools in the system

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| school_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each school |
| school_name | VARCHAR(200) | NOT NULL | Official name of the school |
| school_code | VARCHAR(50) | UNIQUE, NOT NULL | Unique code assigned to the school |
| address | TEXT | NULL | School's physical address |
| city | VARCHAR(100) | NULL | City where school is located |
| state | VARCHAR(100) | NULL | State where school is located |
| zip_code | VARCHAR(20) | NULL | Postal code of school |
| phone_number | VARCHAR(20) | NULL | School's contact phone number |
| email | VARCHAR(255) | NULL | School's official email address |
| principal_name | VARCHAR(100) | NULL | Name of the school principal |
| established_date | DATETIME | NULL | Date when school was established |

### CLASSROOM
**Purpose:** Stores information about individual classrooms

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| classroom_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each classroom |
| school_id | INT | FOREIGN KEY, NOT NULL | Reference to SCHOOL table |
| classroom_code | VARCHAR(50) | UNIQUE, NOT NULL | Unique code for the classroom |
| room_number | VARCHAR(20) | NULL | Physical room number |
| grade_level | VARCHAR(20) | NULL | Grade level taught in this classroom |
| section | VARCHAR(10) | NULL | Section identifier (A, B, C, etc.) |
| capacity | INT | DEFAULT 30 | Maximum number of students |
| teacher_id | INT | FOREIGN KEY, NULL | Assigned teacher for the classroom |
| subject_area | VARCHAR(100) | NULL | Primary subject area taught |
| academic_year | VARCHAR(20) | NULL | Academic year for the classroom |
| created_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | Classroom creation timestamp |

### SUBJECT
**Purpose:** Stores information about subjects/courses offered

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| subject_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each subject |
| subject_name | VARCHAR(100) | NOT NULL | Name of the subject |
| subject_code | VARCHAR(20) | UNIQUE, NOT NULL | Unique code for the subject |
| description | TEXT | NULL | Detailed description of the subject |
| credits | INT | DEFAULT 1 | Number of credits for the subject |
| department | VARCHAR(100) | NULL | Department offering the subject |
| is_core_subject | BOOLEAN | DEFAULT TRUE | Whether it's a core/required subject |

---

## Communication Entities

### MESSAGE
**Purpose:** Stores direct messages between users

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| message_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each message |
| sender_id | INT | FOREIGN KEY, NOT NULL | Reference to USER who sent the message |
| receiver_id | INT | FOREIGN KEY, NOT NULL | Reference to USER who receives the message |
| classroom_id | INT | FOREIGN KEY, NULL | Associated classroom (if applicable) |
| subject | VARCHAR(200) | NULL | Subject line of the message |
| message_content | TEXT | NULL | Content of the message |
| sent_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | Timestamp when message was sent |
| read_at | DATETIME | NULL | Timestamp when message was read |
| priority_level | ENUM | DEFAULT 'medium' | Priority: low, medium, high, urgent |
| message_type | ENUM | DEFAULT 'direct' | Type: direct, announcement, alert |
| is_read | BOOLEAN | DEFAULT FALSE | Whether message has been read |
| parent_message_id | INT | FOREIGN KEY, NULL | Reference to parent message (for replies) |
| attachment_url | VARCHAR(500) | NULL | URL to attached file |

### ANNOUNCEMENT
**Purpose:** Stores announcements made by teachers

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| announcement_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each announcement |
| teacher_id | INT | FOREIGN KEY, NOT NULL | Teacher who created the announcement |
| classroom_id | INT | FOREIGN KEY, NULL | Associated classroom |
| title | VARCHAR(200) | NOT NULL | Title of the announcement |
| content | TEXT | NULL | Content of the announcement |
| posted_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When announcement was posted |
| expires_at | DATETIME | NULL | When announcement expires |
| priority_level | ENUM | DEFAULT 'medium' | Priority: low, medium, high, urgent |
| announcement_type | ENUM | DEFAULT 'general' | Type: general, academic, event, emergency |
| is_active | BOOLEAN | DEFAULT TRUE | Whether announcement is currently active |
| attachment_url | VARCHAR(500) | NULL | URL to attached file |

### NOTIFICATION
**Purpose:** Stores system notifications sent to users

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| notification_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each notification |
| user_id | INT | FOREIGN KEY, NOT NULL | User who receives the notification |
| title | VARCHAR(200) | NOT NULL | Title of the notification |
| content | TEXT | NULL | Content of the notification |
| notification_type | ENUM | NOT NULL | Type: message, announcement, event, grade, attendance |
| created_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When notification was created |
| sent_at | DATETIME | NULL | When notification was sent |
| is_read | BOOLEAN | DEFAULT FALSE | Whether notification has been read |
| is_push_sent | BOOLEAN | DEFAULT FALSE | Whether push notification was sent |
| reference_id | VARCHAR(100) | NULL | Reference to related record |
| priority | ENUM | DEFAULT 'medium' | Priority: low, medium, high |

---

## Document Management

### DOCUMENT
**Purpose:** Stores information about uploaded documents

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| document_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each document |
| uploaded_by | INT | FOREIGN KEY, NOT NULL | User who uploaded the document |
| document_name | VARCHAR(200) | NOT NULL | Display name of the document |
| file_path | VARCHAR(500) | NOT NULL | File system path to the document |
| file_type | VARCHAR(50) | NULL | MIME type of the file |
| file_size | INT | NULL | Size of the file in bytes |
| uploaded_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When document was uploaded |
| document_type | ENUM | DEFAULT 'assignment' | Type: assignment, report, certificate, form |
| description | TEXT | NULL | Description of the document |
| access_level | ENUM | DEFAULT 'classroom' | Access level: public, classroom, private |

---

## Event Management

### EVENT
**Purpose:** Stores information about scheduled events

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| event_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each event |
| created_by | INT | FOREIGN KEY, NOT NULL | User who created the event |
| classroom_id | INT | FOREIGN KEY, NULL | Associated classroom |
| event_title | VARCHAR(200) | NOT NULL | Title of the event |
| description | TEXT | NULL | Detailed description of the event |
| start_datetime | DATETIME | NOT NULL | Event start date and time |
| end_datetime | DATETIME | NOT NULL | Event end date and time |
| location | VARCHAR(200) | NULL | Event location |
| event_type | ENUM | DEFAULT 'meeting' | Type: meeting, conference, activity, exam, holiday |
| status | ENUM | DEFAULT 'scheduled' | Status: scheduled, ongoing, completed, cancelled |
| is_recurring | BOOLEAN | DEFAULT FALSE | Whether event repeats |
| recurrence_pattern | VARCHAR(100) | NULL | Pattern for recurring events |

---

## Academic Records

### ATTENDANCE
**Purpose:** Records student attendance information

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| attendance_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each attendance record |
| student_id | INT | FOREIGN KEY, NOT NULL | Student being recorded |
| classroom_id | INT | FOREIGN KEY, NOT NULL | Classroom where attendance was taken |
| attendance_date | DATE | NOT NULL | Date of attendance |
| status | ENUM | DEFAULT 'present' | Status: present, absent, late, excused |
| check_in_time | TIME | NULL | Time student checked in |
| notes | TEXT | NULL | Additional notes about attendance |
| recorded_by | INT | FOREIGN KEY, NOT NULL | Teacher who recorded attendance |
| created_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When record was created |

---

## System Configuration

### CLASSROOM_ACCESS_CODE
**Purpose:** Stores temporary access codes for classroom enrollment

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| code_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each access code |
| classroom_id | INT | FOREIGN KEY, NOT NULL | Associated classroom |
| access_code | VARCHAR(20) | UNIQUE, NOT NULL | The access code string |
| generated_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When code was generated |
| expires_at | DATETIME | NOT NULL | When code expires |
| is_active | BOOLEAN | DEFAULT TRUE | Whether code is currently active |
| generated_by | INT | FOREIGN KEY, NOT NULL | Teacher who generated the code |

### DEVICE_TOKEN
**Purpose:** Stores device tokens for push notifications

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| token_id | INT | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each token |
| user_id | INT | FOREIGN KEY, NOT NULL | User associated with the device |
| device_token | VARCHAR(255) | NOT NULL | Device-specific token for push notifications |
| device_type | VARCHAR(50) | NULL | Type of device (iOS, Android, etc.) |
| registered_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When token was registered |
| is_active | BOOLEAN | DEFAULT TRUE | Whether token is currently active |

---

## Relationship Tables

### PARENT_STUDENT
**Purpose:** Links parents to their children (many-to-many relationship)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| parent_id | INT | FOREIGN KEY, NOT NULL | Reference to PARENT table |
| student_id | INT | FOREIGN KEY, NOT NULL | Reference to STUDENT table |
| relationship_type | ENUM | NOT NULL | Type: father, mother, guardian, sibling |
| is_primary_contact | BOOLEAN | DEFAULT FALSE | Whether this is the primary contact |
| created_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When relationship was established |

**Composite Primary Key:** (parent_id, student_id)

### STUDENT_CLASSROOM
**Purpose:** Tracks student enrollment in classrooms (many-to-many relationship)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| student_id | INT | FOREIGN KEY, NOT NULL | Reference to STUDENT table |
| classroom_id | INT | FOREIGN KEY, NOT NULL | Reference to CLASSROOM table |
| enrolled_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When student was enrolled |
| status | ENUM | DEFAULT 'active' | Status: active, dropped, completed |
| final_grade | DECIMAL(5,2) | NULL | Final grade for the classroom |

**Composite Primary Key:** (student_id, classroom_id)

### TEACHER_SUBJECT
**Purpose:** Assigns teachers to subjects in specific classrooms (many-to-many relationship)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| teacher_id | INT | FOREIGN KEY, NOT NULL | Reference to TEACHER table |
| subject_id | INT | FOREIGN KEY, NOT NULL | Reference to SUBJECT table |
| classroom_id | INT | FOREIGN KEY, NOT NULL | Reference to CLASSROOM table |
| academic_year | VARCHAR(20) | NOT NULL | Academic year for this assignment |
| assigned_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When assignment was made |

**Composite Primary Key:** (teacher_id, subject_id, classroom_id)

### DOCUMENT_SHARE
**Purpose:** Tracks document sharing between users (many-to-many relationship)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| document_id | INT | FOREIGN KEY, NOT NULL | Reference to DOCUMENT table |
| shared_with | INT | FOREIGN KEY, NOT NULL | User the document is shared with |
| shared_by | INT | FOREIGN KEY, NOT NULL | User who shared the document |
| shared_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When document was shared |
| permission_level | ENUM | DEFAULT 'view' | Permission: view, download, edit |
| expires_at | DATETIME | NULL | When sharing expires |

**Composite Primary Key:** (document_id, shared_with)

### EVENT_PARTICIPANT
**Purpose:** Tracks event participation (many-to-many relationship)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| event_id | INT | FOREIGN KEY, NOT NULL | Reference to EVENT table |
| user_id | INT | FOREIGN KEY, NOT NULL | Reference to USER table |
| participant_type | ENUM | DEFAULT 'attendee' | Type: organizer, attendee, optional |
| response_status | ENUM | DEFAULT 'pending' | Status: pending, accepted, declined, tentative |
| responded_at | DATETIME | NULL | When user responded |
| notes | TEXT | NULL | Additional notes from participant |

**Composite Primary Key:** (event_id, user_id)

### ANNOUNCEMENT_RECIPIENT
**Purpose:** Tracks announcement delivery to users (many-to-many relationship)

| Column Name | Data Type | Constraints | Description |
|-------------|-----------|-------------|-------------|
| announcement_id | INT | FOREIGN KEY, NOT NULL | Reference to ANNOUNCEMENT table |
| user_id | INT | FOREIGN KEY, NOT NULL | Reference to USER table |
| sent_at | DATETIME | DEFAULT CURRENT_TIMESTAMP | When announcement was sent |
| read_at | DATETIME | NULL | When announcement was read |
| is_read | BOOLEAN | DEFAULT FALSE | Whether announcement has been read |

**Composite Primary Key:** (announcement_id, user_id)

---

## Data Types and Constraints Legend

### Data Types:
- **INT:** Integer values, typically used for IDs and counts
- **VARCHAR(n):** Variable-length strings with maximum length n
- **TEXT:** Large text fields for content
- **DATETIME:** Date and time values
- **DATE:** Date-only values
- **TIME:** Time-only values
- **DECIMAL(p,s):** Decimal numbers with precision p and scale s
- **BOOLEAN:** True/false values
- **ENUM:** Predefined list of acceptable values

### Constraints:
- **PRIMARY KEY:** Unique identifier for table records
- **FOREIGN KEY:** Reference to another table's primary key
- **UNIQUE:** Values must be unique across the table
- **NOT NULL:** Field cannot be empty
- **DEFAULT:** Default value when none is provided
- **AUTO_INCREMENT:** Automatically generates sequential numbers
