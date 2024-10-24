# JSON Structure Documentation

## Overview

Our application's Firebase database will hold the following key collections:

1. Notification
2. MCQuestion
3. Note
4. Course
5. Folder
6. User

Some key elements of our application, such as chat messages, will not be stored in Firebase. Chats are not saved unless a user explicitly chooses to do so, in which case the content of the chat message will simply be appended to the content of the note the user saves it to. For this reason, we do not have a JSON structure for chats and chat messages.


### 1. Notification
```json
{
  "id": "e1a2c4d2-4d3f-47b1-90c6-5f9a61d0654f",
  "type": "reminder",
  "scheduledAt": "2024-10-22T10:00:00Z",
  "message": "Time to review the 67443 Firebase lecture from Tuesday!",
  "quizID": "1a84c2f7-758d-4bb4-9a1b-6fb67632e1a2",
  "userID": "bc65f2d7-3055-4db3-840b-96f21a8c6b6e"
}
```
- Purpose: Handles reminders for review quizzes (spaced repetition).
- Attributes:
    - id: Unique identifier for the notification.
    - type: Type of notification (eg. review reminder).
    - scheduledAt: Time the notification is scheduled for.
    - message: Message to be displayed in the notification.
    - quizID: Reference to the related quiz.
    - userId: Reference to the user receiving the notification.


### 2. MCQuestion
```json
{
  "id": "b8f91485-bd68-47f6-9f29-457d8ac57a75",
  "question": "What is the capital of France?",
  "potentialAnswers": ["Paris", "Baris", "Caris", "Daris"],
  "correctAnswer": 0
}
```
- Purpose: Represents multiple-choice questions present in quizzes.
- Attributes:
    - id: Unique identifier for the question set.
    - questions: Text of the question.
    - potentialAnswers: List of possible answers.
    - correctAnswer: The index of the correct answer within potentialAnswers.

### 3. Note
```json
{
  "noteID": "d2b46c71-c0b6-4a2d-ae9b-f6b1a827eae4",
  "userID": "bc65f2d7-3055-4db3-840b-96f21a8c6b6e",
  "title": "Firebase Lecture",
  "summary": "This is a summary of the Firebase lecture.",
  "content": "This is the full content of the Firebase lecture note, including parsed saved chat messages, file imports, etc.",
  "createdAt": "2024-10-21T12:00:00Z",
  "courseID": "f5db67c3-8096-4d18-b4cf-7fd3a87bcf80",
  "fileLocation": "/67443/firebase_lecture",
  "lastAccessed": "2024-10-21T12:00:00Z"
}
```
- Purpose: Stores lecture notes and related content.
- Attributes:
    - noteID: Unique identifier for the note.
    - userID: Reference to the user who created the note.
    - title: Title of the note.
    - summary: AI-generated summary of the note's content.
    - content: Full content of the note, including any parsed saved chat messages, file imports, etc.
    - createdAt: Timestamp for when the note was created.
    - courseID: Reference to the course associated with the note.
    - fileLocation: File path from home as a string.

### 4. Course
```json
{
  "courseID": "f5db67c3-8096-4d18-b4cf-7fd3a87bcf80",
  "userID": "bc65f2d7-3055-4db3-840b-96f21a8c6b6e",
  "courseName": "67443: Mobile App Development",
  "folders": ["a1c9b24d-7696-4e93-8cb6-3b9ab2d8374d", "bd75ec96-83a7-4022-b92a-2ad8c3b9e1c3"],
  "notes": ["d2b46c71-c0b6-4a2d-ae9b-f6b1a827eae4", "b9fbb67e-ccf4-49ae-9053-8be7c8b1a732"],
  "fileLocation": "/67443/"
}
```
- Purpose: Represents a course containing related notes.
- Attributes:
    - courseID: Unique identifier for the course.
    - userID: Reference to the user who created the course.
    - courseName: Name of the course.
    - folders: List of folder IDs located within the course.
    - notes: List of note IDs located within the course.
    - fileLocation: File path from home as a string.

### 5. Folder
```json
{
  "folderID": "a1c9b24d-7696-4e93-8cb6-3b9ab2d8374d",
  "userID": "bc65f2d7-3055-4db3-840b-96f21a8c6b6e",
  "folderName": "Capital One Mentor Meeting Notes",
  "courseID": "f5db67c3-8096-4d18-b4cf-7fd3a87bcf80",
  "notes": ["b9fbb67e-ccf4-49ae-9053-8be7c8b1a732", "6fb4835b-e589-42a2-baff-7ab7f8b30762"],
  "fileLocation": "/67443/capital_one_mentor_meeting_notes/",
  "recentNoteSummary": {
    "noteID": "6fb4835b-e589-42a2-baff-7ab7f8b30762",
    "title": "10/21/2024 Meeting",
    "summary": "AI generated summary of most recent meeting.",
    "createdAt": "2024-10-21T12:00:00Z"
  }
}
```
- Purpose: Organizes notes into folders.
- Attributes:
    - folderID: Unique identifier for the folder.
    - userID: Reference to the user who created the folder.
    - folderName: Name of the folder.
    - courseID: Reference to the course associated with the folder.
    - notes: List of note IDs contained in the folder.
    - fileLocation: File path from home as a string.
    - recentNoteSummary: JSON object containing details of the most recent note, including:
        - noteID: ID of the note.
        - title: Title of the note.
        - summary: Summary of the note.
        - createdAt: Timestamp of when the note was created.

### 6. User
```json
{
  "id": "bc65f2d7-3055-4db3-840b-96f21a8c6b6e",
  "name": "John Doe",
  "notifications": ["e1a2c4d2-4d3f-47b1-90c6-5f9a61d0654f", "5c6d8fcb-7854-4b63-9496-d65ef28d2469"],
  "streak": {
    "currentStreakLength": 5,
    "lastQuizCompletedAt": "2024-10-21T12:00:00Z"
  },
  "courses": ["f5db67c3-8096-4d18-b4cf-7fd3a87bcf80"],
  "settings": {
    "notificationsEnabled": true,
    "notificationFrequency": "daily",
    "notesOnlyQuizScope": false,
    "notesOnlyChatScope": false
  },
  "quizzes": [
    {
      "quizID": "1a84c2f7-758d-4bb4-9a1b-6fb67632e1a2",
      "noteID": "d2b46c71-c0b6-4a2d-ae9b-f6b1a827eae4",
      "questions": ["b8f91485-bd68-47f6-9f29-457d8ac57a75"],
      "passed": true,
      "reattempting": false,
      "completedAt": "2024-10-21T12:00:00Z"
    }
  ]
}
```
- Purpose: Represents a user in the application.
- Attributes:
    - id: Unique identifier for the user.
    - name: Name of the user.
    - notifications: List of notification IDs associated with the user.
    - streak: Streak object containing streak information.
        - currentStreakLength: Number of consecutive days the user has completed a quiz.
        - lastQuizCompletedAt: Timestamp of when the user last completed a quiz.
    - courses: List of course IDs the user has created on the home screen.
    - settings: User settings object containing:
        - notificationsEnabled: Boolean indicating if notifications are enabled.
        - notificationFrequency: Frequency of notifications (daily, weekly, etc.).
        - notesOnlyQuizScope: Boolean indicating if quizzes are generated from contents of notes only.
        - notesOnlyChatScope: Boolean indicating if chat responses are generated from contents of notes only.
    - quizzes: List of quiz objects a user has completed, each containing:
        - quizID: Unique identifier for the quiz.
        - noteID: Reference to the note associated with the quiz.
        - questions: List of multiple-choice question IDs included in the quiz.
        - passed: Boolean indicating if the user passed the quiz.
        - reattempting: Boolean indicating if the user is re-attempting the quiz.
        - completedAt: Timestamp for when the quiz was completed.
