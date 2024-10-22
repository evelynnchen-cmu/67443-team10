# JSON Structure Documentation

## Overview

All JSON files are located in the `/data` folder and are used to define the core data models such as user streaks, multiple-choice questions, and more.

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

3. MCQuestion
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

4. Note
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

5. Course
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

