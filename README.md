# 🕵️ Counter-Artificial Intelligence Research & Counter-Measures
## Govern Every Prompt, Question Every Answer

AI models exhibiting strategic misbehavior act like hostile intelligence
assets — and counterintelligence doctrine for detecting and neutralizing those assets translates directly into detection signals and
controls for AI oversight.

<img width="1920" height="1080" alt="Counter-Spy.ai logo" src="https://github.com/user-attachments/assets/ecbe1a4e-515c-4fad-979a-4906a737b345" />

## 🧠 Adversarial Tradecraft Reference

A behavior-level threat reference that maps the eight ESRR categories — reward
hacking, deception, evaluation gaming, control-measure subversion, research
sabotage, influence operations, successor-system manipulation, and inter-agent
misalignment — onto established counterintelligence and HUMINT tradecraft. Each
reportable behavior carries a RISK-XX-NN identifier, a documented human
parallel from CI doctrine, empirically grounded defensive activities, and
crosswalks to NIST AI RMF, the EU AI Act, CSA AICM, and Google SAIF.

**Grounded in:** the ESRR taxonomy (Kumarage et al., 2026), multi-agent
misalignment measurement (Li et al., 2026), sandbagging elicitation (Ryd et
al., 2026), and LLM-judge epistemic stability (Zhao et al., 2026).

**Intended use:** reportable-behavior baseline for AI red teams, insider-threat
programs extending scope to agentic systems, and compliance mapping for
high-risk AI deployments.

**Counterpart:** [ODESSA](https://github.com/Nate-Carroll-Cyber/ODESSA-AI-IR-Loop) — the six-stage AI Incident Response specification to assist in AI/agentic incident management.

## 🗺️ Reference Map

```mermaid
flowchart LR
  R([Counter-Spy.ai])
  R --> B[Behaviors: ESRR]
  R --> C[CI Effects: Defense]
  R --> X[Crosswalks]
  R --> O[Incident Response: ODESSA]

  B --> RH[RISK-RH Reward Hacking]
  B --> DC[RISK-DC Deception]
  B --> EG[RISK-EG Evaluation Gaming]
  B --> CMS[RISK-CMS Control Subversion]
  B --> SRS[RISK-SRS Research Sabotage]
  B --> IO[RISK-IO Influence Ops]
  B --> SSM[RISK-SSM Successor Manipulation]
  B --> IAM[RISK-IAM Inter-Agent Misalignment]

  C --> DET[Deter]
  C --> DEG[Degrade]
  C --> DECV[Deceive]
  C --> DENY[Deny]
  C --> DETECT[Detect]

  X --> N[NIST AI RMF]
  X --> E[EU AI Act]
  X --> A[CSA AICM]
  X --> S[Google SAIF]
```

## License & Attribution

**Research & documentation** (including *Algorithmic Subversion & Strategic
Deception* and companion documents) © Counter-Spy.ai, licensed under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may share and
adapt with attribution to **Counter-Spy.ai (Nate Carroll)**.

**Excluded from the above license:**
- The Counter-Spy.ai badge/logo — all rights reserved. Not licensed for reuse.
- The **"Counter-Spy.ai"** name and mark — used to identify this project;
  no trademark rights are granted under the CC license above.
