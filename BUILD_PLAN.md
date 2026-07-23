# FY Project Build Plan

## 1. Purpose

This document defines the exact implementation steps for the Developer Intelligence Platform. It is written so a coding agent can understand:
- what to build
- how to build it
- what files and modules are required
- how components should interact

## 2. Project Overview

The project is an AI-powered Developer Intelligence Platform that analyzes GitHub profiles, repositories, resumes, and candidate information to deliver engineering insights, recommendations, README generation, and recruiter intelligence.

Core capabilities:
- GitHub repository and profile analysis
- AI-driven engineering intelligence
- Resume validation
- README and profile generation
- Recruiter dashboard and candidate scoring
- CI/CD and deployment automation

## 3. Technology Stack

Backend:
- Python
- FastAPI
- SQLAlchemy
- Pydantic
- Celery
- Redis
- PostgreSQL

Frontend:
- Next.js
- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- React Query or SWR
- Zustand

AI:
- OpenAI API
- Embeddings
- Prompt orchestration
- Agent-based AI orchestration

Infrastructure:
- Docker
- Docker Compose
- GitHub Actions
- Vercel / cloud hosting
- S3-compatible storage
- Redis cache

## 4. Required Project Structure

Root folders:
- `backend/`
- `frontend/`
- `infra/`
- `docs/`
- `tests/`

Suggested files:
- `backend/app/main.py`
- `backend/app/api/routers/*.py`
- `backend/app/models/*.py`
- `backend/app/schemas/*.py`
- `backend/app/services/*.py`
- `backend/app/ai/*.py`
- `backend/app/tasks/*.py`
- `backend/Dockerfile`
- `frontend/package.json`
- `frontend/app/page.tsx`
- `frontend/components/*.tsx`
- `frontend/utils/*.ts`
- `infra/docker-compose.yml`
- `infra/backend.env`
- `infra/frontend.env`
- `BUILD_PLAN.md`

## 5. Step-by-step Implementation

### Step 1 - Setup Repository and Environment

1. Create project root structure.
2. Initialize Git and confirm `main` branch.
3. Create `.gitignore` for Python, Node, Docker.
4. Add `README.md` with high-level project summary.
5. Create `BUILD_PLAN.md`.

### Step 2 - Backend Boilerplate

1. Create Python virtual environment.
2. Install dependencies:
   - fastapi
   - uvicorn
   - sqlalchemy
   - asyncpg
   - pydantic
   - celery
   - redis
   - python-dotenv
   - httpx
   - openai
3. Create `backend/app/main.py` with FastAPI app instance.
4. Add `backend/app/core/config.py` to load env variables.
5. Add `backend/app/db/session.py` to initialize SQLAlchemy engine and session.
6. Add models:
   - `User`
   - `Project`
   - `RepositoryAnalysis`
   - `Resume`
   - `Candidate`
   - `AnalysisReport`
7. Add schemas using Pydantic for request/response validation.
8. Add routers:
   - `auth.py`
   - `github.py`
   - `analysis.py`
   - `resume.py`
   - `recruiter.py`
9. Add service modules:
   - `github_service.py`
   - `analysis_service.py`
   - `resume_service.py`
   - `recruiter_service.py`
10. Add utility modules:
   - `security.py`
   - `github_client.py`
   - `openai_client.py`
   - `storage.py`

### Step 3 - AI Intelligence Layer

1. Create `backend/app/ai/orchestrator.py` for agent coordination.
2. Create specialized agent modules:
   - `repo_intelligence_agent.py`
   - `resume_validation_agent.py`
   - `readme_generation_agent.py`
   - `career_insights_agent.py`
3. Define prompt templates for each agent.
4. Add evidence extraction logic:
   - convert GitHub repo metadata to facts
   - parse README and CI files
   - validate resume claims against repo evidence
5. Add `backend/app/ai/utils.py` for embeddings and answer formatting.
6. Add `backend/app/services/ai_service.py` to invoke orchestrator and return results.

### Step 4 - GitHub Data Integration

1. Create GitHub client with OAuth or PAT support.
2. Add endpoints to fetch:
   - user profile
   - repositories
   - README contents
   - commits and languages
   - CI/CD config files
3. Normalize data into structured objects.
4. Add DB write logic to store scan results.
5. Add caching with Redis for repeated requests.

### Step 5 - Resume and Candidate Data

1. Add resume upload endpoint.
2. Add parser for resume text and PDF if required.
3. Create schema for resume fields:
   - education
   - experience
   - skills
   - roles
4. Build resume validation flow:
   - compare claims to GitHub repo evidence
   - generate confidence score

### Step 6 - Frontend Application

1. Initialize Next.js app.
2. Install dependencies:
   - react
   - next
   - typescript
   - tailwindcss
   - shadcn/ui
   - react-query or swr
   - axios
   - lucide-react
3. Create pages and routes:
   - `/` home/dashboard
   - `/login`
   - `/profile`
   - `/analysis`
   - `/resume`
   - `/recruiter`
4. Build UI components:
   - header/navigation
   - analysis cards
   - repo summary list
   - AI insight panel
   - candidate filter table
   - resume upload form
5. Create data services:
   - `frontend/utils/api.ts`
   - hooks for fetching backend endpoints
6. Connect with backend endpoints.
7. Add state management for auth and selected candidate.

### Step 7 - Background Task Processing

1. Setup Celery with Redis broker.
2. Add worker tasks:
   - `fetch_github_data`
   - `run_ai_analysis`
   - `generate_readme`
   - `validate_resume`
3. Call tasks asynchronously from API endpoints.
4. Add status tracking in DB for task progress.

### Step 8 - Testing

1. Backend tests:
   - unit tests for services, AI prompt logic, schema validation
   - integration tests for API endpoints
2. Frontend tests:
   - component rendering
   - page flows
3. Add CI test commands:
   - `pytest`
   - `npm test`
4. Add mocks for OpenAI and GitHub API calls.

### Step 9 - CI/CD

1. Create `.github/workflows/backend.yml`
2. Create `.github/workflows/frontend.yml`
3. Create `.github/workflows/integration.yml`
4. CI steps:
   - install dependencies
   - lint
   - type check
   - run tests
   - build Docker images
   - run security scans
   - deploy on successful main branch
5. Add secrets for OpenAI, GitHub, DB, and deploy targets.

### Step 10 - Deployment

1. Add Dockerfiles:
   - `backend/Dockerfile`
   - `frontend/Dockerfile`
2. Create `infra/docker-compose.yml` for local development:
   - backend
   - frontend
   - postgres
   - redis
   - celery
3. Add deployment manifests if using cloud provider.
4. Deploy frontend to Vercel or static host.
5. Deploy backend to cloud host with PostgreSQL and Redis.
6. Configure environment variables and secrets.

## 6. Detailed Build Flow for Coding Agent

The coding agent should follow this order:

1. Read the project vision and requirements files:
   - `01_Project_Vision.md`
   - `02_PRD.md`
   - `03-Trd/part1`..`part4`
   - `04_system_arch/part1`..`part3`
   - `CI&CD`

2. Create backend skeleton.
3. Build repository data ingestion.
4. Build AI layer and prompts.
5. Build frontend pages and connect APIs.
6. Add async processing and worker tasks.
7. Test at each phase.
8. Add CI/CD and deployment config.

## 7. Key Deliverables

- Working backend API
- Working frontend app
- AI orchestration and insight generation
- GitHub data ingestion and analysis
- Resume validation and recommendation
- Recruiter dashboard
- Test coverage
- CI/CD automation
- Deployment configuration

## 8. Important Notes

- Keep AI outputs explainable by attaching evidence from GitHub data.
- Keep API contract stable and versioned.
- Use background processing for heavy AI tasks.
- Ensure each endpoint has validations and error handling.
- Keep frontend responsive and usable.

## 9. Recommended File to Add

Add this file to the repo as `BUILD_PLAN.md`.
