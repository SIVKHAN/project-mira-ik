# Project Mira
**AI-Powered Project Intelligence Assistant**  
Capstone Project | Applied Agentic AI  

**Author:** Sivakumar Ganesan  
**Organization:** Nexora Pvt. Ltd. (Client: ABCDE Ltd.)

---

## Try Mira Live
You can chat with Mira directly here:  
**[Open Mira Chat](https://ikmira.app.n8n.cloud/webhook/ef4f4d56-0dbc-4301-9617-1ed03cac6433/chat)**

Example prompts you can try:
- `Generate a project plan for the AI Adoption Project at ABCDE Ltd.`
- `Which tasks are blocked or at risk of missing their deadline based on the task board?`
- `Generate a weekly status report for: "Things are going fine."` (tests the guardrail)

---

## Overview
Mira is a multi-agent system built with **n8n + GPT-4o-mini + Langfuse** that helps Project Managers and TPMs by:

- Generating grounded project plans
- Producing risk assessments
- Creating weekly status reports from task boards
- Detecting blockers (e.g. security reviews)
- Refusing vague / underspecified requests instead of hallucinating

---

## Architecture
Mira uses a **Router / Dispatcher** pattern:

- User request → Dispatcher Agent → Router Switch
- Routes to one of four specialist agents:
  - Planner Agent
  - Risk Assessor Agent
  - Timeline & Schedule Advisor
  - Status Reporter Agent
- Supporting flows:
  - Weekly Status Automation (scheduled)
  - Error Handler (logs failures to Langfuse)

See the architecture diagram in the repository.

---

## Key Design Decisions
- **Router pattern** chosen because request types vary widely (plan vs risk vs status)
- **Direct file grounding** (no RAG in baseline) using project CSVs/TXT files
- **Strong guardrails** against vague inputs (T2, T4, T6, T9)
- **Full observability** via Langfuse
- **Cost-efficient**: GPT-4o-mini (~$0.000069 per run)

---

## Baseline Evaluation (T1–T12)
| Metric                        | Result      |
|------------------------------|-------------|
| Total Tests                  | 12          |
| Pass                         | 11          |
| Partial                      | 1           |
| Vague Input Rejection Rate   | 4/4 (100%)  |
| Blocker Detection (T024)     | Pass        |
| Average Latency              | ~2 seconds  |

Known limitations (documented honestly):
- Exact deterministic task counts (T10) still imperfect
- Top-3 risk ranking (T7) inconsistent in some runs

---

## Repository Contents
- `Project Mira - Core Pipeline.json` – Main n8n workflow
- `MIRA Error Handler.json` – Error logging workflow
- Architecture diagram & writeup
- Baseline Test Results
- Cost Analysis & Metrics
- Capstone Slide Deck
- Screenshots (canvas + positive/negative examples)
- Supporting BRD / PRD / Ground Truth documents

---

## Tech Stack
- n8n (orchestration)
- OpenAI GPT-4o-mini
- Langfuse (tracing & observability)
- Google Drive (project data source)

---

## License
This project was created as part of an Applied Agentic AI capstone.  
Feel free to explore and learn from it.
