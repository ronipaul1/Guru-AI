# Guru AI — Adaptive Human-Like AI Educator

[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-19.0-61dafb.svg)](https://react.dev/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-4.1-38b2ac.svg)](https://tailwindcss.com/)
[![Gemini API](https://img.shields.io/badge/Google_Gemini-2.5-orange.svg)](https://ai.google.dev/)
[![Firebase](https://img.shields.io/badge/Firebase-Auth_%26_Firestore-ffca28.svg)](https://firebase.google.com/)

**Guru AI** is an adaptive, human-like AI educator that understands, profiles, plans, explains, questions, evaluates, diagnoses misconceptions, and dynamically adapts lessons with subject-aware blackboard visuals. Built with a full-stack Express and React architecture powered by the Google Gen AI SDK (`@google/genai`) and Cloud Firestore.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Tech Stack](#tech-stack)
- [Folder Structure](#folder-structure)
- [API Endpoints](#api-endpoints)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
  - [Running Locally](#running-locally)
  - [Production Build](#production-build)
- [Core AI Engines](#core-ai-engines)
- [Database & Authentication](#database--authentication)
- [License](#license)

---

## Overview

Traditional learning platforms often present static, one-size-fits-all content. **Guru AI** emulates an empathetic, world-class personal tutor. It assesses existing knowledge, diagnoses root misconceptions, formulates structured pedagogical lesson plans, draws interactive blackboard diagrams, and speaks with natural voice synthesis across multiple languages.

Whether you are revising quantum mechanics, learning recursion in Python, or studying photosynthesis, Guru AI tailors every concept, checkpoint question, and visual demonstration to your unique learning style.

---

## Key Features

### 1. Pedagogical Teaching Cycle
- **Diagnostic Ingestion**: Automatically breaks complex topics into bite-sized pedagogical concepts with estimated durations, strategies, and real-world analogies.
- **Adaptive Explanations**: Switches explanations dynamically (e.g., from technical depth to intuitive analogies or step-by-step breakdowns) if the learner struggles.
- **Cognitive Load Optimization**: Balances theory, visual modeling, and practice questions to prevent cognitive overload.

### 2. Socratic Misconception Diagnosis
- Goes beyond marking answers right or wrong.
- Identifies underlying misconceptions (e.g., confusing velocity with acceleration, or referencing by value vs reference in programming).
- Provides immediate constructive guidance and targeted re-testing.

### 3. Subject-Aware Visual Blackboard
Interactive visual canvas that renders domain-specific diagrams:
- **Physics**: Force vectors, projectile trajectories, spring-mass systems, optics.
- **Mathematics**: Function plots, calculus tangent lines, geometric proofs.
- **Computer Science & Coding**: Call stacks, memory pointers, recursion trees, runtime execution steps.
- **Biology & Chemistry**: Cellular respiration, enzyme-substrate complexes, molecular bonding.
- **History & Humanities**: Chronological timelines, comparative matrices.

### 4. Multimodal Educational Material Ingestion
- Upload lecture slides, textbook pages, handwritten notes, or syllabus PDFs/images.
- Guru AI extracts learning objectives, identifies prerequisite gaps, and auto-generates custom lesson plans directly from your study material.

### 5. Multi-Language & Voice Support
- Native instruction across **English, Hindi, Hinglish, Bengali, Tamil, Telugu, Marathi, Gujarati, Kannada, Malayalam, Punjabi, Spanish, and French**.
- Natural teacher speech synthesis with fallback to the Web Speech API, with adjustable speaking rate and voice tone.

### 6. Diagnostic Learning Reports & Roadmaps
- Multi-question final assessments (Multiple Choice, Conceptual, Application-based).
- Detailed diagnostic reports featuring overall mastery percentage, identified strengths, diagnosed misconceptions, and scheduled spaced-repetition reviews.
- Multi-week structured learning paths with prerequisites and milestone checkpoints.

---

## System Architecture

Guru AI adopts a full-stack architecture with clear separation between the server-side AI execution layer and client-side reactive interface:

```
┌─────────────────────────────────────────────────────────┐
│                    Client (React 19)                    │
│  Classroom • Visual Blackboard • Teacher Avatar • UI    │
└────────────────────────────┬────────────────────────────┘
                             │ REST /api/*
┌────────────────────────────▼────────────────────────────┐
│                  Server (Express + Vite)                │
│  • API Key Protection (Gemini never exposed to browser) │
│  • Server-side AI Orchestration via @google/genai       │
└──────────────┬───────────────────────────┬──────────────┘
               │                           │
┌──────────────▼──────────────┐ ┌──────────▼──────────────┐
│       Google Gemini         │ │   Firebase Cloud Suite  │
│  • Lesson Planning          │ │  • Firebase Auth (Google│
│  • Teaching Cycles          │ │    & Email/Password)    │
│  • Misconception Engine     │ │  • Cloud Firestore Data │
│  • Visual & TTS Engines     │ │    (Profiles, Reports)  │
└─────────────────────────────┘ └─────────────────────────┘
```

---

## Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend Framework** | React 19, TypeScript, Vite |
| **Styling & UI** | Tailwind CSS v4, Motion (Framer Motion), Lucide React |
| **Backend Server** | Node.js, Express 4.x, tsx, esbuild |
| **AI Intelligence** | Google Gen AI SDK (`@google/genai`), Gemini 2.5 models |
| **Authentication** | Firebase Authentication (Email/Password & Google OAuth) |
| **Cloud Database** | Google Cloud Firestore |
| **Fonts** | Plus Jakarta Sans, Lora, JetBrains Mono |

---

## Folder Structure

```
├── public/                     # Static assets and brand logos
├── server/                     # Server-side AI services & engines
│   └── gemini/
│       ├── assessmentEngine.ts      # Assessment & learning report generation
│       ├── client.ts                # Initialized @google/genai client
│       ├── evaluationEngine.ts      # Student answer scoring & feedback
│       ├── learningPathEngine.ts    # Multi-stage learning roadmap generation
│       ├── lessonPlanner.ts         # Structured lesson planning
│       ├── materialAnalyzer.ts      # Multimodal syllabus/note ingestion
│       ├── misconceptionEngine.ts   # Root-cause misconception diagnosis
│       ├── questionEngine.ts        # Socratic Q&A and student queries
│       ├── teachingEngine.ts        # Live adaptive teaching cycle segments
│       ├── ttsEngine.ts             # Audio synthesis & speech generation
│       └── visualPlanner.ts         # Blackboard diagram planning
├── src/                        # React frontend application
│   ├── assets/                 # App images and illustrations
│   ├── components/             # Reusable UI & screen components
│   │   ├── AuthScreen.tsx           # Authentication modal & guest mode
│   │   ├── Classroom.tsx            # Interactive live teaching workspace
│   │   ├── CreateLessonModal.tsx    # Custom topic lesson creator
│   │   ├── DocumentUploadModal.tsx  # Document/image uploader
│   │   ├── FinalAssessment.tsx      # Comprehensive post-lesson test
│   │   ├── InteractiveQuestionCard  # Checkpoint question component
│   │   ├── LandingHero.tsx          # Main dashboard & quick starts
│   │   ├── LearnerProfileModal.tsx  # Learner calibration modal
│   │   ├── LearningPathView.tsx     # Roadmap visualization
│   │   ├── LearningReportView.tsx   # Diagnostic report visualization
│   │   ├── Navbar.tsx               # Top navigation bar & theme toggle
│   │   ├── SettingsModal.tsx        # Voice & teaching settings
│   │   ├── TeacherAvatar.tsx        # Animated teacher avatar
│   │   ├── TeachingIntelligencePanel# AI thought process readout
│   │   └── VisualPanel.tsx          # Dynamic blackboard renderer
│   ├── data/                   # Demo subjects and default states
│   ├── services/               # Client-side API, Firebase & voice services
│   ├── types/                  # TypeScript interfaces and domain models
│   ├── App.tsx                 # Root application component
│   ├── index.css               # Design system & CSS custom properties
│   └── main.tsx                # Vite React entry point
├── firestore.rules             # Cloud Firestore security rules
├── server.ts                   # Express server entry point & API routes
├── package.json                # Dependencies and build scripts
└── vite.config.ts              # Vite configuration
```

---

## API Endpoints

The Express server exposes the following endpoints (with all Gemini calls executed securely server-side):

| Endpoint | Method | Description |
| :--- | :---: | :--- |
| `/api/health` | `GET` | Health check and Gemini API key status |
| `/api/analyze-material` | `POST` | Ingests PDF/image study material and extracts topics |
| `/api/generate-lesson-plan` | `POST` | Generates a structured pedagogical lesson plan |
| `/api/teaching-cycle` | `POST` | Generates a teaching segment (Explanation, Visual, Analogy, Question) |
| `/api/evaluate-answer` | `POST` | Evaluates learner response and detects misconceptions |
| `/api/student-question` | `POST` | Answers student's hand-raise query Socratically |
| `/api/diagnose-misconception` | `POST` | Diagnoses root misconceptions for incorrect responses |
| `/api/plan-visual` | `POST` | Plans blackboard diagrams and mathematical specs |
| `/api/generate-assessment` | `POST` | Generates final assessment questions |
| `/api/generate-report` | `POST` | Compiles comprehensive diagnostic report & recommendations |
| `/api/generate-learning-path` | `POST` | Builds structured multi-stage learning roadmaps |
| `/api/tts` | `POST` | Generates speech audio using Gemini TTS |

---

## Getting Started

### Prerequisites

- **Node.js**: v20.x or higher
- **npm** or **bun**
- **Google Gemini API Key**: Obtainable from [Google AI Studio](https://aistudio.google.com/)

### Installation

1. Clone the repository or open the project directory:
   ```bash
   cd new-guru-ai
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

### Environment Variables

Create a `.env` file in the project root by copying `.env.example`:

```bash
cp .env.example .env
```

Set the required environment variables:

```env
# Required for all AI educator capabilities
GEMINI_API_KEY="your-gemini-api-key-here"

# Application URL (optional in local development)
APP_URL="http://localhost:3000"
```

> **Security Notice**: Never expose `GEMINI_API_KEY` on the client-side. The Express backend handles all Gemini operations via `/server/gemini/*` proxies.

### Running Locally

Start the full-stack development server (Express backend + Vite frontend):

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Production Build

To build the application for deployment:

```bash
npm run build
```

This compiles:
1. The Vite client bundle to `dist/`
2. The Express server to a standalone bundle in `dist/server.cjs` via `esbuild`

To start the production server:

```bash
npm start
```

---

## Core AI Engines

- **Lesson Planner (`lessonPlanner.ts`)**: Analyzes student background, target time, and objectives to create step-by-step concept maps.
- **Teaching Engine (`teachingEngine.ts`)**: Drives interactive segments with adaptive strategies (Analogy-first, Intuitive, Step-by-step, or Mathematical).
- **Misconception Engine (`misconceptionEngine.ts`)**: Employs diagnostic prompts to uncover *why* a student answered incorrectly, distinguishing silly mistakes from fundamental misunderstandings.
- **Visual Planner (`visualPlanner.ts`)**: Synthesizes diagram parameters, formulas, and visual elements dynamically adapted to the topic.
- **Assessment Engine (`assessmentEngine.ts`)**: Evaluates post-lesson mastery across recall, comprehension, and practical application.

---

## Database & Authentication

- **Authentication**: Supports Google Sign-In and Email/Password authentication via Firebase Authentication. A guest mode is also provided for frictionless exploration.
- **Firestore Persistence**: Automatically persists learner profiles, custom settings, past completed lessons, and diagnostic reports to Cloud Firestore.
- **Offline Recovery**: Synchronizes with `localStorage` for instant hydration and offline resilience.

---

## License

This project is licensed under the MIT License.
