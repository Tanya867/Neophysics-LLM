Neophysics LLM – Multi-Agent Tutor System
Table of Contents

Project Overview

Live Demo

Screenshots

Key Features

Architecture

Directory Structure

Setup & Installation

Configuration

Usage Guide

Development Playbook

Deployment

Best Practices

Contributing

FAQ

Challenges & Solutions

References
Project Overview

Neophysics LLM (Tutor Agent) is an AI-powered educational assistant built using a multi-agent, multi-turn architecture. It specializes in providing step-by-step tutoring for Mathematics and Physics, with an easily extensible design for adding more domains.

It uses:

Google Gemini API for intelligent reasoning

MongoDB for conversation persistence

Redis for caching and rate limiting

Flask as backend and React as frontend

The Tutor Agent intelligently routes every query to the most suitable specialist agent (Math, Physics, etc.) and uses tools like calculators and knowledge bases to generate accurate and transparent answers.

Live Demo

👉 Visit Website: https://ai-tuto.vercel.app/

Screenshots




Key Features
1. Smart Routing

Auto-detects subject from user query

Selects the right specialist agent

Switches agents smoothly when needed

Multi-agent collaboration for complex tasks

2. Specialist Agents

Math Agent: Algebra, calculus, equations

Physics Agent: Concepts, laws, formulas

Easily extendable for new domains

3. Multi-Turn Conversation Handling

Maintains full context

Allows follow-up questions

Conversation history stored in MongoDB

4. Rate Limiting (Redis)

Prevents API abuse

Per user/IP configuration

User-friendly limit-exceeded messages

5. Redis Caching

Fast response caching

Temporary session storage

Customizable TTL policies

Architecture
Frontend (React)
       ⬇
Backend API (Flask)
       ⬇
Tutor Agent (Router)
  ├── Math Agent
  ├── Physics Agent
  └── Future Agents
       ⬇
Tools (Calculator, Knowledge Base, Physics Constants)
       ⬇
Services: Gemini API, MongoDB, Redis


Frontend: React SPA UI

Backend: Flask REST API managing routing & context

Agents: Subject-specific logic

Tools: Modular utilities for real-time calculations

Databases:

MongoDB → Conversations

Redis → Rate limit + caching

LLM: Google Gemini 1.5

Directory Structure
tutor-agent/
├── backend/
│   ├── app.py
│   ├── run.py
│   ├── agents/
│   │   ├── base_agent.py
│   │   ├── tutor_agent.py
│   │   ├── math_agent.py
│   │   └── physics_agent.py
│   ├── tools/
│   │   ├── calculator.py
│   │   ├── knowledge_base.py
│   │   └── physics_constants.py
│   ├── utils/
│   ├── data/
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   ├── public/
│   └── package.json
│
├── .env.example
└── README.md

Setup & Installation
Prerequisites

Python 3.9+

Node.js 16+

MongoDB (local/Atlas)

Redis

Google Gemini API key

Backend Setup
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python3 run.py

Frontend Setup
cd frontend
npm install
npm start

Configuration

Rename .env.example → .env and fill in:

GEMINI_API_KEY=
MONGODB_URI=
DATABASE_NAME=
REDIS_HOST=
REDIS_USERNAME=
REDIS_PASSWORD=
REDIS_PORT=


Set REACT_APP_API_URL for frontend-backend communication.

Usage Guide

Start backend & frontend

Open: http://localhost:3000

Enter a question like:

Solve 2x + 3 = 9

Explain Newton’s Second Law

System flow:

Analyze → Route → Use tools → Generate answer

Manage conversations from sidebar:

View

Continue

Delete

Development Playbook
Add a New Agent

Create file under backend/agents/

Inherit BaseAgent

Implement:

identify_subject()

process_question()

Register in TutorAgent

Add a New Tool

Create file in backend/tools/

Inherit BaseTool

Implement execute()

Register tool inside agent constructor

API Endpoints (Summary)
✔ Health Check

GET /health

✔ Ask a Question

POST /ask
Body:

{
  "question": "",
  "user_id": "",
  "conversation_id": ""
}

✔ Conversations

GET /conversations

GET /conversations/<id>

DELETE /conversations/<id>

Deployment

Backend: Render / Railway / Docker

Frontend: Vercel

Secrets: Environment variables stored in each platform

Persistent DB: MongoDB Atlas

Cache: Redis Cloud

Best Practices

Modular codebase

Use .env.example to document config

Follow semantic commits

Use protected routes for production

Keep logs clean and structured

Monitor API rate usage

Cache expensive operations

Contributing

Fork repo

Create feature branch

Commit changes

Open Pull Request with clear explanation

FAQ

Q: How do I add new subjects?
Create a new agent and register it in Tutor Agent.

Q: Where is conversation history stored?
MongoDB (per user + session).

Q: How do I get a Gemini API key?
Visit Google AI Studio.

Challenges & Solutions
1. LLM Prompt Reliability

Problem: Unstructured or inconsistent responses
Solution:

Stable prompt templates

Strict JSON parsing & error handling

2. Multi-Turn Conversation Memory

Problem: Maintaining long contextual chats
Solution:

MongoDB for message history

Redis for quick session lookup

3. Fast and Safe API Requests

Problem: Risk of overuse or slow responses
Solution:

Redis-based rate limiting

Response caching

References

Google Gemini Docs

Flask Documentation

React Documentation

Maintainer

Tanya
LinkedIn: www.linkedin.com/in/tanyakanojiya
