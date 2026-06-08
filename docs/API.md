# CodePath API Documentation

## Base URL
```
http://localhost:5000/api
```

## Authentication
All protected endpoints require a JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

## Endpoints

### Auth

#### Register User
```
POST /auth/register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "secure_password",
  "full_name": "John Doe"
}
```

#### Login
```
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "secure_password"
}

Response:
{
  "token": "eyJ0eXAiOiJKV1QiLCJhbGc...",
  "user": { ... }
}
```

#### Get Current User
```
GET /auth/me
Authorization: Bearer <token>
```

### Courses

#### Get All Courses
```
GET /courses?level=beginner&language=python
```

#### Get Course Details
```
GET /courses/:id
```

#### Create Course (Admin)
```
POST /courses
Authorization: Bearer <admin_token>
Content-Type: application/json

{
  "title": "Python Basics",
  "description": "Learn Python fundamentals",
  "level": "beginner",
  "language": "python",
  "duration_weeks": 4
}
```

### Lessons

#### Get Course Lessons
```
GET /lessons?course_id=1
```

#### Get Lesson Details
```
GET /lessons/:id
```

#### Complete Lesson
```
POST /lessons/:id/complete
Authorization: Bearer <token>
```

### Challenges

#### Get Course Challenges
```
GET /challenges?course_id=1
```

#### Get Challenge Details
```
GET /challenges/:id
```

#### Submit Challenge Solution
```
POST /challenges/:id/submit
Authorization: Bearer <token>
Content-Type: application/json

{
  "code": "console.log('Hello');"
}

Response:
{
  "passed": true,
  "passed_tests": 5,
  "total_tests": 5,
  "execution_time": 45
}
```

#### Get Leaderboard
```
GET /challenges/:id/leaderboard
```

### Users

#### Get User Profile
```
GET /users/:id
```

#### Update User Profile
```
PUT /users/:id
Authorization: Bearer <token>
Content-Type: application/json

{
  "full_name": "John Doe Updated",
  "bio": "Passionate learner"
}
```

#### Get User Progress
```
GET /users/:id/progress
Authorization: Bearer <token>
```

## Error Responses

All error responses follow this format:
```json
{
  "status": "error",
  "message": "Error description"
}
```

## Rate Limiting
- 100 requests per minute per IP address
- 1000 requests per hour per user

## WebSocket Events

### Connection
```javascript
const socket = io('http://localhost:5000');
```

### Events
- `code-execution`: Execute code in real-time
- `lesson-progress`: Update lesson progress
- `challenge-submitted`: Submit challenge solution
