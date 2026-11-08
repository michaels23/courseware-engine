# courseware-engine

A configuration-driven static site engine built with Astro and GitHub Actions that transforms a Google Sheets curriculum manifest into a unified, clean-URL courseware experience on your domain.

---

## 🏛️ Architecture Overview

The `courseware-engine` decouples content editing and distribution from layout and routing. It follows standard software architecture principles:

* **Facade Pattern:** Serves a single, cohesive classroom experience at `mikesteigerwald.com/courses/[category]/[slug]` regardless of where source materials live.
* **Adapter Pattern:** Wraps third-party platforms (Substack articles, YouTube lectures, and Google Forms quizzes) into standardized layout components.
* **Flyweight Pattern:** Reuses a single visual shell (`LessonLayout.astro`) across all dynamic lesson pages to keep the codebase minimal (DRY).

---

## 🛠️ Stack & Data Pipeline

* **Framework:** [Astro](https://astro.build/) (Static Site Generation)
* **Data Source:** Google Sheets manifest (exported/fetched as JSON at build time)
* **Hosting & CI/CD:** GitHub Pages + GitHub Actions
* **Embedded Content:** Substack (reading), YouTube (video), Google Forms (quizzes)

---

## 📁 Directory Structure

```text
├── .github/
│   └── workflows/
│       └── deploy.yml          # Automated CI/CD deployment
├── src/
│   ├── components/
│   │   ├── LessonLayout.astro  # Shared UI wrapper across lessons
│   │   ├── SubstackEmbed.astro # Adapter for Substack articles
│   │   ├── YouTubePlayer.astro # Adapter for video lectures
│   │   └── QuizEmbed.astro     # Adapter for Google Forms quizzes
│   └── pages/
│       └── courses/
│           └── [category]/
│               └── [slug].astro # Dynamic route generator
├── astro.config.mjs
└── package.json
