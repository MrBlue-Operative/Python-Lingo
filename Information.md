# Project Blueprint: Python Learning Platform (SaaS)

## Project Vision

Build a self-paced Python learning platform that combines the structured learning experience of Codecademy with the practice-driven approach of LeetCode.

**Core Promise:**

> "Learn Python by doing, from absolute beginner to a complete Machine Learning project."

The platform is intended primarily for the Pakistani market, offering an affordable, structured alternative to scattered free resources.

---

## Business Idea

### Target Audience

* Beginners wanting to learn Python.
* Students interested in AI and Machine Learning.
* Pakistani learners looking for an affordable structured course.

### Pricing Strategy

* **Free Trial**
* First 1 to 2 lessons.
* First 10 coding problems.


* **Paid Plan**
* Approximately Rs.699.
* Remaining lessons.
* Remaining 90+ coding challenges.



Future premium tiers can be added later, but the MVP launches with a single paid plan.

### Main Selling Point

Unlike YouTube, which provides information without structure, this platform forces learners to progress step by step.

**Key differentiators:**

* Locked progression.
* Interactive coding exercises.
* Hidden test cases.
* LeetCode-style challenges.
* Full roadmap ending in a Machine Learning project.
* Curriculum specifically designed for beginners.

The platform should feel more like a GPS than a content library.

---

## Market Analysis

### Strengths

* Strong demand for Python and AI education in Pakistan.
* Affordable pricing.
* Structured curriculum solves beginner confusion.
* Existing teaching experience (Preply) provides initial credibility.

### Biggest Competition

The real competitor is free content, including:

* YouTube
* freeCodeCamp
* CS50
* Codecademy free version
* Coursera financial aid
* ChatGPT

Therefore, the product must sell structure, not information.

### Estimated Rating

| Area | Assessment |
| --- | --- |
| Demand | High |
| Competition | Very High |
| Monetization | Good |
| Technical Feasibility | High |
| Overall Potential | Good if execution is strong |

---

## Major Risks

### 1. Low Completion Rate

Most learners abandon courses.

**Solution:**

* XP
* Streaks
* Badges
* Locked lessons
* Daily challenges

### 2. Trust

Unknown creators struggle to sell.

**Advantage:**

* Existing tutoring experience.
* Student reviews.
* Real teaching background.

### 3. Customer Acquisition

Marketing costs can destroy profits.

**Recommendation:**

* Focus heavily on organic content.
* Use Preply students.
* Short-form educational videos.
* Referrals.

---

## Financial Estimates

### Revenue Example

If:

* 100,000 people see marketing.
* 5% visit.
* 5% purchase.

Result:

* 5,000 visitors.
* 250 purchases.
* Revenue around Rs.175,000 before expenses.

---

## Project Feasibility

### Can One Person Build It?

Yes.

The MVP is achievable by a single developer.

Important advice:

* Build an MVP first instead of attempting a full LeetCode clone.

### Development Timeline

| Stage | Estimated Time |
| --- | --- |
| MVP | 3 to 5 months |
| Polished Version | 6 to 12 months |

**Assumption:**

* Approximately 3 to 4 hours of work daily.

---

## Initial Costs

### One-Time
```````````````````                                                                                                                                                         
| Item | Cost |
| --- | --- |
| Domain | Rs.3,000 to Rs.5,000/year |

### Monthly

| Item | Cost |
| --- | --- |
| VPS | Rs.2,000 to Rs.5,000 |
| Domain Equivalent | Rs.250 to Rs.400 |
| SSL | Free |
| PostgreSQL | Free |   
| Judge0 | Free |
| Docker | Free |
| Redis | Free |
| GitHub | Free |

Expected monthly cost: Rs.2,500 to Rs.8,000

No paid APIs are required for the MVP.

---

## Technology Stack

| Layer | Technology |
| --- | --- |
| Frontend | Next.js |
| Styling | Tailwind CSS |
| Backend | FastAPI |
| Database | PostgreSQL |
| Authentication | JWT |
| Code Execution | Judge0 |
| Containerization | Docker |
| Queue | Redis |
| Deployment | Ubuntu VPS |

**Reasoning:**

* Python-first ecosystem.
* Modern frontend.
* Fast backend.
* Mostly free.

---

## System Architecture

High-level flow:

1. Student opens website.
2. Frontend communicates with FastAPI.
3. FastAPI:
* stores data in PostgreSQL,
* sends execution requests to Judge0,
* uses Redis for queued jobs.


4. Results return to the user.

The browser never communicates directly with the database or execution engine.

### PostgreSQL Hosting Clarification

"Self-hosted PostgreSQL" means:

* PostgreSQL runs on the rented VPS.
* The laptop is not the production database.
* The laptop can be turned off.
* The VPS remains online 24/7.

**Production server responsibilities:**

* Next.js
* FastAPI
* PostgreSQL
* Judge0
* Redis

All run continuously on the VPS.

---

## Online Python Interpreter

### Is It Feasible?

Yes.

The interpreter should not execute code directly on the backend process.

Instead:

1. FastAPI sends code to Judge0.
2. Judge0 launches an isolated Docker container.
3. Python executes inside the container.
4. Container is destroyed afterward.

This is similar to platforms like:

* LeetCode
* HackerRank
* Codewars

### Safety Measures

Every execution should have:

* No internet access.
* Memory limits.
* Time limits.
* Container isolation.
* Automatic destruction after execution.
* Rate limiting.

This prevents malicious or infinite-loop code.

### Can One Server Handle Many Users?

Initially, yes.

Important distinction:

* The challenge is concurrent executions, not total daily submissions.

**Future scaling path:**

* Queue submissions.
* Multiple workers process jobs.
* Separate Judge0 server.
* Separate database server.
* Horizontal scaling later.

---

## Core Platform Features

### Authentication

* Signup
* Login
* Premium access
* JWT authentication

### Dashboard

Displays:

* Current lesson
* XP
* Streak
* Progress
* Locked content

### Course System

Structure:

* Lesson
* Explanation
* Examples
* Exercise
* Hidden tests
* Unlock next lesson

Progression remains locked until completion.

### Coding Playground

Each lesson includes:

* Code editor
* Instructions
* Run button
* Submit button
* Output window
* Hidden test evaluation

### LeetCode-Style Problems

Each problem contains:

* Title
* Difficulty
* Topic
* Starter code
* Hidden tests

Problems appear exactly when relevant in the curriculum.

**Example progression:**

* Variables
* Strings
* Loops
* Functions
* OOP
* Machine Learning

---

## Database Design

### Users

* `id`
* `name`
* `email`
* `password`
* `premium`
* `streak`
* `xp`

### Lessons

* `id`
* `title`
* `order`
* `content`
* `premium`

### Problems

* `id`
* `lesson_id`
* `title`
* `difficulty`
* `starter_code`
* `hidden_tests`

### Submissions

* `id`
* `user_id`
* `problem_id`
* `code`
* `result`
* `runtime`
* `timestamp`

### Progress

* `user_id`
* `lesson_id`
* `completed`

---

## Project Structure

Suggested folders:

```text
project/
├── frontend/
├── backend/
├── judge0/
├── database/
├── docker/
└── nginx/

```

Each component remains independent.

---

## Deployment Plan

Everything initially lives on one Ubuntu VPS.

**Server hosts:**

* Nginx
* Next.js
* FastAPI
* Judge0
* PostgreSQL

One server is sufficient for the first few hundred users.

---

## MVP Feature Priority

Build in this order.

| Phase | Feature |
| --- | --- |
| 1 | Authentication |
| 2 | Dashboard |
| 3 | Course System |
| 4 | Code Editor |
| 5 | Judge0 Integration |
| 6 | Progress Tracking |
| 7 | Around 50 Problems |
| 8 | Payment Integration |
| 9 | Testing |
| 10 | Launch |

Do not build advanced features before launch.

---

## Future Features

After validation:

* AI hints
* Competitive contests
* Multiple programming languages
* Separate execution servers
* Cloud storage
* Premium plans

---

## Branding Insight

Instead of positioning it as:

> "LeetCode + Codecademy"

A clearer positioning is:

> "Duolingo for Python."

It immediately communicates:

* structured lessons,
* mandatory practice,
* visible progression,
* beginner-friendly learning.

---

## Final Philosophy

The MVP should not aim to become the next LeetCode immediately.

Instead, build the smallest version that delivers the core promise:

A beginner can join, complete guided lessons, solve progressively unlocked coding challenges, and finish with a real Machine Learning project, all on one affordable platform.

Everything else can evolve after the first paying customers validate the idea.