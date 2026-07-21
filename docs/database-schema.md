# Database Schema

## User

| Column | Type | Constraints | Notes |
| --- | --- | --- | --- |
| id | Integer | PK, autoincrement | |
| name | String(100) | not null | |
| email | String(120) | unique, not null | used for login |
| password_hash | String(255) | not null | never store raw passwords |
| role | Enum(student, admin) | default='student' | determines access to admin catalog endpoints |
| created_at | DateTime | default=now | |

## AssessmentResult

| Column | Type | Constraints | Notes |
| --- | --- | --- | --- |
| id | Integer | PK | |
| user_id | Integer | FK → User.id | One-to-many: one User → many AssessmentResults |
| skill_scores | JSON/Text | not null | tag:score pairs, e.g. `{"analytical": 8, "creative": 5}` |
| personality_scores | JSON/Text | not null | same tag-based structure |
| completed_at | DateTime | default=now | |

## Career

| Column | Type | Constraints | Notes |
| --- | --- | --- | --- |
| id | Integer | PK | |
| title | String(120) | not null | |
| description | Text | | |
| industry | String(100) | | used for filtering/display |
| tag_weights | JSON/Text | not null | drives the matching algorithm |

## Roadmap

| Column | Type | Constraints | Notes |
| --- | --- | --- | --- |
| id | Integer | PK | |
| career_id | Integer | FK → Career.id | One-to-many: one Career → many Roadmap steps |
| step_title | String(150) | not null | |
| resource_link | String(255) | | external learning resource URL |
| step_order | Integer | not null | controls display sequence |

## SavedCareer (join table)

| Column | Type | Constraints | Notes |
| --- | --- | --- | --- |
| id | Integer | PK | |
| user_id | Integer | FK → User.id | |
| career_id | Integer | FK → Career.id | |
| status | Enum(saved, in_progress, completed) | default='saved' | tracks the student's progress on this match |
| saved_at | DateTime | default=now | |

This table is what makes User ↔ Career a many-to-many relationship — a student can save multiple careers, and a career can be saved by multiple students.

## Relationship Summary

```
User (1) ──< (many) AssessmentResult
Career (1) ──< (many) Roadmap
User (many) ──< SavedCareer >── (many) Career
```