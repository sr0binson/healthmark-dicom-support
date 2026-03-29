# HealthMark DICOM Transfer Support System

A self-service troubleshooting system built for HealthMark's Purview clients and support team — designed in response to the February 2026 Purview acquisition and the wave of DICOM transfer support tickets that will follow as existing HealthMark clients onboard to cloud-based medical imaging.

---

## Why this exists

Two-thirds of radiological images are still shared via physical discs. HealthMark's acquisition of Purview is designed to change that — but moving hospitals and clinics from CDs to digital DICOM transfers creates a predictable first wave of support issues: AE Title mismatches, network connectivity failures, partial transfers, new device setup, and patient matching errors.

This project builds the support infrastructure for that transition — a two-audience system where client-facing and agent-facing tools draw from a single updatable knowledge base.

---

## The system

Three files. One source of truth.

```
knowledge-base.json          ← all issue content lives here
dicom-customer-app.html      ← client-facing self-service tool
dicom-agent-app.html         ← internal agent diagnostic console
```

### `knowledge-base.json`
The single source of truth. Every issue, every resolution step, every escalation path is stored here in structured JSON. To add a new issue or update existing steps, edit this file — no code knowledge required. Both apps read from this data structure.

Each issue contains two complete content sets:
- **`customer`** — plain language, safe self-checks, "go deeper" optional content, and a "tell support" summary
- **`agent`** — technical summary, plus three tiers: Basic, Investigative, and Escalate

### `dicom-customer-app.html`
Built for clinic coordinators, medical records staff, and hospital admins — the people who will call HealthMark support when Purview transfers fail. Written for someone who has never heard of DICOM.

Features:
- Symptom picker — select what you're seeing, get immediate guidance
- Keyword search — searches across titles, symptoms, summaries, and steps
- Checkable self-service steps — a few safe things clients can try themselves
- Optional "go deeper" section — for clients who want to understand more without being overwhelmed
- "Tell support" summary — what to have ready before calling
- No technical jargon, no commands, no assumptions

### `dicom-agent-app.html`
Built for HealthMark support staff — written for someone who is smart and capable but may be new to DICOM specifically. Every issue has three tiers:

| Tier | For |
|------|-----|
| **Basic** | First-response questions to ask the caller. No tools needed. |
| **Investigative** | Exact commands with expected output explained. Step-by-step technical resolution. |
| **Escalate** | Specific conditions that mean hand it off — and exactly who to hand it to. |

The three-tier structure mirrors real help desk methodology: handle what you can, dig deeper when needed, escalate with precision.

---

## Issues covered

| # | Issue | Severity |
|---|-------|----------|
| 01 | Scanner says Transfer Complete but images never arrived | 🔴 Urgent |
| 02 | Scanner shows an error immediately — won't connect | 🔴 Urgent |
| 03 | Only some images arrived — incomplete study | 🟡 Moderate |
| 04 | New scanner or device can't send images | 🟡 Moderate |
| 05 | Images transferred but under the wrong patient | 🟢 Non-urgent |

---

## How to use

Both apps are fully self-contained HTML files — open either one directly in any browser. No server, no dependencies, no install.

The knowledge base is embedded in each app at build time. To update content, edit `knowledge-base.json` and rebuild the apps. This keeps the content decoupled from the code — a support manager can maintain the knowledge base without touching HTML.

---

## Built by

**Stacy Robinson** — IT Support Intern, Boise School District  
Portfolio: [s-rportfolio.vercel.app](https://s-rportfolio.vercel.app)  
LinkedIn: [linkedin.com/in/sr0binson](https://linkedin.com/in/sr0binson)

Built as a portfolio project demonstrating DICOM troubleshooting knowledge, two-audience content design, and support systems architecture — timed to HealthMark's Purview acquisition and the imaging support needs it creates.
