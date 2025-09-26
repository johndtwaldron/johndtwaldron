# JDW — z/OS Proof-of-Work (IBM MQ on z/OS)

A living, markdown write up no-fluff record of my **IBM MQ on z/OS** experience: what I’ve shipped, how I diagnose, and the practices I use to keep regulated banking systems healthy. Written to be skim-friendly for recruiters but deep enough for engineers.

---

## Snapshot

- **Role & tenure:** IBM UK — Software Engineer (MQ on z/OS), **2017–2024**. Focus on MQ for z/OS across global banking/payments: QA, L3 triage/APARs, SMP/E installs, CST integration, CI/CD. :contentReference[oaicite:0]{index=0}  
- **Recognition:** **IBM MQ “ROCK IT” Award – Best Newcomer (2017)**; **IBM Systems Technical University Speaker (2019)**; Lab Advocate for major banks. :contentReference[oaicite:1]{index=1}  
- **Core stack:** z/OS, ISPF/SDSF/TSO/OMVS, **JCL, REXX, C/HLASM**, RACF, TCP/IP, **SMP/E**, MQ QMgr setup, automation tooling (Git/Jenkins/RTC). :contentReference[oaicite:2]{index=2}

---

## Career Highlights (IBM 2017–2024)

- **CST lead for MQ on z/OS:** owned validation flows, unblocked integrations, and drove readiness across complex mainframe environments. :contentReference[oaicite:3]{index=3}  
- **Defect triage & APARs:** daily root-cause on red builds & customer issues (product vs env vs harness); contributed L3 fixes/APARs to stabilize live systems. :contentReference[oaicite:4]{index=4}  
- **SMP/E installs & maintenance:** regular z/OS MQ installs and maintenance verification for delivery sign-off. :contentReference[oaicite:5]{index=5}  
- **Banking workflows:** strong grasp of batch flows, transaction integrity & compliance in financial environments. :contentReference[oaicite:6]{index=6}  
- **Advocacy & enablement:** Lab Advocate for banks; authored runbooks/onboarding; delivered international zTech talks (e.g., TechU Las Vegas). :contentReference[oaicite:7]{index=7}

---

## Deeper Dive (how I work)

### 1) Build, install & operate MQ on z/OS
- **Install/maintain via SMP/E**; confirm CSI health, APPLY CHECK, log review. :contentReference[oaicite:8]{index=8}  
- **Queue manager bring-up:** TODL-driven configuration; step-by-step “from scratch” QMgr setup references from internal education material. :contentReference[oaicite:9]{index=9}  
- **z/OS vs Distributed mental model:**  
  - z/OS exploits **SAF/RACF** authorization (security admin in the loop).  
  - Storage via **pagesets & bufferpools** (contention awareness); BSDS & **dual logging**.  
  - Shared Queues in CF (DB2 prereqs). 

### 2) Problem determination & dump/trace workflow
- **IPCS/ICPS quick-hits I keep handy:**
  ```text
  ip verbx csqwdprd,'subsys=MQ##,tt'   ; Queue manager dump formatter
  ip verbx csqxdprd,'subsys=MQ##,tt'   ; CHINIT dump formatter
  ip st regs                           ; Registers/PSW snapshot
(tt = trace id; MQ## = subsystem). ICPS Dump help

When to capture & how: console DUMP, SLIP, or RECOVER QMGR(MQRD,xxxx,n) for reason-code triggered dumps; format with CSQWDPRD/CSQXDPRD. 10541 Diagnosing problems for M…

Diagnose like an L3: start with concrete symptoms (CC/RC), get specifics (queue, app, when/how often), then correlate joblog (CSQx**) messages/abends (5C6/6C6 + reason bytes). 10541 Diagnosing problems for M…

Assembler-level awareness: PSW/registers, common abends (0C1/0C4/0C7) to orient on failing path quickly. zEducation_Stage2_ASM_RuntimeDe…

#3) Monitoring & “normal state” baselining
Real-time checks: DISPLAY QSTATUS/CHSTATUS (watch XQTIME/NETTIME/XBATCHSZ etc.), dspmqrte for route expectations. 10541 Diagnosing problems for M…

SMF data: performance stats SMF 115, accounting SMF 116; feed into tools for trend/alerting; configure instrumentation events (queue/channel/perf/config/command). 10541 Diagnosing problems for M…

#4) MQ on z/OS in the enterprise
Integration touchpoints: CICS/COBOL batch, DB2, IMS, WAS; I’ve validated cross-product flows in CST and in-house harnesses. John Waldron Mainframe QA Aug 2…

Customer rhythm: I’ve acted as Lab Advocate—triaging live issues, aligning requirements, and translating deep tech to business outcomes. JDW Mainframe CV June 25

Selected Snippets I keep close (to be expanded in this repo)
SMP/E APPLY CHECK JCL skeleton & CSI sanity checks. (Will publish here.) JDW Mainframe CV June 25

QMgr “from scratch” checklist (TODL tags, attributes, CHINIT bring-up). Setting up QMGR from Scratch

IPCS one-pagers (CSQWDPRD/CSQXDPRD verbx options & symptom dump triage).

SMF 115/116 extraction notes for perf/accounting reviews. 10541 Diagnosing problems for M…

Credentials (anchor items for MQ/z/OS)
IBM MQ “ROCK IT” Award – Best Newcomer (2017); IBM Systems Technical University Speaker (2019). JDW Mainframe CV June 25

IBM MQ Developer Essentials (Credly, 2023); Interskill – IBM Mainframe Environment Fundamentals 2.4 (2023). John Waldron Mainframe QA Aug 2…

---
#Recent Upskilling PoW (post-2014, z/OS-relevant)
IBM: Introduction to System Programming on IBM Z (Jul 2025); Introduction to z/OS Commands & Panels (Jul 2025); TCP/IP on z/OS Essentials – L1 (Jul 2025); z/OS TCP/IP Configuration with NCA (Jul 2025); z/Architecture Assembler Language — Part 1 (Jul 2025); IBM COBOL Basics (Jul 2025). John Waldron Mainframe QA Aug 2…

Why this matters for my next role
I bring a rare blend of hands-on MQ z/OS delivery, production-grade diagnostics, and banking-grade QA/DevOps discipline. I’m comfortable deep in IPCS, on the SMP/E side, or at the CST pipeline—and translating all of it for stakeholders who just need it to work.
