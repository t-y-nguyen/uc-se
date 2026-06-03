# EECE/CS 3093C — Software Engineering
**Instructor:** Dr. Phu Phung  
**Department:** Electrical and Computer Engineering/Computer Science, University of Cincinnati  
**Term:** Summer 2026  
**Published:** June 3, 2026  
**Latest Updated:** June 3, 2026

---

# Team Project Description and Requirements

> **Note:** This document and the requirements are subject to change. Any updates will be announced on Canvas with at least 24 hours advance notice.

## Overview

In this course, students are required to collaborate on a large group project to develop a software product using covered software engineering topics. We will practice the Scrum agile software engineering method to build an application called `Messenger`, a real-time web-based chat system. In a nutshell, `Messenger` allows registered users to communicate through public, private, and group messaging with additional features. Using the Scrum framework, teams will develop the application incrementally over multiple sprint cycles. In particular, your team will apply software and secure lifecycle models, requirements analysis, and specification topics to design, implement, deploy, test, and maintain the application using the toolchain: **Node.js** web application (development stack), **Azure App Services** (cloud deployment), **MongoDB Atlas** (cloud database), and **GitHub** (version control) with **GitHub Projects** for project management.

This document defines the requirements for the team project across all sprint cycles. Each sprint builds on the previous one, adding functionality, security, and quality to the Messenger application.

| Sprint | Version | Focus | Weeks |
|--------|---------|-------|-------|
| Sprint 0 | — | Team Building, Project Setup, System Analysis, Requirements Engineering, and System Design | 3–5 |
| Sprint 1 | v0.1 | Core UI, public & private chat, basic authentication, initial deployment | 6–7 |
| Sprint 2 | v0.2 | Secure auth with MongoDB Atlas, input validation, password hashing, CI/CD pipeline | 8–9 |
| Sprint 3 | v0.3 | Open design — team-chosen features with GenAI-assisted development | 10–11 |
| Final | — | Complete deployed application, final report, team presentation | 12–13 |

### GitHub Team Organization, Repositories, and Project Management

As an outcome of the first teamwork (Team Building activities in Sprint 0), each team must have a GitHub **organization** named `uc-se-sm26-team#` (where `#` is your Canvas team number, e.g., `uc-se-sm26-team3`), shared with all members and `phung-se` (the instructor and TAs) with appropriate roles.

#### Code Repository and Structure (private)

Each team must have one **private** repository named `scrum-project` inside the team organization with the `README.md` using the [`README.md`](./README.md) template from the course repository.

From Sprint 1, each sprint is developed on its own branch and merged to `main` via a pull request at completion:

```
sprint1/   ← v0.1 implementation
sprint2/   ← v0.2 implementation
sprint3/   ← v0.3 implementation
```

Each sprint branch must contain:
- `README.md` — sprint report (use the template provided in this folder as your starting point)
- `docs/` — diagrams and screenshots
- `src/` — all source code

Your repository must include a `.gitignore` that excludes `node_modules`, `.env`, and any OS/editor metadata files.

---

#### Team Homepage Repository (public)

Each team must have one **public** repository named `uc-se-sm26-team#.github.io` inside the team organization with an `index.html` file, initially using [the template](./index.html) from the course repository. This HTML file serves as your team homepage, automatically published at `https://uc-se-sm26-team#.github.io` when pushed.

> This homepage is your team's public-facing project page. All sprint video demos will be embedded here throughout the semester.

#### GitHub Projects Board

Each team must have one **GitHub Projects** board created inside the team organization using the Team Planning template. Add all sprint PBIs (product backlog items) as issues in three main columns:

- New items start in **Todo**
- Move to **In Progress** with member comments as work proceeds
- Move to **Done** by the submission deadline

---

## Sprint 0 — Team Setup, System Analysis and Design
**Weeks 3–5**

### Introduction

Sprint 0 is the foundation of your team project. There is no code to write — the goal is to form your team, set up your collaborative infrastructure, and produce a thorough requirements and design document that will guide all subsequent sprints. Completing Sprint 0 well directly determines how smoothly Sprints 1–3 go.

---

### Expected Outcomes

| # | Artifact | Details |
|---|----------|---------|
| 1 | GitHub Organization | `uc-se-sm26-team#` shared with all members and `phung-se` |
| 2 | `scrum-project` (private repo) | `README.md` template populated with team, course info, and system analysis and design |
| 3 | `uc-se-sm26-team#.github.io` (public repo) | `index.html` updated; homepage live at `https://uc-se-sm26-team#.github.io` |
| 4 | GitHub Projects board | All Sprint 0 and Sprint 1 PBIs created in Todo; system analysis discovery artifacts added in `System Analysis` column |

---

### Sprint 0 Deliverables & Grading

_To be updated and posted on Canvas._

---

## Sprint 1 — Messenger v0.1
**Weeks 6–7**

### Introduction

In this sprint, your team will build the first working prototype of the Messenger. The outcome is a deployed application with a functional UI, basic authentication, and real-time public and private chat. Before implementation begins, your team must complete the requirements engineering activities described below — connecting the personas, scenarios, and user stories from Lecture 6 directly to the features you build.

### Requirements Engineering (pre-implementation)

Completing the following before writing code is a graded requirement. Document the outputs in your `sprint1/README.md` under the **Requirements Engineering** section.

- Define at least **three personas** (e.g., a regular user, a new visitor), each with a name, background, and goals — including the persona for your team-chosen feature (F1.9)
- Write at least **one scenario** per persona, narrating a realistic interaction with the Messenger — including the scenario for F1.9
- Derive at least **six user stories** from your scenarios: *As a [persona], I want to [goal] so that [benefit]* — including the two user stories for F1.9
- Assign Sprint 1's user stories to a use case as a PBI to your **GitHub Projects** board before development starts

### Functional Requirements

| ID | Requirement |
|----|-------------|
| F1.1 | Login and chat UIs are visually and functionally separated |
| F1.2 | Users can log in with a username (no password required yet) |
| F1.3 | Only logged-in users can access the chat interface |
| F1.4 | Logged-in users can send and receive public messages in real time |
| F1.5 | Logged-in users can send and receive private (direct) messages to/from a specific online user |
| F1.6 | An online user list is displayed and updated in real time |
| F1.7 | Public chat and private chat are visually distinct (separate views or panels) |
| F1.8 | Real-time typing status indicator for public and private chat |
| F1.9 | **Team-chosen feature:** your team identifies one additional user-facing feature, driven by your own persona, scenario, and two user stories (documented in the Requirements Engineering section of your README) |

> **F1.9 guidance:** The feature must be realistic for a Sprint 1 prototype and scoped to what your team can deliver in two weeks. Examples: message timestamps, user avatars, sound notifications, message character limit indicator. Document the rationale in your README — why does this feature matter to your persona?

_Grading rubric to be updated and posted on Canvas._

---

## Sprint 2 — Messenger v0.2
**Weeks 8–9**

### Introduction

In this sprint, your team upgrades the Messenger with secure authentication backed by MongoDB Atlas, implements input validation and sanitization across all layers, and establishes a CI/CD pipeline with GitHub Actions. The focus is on transitioning from a prototype to a more secure, production-ready application.

Before starting, merge the `sprint1` branch into `main` and create a `sprint2` branch.

_To be updated._

---

## Sprint 3 — Messenger v0.3 (Open Design)
**Weeks 10–11**

### Introduction

Sprint 3 is open-ended. Your team selects the features to implement, driven by your own product vision and the requirements you identified in Sprint 0. The goal is to demonstrate that your team can plan, prioritize, and deliver a coherent set of features end-to-end — using an AI-assisted development tool.

Before starting, merge the `sprint2` branch into `main` and create a `sprint3` branch.

_To be updated._
