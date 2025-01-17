To conduct a Domain-Driven Design (DDD) analysis of the given acceptance criteria, we can break down the requirements into different components and aspects relevant to DDD.

### 1. User Participation
- **Users should be able to join a quiz session using a unique quiz ID.**
    - **Domain Concept**: Quiz Session
    - **Entity**: User, Quiz Session
    - **Value Object**: Quiz ID
    - **Service**: Quiz Joining Service
    - **Domain Event**: UserJoinedQuizSession
- **The system should support multiple users joining the same quiz session simultaneously.**
    - **Domain Concept**: Concurrent Participation
    - **Entity**: User, Quiz Session
    - **Service**: Concurrent User Handling Service
    - **Domain Event**: MultipleUsersJoinedQuizSession

### 2. Real-Time Score Updates
- **As users submit answers, their scores should be updated in real-time.**
    - **Domain Concept**: Real-Time Score Updating
    - **Entity**: User, Answer, Score
    - **Service**: Score Updating Service
    - **Domain Event**: ScoreUpdated
- **The scoring system must be accurate and consistent.**
    - **Domain Concept**: Scoring System
    - **Entity**: Score
    - **Service**: Scoring Accuracy Service
    - **Domain Event**: ScoreConsistencyChecked

### 3. Real-Time Leaderboard
- **A leaderboard should display the current standings of all participants.**
    - **Domain Concept**: Leaderboard
    - **Entity**: Leaderboard, User, Score
    - **Service**: Leaderboard Display Service
    - **Domain Event**: LeaderboardUpdated
- **The leaderboard should update promptly as scores change.**
    - **Domain Concept**: Real-Time Leaderboard Updating
    - **Entity**: Leaderboard, Score
    - **Service**: Leaderboard Update Service
    - **Domain Event**: LeaderboardScoreChanged

### Bounded Contexts
1. **Quiz Management Context**:
    - Manages quiz creation, sessions, and user participation.
    - Entities: Quiz, Quiz Session, User
    - Services: Quiz Creation Service, Quiz Session Management Service
    - Domain Events: QuizCreated, UserJoinedQuizSession

2. **Scoring Context**:
    - Handles score updates and ensures accuracy and consistency.
    - Entities: Score, Answer
    - Services: Score Updating Service, Scoring Accuracy Service
    - Domain Events: ScoreUpdated, ScoreConsistencyChecked

3. **Leaderboard Context**:
    - Displays and updates the leaderboard in real-time.
    - Entities: Leaderboard, User, Score
    - Services: Leaderboard Display Service, Leaderboard Update Service
    - Domain Events: LeaderboardUpdated, LeaderboardScoreChanged

### Aggregates and Entities
- **Quiz**: Aggregate Root
    - Contains: Quiz Session, Quiz ID
- **Quiz Session**: Aggregate Root
    - Contains: Users, Session Details
- **User**: Entity
    - Contains: User ID, Name, Scores
- **Score**: Entity
    - Contains: User ID, Points, Timestamp
- **Leaderboard**: Aggregate Root
    - Contains: User Scores, Rankings

### Domain Events
- UserJoinedQuizSession
- MultipleUsersJoinedQuizSession
- ScoreUpdated
- ScoreConsistencyChecked
- LeaderboardUpdated
- LeaderboardScoreChanged

### Services
- **Quiz Joining Service**: Manages user participation in quiz sessions.
- **Concurrent User Handling Service**: Ensures multiple users can join a quiz session simultaneously.
- **Score Updating Service**: Handles real-time score updates as users submit answers.
- **Scoring Accuracy Service**: Ensures scoring accuracy and consistency.
- **Leaderboard Display Service**: Manages the display of the leaderboard.
- **Leaderboard Update Service**: Updates the leaderboard promptly as scores change.

### Summary
This analysis provides a detailed breakdown of the domain concepts, entities, services, and events required to fulfill the acceptance criteria using Domain-Driven Design principles. It ensures a clear understanding of the responsibilities and interactions within the system.

---
### Detailed DDD Analysis of Acceptance Criteria

#### 1. User Participation

**Requirement:** Users should be able to join a quiz session using a unique quiz ID.
- **Domain Concept:** Quiz Session Management
- **Entities:**
    - **User:** Represents a participant in the quiz.
        - Attributes: `userID`, `name`, `sessionID`
    - **Quiz Session:** Represents an ongoing quiz session.
        - Attributes: `sessionID`, `quizID`, `participants`
- **Value Object:** Quiz ID
    - Attributes: `quizID`
- **Services:**
    - **Quiz Joining Service:** Manages the process of users joining a quiz session.
        - Operations: `joinQuiz(sessionID, userID)`
- **Domain Events:**
    - `UserJoinedQuizSession`: Triggered when a user joins a quiz session.
        - Attributes: `userID`, `sessionID`, `timestamp`

**Requirement:** The system should support multiple users joining the same quiz session simultaneously.
- **Domain Concept:** Concurrent Participation Management
- **Entities:**
    - **User:** Already defined above.
    - **Quiz Session:** Already defined above.
- **Services:**
    - **Concurrent User Handling Service:** Manages the concurrent joining of multiple users to the same session.
        - Operations: `handleConcurrentJoin(sessionID, userIDs)`
- **Domain Events:**
    - `MultipleUsersJoinedQuizSession`: Triggered when multiple users join a quiz session simultaneously.
        - Attributes: `userIDs`, `sessionID`, `timestamp`

#### 2. Real-Time Score Updates

**Requirement:** As users submit answers, their scores should be updated in real-time.
- **Domain Concept:** Real-Time Scoring
- **Entities:**
    - **User:** Already defined above.
    - **Answer:** Represents an answer submitted by a user.
        - Attributes: `answerID`, `userID`, `questionID`, `answer`, `timestamp`
    - **Score:** Represents the score of a user.
        - Attributes: `scoreID`, `userID`, `points`, `timestamp`
- **Services:**
    - **Score Updating Service:** Manages the real-time update of scores.
        - Operations: `updateScore(userID, points)`
- **Domain Events:**
    - `ScoreUpdated`: Triggered when a user's score is updated.
        - Attributes: `userID`, `newScore`, `timestamp`

**Requirement:** The scoring system must be accurate and consistent.
- **Domain Concept:** Scoring Accuracy and Consistency
- **Entities:**
    - **Score:** Already defined above.
- **Services:**
    - **Scoring Accuracy Service:** Ensures the accuracy and consistency of the scoring system.
        - Operations: `validateScore(userID, expectedScore)`
- **Domain Events:**
    - `ScoreConsistencyChecked`: Triggered when the scoring system's consistency is validated.
        - Attributes: `userID`, `isValid`, `timestamp`

#### 3. Real-Time Leaderboard

**Requirement:** A leaderboard should display the current standings of all participants.
- **Domain Concept:** Leaderboard Management
- **Entities:**
    - **Leaderboard:** Represents the current standings of all participants.
        - Attributes: `leaderboardID`, `sessionID`, `standings`
- **Services:**
    - **Leaderboard Display Service:** Manages the display of the leaderboard.
        - Operations: `displayLeaderboard(sessionID)`
- **Domain Events:**
    - `LeaderboardUpdated`: Triggered when the leaderboard is updated.
        - Attributes: `leaderboardID`, `sessionID`, `timestamp`

**Requirement:** The leaderboard should update promptly as scores change.
- **Domain Concept:** Real-Time Leaderboard Updating
- **Entities:**
    - **Leaderboard:** Already defined above.
    - **Score:** Already defined above.
- **Services:**
    - **Leaderboard Update Service:** Updates the leaderboard promptly as scores change.
        - Operations: `updateLeaderboard(sessionID)`
- **Domain Events:**
    - `LeaderboardScoreChanged`: Triggered when a score change affects the leaderboard.
        - Attributes: `leaderboardID`, `sessionID`, `userID`, `newScore`, `timestamp`

### Aggregates and Relationships

#### Aggregates:
- **QuizAggregate:**
    - Root Entity: Quiz
    - Contained Entities: QuizSession, User
- **ScoreAggregate:**
    - Root Entity: Score
    - Contained Entities: User, Answer
- **LeaderboardAggregate:**
    - Root Entity: Leaderboard
    - Contained Entities: User, Score

### Relationships:
- **Quiz -> QuizSession:** A quiz can have multiple sessions.
- **QuizSession -> User:** A session can have multiple users.
- **User -> Score:** A user can have multiple scores over different sessions.
- **Score -> Answer:** Each score is composed of answers provided by the user.
- **Leaderboard -> User:** A leaderboard tracks the scores of multiple users.
- **Leaderboard -> Score:** A leaderboard is updated based on the changes in scores.

### Detailed Workflow

1. **User Participation:**
    - A user initiates a request to join a quiz session by providing a unique quiz ID.
    - The Quiz Joining Service validates the quiz ID and adds the user to the Quiz Session.
    - The system triggers the `UserJoinedQuizSession` event.
    - Multiple users can join the session concurrently, managed by the Concurrent User Handling Service, which ensures data consistency and triggers `MultipleUsersJoinedQuizSession`.

2. **Real-Time Score Updates:**
    - As users submit their answers, the Score Updating Service processes these answers.
    - The user's score is calculated and updated in real-time.
    - The system triggers the `ScoreUpdated` event to reflect this change.
    - The Scoring Accuracy Service continuously validates the scores to ensure accuracy and consistency, triggering `ScoreConsistencyChecked` events as needed.

3. **Real-Time Leaderboard:**
    - The Leaderboard Display Service queries the current scores and displays the standings.
    - Whenever a score changes, the Leaderboard Update Service updates the leaderboard in real-time.
    - The system triggers `LeaderboardUpdated` and `LeaderboardScoreChanged` events to ensure the display is current and accurate.

### Conclusion

This detailed analysis provides a comprehensive view of how the acceptance criteria can be modeled using Domain-Driven Design principles. It includes a clear breakdown of domain concepts, entities, services, aggregates, and domain events, ensuring that the system is both robust and maintainable.

# System Design for a Quiz Application
---
![elsa_system_design.drawio.png](images%2Felsa_system_design.drawio.png)

The provided diagram illustrates a comprehensive system architecture that integrates multiple services, databases, and monitoring tools within an AWS environment. Here's a detailed explanation of each component and their interactions:

1. **AWS Cloud Services:**
    - **Route 53**: This is AWS’s DNS service, handling domain name resolution for the system.
    - **API Gateway**: It provides a unified API front for multiple backend services, including Quiz Service, Scoring Service, and Leaderboard Service.
    - **Lambda Functions**: Serverless functions for various operations like authorizing requests (AuthLambda) and updating scores and standings (Update Score, Update Standing).
    - **VPC (Virtual Private Cloud)**: This isolates and secures the environment for running the services.

2. **Backend Services (BFF - Backend for Frontend):**
    - **Quiz Service**: Manages quiz-related operations.
    - **Scoring Service**: Handles score calculations and updates.
    - **Leaderboard Service**: Manages leaderboard updates and standings.
    - **Containers**: The services run in Docker containers orchestrated by AWS services, ensuring scalability and manageability.

3. **Authentication and Authorization:**
    - **Cognito**: AWS’s service for user authentication and authorization.
    - **Lambda Authorizer**: A custom authorizer function for managing authentication logic before requests reach the API Gateway.

4. **Databases:**
    - **PostgreSQL**: Used for persistent storage of quiz, scoring, and leaderboard data. Each service has its dedicated database instance within a private subnet for security.
    - **Redis**: Used for caching and real-time data handling, ensuring quick access to frequently used data.

5. **Private Subnet:**
    - **EC2 Instances**: Each service has its EC2 instance for more control over the environment, running the Quiz, Scoring, and Leaderboard services.
    - **Security**: These instances are placed within a private subnet to restrict direct internet access, enhancing security.

6. **Logging and Monitoring:**
    - **FluentBit**: Collects logs from various services.
    - **Datadog**: Aggregates logs and metrics for monitoring and alerting.
    - **Prometheus**: Used for collecting metrics.
    - **Grafana**: Provides dashboards for visualizing metrics and logs.
    - **Slack**: Integrated for sending alerts and notifications to the development and operations teams.

7. **Developer Interaction:**
    - **SSO (Single Sign-On)**: Developers authenticate through a company SSO system.
    - **SSH Tunnel**: Secure access to the private subnets and EC2 instances for maintenance and updates.

8. **Event Handling and Synchronization:**
    - **GraphQL**: Used for updating the leaderboard in real-time, ensuring that changes in scores and standings are immediately reflected.
    - **Real-time Handling**: Managed through Lambda functions and a real-time database to handle updates promptly and efficiently.

### Key Processes:
- **User Interaction**: Devices interact with the system via APIs exposed by the API Gateway.
- **Authorization**: Requests are authenticated through Cognito and the Lambda Authorizer.
- **Service Coordination**: Backend services (Quiz, Scoring, Leaderboard) process requests and update the databases.
- **Real-time Updates**: Changes in scores and standings are handled in real-time using GraphQL and Lambda functions.
- **Monitoring and Alerts**: FluentBit, Datadog, Prometheus, and Grafana monitor system health, with alerts sent to Slack for quick response.

This architecture ensures a secure, scalable, and efficient environment for running a quiz application with real-time scoring and leaderboard updates, along with robust monitoring and alerting mechanisms.
# CI/CD Pipeline for a Quiz Application
![elsa_system_assignments.drawio.png](images%2Felsa_system_assignments.drawio.png)

# Database design
---
To design the database for the quiz application, we will create tables that represent the core entities: users, quiz sessions, answers, scores, and the leaderboard. Below is the SQL code to create these tables, along with their relationships.

### Database Schema
![elsa_database_design.png](images%2Felsa_database_design.png)

```sql
-- Users table to store user information
CREATE TABLE Users (
    ID VARCHAR(36) PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    SessionID VARCHAR(36)
);

-- QuizSessions table to store quiz session information
CREATE TABLE QuizSessions (
    SessionID VARCHAR(36) PRIMARY KEY,
    QuizID VARCHAR(36) NOT NULL,
    Participants TEXT -- Could be a JSON array of user IDs
);

-- Answers table to store user answers
CREATE TABLE Answers (
    AnswerID VARCHAR(36) PRIMARY KEY,
    UserID VARCHAR(36) NOT NULL,
    QuestionID VARCHAR(36) NOT NULL,
    Answer TEXT NOT NULL,
    Timestamp TIMESTAMP NOT NULL,
    FOREIGN KEY (UserID) REFERENCES Users(ID)
);

-- Scores table to store user scores
CREATE TABLE Scores (
    ScoreID VARCHAR(36) PRIMARY KEY,
    UserID VARCHAR(36) NOT NULL,
    Points INT NOT NULL,
    Timestamp TIMESTAMP NOT NULL,
    FOREIGN KEY (UserID) REFERENCES Users(ID)
);

-- Leaderboard table to store the leaderboard standings
CREATE TABLE Leaderboard (
    LeaderboardID VARCHAR(36) PRIMARY KEY,
    SessionID VARCHAR(36) NOT NULL,
    UserID VARCHAR(36) NOT NULL,
    Rank INT NOT NULL,
    Points INT NOT NULL,
    FOREIGN KEY (SessionID) REFERENCES QuizSessions(SessionID),
    FOREIGN KEY (UserID) REFERENCES Users(ID)
);
```

### Explanation of the Tables

1. **Users Table**
    - **ID**: Unique identifier for each user.
    - **Name**: The name of the user.
    - **SessionID**: The ID of the session the user is participating in (nullable, as the user may not always be in a session).

2. **QuizSessions Table**
    - **SessionID**: Unique identifier for each quiz session.
    - **QuizID**: Identifier for the quiz.
    - **Participants**: A text field (or JSON) containing the IDs of users participating in the session.

3. **Answers Table**
    - **AnswerID**: Unique identifier for each answer.
    - **UserID**: The ID of the user who submitted the answer.
    - **QuestionID**: The ID of the question being answered.
    - **Answer**: The actual answer text.
    - **Timestamp**: The time when the answer was submitted.

4. **Scores Table**
    - **ScoreID**: Unique identifier for each score entry.
    - **UserID**: The ID of the user to whom the score belongs.
    - **Points**: The score points.
    - **Timestamp**: The time when the score was recorded.

5. **Leaderboard Table**
    - **LeaderboardID**: Unique identifier for each leaderboard entry.
    - **SessionID**: The ID of the session to which the leaderboard belongs.
    - **UserID**: The ID of the user.
    - **Rank**: The rank of the user in the leaderboard.
    - **Points**: The points scored by the user.

### Indexes

To optimize the performance of the database, especially for queries that are frequently executed, we can add indexes:

```sql
CREATE INDEX idx_users_sessionid ON Users (SessionID);
CREATE INDEX idx_answers_userid ON Answers (UserID);
CREATE INDEX idx_scores_userid ON Scores (UserID);
CREATE INDEX idx_leaderboard_sessionid ON Leaderboard (SessionID);
CREATE INDEX idx_leaderboard_userid ON Leaderboard (UserID);
```

### Relationships and Foreign Keys

The foreign key constraints ensure referential integrity:

- `Answers` table references the `Users` table through `UserID`.
- `Scores` table references the `Users` table through `UserID`.
- `Leaderboard` table references the `QuizSessions` table through `SessionID` and the `Users` table through `UserID`.

This database schema design ensures the core entities are well-defined and their relationships are maintained, which aligns with the requirements of the quiz application.

# Video Explanation
---
[Video Submission](https://drive.google.com/file/d/13iCAh_BVJnERSxhY4y9pPSe3mivLCSql/view?usp=sharing)
