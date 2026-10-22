# BACSE203: Computer Networks — Case Study 5
## POP3 Mailbox Access in a Low-Bandwidth Branch

[![Course](https://img.shields.io/badge/Course-BACSE203%20Computer%20Networks-blue)](https://github.com/ArunyaSrivastava/BACSE203-CaseStudy5-POP3)
[![Status](https://img.shields.io/badge/Status-Complete%20%26%20Verified-success)](https://github.com/ArunyaSrivastava/BACSE203-CaseStudy5-POP3)
[![Target](https://img.shields.io/badge/Evaluation%20Target-100%2F100%20Marks-gold)](https://github.com/ArunyaSrivastava/BACSE203-CaseStudy5-POP3)

This repository contains the complete research, architectural design, network simulation, packet captures, and final academic reports for **Case Study 5: POP3 Mailbox Access in a Low-Bandwidth Branch** under the **BACSE203: Computer Networks** curriculum at the **School of Computer Science and Engineering (SCOPE), Vellore Institute of Technology**.

---

## 📌 Repository Contents & Quick Links

| File / Artifact | Description |
| :--- | :--- |
| **[`TEAM_AGENT_HANDOFF.md`](./TEAM_AGENT_HANDOFF.md)** | **Master Team Handoff & AI Agent Prompts for Persons 1 to 5.** Contains copy-paste prompts for teammates to execute their parts using AI assistants. |
| **[`AGENT_PROGRESS_LOG.md`](./AGENT_PROGRESS_LOG.md)** | **Project Continuity & Turn Changelog.** Turn-by-turn operational log documenting actions, context, and instructions for incoming AI agents. |
| **[`Case Study 5 - POP3 Mailbox Access in a Low-Bandwidth Branch.docx`](./Case%20Study%205%20-%20POP3%20Mailbox%20Access%20in%20a%20Low-Bandwidth%20Branch.docx)** | **The Complete Master Report** formatted in the official university template (260+ paragraphs, 6 tables, diagrams, complete answers to a, b, c). |
| **[`Case Study 5 - Person 1 - Protocol Theory & Limitations.docx`](./Case%20Study%205%20-%20Person%201%20-%20Protocol%20Theory%20&%20Limitations.docx)** | **Person 1 Standalone Deliverable:** Section 1 Overview + Section 6.1 (Question a) with embedded high-resolution diagrams. |
| **[`Case Study 5 - Person 3 - Simulation & Packet Analysis.docx`](./Case%20Study%205%20-%20Person%203%20-%20Simulation%20&%20Packet%20Analysis.docx)** | **Person 3 Standalone Deliverable:** Section 5 with Table 4, live terminal logs, and Wireshark packet capture frame analysis. |
| **[`pop3_wireshark_capture.pcap`](./pop3_wireshark_capture.pcap)** | **Standard Wireshark PCAP file** with 25 simulated frames (TCP handshake, plaintext credentials, link flap, and `-ERR [IN-USE]` lock contention). |
| **[`run_wireshark_pop3_sim.py`](./run_wireshark_pop3_sim.py)** | **Live Python Simulation Script** generating live traffic on `Loopback: lo0` (Port 1110) for Wireshark live captures. |
| **[`pop3_state_machine.png`](./pop3_state_machine.png)** | High-resolution diagram of the RFC 1939 Finite State Machine (Authorization $\rightarrow$ Transaction $\rightarrow$ Update). |
| **[`pop3_bottlenecks.png`](./pop3_bottlenecks.png)** | High-resolution architectural diagram illustrating the 4 core failure bottlenecks across satellite WAN links. |
| **[`Team_Work_Split_Quick_Action_Plan.pdf`](./Team_Work_Split_Quick_Action_Plan.pdf)** | Concise 2-page task delegation guide for the 5-member team. |
| **[`Case_Study_5_Team_Work_Split_Charter.pdf`](./Case_Study_5_Team_Work_Split_Charter.pdf)** | Full 4-page execution charter with responsibility matrices, viva defense questions, and rubric mappings. |

---

## 🎯 Case Study Scenario & Constraints

* **Scenario:** A remote enterprise branch office operates over an intermittent, high-latency satellite WAN and requires reliable email access.
* **Bandwidth:** 256 kbps (rate-limited backhaul).
* **Latency:** 450 ms Round-Trip Time (RTT) geostationary propagation delay.
* **Packet Loss:** 5% random bit error rate / drop rate.
* **Email Payload:** Multi-part MIME messages with 3 MB attachments inflating to 4.11 MB (~37% Base64 + CRLF expansion).
* **The Solution:** A 5-tier resilient email access workflow utilizing a local branch edge store-and-forward proxy (Dovecot/Fetchmail), selective two-phase header pre-fetching via `TOP msg 0`, wire-level compression, and outbound SMTP spooling with exponential backoff.

---

## 👥 Team Work-Split Summary

| Member | Assigned Role | Primary Section Ownership |
| :--- | :--- | :--- |
| **Person 1** | **Lead Protocol Analyst & FSM Architect** | Section 1 (Overview) & Section 6.1 (Question a: Theory & Limitations) |
| **Person 2** | **WAN Systems & Workflow Architect** | Section 1.1–1.4 (WAN Modeling) & Section 6.2 (Question b: 5-Tier Workflow Design) |
| **Person 3** | **Simulation & Packet Analysis Specialist** | Section 5 (Implementation, Wireshark Trace Disassembly & Terminal Logs) |
| **Person 4** | **Cybersecurity & Threat Analyst** | Section 6.3 (Question c: Security Threats, APOP MD5 Flaws & Hardening Blueprint) |
| **Person 5** | **Standards, Benchmarks & Polish Lead** | Tables 2, 3, 5, Section 4 (Findings), Section 7 (Conclusion), Section 8 (References) |

*(For detailed AI prompts and instructions for each member, see **[`TEAM_AGENT_HANDOFF.md`](./TEAM_AGENT_HANDOFF.md)**).*

---

## 🚀 How to Run the Wireshark Simulation Live

1. Open **Wireshark** on your machine and double-click the **`Loopback: lo0`** interface.
2. In the display filter bar at the top, enter:
   ```text
   tcp.port == 1110
   ```
3. In a terminal, run:
   ```bash
   python3 run_wireshark_pop3_sim.py
   ```
4. Wireshark will capture the live frames showing the TCP handshake, cleartext password exposure, link drop, and `-ERR [IN-USE]` mailbox lock contention!
5. In Wireshark, right-click any packet $\rightarrow$ select **Follow** $\rightarrow$ **TCP Stream** to inspect the full color-coded conversation.

---

## 📄 License & Academic Integrity
Prepared for educational purposes for **BACSE203 Computer Networks** at VIT (SCOPE).
