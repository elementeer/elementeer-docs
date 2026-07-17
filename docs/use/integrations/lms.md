# LMS Platforms Integration

Elementeer integrates with WordPress Learning Management Systems — LearnDash and Tutor LMS. Your AI agent can detect active LMS platforms, analyze course structures, and manage course content.

## Supported Plugins

| Plugin | Detection | Capabilities |
|--------|-----------|-------------|
| **LearnDash** | sfwd-lms | Course detection, lesson/quiz structure, user enrollment |
| **Tutor LMS** | tutor | Course detection, lesson structure, instructor info |

## LearnDash Integration

LearnDash is a comprehensive LMS plugin. Elementeer auto-detects it and provides structured course analysis:

```
Check if LearnDash is installed and analyze the course structure.
```

### Detection and Status

```json
{
  "learndash": {
    "active": true,
    "version": "4.15",
    "courses": 8,
    "lessons": 94,
    "quizzes": 32,
    "enrolled_users": 156
  }
}
```

### Course Structure Analysis

```
Show me the full structure of the "Web Development Fundamentals" course.
```

```json
{
  "course": {
    "id": 45,
    "title": "Web Development Fundamentals",
    "status": "publish",
    "sections": [
      {
        "title": "Introduction",
        "order": 1,
        "lessons": [
          {
            "id": 201,
            "title": "Welcome to Web Development",
            "type": "lesson",
            "duration": "15 min",
            "topics": [
              { "id": 301, "title": "What is HTML?", "type": "topic" },
              { "id": 302, "title": "Setting Up Your Environment", "type": "topic" }
            ]
          },
          {
            "id": 202,
            "title": "HTML Basics Quiz",
            "type": "quiz",
            "questions": 10,
            "passing_score": 80
          }
        ]
      },
      {
        "title": "CSS Foundations",
        "order": 2,
        "lessons": []
      }
    ]
  }
}
```

### Course Inventory

```
List all published LearnDash courses with lesson and quiz counts.
```

```json
{
  "courses": [
    {
      "id": 45,
      "title": "Web Development Fundamentals",
      "lessons": 24,
      "quizzes": 8,
      "enrolled": 89,
      "status": "publish"
    },
    {
      "id": 46,
      "title": "Advanced JavaScript",
      "lessons": 32,
      "quizzes": 12,
      "enrolled": 45,
      "status": "publish"
    }
  ]
}
```

### Lesson and Quiz Management

```
List all lessons in course ID 45 grouped by section.
```

```
Show quiz details for quiz ID 202 — question types, passing score, and prerequisites.
```

### Enrollment

```
How many users are enrolled in "Web Development Fundamentals"?
```

```json
{
  "course_id": 45,
  "total_enrolled": 89,
  "in_progress": 52,
  "completed": 37,
  "completion_rate": "41.6%"
}
```

## Tutor LMS Integration

### Course Detection

```
List all Tutor LMS courses with their instructors.
```

```json
{
  "courses": [
    {
      "id": 12,
      "title": "Digital Marketing Masterclass",
      "instructor": "Sarah Chen",
      "lessons": 18,
      "duration": "4h 30m",
      "level": "intermediate",
      "enrolled": 234
    }
  ]
}
```

### Instructor Information

```
Show details for the instructor "Sarah Chen" — courses, total students, ratings.
```

### Content Structure

Tutor LMS courses are organized as topics containing lessons. Elementeer traverses this structure:

```
Show the topic-by-topic breakdown of course ID 12.
```

## LMS Architecture Analysis

Beyond individual plugin features, Elementeer provides cross-LMS analysis:

```
Analyze the LMS content structure: which courses have the highest completion rates, 
and where do students tend to drop off?
```

The agent reads course structure, enrollment data, and quiz results to provide actionable insights.

## Content Integration with Elementor

LMS courses often use Elementor for landing pages and lesson content. Elementeer bridges these:

```
List all Elementor templates related to LMS content (course pages, lesson templates, etc.).
```

```
Update the course landing page template to use the new brand colors.
```

## Governance

LMS operations follow Elementeer's standard governance:

- **L0:** Reading course structures, lesson content, quiz data
- **L1:** Updating lesson content, course metadata
- **L2:** Modifying quiz questions, enrollment management
- **L3:** Deleting courses, resetting enrollment data
