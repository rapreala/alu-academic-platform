# Requirements Document: ALU Student Academic Platform

## Introduction

The ALU Student Academic Platform is a Flutter mobile application designed to help African Leadership University students manage their academic responsibilities. The application provides tools for tracking assignments, managing class schedules, recording attendance, and monitoring academic progress. Built for a 48-hour competition timeline with a team of 4 developers, the platform emphasizes practical functionality, clean UI/UX, and collaborative development practices.

## Glossary

- **System**: The ALU Student Academic Platform mobile application
- **Student**: An ALU student user of the application
- **Assignment**: A task with a title, due date, course, priority level, and completion status
- **Session**: A scheduled academic event with title, date, time range, location, type, and attendance record
- **Session_Type**: One of: Class, Mastery Session, Study Group, or PSL Meeting
- **Attendance_Percentage**: The ratio of sessions marked Present to total sessions with recorded attendance
- **Dashboard**: The home screen displaying summary information and alerts
- **Navigation_Bar**: The bottom navigation bar with three tabs (Dashboard, Assignments, Schedule)
- **Data_Store**: Firebase Firestore - the cloud-based NoSQL database for storing application data
- **Firestore**: Google's cloud-hosted NoSQL database that stores data in collections and documents
- **ALU_Color_Palette**: The official branding colors for African Leadership University

## Requirements

### Requirement 1: Dashboard Display

**User Story:** As a student, I want to see a summary dashboard when I open the app, so that I can quickly understand my current academic status and upcoming obligations.

#### Acceptance Criteria

1. WHEN the Dashboard screen loads, THE System SHALL display the current date in a readable format
2. WHEN the Dashboard screen loads, THE System SHALL display the current academic week number
3. WHEN the Dashboard screen loads, THE System SHALL display all sessions scheduled for the current date
4. WHEN the Dashboard screen loads, THE System SHALL display all assignments with due dates within the next 7 days
5. WHEN the Dashboard screen loads, THE System SHALL display the overall Attendance_Percentage
6. WHEN the Attendance_Percentage is less than 75%, THE System SHALL display a visual warning indicator
7. WHEN the Dashboard screen loads, THE System SHALL display a count of pending (incomplete) assignments

### Requirement 2: Assignment Creation and Management

**User Story:** As a student, I want to create and manage assignments, so that I can track my academic tasks and deadlines.

#### Acceptance Criteria

1. WHEN a student provides valid assignment data (title, due date, course, priority level), THE System SHALL create a new Assignment and add it to the assignment list
2. WHEN a student attempts to create an assignment with missing required fields, THE System SHALL prevent creation and display a validation error message
3. WHEN a student views the assignment list, THE System SHALL display all assignments sorted by due date in ascending order
4. WHEN a student marks an assignment as completed, THE System SHALL update the assignment's completion status
5. WHEN a student deletes an assignment, THE System SHALL remove it from the assignment list
6. WHEN a student edits an assignment, THE System SHALL update the assignment with the new data and maintain proper validation

### Requirement 3: Session Scheduling and Management

**User Story:** As a student, I want to create and manage academic sessions, so that I can organize my weekly schedule and track my attendance.

#### Acceptance Criteria

1. WHEN a student provides valid session data (title, date, start time, end time, location, Session_Type), THE System SHALL create a new Session and add it to the schedule
2. WHEN a student attempts to create a session with invalid date or time data, THE System SHALL prevent creation and display a validation error message
3. WHEN a student views the schedule, THE System SHALL display sessions organized by week
4. WHEN a student selects a Session_Type, THE System SHALL only allow one of: Class, Mastery Session, Study Group, or PSL Meeting
5. WHEN a student deletes a session, THE System SHALL remove it from the schedule
6. WHEN a student edits a session, THE System SHALL update the session with the new data and maintain proper validation

### Requirement 4: Attendance Recording and Tracking

**User Story:** As a student, I want to record and track my attendance, so that I can monitor my attendance percentage and stay above the required threshold.

#### Acceptance Criteria

1. WHEN a student marks a session attendance as Present or Absent, THE System SHALL record the attendance status for that session
2. WHEN attendance is recorded for any session, THE System SHALL recalculate the Attendance_Percentage as (Present sessions / Total sessions with attendance) × 100
3. WHEN the Attendance_Percentage is calculated, THE System SHALL display it on the Dashboard
4. WHEN the Attendance_Percentage falls below 75%, THE System SHALL display a visual alert on the Dashboard
5. WHEN a student views their attendance history, THE System SHALL display all sessions with recorded attendance status

### Requirement 5: Navigation and Screen Structure

**User Story:** As a student, I want to navigate between different sections of the app easily, so that I can access assignments, schedule, and dashboard information efficiently.

#### Acceptance Criteria

1. THE System SHALL provide a Navigation_Bar with exactly three tabs: Dashboard, Assignments, and Schedule
2. WHEN a student taps a tab in the Navigation_Bar, THE System SHALL navigate to the corresponding screen
3. WHEN navigating between screens, THE System SHALL maintain the application state without data loss
4. THE System SHALL display the Navigation_Bar at the bottom of the screen on all main screens

### Requirement 6: Data Persistence with Firebase Firestore

**User Story:** As a student, I want my data to be saved to the cloud, so that I don't lose my assignments, sessions, and attendance records when I close the app, and I can access my data from any device.

#### Acceptance Criteria

1. WHEN a student creates, updates, or deletes an Assignment, THE System SHALL persist the change to Firestore in real-time
2. WHEN a student creates, updates, or deletes a Session, THE System SHALL persist the change to Firestore in real-time
3. WHEN a student records attendance, THE System SHALL persist the attendance record to Firestore in real-time
4. WHEN the application starts, THE System SHALL load all persisted data from Firestore
5. THE System SHALL use Firebase Firestore as the Data_Store with the following collections:
   - `assignments` collection for storing Assignment documents
   - `sessions` collection for storing Session documents
   - Each document SHALL have a unique ID generated by Firestore
6. WHEN the device is offline, THE System SHALL queue data changes and sync them when connectivity is restored (using Firestore offline persistence)
7. THE System SHALL handle Firestore connection errors gracefully and display appropriate error messages to the user

### Requirement 7: User Interface and Visual Design

**User Story:** As a student, I want a visually appealing and responsive interface, so that I can use the app comfortably on my mobile device.

#### Acceptance Criteria

1. THE System SHALL use the ALU_Color_Palette for all branding elements
2. WHEN rendering any screen, THE System SHALL ensure no pixel overflow occurs on standard mobile device screen sizes
3. WHEN displaying forms, THE System SHALL provide clear labels and input validation feedback
4. THE System SHALL follow Flutter Material Design guidelines for UI components
5. WHEN displaying lists (assignments, sessions), THE System SHALL use appropriate spacing and visual hierarchy

### Requirement 8: Input Validation

**User Story:** As a student, I want the app to validate my input, so that I don't create invalid assignments or sessions with incorrect data.

#### Acceptance Criteria

1. WHEN a student enters a date field, THE System SHALL validate that the date is in a valid format
2. WHEN a student enters a time field, THE System SHALL validate that the time is in a valid format
3. WHEN a student enters a start time and end time for a session, THE System SHALL validate that the end time is after the start time
4. WHEN validation fails, THE System SHALL display a clear error message indicating the issue
5. WHEN all required fields are valid, THE System SHALL enable the save/create action

### Requirement 9: Mobile Platform Requirements

**User Story:** As a student, I want to use the app on my mobile device, so that I can manage my academic tasks on the go.

#### Acceptance Criteria

1. THE System SHALL be built using Flutter framework
2. THE System SHALL run on Android or iOS mobile devices or emulators
3. THE System SHALL NOT run in a web browser
4. WHEN the application is built, THE System SHALL produce a mobile application package (APK or IPA)
5. THE System SHALL be responsive to different mobile screen sizes and orientations

### Requirement 10: Firebase Integration and Configuration

**User Story:** As a developer, I want to properly configure Firebase in the application, so that the app can securely connect to Firestore and persist data.

#### Acceptance Criteria

1. THE System SHALL integrate Firebase SDK for Flutter (firebase_core and cloud_firestore packages)
2. THE System SHALL initialize Firebase when the application starts, before any Firestore operations
3. THE System SHALL include proper Firebase configuration files:
   - `google-services.json` for Android
   - `GoogleService-Info.plist` for iOS
4. THE System SHALL implement proper error handling for Firebase initialization failures
5. THE System SHALL enable Firestore offline persistence to allow the app to work without internet connectivity
6. THE System SHALL structure Firestore data with proper indexing for efficient queries (e.g., assignments sorted by due date)
