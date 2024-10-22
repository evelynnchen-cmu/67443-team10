# JSON Structure Documentation

## Overview

Our application will consist of the following key collections:

1. Notification
2. Streak
3. MCQuestion
4. Note
5. Course
6. Folder
7. User
8. Quiz
9. Chat
10. Message

### 1. Notification
```json
{
  "id": "UUID",
  "type": "reminder",
  "scheduledAt": "2024-10-22T10:00:00Z",
  "message": "time to review the 67443 Firebase lecture from Tuesday!",
  "quizID": "UUID",
  "userID": "UUID"
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


### 2. Streak
```json
{
  "userId": "UUID",
  "streakPoints": 200,
  "currentStreakLength": 5,  // Num consecutive days
  "lastQuizCompletedAt": "2024-10-21T12:00:00Z",
  "activityLog": [
    {
      "date": "2024-10-20",
      "completedQuiz": true,
      "pointsAwarded": 20
    },
    {
      "date": "2024-10-21",
      "completedQuiz": true,
      "pointsAwarded": 20
    }
  ]
}
```
- Purpose: Tracks the user's streak and points earned through consistent quiz completion.
- Attributes:
    - userID: Unique identifier for the user.
    - streakPoints: Total points earned.
    - currentStreak: Number of consecutive days of quiz completion.
    - lastQuizCompletedAt: Timestamp for the last completed quiz.
    - activityLog: List of activity log objects containing:
        - date: Date of the activity.
        - completedQuiz: Boolean indicating if a quiz was completed on that day.
        - pointsAwarded: Number of points awarded for the completed quiz.

### 3. MCQuestion
```json
{
  "messageID": "UUID",
  "questions": [
    {
      "questionText": "What is the capital of France?",
      "potentialAnswers": ["A. Paris", "B. Baris", "C. Caris", "D. Daris"],
      "correctAnswer": "A. Paris"
    }
  ]
}
```
- Purpose: Represents multiple-choice questions present in quizzes.
- Attributes:
    - messageID: Unique identifier for the question set.
    - questions: List of question objects, each containing:
        - questionText: Text of the question.
        - potentialAnswers: List of possible answers.
        - correctAnswer: The correct answer that matches one of the potential answers.

### 4. Note
```json
{
  "noteID": "UUID",
  "title": "Firebase Lecture",
  "summary": "This is a summary of the Firebase lecture.",
  "content": "This is the full content of the note, including parsed saved chat messages, file imports, etc.",
  "createdAt": "2024-10-21T12:00:00Z",
  "courseID": "UUID",
  "fileLocation": "/67443/firebase_lecture"
}
```
- Purpose: Stores lecture notes and related content.
- Attributes:
    - noteID: Unique identifier for the note.
    - title: Title of the note.
    - summary: AI-generated summary of the note's content.
    - content: Full content of the note, including any parsed saved chat messages, file imports, etc.
    - createdAt: Timestamp for when the note was created.
    - courseID: Reference to the course associated with the note.
    - fileLocation: File path from home as a string.

### 5. Course
```json
{
  "courseID": "UUID",
  "courseName": "67443: Mobile App Development",
  "folders": ["UUID1", "UUID2"],
  "notes": ["UUID1", "UUID2"],
  "fileLocation": "/67443/"
}
```
- Purpose: Represents a course containing related notes.
- Attributes:
    - courseID: Unique identifier for the course.
    - courseName: Name of the course.
    - folders: List of folder IDs located within the course.
    - notes: List of note IDs located within the course.
    - fileLocation: File path from home as a string.

### 6. Folder
```json
{
  "folderID": "UUID",
  "folderName": "Capital One Mentor Meeting Notes",
  "courseID": "UUID",
  "notes": ["UUID1", "UUID2"],
  "fileLocation": "/67443/capital_one_mentor_meeting_notes/",
  "recentNoteSummary": {
    "noteID": "UUID",
    "title": "10/21/2024 Meeting",
    "summary": "AI generated summary of most recent meeting.",
    "createdAt": "2024-10-21T12:00:00Z"
  }
}
```
- Purpose: Organizes notes into folders.
- Attributes:
    - folderID: Unique identifier for the folder.
    - folderName: Name of the folder.
    - courseID: Reference to the course associated with the folder.
    - notes: List of note IDs contained in the folder.
    - fileLocation: File path from home as a string.
    - recentNoteSummary: JSON object containing details of the most recent note, including:
        - noteID: ID of the note.
        - title: Title of the note.
        - summary: Summary of the note.
        - createdAt: Timestamp of when the note was created.

### 7. User
```json
{
  "id": "UUID",
  "name": "John Doe",
  "notifications": ["UUID1", "UUID2"],
  "streak": {
    "userID": "UUID",
    "streakPoints": 200,
    "currentStreakLength": 5,
    "lastQuizCompletedAt": "2024-10-21T12:00:00Z"
  }
}
```
- Purpose: Represents a user in the application.
- Attributes:
    - id: Unique identifier for the user.
    - name: Name of the user.
    - notifications: List of notification IDs associated with the user.
    - streak: Streak object containing streak information.

### 8. Quiz
```json
{
  "quizID": "UUID",
  "userID": "UUID",
  "noteID": "UUID",
  "questions": ["UUID1", "UUID2"],
  "score": 100,
  "passed": true,
  "reattempting": false,
  "completedAt": "2024-10-21T12:00:00Z"
}
```
- Purpose: Stores information about user quizzes.
- Attributes:
    - quizID: Unique identifier for the quiz.
    - userID: Reference to the user who completed the quiz.
    - noteID: Reference to the note associated with the quiz.
    - questions: List of multiple-choice question IDs included in the quiz.
    - score: Score achieved by the user.
    - passed: Boolean indicating if the user passed the quiz.
    - reattempting: Boolean indicating if the user is re-attempting the quiz.
    - completedAt: Timestamp for when the quiz was completed.

### 9. Chat
```json
{
  "chatID": "UUID",
  "lastUpdated": "2024-10-21T12:00:00Z",
  "savedMessages": [
    {
      "messageID": "UUID",
      "noteID": "UUID",
      "content": "Hello, this is a message."
    },
    {
      "messageID": "UUID",
      "noteID": "UUID",
      "content": "Another message content."
    }
  ]
}
```
- Purpose: Represents a chat conversation in the application.
- Attributes:
    - chatID: Unique identifier for the chat.
    - lastUpdated: Timestamp for when the chat was last updated (ISO 8601 format).
    - savedMessages: List of message objects, each containing:
        - messageID: Unique identifier for the message.
        - noteID: Reference to the note where the message is saved.
        - content: Content of the message.


### 10. Message
```json
{
  "messageID": "UUID",
  "messageContent": "Chat message further explaining Firebase setup process.",
  "saveLocation": {
    messageID: "/67443/firebase_lecture"
  }
}
```
- Purpose: Represents a message in the chat.
- Attributes:
    - messageID: Unique identifier for the message.
    - messageContent: Content of the message.
    - saveLocation: Dictionary where the key is the message ID and the value is the file path where the message is saved.
