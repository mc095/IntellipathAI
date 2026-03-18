<p align="center">
  <img src="https://img.shields.io/badge/Django-3.1-092E20?style=for-the-badge&logo=django&logoColor=white" alt="Django" />
  <img src="https://img.shields.io/badge/MongoDB-Djongo-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
  <img src="https://img.shields.io/badge/Gemini_AI-Agent-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Gemini AI" />
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License" />
</p>

<h1 align="center">🤖 IntellipathAI — Agentic Job AI</h1>

<p align="center">
  <strong>An AI-powered career development platform that uses agentic workflows to help job seekers build resumes, prepare for interviews, ace exams, check ATS compatibility, and generate professional portfolios — all in one place.</strong>
</p>

<p align="center">
  <a href="#-features">Features</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-project-structure">Project Structure</a> •
  <a href="#-modules-deep-dive">Modules</a> •
  <a href="#-screenshots">Screenshots</a> •
  <a href="#-contributing">Contributing</a>
</p>

---

## 🌟 Features

| Module | Description |
|--------|-------------|
| **📝 Resume Builder** | Build professional resumes with a structured form, export to LaTeX/PDF with `moderncv` templates. Supports education, experience, skills, projects, certifications, and custom sections. |
| **📊 Resume Analysis** | AI-driven resume analysis against job descriptions using client-side Puter.js integration. Get actionable suggestions and a rewritten resume tailored to the target role. |
| **🎯 ATS Scanner** | Real Applicant Tracking System simulation — keyword density, section completeness, format compatibility, experience relevance scoring. Weighted final score with missing keyword reports. |
| **📚 Exam Prep** | AI-generated 30-question MCQ exams customized to your target job role. Deduplication, adaptive difficulty, per-question explanations, topic tagging, and persistent scoring history. |
| **🎙️ Mock Interview** | Text-based interview sessions powered by Gemini AI. Context-aware follow-up questions based on your resume and job description with comprehensive feedback scoring. |
| **💬 Training Chat** | Interactive training sessions with an AI interviewer. Role-play interview prep with memory — tracks past performance, ATS scores, and exam results to personalize sessions. |
| **🌐 Portfolio Generator** | Generate stunning portfolio websites from your data. Three template options (Creative, Minimal, Professional) with animated navigation, Typed.js hero sections, and modals. |
| **👤 User Profiles** | Photo + resume upload, text extraction from resumes, secure auth with login/signup/forgot-password flows. |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Browser / Client                      │
│  ┌──────────┐  ┌──────────┐  ┌────────────────────────┐ │
│  │  Django   │  │  Puter.js│  │   Typed.js / Tailwind  │ │
│  │ Templates │  │  AI Chat │  │   Portfolio Frontend   │ │
│  └────┬─────┘  └────┬─────┘  └───────────┬────────────┘ │
└───────┼──────────────┼───────────────────┼──────────────┘
        │              │                   │
        ▼              ▼                   ▼
┌─────────────────────────────────────────────────────────┐
│                   Django Backend                         │
│                                                          │
│  ┌──────────┐ ┌─────────┐ ┌─────┐ ┌──────┐ ┌─────────┐ │
│  │ accounts │ │ resume  │ │ ats │ │ exam │ │interview│ │
│  ├──────────┤ ├─────────┤ ├─────┤ ├──────┤ ├─────────┤ │
│  │ Models   │ │ LaTeX   │ │Score│ │Agents│ │ Gemini  │ │
│  │ Views    │ │ PDF Gen │ │ Svc │ │ Svc  │ │  Q&A    │ │
│  └──────────┘ └─────────┘ └─────┘ └──────┘ └─────────┘ │
│                                                          │
│  ┌──────────┐ ┌──────────────┐ ┌────────────────────────┐│
│  │ training │ │  portfolio   │ │     ai_agents          ││
│  ├──────────┤ ├──────────────┤ ├────────────────────────┤│
│  │ Sessions │ │ HTML Gen     │ │ AIService (Gemini)     ││
│  │ Memory   │ │ 3 Templates  │ │ Q-Gen, Interview, FB   ││
│  └──────────┘ └──────────────┘ └────────────────────────┘│
└──────────────────────┬──────────────────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │   MongoDB      │
              │  (via Djongo)  │
              └────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Django 3.1, Python 3.10+ |
| **Database** | MongoDB via Djongo ORM |
| **AI / LLM** | Google Gemini API (`google-genai` / `google-generativeai`), Puter.js (client-side) |
| **PDF Generation** | LaTeX (`pdflatex`, `moderncv` package) |
| **Resume Parsing** | `pdfminer.six`, `python-docx` |
| **NLP** | spaCy (`en_core_web_sm`) |
| **Frontend** | Django Templates, Tailwind CSS (CDN), Font Awesome, Typed.js |
| **Auth** | Django built-in auth with custom `UserProfile` model |
| **Environment** | `python-dotenv` for secrets management |

---

## 🚀 Getting Started

### Prerequisites

- **Python 3.10+**
- **MongoDB** (local or Atlas URI)
- **LaTeX** distribution (for PDF resume export — optional)
  - Windows: [MiKTeX](https://miktex.org/) or [TeX Live](https://tug.org/texlive/)
  - macOS: `brew install --cask mactex`
  - Linux: `sudo apt install texlive-full`
- **Google Gemini API Key** — [Get one here](https://aistudio.google.com/apikey)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/Agentic-Job-AI.git
cd Agentic-Job-AI

# 2. Create and activate a virtual environment
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Download the spaCy language model
python -m spacy download en_core_web_sm
```

### Configuration

Create a `.env` file inside the `ai_job_helper/` directory:

```env
# MongoDB connection
MONGO_URI=mongodb://localhost:27017
MONGO_DB_NAME=ai_job_helper_db

# Google Gemini API
GEMINI_API_KEY=your_gemini_api_key_here
GEMINI_MODEL=gemini-2.5-flash

# Django
SECRET_KEY=your-secret-key-here
DEBUG=True
```

### Run the Server

```bash
cd ai_job_helper
python manage.py migrate
python manage.py createsuperuser   # (optional) create an admin user
python manage.py runserver
```

Visit **http://127.0.0.1:8000** and sign up to get started!

---

## 📂 Project Structure

```
Agentic-Job-AI/
├── ai_job_helper/                 # Django project root
│   ├── ai_job_helper/             # Project settings & config
│   │   ├── settings.py            # Django settings (MongoDB, apps, etc.)
│   │   ├── urls.py                # Root URL routing
│   │   ├── wsgi.py                # WSGI entry point
│   │   └── asgi.py                # ASGI entry point
│   │
│   ├── accounts/                  # 👤 User authentication & profiles
│   │   ├── models.py              # UserProfile (photo, resume, extracted text)
│   │   ├── views.py               # Login, signup, profile management
│   │   ├── forms.py               # Registration & profile forms
│   │   └── urls.py                # Auth routes
│   │
│   ├── ai_agents/                 # 🤖 Core AI service layer
│   │   └── ai_service.py          # AIService class (Gemini integration)
│   │                              #   → Exam question generation
│   │                              #   → Interview question generation
│   │                              #   → Interview feedback generation
│   │
│   ├── resume/                    # 📝 Resume builder
│   │   ├── models.py              # Resume, Education, Experience, etc.
│   │   ├── services.py            # LaTeX compilation & PDF generation
│   │   ├── views.py               # Builder UI logic
│   │   └── static/resume/css/     # Builder-specific styles
│   │
│   ├── analysis/                  # 📊 Resume analysis
│   │   ├── models.py              # AnalysisResult, AgentMemory
│   │   └── views.py               # Puter.js-powered analysis flow
│   │
│   ├── ats/                       # 🎯 ATS compatibility scanner
│   │   ├── services.py            # Real ATS scoring engine
│   │   │                          #   → Keyword extraction (tech + soft skills)
│   │   │                          #   → Section completeness analysis
│   │   │                          #   → Format scoring (action verbs, quantified)
│   │   │                          #   → Missing keyword detection
│   │   ├── models.py              # ATSResult model
│   │   └── templatetags/          # Custom template filters
│   │
│   ├── exam/                      # 📚 AI exam preparation
│   │   ├── models.py              # Exam, Question, Answer, ExamResult
│   │   ├── views.py               # Loading → Test → Result flow
│   │   └── signals.py             # Auto-scoring signals
│   │
│   ├── interview/                 # 🎙️ Mock interview system
│   │   ├── models.py              # InterviewSession
│   │   └── views.py               # Session management & chat
│   │
│   ├── training/                  # 💬 AI training chat
│   │   ├── models.py              # TrainingSession, TrainingMessage
│   │   └── views.py               # Chat with AgentMemory integration
│   │
│   ├── portfolio/                 # 🌐 Portfolio generator
│   │   ├── portfolio_generator.py # HTML generation (3 templates)
│   │   ├── views.py               # Template selection & preview
│   │   └── forms.py               # Portfolio data forms
│   │
│   ├── templates/                 # 🎨 HTML templates
│   │   ├── base.html              # Master layout
│   │   ├── home.html              # Dashboard with stats & services
│   │   ├── registration/          # Login, signup, forgot password
│   │   ├── exam/                  # Exam flow (home → test → result)
│   │   ├── interview/             # Chat & feedback
│   │   ├── training/              # Training chat
│   │   ├── portfolio/             # 3 portfolio templates
│   │   └── ...                    # Other module templates
│   │
│   └── manage.py                  # Django management script
│
├── requirements.txt               # Python dependencies
├── README.md                      # ← You are here
└── .gitignore
```

---

## 🔍 Modules Deep Dive

### 🤖 AI Service (`ai_agents/ai_service.py`)

The central AI brain of the application. Wraps Google Gemini API with fallback support:

- **`generate_exam_questions_for_user()`** — Generates 30 unique MCQ questions in a single API call. Includes question deduplication, avoidance lists, option normalization, and explanation generation.
- **`generate_interview_question()`** — Produces contextual interview questions based on the conversation history, resume, and job description.
- **`generate_interview_feedback()`** — Evaluates complete interview transcripts and provides scores across Technical Competency, Communication, Problem-Solving, and Overall Performance.

### 🎯 ATS Scanner (`ats/services.py`)

A real ATS simulation engine with weighted scoring:

| Component | Weight | What It Measures |
|-----------|--------|------------------|
| Keyword Match | 40% | Technical skills & soft skills from JD |
| Section Completeness | 25% | Header, summary, experience, education, skills, projects |
| Format Score | 20% | Action verbs, quantified achievements, proper formatting |
| Experience Relevance | 15% | Industry & role keyword alignment |

### 📝 Resume Builder (`resume/services.py`)

Generates publication-quality PDFs using LaTeX:
- Uses the `moderncv` document class with the `classic` style
- Supports structured sections: personal info, education, experience, skills, projects, certifications
- Compiles via `pdflatex` in a sandboxed temp directory

### 💬 Agent Memory (`analysis/models.py`)

The `AgentMemory` model provides cross-module intelligence:
- Tracks user preferences, strengths, and weaknesses
- Records session summaries across training and interview modules
- Feeds historical performance data into AI prompts for adaptive difficulty

---

## 🖼️ Screenshots

> *Coming soon — to add screenshots, place images in a `docs/screenshots/` directory and reference them here.*

| Dashboard | ATS Scanner | Exam Prep |
|-----------|-------------|-----------|
| ![Dashboard](docs/screenshots/dashboard.png) | ![ATS](docs/screenshots/ats.png) | ![Exam](docs/screenshots/exam.png) |

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. **Fork** the repository
2. **Create** a feature branch: `git checkout -b feature/amazing-feature`
3. **Commit** your changes: `git commit -m "Add amazing feature"`
4. **Push** to the branch: `git push origin feature/amazing-feature`
5. **Open** a Pull Request

### Development Guidelines

- Follow PEP 8 for Python code
- Write docstrings for all new functions and classes
- Update `requirements.txt` if adding new dependencies
- Test your changes against the MongoDB backend before submitting

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **[Google Gemini](https://ai.google.dev/)** — Large language model powering AI features
- **[Django](https://www.djangoproject.com/)** — Web framework
- **[Djongo](https://github.com/doableware/djongo)** — MongoDB connector for Django ORM
- **[spaCy](https://spacy.io/)** — NLP library for keyword extraction
- **[Puter.js](https://puter.com/)** — Client-side AI integration
- **[Typed.js](https://mattboldt.com/demos/typed-js/)** — Typing animation library
- **[Tailwind CSS](https://tailwindcss.com/)** — Utility-first CSS framework
- **[Font Awesome](https://fontawesome.com/)** — Icon library

---

<p align="center">
  <strong>Built with ❤️ for job seekers everywhere</strong>
  <br />
  <em>If this project helped you, please ⭐ the repo!</em>
</p>