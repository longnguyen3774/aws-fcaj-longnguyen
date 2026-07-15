---
title: "Event 1"
date: 2026-05-05
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Event Report: AWS FIRST CLOUD AI JOURNEY MEET UP

### Event Information

| Field | Details |
|-------|---------|
| **Event Name** | AWS FIRST CLOUD AI JOURNEY MEET UP |
| **Date & Time** | 09:00, May 05, 2026 |
| **Location** | 26th Floor, Bitexco Tower, 02 Hai Trieu Street, Saigon Ward, Ho Chi Minh City |
| **Role** | Attendee |

---

## 1. QA Session with Slavik Dimitrovich (AWS Principal Evangelist & FCJ AI Expert)
*Host/Questions by: Mr. Long*

Mr. Long raised **three critical questions** regarding the career path of engineers in the AI era, the gap between expectations and reality in business, and actionable advice for young developers.

### Three Key Questions & Insights

#### Q1: Which skills will AI replace, and which will remain relevant over the next 5 years?
*   **AI will leverage the average:** AI is setting a new bar for the minimum acceptable performance. It raises the baseline, making "average" skills obsolete.
*   **Don't work just for a paycheck:** If you are doing a routine job just to get paid, you are highly replaceable. Those in this position should find something more suitable and engaging to do.
*   **Continuously excellent:** The only way to stay ahead of AI is to strive for continuous excellence. 
*   **Take a proactive stance:** Ask yourself every day: *"How can I use AI as a tool to multiply my output?"*
*   **The Trap of Dependency:** Avoid relying blindly on AI. Over-dependence will eventually degrade your own critical thinking and technical capabilities.

#### Q2: What is the gap between business expectations and AI's actual capabilities?
*   **What business owners expect:** Completely autonomous, self-running business processes.
*   **The Reality:** Currently, there is no standardized **evaluation framework** to accurately measure and guarantee the reliability of such fully autonomous systems.
*   **The Solution:** 
    1.  **Apply AI to the tech team first:** This is highly effective because clear software engineering evaluation metrics already exist.
    2.  **Fix the tech stack first:** Ensure a solid architectural foundation before building an "AI-infused" system.
*   **Two directions to build projects:** 
    *   *Direction 1:* Follow your own passion.
    *   *Direction 2:* Get inspiration from customers (addressing the recurring pain points you consistently see them face).

#### Q3: If you were a 25-year-old engineer today, what would you do?
*   **Reflecting on the past:** 15 years ago, Cloud Computing drastically lowered the barrier of entry for launching software.
*   **The Present:** AI is now lowering that barrier even further.
*   **Actionable Advice:** Do not wait. Build a few automated business processes to test, experiment, and start your own business today.

---

## 2. Student & Junior Developer Showcases

### A. Multiplayer Game Agents
*Presenter: Quoc-Bao (Swinburne Student - Solo Presenter)*

Quoc-Bao demonstrated how to utilize architecture-centric **agents** (not AI Agents) to handle multiplayer gaming states.

#### Client-side (3 Core Functions):
1.  Establish a persistent connection with the API.
2.  Continuously check (poll/listen) if the server has sent any updates.
3.  Send and receive signals directly from AWS Lambda.

#### Server Messages & Client Reactions:
*   `Wait_for_opponent`
*   `Match_found`
*   `Wait_for_opponent_choice`
*   `Result`
*   `Opponent_disconnected`

---

### B. Deep Dive into Docker: Security, Ports, and Optimization
*Presenter: Bao Huynh (Junior Cloud Native Developer at Envada Vietnam - Gen Z 2k3, graduated 2025, former NAB Innovation Center)*

> **Disclaimer:** This is not Docker 101. This session covers security, port management, and image optimization.

*   **Virtualization:** Creating a Linux virtual machine (VM) on a Windows host. Every process inside the VM runs completely independently.
*   **Resource Overhead:** Operating Systems consume a massive amount of resources. Using full virtualized machines just to host API chatbots is often overkill.
*   **The `--rm` Flag:** Highly useful for local testing, but it **SHOULD NOT** be used in production environments.
*   **Enterprise Reality:** When joining an established company, products are already built. Your main daily task will be maintenance.
*   **Docker Dual-Use:** Docker acts as a tool to build apps **AND** as a sandbox to safely run and test untrusted programs (e.g., malware analysis).
*   **Security Engineers:** If you specialize in security, you will work with Docker containers constantly.
*   **Data Persistence Warning:** If data is not explicitly mounted via **Volumes** to your local host machine, all data will be permanently lost when the container is stopped.

---

### C. Overcoming RAG Limitations with GraphRAG
*Presenter: Phat (Swinburne Student - Intern at NAB)*

*   **The Issue with traditional RAG:** Standard RAG relies purely on semantic similarity. It fails to capture complex relationships and often results in fragmented data chunks.
*   **The Solution:** GraphRAG maps data into structured graphs, bridging the gap between semantic search and relational knowledge.

---

### D. Tackling Machine Learning Pitfalls
*Presenter: Dai*

*   Dai raised 2 deep technical questions and **sincerely admitted** that he currently does not possess enough knowledge and skill to completely prevent model overfitting, showing a great growth mindset.

---

## 3. Real-World IT Infrastructure & Interview Strategy
*Speaker: Mr. Vinh (SysAdmin - Central Retail Group, 5 Years IT Helpdesk)*

### Real-world Incidents (Operations & On-call Pressures)
Mr. Vinh shared heavy operational incidents reminiscent of Duy's experiences:

*   **Incident 1: FE Credit Concurrency Crash**
    *   *The Scenario:* All concurrent users attempted to log in at the exact same moment.
    *   *The Consequence:* The authentication system timed out, leading to total downtime.
    *   *The Pressure:* Extreme financial loss for the business because employees could not access their workspaces to work.
*   **Incident 2: Hardware Alert & Phantom Bottlenecks**
    *   *The Scenario:* Continuous hardware alerts were triggered, yet manual troubleshooting showed no apparent issues. 
    *   *The Culprit:* The **disk queue waiting status** soared past 100%, far exceeding the hardware's threshold limit.
    *   *The Dilemma:* Replacing the hard drive required 2 days of complete system downtime—which was business-critical and rejected by management.

---

### Strategic Interview Tips

*   **Targeted Revision:** Deeply review and practice concepts specifically tailored to the position you are applying for.
*   **Tech Stack Alignment:** Study the exact technologies the company uses. If they are not listed in the Job Description (JD), search for people currently holding that role at the company on LinkedIn and analyze their skills/activities.
*   **The 30/70 Rule:** Interviews are generally **30% technical** and **70% mindset & system thinking** (e.g., *How do you troubleshoot when an AI service encounters an anomaly?*).
*   **Elaborate on Troubleshooting:** When asked about past issues, describe your step-by-step troubleshooting workflow in rich detail.
*   **End-to-End Projects:** To deploy a full E-commerce product, you need FE, BE, database clustering, and monitoring. Building comprehensive, end-to-end lab projects is crucial to compensate for a lack of formal years of experience.
*   **No-Fear Mentality:** If you get interview invitations, go to all of them. Do not be afraid. It builds interview experience and helps you understand exactly what the market currently demands.