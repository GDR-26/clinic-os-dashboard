# Clinic OS Dashboard

The operational dashboard for Clinic OS — a staff-facing interface for monitoring appointments, recovery analytics, and AI workflow activity.

---

## Overview

This repository contains the frontend dashboard for Clinic OS. It is the interface clinic staff use to see, at a glance, what's happening across their appointment pipeline: what's scheduled, what's been confirmed, what's been recovered after a cancellation or no-show, and what the AI automation layer did on a given day.

This dashboard does not contain the backend, the database, or the AI workflow automation itself — those live in separate repositories. What's here is the operational UI: a set of static HTML/CSS/JS screens that present clinic data in a form staff can scan quickly during a shift, without digging through spreadsheets or WhatsApp threads.

---

## Highlights

- Daily appointment overview (scheduled, cancellations, confirmation rate)
- Booking-to-attended pipeline visualization
- Revenue recovery and revenue leakage breakdown
- AI automation activity summary ("AI Worked Today")
- Automated operational insights based on clinic metrics
- Staff login screen
- Lightweight, dependency-free frontend (HTML/CSS/JS)

---

## Why I Built This

Most of the clinic automation work in Clinic OS happens invisibly — reminders get sent, no-shows get flagged, recovery messages go out over WhatsApp. Without a dashboard, none of that is visible to the people actually running the clinic. Receptionists and clinic staff have no way to see confirmation rates, spot which service has the highest cancellation rate, or know whether a recovery message actually worked, unless someone is manually checking logs or a spreadsheet.

This dashboard exists to close that gap: to give staff a single screen that answers "what happened today, and is it working?" without needing to understand the automation underneath it. Operational visibility matters here specifically because the automation is making decisions (who gets reminded, who gets flagged as a no-show) that staff need to be able to verify and trust.

---

## Dashboard Architecture

This dashboard is one piece of the larger Clinic OS system, not a standalone application. Conceptually, it sits at the top of the stack, consuming data produced by the layers below it:

![Clinic OS Dashboard Architecture](screenshots/clinic-os-dashboard-architecture.png)

The dashboard is responsible only for presenting operational data. Business logic, authentication, workflow orchestration, and data processing are handled by the Clinic OS backend and n8n automation layer. Google Sheets serves as the operational datastore for this prototype, while the dashboard focuses on providing staff with a clear operational view of clinic activity.


---

## Dashboard Modules

### Dashboard Overview
The main landing screen. Shows a "Today at a Glance" summary — scheduled appointments, cancellations, confirmation rate, and patients recovered — followed by a revenue intelligence panel showing recovered revenue for the current month.

### Login Screen
A staff-only sign-in screen for the clinic's "AI Command Center," gated behind an email and password field. Branded per-clinic (e.g. "Smile Dental") with a note that the system is powered by WhatsApp AI automation.

### Smart Insights
Surfaces a booking-to-attended pipeline (total booked → confirmed → attended → recovered) alongside rule-based operational insights derived from clinic metrics—for example, identifying the service with the highest cancellation rate or highlighting recovery message effectiveness.

### Recovery Analytics
Breaks down revenue recovered for the current period, plus a "Revenue Leakage" panel splitting out money lost to cancellations, money lost to no-shows, and money recovered by the AI automation layer.

### Appointment Intelligence
Combines an "AI Worked Today" activity log (reminders sent, appointments confirmed, patients recovered, reviews generated, recovery messages delivered) with a live view of today's schedule and pending-attention items.

---

## Design Principles

- **Information hierarchy** — the most time-sensitive numbers (today's scheduled count, cancellations, confirmation rate) sit at the top of the screen; deeper analytics live further down.
- **Operational efficiency** — the dashboard is built to be scanned in seconds during a shift, not read like a report.
- **Clarity over density** — each panel focuses on one question (What's today's status? What did AI do today? Where is revenue leaking?) rather than combining everything into one dense view.
- **AI assists, doesn't replace** — the interface is designed to make automation legible to staff (what did the AI do, and did it work), not to hide the automation behind a black box.

---

## Engineering Decisions

**Why HTML/CSS/JS?** This dashboard was built to validate product design and the operational workflow itself — what staff actually need to see, and in what order — before investing in a framework. A plain HTML/CSS/JS implementation kept iteration fast and made it easy to test the layout against real screenshots of real clinic data.

**Why dashboard-first design?** Clinic staff don't need a general-purpose admin panel; they need direct answers to a small set of recurring questions during a shift. Structuring the UI as a small number of focused panels (today's status, pipeline, revenue, AI activity) mirrors those actual questions instead of exposing raw data tables.

**Why KPI cards?** The top-level metrics (scheduled, cancellations, confirmation rate, recovered) are the numbers staff need to check first and most often, so they're surfaced as large, high-contrast cards rather than buried in a table.

**Why a healthcare-oriented layout?** The visual language (clinic branding, tooth icon, "AI Command Center" framing) is intentionally specific to a dental/healthcare context, since the dashboard was designed and tested against a real dental clinic use case rather than as a generic business dashboard template.

---

## Tech Stack

| Layer | Technology |
|--------|------------|
| Frontend | HTML |
| Styling | CSS |
| Interactivity | JavaScript |
| Backend API | Node.js / Express (Separate Repository) |
| Workflow Automation | n8n (Separate Repository) |
| Database | Google Sheets |

---

## Screenshots

### Dashboard Overview
![Dashboard Overview](screenshots/dashboard-overview.png)
Today's scheduled appointments, cancellations, confirmation rate, and patients recovered, alongside this month's recovered revenue.

### Login Screen
![Login Screen](screenshots/login-screen.png)
Staff-only sign-in for the clinic's AI Command Center.

### Smart Insights
![Smart Insights](screenshots/smart-insights.png)
Booking-to-attended pipeline alongside rule-based operational insights generated from clinic metrics.

### Recovery Analytics
![Recovery Analytics](screenshots/recovery-analytics.png)
Revenue recovered this month, plus a breakdown of revenue lost to cancellations and no-shows versus revenue recovered by automation.

### Appointment Intelligence
![Appointments](screenshots/appointments.png)
A daily automation activity log ("AI Worked Today") paired with today's live schedule and pending-attention items.

---

## Lessons Learned

Designing this dashboard was less about the frontend code and more about figuring out what clinic staff actually need to see, and in what order, during a busy shift. Early iterations tried to show everything at once; the more useful version turned out to be a small number of focused panels that each answer one question clearly.

The other lesson was that building automation is only half of the solution. Operational teams also need visibility into what the automation is doing, why certain outcomes occurred, and whether those workflows are actually improving clinic operations. Features like "AI Worked Today", recovery analytics, and operational insights were designed to provide that transparency and help staff trust the automation running behind the scenes.

---

## Connect

* 💼 **LinkedIn:** https://linkedin.com/in/dhruva-reddy-gaddam
* 💻 **GitHub:** https://github.com/GDR-26
* 🌐 **Portfolio:** *Coming Soon*
