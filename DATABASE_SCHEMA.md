# Database Schema for Healthcare Facility Management

## Users Table
This table stores information about the users of the healthcare facility management system.

### SQL Definition:
```sql
CREATE TABLE Users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

## Case Entries Table
This table captures the details of each case entered into the system.

### SQL Definition:
```sql
CREATE TABLE CaseEntries (
    case_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    case_details TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

## Case Approvals Table
This table tracks approvals for cases.

### SQL Definition:
```sql
CREATE TABLE CaseApprovals (
    approval_id INT PRIMARY KEY AUTO_INCREMENT,
    case_id INT,
    approved_by INT,
    approval_status ENUM('approved', 'rejected', 'pending') NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (case_id) REFERENCES CaseEntries(case_id),
    FOREIGN KEY (approved_by) REFERENCES Users(user_id)
);
```

## Discussions Table
This table manages discussions related to cases.

### SQL Definition:
```sql
CREATE TABLE Discussions (
    discussion_id INT PRIMARY KEY AUTO_INCREMENT,
    case_id INT,
    user_id INT,
    discussion_text TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (case_id) REFERENCES CaseEntries(case_id),
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

## Discussion Messages Table
This table holds messages within discussions.

### SQL Definition:
```sql
CREATE TABLE DiscussionMessages (
    message_id INT PRIMARY KEY AUTO_INCREMENT,
    discussion_id INT,
    user_id INT,
    message_text TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (discussion_id) REFERENCES Discussions(discussion_id),
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

## Schedules Table
This table defines schedules for users or cases.

### SQL Definition:
```sql
CREATE TABLE Schedules (
    schedule_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    scheduled_time DATETIME NOT NULL,
    status ENUM('upcoming', 'completed', 'canceled') NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

## Attendance Table
This table records user attendance related to scheduled events.

### SQL Definition:
```sql
CREATE TABLE Attendance (
    attendance_id INT PRIMARY KEY AUTO_INCREMENT,
    schedule_id INT,
    user_id INT,
    attended BOOLEAN NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (schedule_id) REFERENCES Schedules(schedule_id),
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

## Notifications Table
This table manages notifications for users.

### SQL Definition:
```sql
CREATE TABLE Notifications (
    notification_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    notification_text TEXT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    read_at DATETIME,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
```

## Relationships:
- Each User can create multiple Case Entries.
- Each Case Entry can have multiple Case Approvals.
- Each Case Entry can have multiple Discussions.
- Each Discussion can have multiple Discussion Messages.
- Each User has multiple Schedules.
- Each Schedule can have multiple Attendance records.
- Each User can receive multiple Notifications.