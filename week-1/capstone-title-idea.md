# 📚 Capstone Definition

## Title:
**Smart Engagement Tracker: Post-Class KPIs for Students & Mentors**

## Problem Statement:
In distance learning, real-time participation is hard to monitor and post-class feedback is superficial. Students can quietly drop out, and guides do not have in-depth insights into their teaching efficacy. Conventional attendance and manual feedback are not sufficient to really gauge participation and learning outcomes.
## Objective:
To design and develop an **AI-powered system** that tracks, analyzes, and generates **post-class KPI reports** summarizing engagement levels for **both students and mentors** in online classes, helping improve educational experiences and learning outcomes.

---

## Key Features:
- 📊 **Post-Class KPI Reports**
  - **For Students:** Attendance, participation level, attention score.
  - **For Mentors:** Average class engagement, sentiment analysis from chats/questions, participation rates, teaching improvement suggestions.

- 🧠 **AI Engagement Analysis**
  - Sentiment analysis on chat/Q&A.
  - Participation event tracking (messages, reactions, polls).
  - Optional: Eye contact or presence detection (if camera input is allowed).

- 🚀 **Personalized Insights**
  - Students receive **personal learning engagement summaries**.
  - Mentors receive **class performance heatmaps** and trends over time.

- 📈 **Performance Dashboards**
  - Interactive visualizations: Engagement trends, leaderboard of top participants, class mood over time.

- 🔔 **At-Risk Student Detection**
  - Identify students with low participation or declining engagement for early intervention.

---

## Scope:
- **Supported Platforms:** Google Meet (via APIs or logs)
- **Data Sources:** Chat logs, participation logs
- **Privacy Focused:** Fully GDPR compliant, with options for anonymous analysis if needed.

---

## Technologies:
- **Frontend:** React.js / Nuxt.js (for dashboards and reports)
- **Backend:** Spring Boot / Node.js (for data processing APIs)
- **Database:** PostgreSQL / MongoDB (for storing participation and KPI data)
- **AI Models:**
  - Sentiment Analysis (using Hugging Face Transformers / TensorFlow Lite models)
  - Engagement Scoring Algorithm (custom logic or LightGBM)
- **Visualization:** Chart.js / D3.js / Recharts

---

## Target Users:
- 🎓 **Students:** Receive detailed feedback on their online learning engagement.
- 👩‍🏫 **Mentors:** Get actionable insights to improve their teaching strategies.

---

## Expected Outcomes:
- Improve overall student engagement and class effectiveness.
- Help mentors tailor their teaching based on real data.
- Create an easy-to-understand reporting system for academic institutions to monitor online class health.

---

# 🚀 Short Pitch / Tagline:
> **"Turn online class data into actionable insights with smart AI-powered post-class reports for students and mentors."**
