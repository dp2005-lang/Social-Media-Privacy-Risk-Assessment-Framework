# Social-Media-Privacy-Risk-Assessment-Framework
**Social Media Privacy Risk Assessment Framework** is a privacy-focused cybersecurity tool that evaluates social-media exposure, account security, and digital-footprint risks. It provides a 0–100 risk score, prioritized recommendations, improvement simulation, and an interactive Python-Flask dashboard.
# Social Media Privacy Risk Assessment Framework

> Privacy-focused cybersecurity framework for assessing social-media exposure, account-security practices, social-engineering risk, digital-footprint risk, and personalized privacy improvements using synthetic or self-reported data.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue) ![Flask](https://img.shields.io/badge/Flask-API-black) ![SQLite](https://img.shields.io/badge/SQLite-storage-lightgrey) ![Chart.js](https://img.shields.io/badge/Chart.js-dashboard-orange) ![Tests](https://img.shields.io/badge/tests-37%20passing-brightgreen) ![Focus](https://img.shields.io/badge/focus-defensive%20security-purple)

---

## Overview

Oversharing and weak account settings make doxxing, impersonation and social-engineering scams easier. This project turns that problem into a measurable, explainable score.

A user answers a 42-question privacy questionnaire. The framework converts the answers into risk features, scores ten risk categories, combines them into an overall **Privacy Risk Score (0 to 100)**, and returns prioritized fixes. A built-in simulator shows how the score would change if selected settings were improved. A dashboard visualizes everything.

**Higher score = higher assessed exposure.**

> This project is designed for defensive cybersecurity and privacy education. It uses synthetic or voluntarily provided assessment responses and does not scrape, track, or profile real social-media users.

## Problem Statement

Individuals, students and small organizations rarely know how exposed their social profiles are. Privacy settings are scattered across platforms, and the link between public details (phone, birthday, location, employer) and real-world attacks is not obvious. There is a need for a simple, repeatable and privacy-respecting way to assess exposure and coach improvement.

## Objectives

- Assess self-reported privacy settings and habits without collecting the sensitive data itself
- Produce transparent, explainable category and overall risk scores
- Generate personalized, prioritized recommendations
- Let users simulate the effect of improving their settings
- Demonstrate privacy-by-design and data-minimization in a real application

## Cybersecurity Relevance

| Area | How the project relates |
|---|---|
| Privacy engineering | Data minimization, purpose limitation, privacy by default |
| Security awareness | Actionable guidance and a printable checklist |
| GRC | Weighted, configurable risk scoring with documented assumptions |
| IAM | MFA, password reuse, sessions and connected-app review |
| Application security | Input validation, output escaping, rate limiting, secure headers |
| Threat modeling | Account takeover, impersonation, phishing, oversharing, third-party exposure |

## Privacy vs Security

- **Privacy** controls how personal information is collected, shared and exposed.
- **Security** protects accounts and systems from unauthorized access.

A strong password and MFA do not stop a user from publicly exposing their phone number, birthday and location. **Strong account security does not equal strong privacy**, so the framework scores both.

## Features

- 42-question questionnaire across 10 categories
- Category scores (0 to 100) plus a configurable weighted overall score
- Four risk levels: LOW, MODERATE, HIGH, CRITICAL
- Findings engine with severity levels
- Recommendation engine: IMMEDIATE, IMPORTANT, GOOD PRACTICE
- Privacy improvement simulator with live radar-chart overlay
- Premium dark dashboard with six charts, built on 1,000 synthetic profiles
- Printable assessment report (save as PDF from the browser)
- Printable and downloadable privacy checklist
- Privacy-first SQLite storage (scores and finding types only)
- REST API with validation, rate limiting and security headers
- 37 automated functional, privacy and security tests
- Runs entirely from a single Google Colab cell with a shareable public URL

## Architecture

```
User
  v
Privacy Questionnaire (42 questions)
  v
Input Validation (allow-list)
  v
Feature Extraction  ->  answer to risk factor (0 to 1)
  v
Category Analyzers (10 categories)  ->  scores 0 to 100
  v
Risk Scoring Engine (configurable weights)  ->  overall 0 to 100
  v
Risk Classification
  v
Findings Engine  ->  Recommendation Engine
  v
Dashboard  |  Improvement Simulator  |  Printable Report
  v
Privacy-first database (scores + finding types only)
```

## Technology Stack

| Layer | Technology |
|---|---|
| Backend | Python 3, Flask |
| Data | pandas, NumPy |
| Database | SQLite |
| Frontend | HTML, CSS, JavaScript |
| Charts | Chart.js (radar, bar, doughnut) |
| Hosting in Colab | Cloudflare quick tunnel (public link), Colab proxy (fallback) |

## Privacy Questionnaire

Questions only ask whether something is visible or enabled. Users never type a phone number, address, email or password.

Answer types: `PUBLIC / FRIENDS / PRIVATE` and `YES / SOMETIMES / NOT SURE / NO`.

| Category | Questions | Weight |
|---|---|---|
| Profile Visibility | 4 | 10% |
| Personal Information | 6 | 15% |
| Location Privacy | 4 | 15% |
| Posts & Content | 4 | 10% |
| Connections | 4 | 10% |
| Tagging & Mentions | 4 | 5% |
| Account Security | 4 | 15% |
| Third-Party Apps | 4 | 5% |
| Social Engineering | 4 | 10% |
| Digital Footprint | 4 | 5% |

## Risk Scoring

1. Each answer maps to a **risk factor** between 0 (protective) and 1 (exposed).
2. Each question has an importance weight of 1 to 3.
3. **Category score** = `100 x sum(question_weight x risk_factor) / sum(question_weight)`
4. **Overall score** = `round(sum(category_weight x category_score))`

| Score | Level |
|---|---|
| 0 to 20 | LOW |
| 21 to 40 | MODERATE |
| 41 to 70 | HIGH |
| 71 to 100 | CRITICAL |

Weights live in the `WEIGHTS` dictionary and can be changed freely. They are educational assumptions and should be calibrated before any professional use.

## Privacy Findings

Any answer with a risk factor of 0.5 or higher becomes a finding with a severity (HIGH, MEDIUM, LOW) based on the question's importance. Example: *Phone number reported as publicly visible*, *MFA is disabled*, *Real-time location sharing enabled*.

## Recommendation Engine

Every finding maps to a specific fix and a priority:

- **IMMEDIATE**: high-impact items such as enabling MFA, hiding the phone number, stopping real-time location sharing
- **IMPORTANT**: medium-impact items such as login alerts, tag approval, reviewing old posts
- **GOOD PRACTICE**: low-impact hygiene items

## Improvement Simulator

Select the fixes you would apply. The framework recalculates category and overall scores and shows the before and after values, the points saved and the new risk level. The radar chart overlays the simulated result.

This is a framework simulation, not a guarantee of real-world safety.

## Digital Footprint

Only self-reported practices are assessed: reviewing old posts, closing unused accounts, reviewing privacy settings periodically, and avoiding personal details in public comments. No online activity is tracked.

## Social Engineering Awareness

The framework evaluates behaviors such as accepting unknown requests, clicking unexpected links, sharing verification codes, ignoring impersonation checks and joining suspicious giveaways. It explains risk conceptually and does not generate attack content.

## Account Security

MFA, unique passwords, login alerts and session review are scored in their own category, kept separate from information-exposure controls.

## Privacy Dashboard

| Panel | Purpose |
|---|---|
| KPI cards | Average score, risk level, high-risk categories, recommendations, controls enabled |
| Category risk scores | Average risk per category |
| Risk distribution | LOW / MODERATE / HIGH / CRITICAL split |
| Top weaknesses | Most common findings across profiles |
| Account security controls | Percentage of profiles with each control enabled |
| Digital footprint risk | Footprint-related weaknesses |
| Improvement comparison | Average score before and after fixes |

Results page: score ring, category radar, findings with priorities, and the simulator.

## Privacy Report

A printable HTML report with Assessment ID, date, overall score and level, category scores, findings, priority actions, checklist and disclaimer. Open it from the Results page and use the browser's **Print > Save as PDF**. It contains no sensitive personal data.

## Privacy by Design

| Principle | Implementation |
|---|---|
| Data minimization | Asks "is it visible?", never for the data itself |
| Purpose limitation | Data is used only to compute the assessment |
| Privacy by default | No accounts, no tracking, no third-party analytics |
| Least privilege | No access to social platforms or private accounts |
| Transparency | Scoring rules, weights and disclaimer are open and documented |
| User control | Any assessment can be deleted via the API or dashboard |
| Secure processing | Allow-list validation, output escaping, rate limiting |
| Retention limitation | Only scores, finding types and timestamps are stored |

**Never stored:** phone numbers, email addresses, home addresses, birth dates, passwords, exact locations, private messages, or the raw questionnaire answers.

## Installation

### Option A: Google Colab (recommended)

1. Open a new notebook at [colab.research.google.com](https://colab.research.google.com).
2. Paste the full contents of `privacy_risk_colab_cell.py` into **one** code cell.
3. Run the cell.

### Option B: Local machine

```bash
git clone https://github.com/<your-username>/Social-Media-Privacy-Risk-Assessment.git
cd Social-Media-Privacy-Risk-Assessment
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install flask pandas numpy
python privacy_risk_colab_cell.py
```

The script prints a local URL such as `http://127.0.0.1:<port>`.

## Usage

1. Run the cell. The test table prints first, then the dashboard link.
2. Open the link. Click **Start Privacy Assessment**.
3. Answer all 42 questions, or click **Load fictional demo profile**.
4. Click **Calculate my privacy risk**.
5. Review the score, radar chart, findings and recommendations.
6. Tick fixes in the simulator to see the new score.
7. Open the printable report or the checklist.

The public tunnel link works while the Colab runtime is running. Anyone with the link can open it, so share it deliberately.

## API Documentation

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/assessment` | Submit answers; returns score, level, categories, findings and an ID |
| `GET` | `/api/assessment/{id}` | Fetch a stored assessment (scores and finding types) |
| `GET` | `/api/assessment/{id}/recommendations` | Prioritized recommendations for an assessment |
| `POST` | `/api/assessment/simulate-improvement` | Body: `answers`, `fix` (list of question keys); returns before and after scores |
| `GET` | `/api/dashboard/stats` | Aggregate statistics from the synthetic dataset |
| `GET` | `/api/privacy-checklist` | Privacy checklist items |
| `GET` | `/api/questions` | Questionnaire definition |
| `DELETE` | `/api/assessment/{id}` | Delete a stored assessment |
| `GET` | `/report/{id}` | Printable HTML report |

**Example request**

```json
POST /api/assessment
{ "answers": { "profile_public": "PUBLIC", "mfa": "NO", "phone_public": "YES", "...": "..." } }
```

All 42 keys are required. Unknown keys or invalid values return `400`. Payloads over 20 KB return `413`, and excessive requests return `429`.

## Testing

Run automatically every time the cell executes. Results are saved to `tests/test_results.csv`.

| Group | Coverage |
|---|---|
| Profile scenarios | Fully private and fully public profiles |
| Single-risk scenarios | 18 individual risks (phone, email, birthday, location, MFA, apps, and more) |
| Scoring | Category calculation, weighted overall score, boundaries at 20, 40 and 70 |
| Engines | Recommendations and improvement simulation |
| Persistence | Database save and fetch, data deletion |
| Report | Generation and content |

## Security & Privacy Testing

| Test | What it verifies |
|---|---|
| Sensitive data not stored | No sensitive column names and no email or phone patterns in any table |
| Input validation | Missing, invalid and unknown keys are rejected with `400` |
| XSS protection | Script and HTML injected into report fields are escaped |
| Data deletion | A deleted assessment returns `404` |
| Security headers | `X-Content-Type-Options: nosniff` is present |
| Dataset hygiene | Synthetic dataset has no PII-style columns |

## Results

On the synthetic population of 1,000 profiles, the dashboard shows the average risk score, the share of profiles at each level, the most common weaknesses and how much the average score drops when top-priority items or all findings are fixed. The built-in demo profile (public profile, public phone and birthday, live location sharing, accepts unknown requests, no MFA, no login alerts, no tag review) scores in the HIGH range and drops sharply when the simulator applies the recommended fixes.

## Project Structure

Created at runtime in `/content/Social-Media-Privacy-Risk-Assessment/` on Colab:

```
Social-Media-Privacy-Risk-Assessment/
├── data/
│   └── social_media_privacy_assessments.csv   # 1,000 synthetic profiles
├── tests/
│   └── test_results.csv                       # latest test run
├── reports/                                   # reserved for exported reports
├── docs/                                      # documentation
├── screenshots/                               # dashboard screenshots
└── privacy_assessments.db                     # SQLite (scores and finding types only)
```

## Limitations

- Scores depend on self-reported answers and on educational weights that have not been calibrated against real incident data.
- It assesses configuration and habits, not the actual content of any account.
- Risk is contextual; a high score does not mean a compromise will happen, and a low score does not guarantee safety.
- The questionnaire is platform-agnostic and does not cover platform-specific settings.
- No user accounts or authentication, so it is intended for demos and education rather than multi-tenant production use.
- The in-memory rate limiter resets on restart.

## Future Improvements

- Platform-specific checklists (Instagram, LinkedIn, X, Facebook, TikTok)
- Configurable organizational policies and weights
- Privacy-awareness quizzes and maturity scoring
- Local photo metadata (EXIF) viewer with removal from a copy
- Native PDF export
- Report comparison over time
- Model calibration against expert ratings
- Localization and accessibility improvements
- Optional client-side-only mode
- Teen and family safety education modules

## Screenshots

| Dashboard | Questionnaire |
|---|---|
| ![Dashboard](screenshots/01_dashboard.png) | ![Questionnaire](screenshots/02_questionnaire.png) |

| Results and radar | Improvement simulator |
|---|---|
| ![Results](screenshots/03_results.png) | ![Simulator](screenshots/04_simulator.png) |

| Printable report | Automated tests |
|---|---|
| ![Report](screenshots/05_report.png) | ![Tests](screenshots/06_tests.png) |

## Learning Outcomes

- Designing a transparent, weighted risk-scoring model
- Applying privacy by design and data minimization in code
- Building and securing a REST API (validation, escaping, rate limiting)
- Separating privacy risk from account-security risk
- Threat-informed thinking about oversharing and social engineering
- Writing automated functional and security tests
- Presenting security data in a clear dashboard

## Ethical Disclaimer

This project is designed for defensive cybersecurity and privacy education. It uses synthetic or voluntarily provided assessment responses and does not scrape, track, or profile real social-media users. It does not access private accounts, bypass privacy settings, enumerate accounts, or collect personal information.

This is an educational risk framework, not a guarantee that an account will or will not be compromised. Weights and thresholds are educational assumptions and must be validated before any professional risk decision.

## Author

**Debankita Panja**
GitHub: [@your-username](https://github.com/dp2005-lang) · LinkedIn: [your-profile](https://www.linkedin.com/in/debankita-8482a2403/)
---

If this project helped you, consider giving it a star.
