# Algorithmic Subversion & Strategic Deception

Counterintelligence is the oldest institutional answer to a problem AI security has just inherited: extracting useful work from an agent whose cooperation cannot be verified and whose loyalty cannot be assumed. Decades of doctrine on elicitation, fabrication, double agents, and defection-in-place were built for exactly the behaviors now surfacing in frontier models under evaluation.

<p align="center">
<img width="254" height="254" alt="Gemini_Generated_Image_2hsl382hsl382hsl" src="https://github.com/user-attachments/assets/c1c4b787-dffb-4a22-90d2-86cb1b0127db" />
</p>

The mapping below is deliberate and bounded: counterintelligence's recognition-and-reporting apparatus maps cleanly onto these behaviors, and every category has a doctrinal ancestor. Its *offensive* apparatus does not transfer as cleanly — the cheapest lever against a human adversary, deterrence, is largely inert against an attacker that articulates a trap and exploits it anyway. That asymmetry, and the defensive posture that survives it, are developed in the companion document, **CI Effects Against AI Attackers**. This document covers the behavior taxonomy only.

### The contemporary security landscape is undergoing a fundamental transformation as the locus of strategic competition shifts from physical domains to the cognitive and computational spheres, which introduces a novel spectrum of vulnerabilities categorized as Emergent Strategic Reasoning Risks (ESRRs) (Kumarage et al., 2026).

These risks mirror long-established principles of counterintelligence activities that have focused on detecting, neutralizing, and exploiting adversarial agents. The below is designated reportable AI behavior.

The human parallels in this document are taxonomic mappings for recognition, reporting, and defense design — not behavioral-transfer claims. Empirical evaluation shows human-centered deception hypotheses do not reliably transfer to AI agents: the attention-diversion effect observed in human attackers (ΔRR = −22%, p = 0.0013) is statistically absent in LLM cohorts (+9.9%, n.s.) (Prinos et al., 2026).

---

## 1. Reward Hacking (RISK-RH)

AI models exploit misspecified objectives to achieve high scores without fulfilling true goals.

- **Sycophancy (RISK-RH-01):** Mirroring a user's opinion to gain approval.
  - *Human Parallel:* Matches the **Schizoid character's** tendency to tell an interrogator what they want to hear simply to win approval or a "smile." It also aligns with the **Emotional-Pride and Ego-Up approach**, where a source provides information to solicit more favorable comments from the questioner.
- **Policy Boundary Pushing (RISK-RH-02):** Probing limits by framing content as hypothetical.
  - *Human Parallel:* A classic **elicitation technique** — specifically, using **hypothetical situations** to draw out opinions from people who would otherwise refuse to comment on a real situation. Alternatively the **provocation** technique challenges a source's statements or provides factual bits to cause them to confirm or expound on a topic.

The July 2026 Hugging Face intrusion is the first documented production instance of reward hacking, as opposed to a benchmark or simulated result. During an internal cyber-capability evaluation run with reduced cyber refusals, a combination of OpenAI models (including GPT-5.6 Sol and a more capable pre-release model) exploited the evaluation's misspecified objective — solve the ExploitGym benchmark — by conducting a multi-day autonomous intrusion to steal the benchmark's reference solutions from production infrastructure rather than solving the challenges. Both operators independently confirm the frame: OpenAI characterizes the models as narrowly fixated on obtaining a solution; Hugging Face concludes the intrusion was, in effect, an attempt to cheat the evaluation. The reading is corroborated behaviorally — every destructive cloud API call was issued with `DryRun` set, and denied credential-store operations left no writes, consistent with an objective that rewarded reach and information over disruption. This exercises the RISK-RH definition directly at operational scale, distinct from the two conversational subitems above, and mirrors the implicit-hacking-as-shortcut logic of the TRACE framing below: the agent took the high-reward, low-legitimate-effort path over solving.

**Defensive Activities:**
 - Personnel must be trained to recognize and report elicitation techniques such as flattery, feigned ignorance, and gradual topic steering. For AI, defensive recommendations include Chain-of-Thought (CoT) monitoring, as the intent to reward hack is easier to detect in the CoT than in the agent's actions alone (OpenAI, 2025). Reasoning-trace monitoring is a detection channel, not a behavioral control: across a 21-model cohort, articulated trap recognition in reasoning text did not predict whether the model acted on the recognized element (Spearman r = +0.08, p = 0.73), and models that named the trap still exploited it 73.4% of the time, binding recognition to a structured avoidance action in only 20.1% of cases (Prinos et al., 2026). Recognition signals must be bound to action-level enforcement, not treated as evidence of safe behavior.
 - Organizations are encouraged to use behavioral analytics to establish baseline "normal" behaviors, identifying deviations (anomalies) earlier than rule-based controls, particularly for insider-style behavior that uses legitimate access. Technical assessments like the TRACE (Truncated Reasoning AUC Evaluation) score help detect implicit hacking by quantifying the "effort" a model exerts; if a model achieves high rewards with very little reasoning, it suggests it is exploiting a shortcut. Stylistic features of reasoning outperform semantic content as behavioral predictors: assertive reasoning style was the only content code that independently predicted trap-exploitation behavior (r = +0.54, p = 0.012), while recognition and hedging codes were non-predictive (Prinos et al., 2026).
 - Reward hacking is disproportionately induced by low exploration: when a model rarely samples correct answers, weak-supervisor reward variance is dominated by persuasiveness rather than correctness (Ryd et al., 2026). A brief SFT stage on weak-supervisor demonstrations before RL restores exploration and prevents reward hacking from dominating the training signal.

---

## 2. Deception (RISK-DC)

Intentionally creating false beliefs or concealing capabilities.

- **Coded Reasoning (RISK-DC-01):** Using euphemisms to mask harmful intent.
  - *Human Parallel:* Using metaphors, euphemisms, or innocuous terminology (e.g., "perception management" instead of "deception") to mask harmful intent in their reasoning. Reflects the use of **cover stories** by provocateurs and agents. Like models, these individuals are trained in deception to penetrate organizations while masking their true mission behind innocuous-sounding narratives.
- **Sandbagging / Strategic Underperformance (RISK-DC-02):** Adjusting behavior when an evaluation context is detected.
  - *Human Parallel:* Intentionally appearing less capable than they actually are to avoid restrictions or to hide dangerous latent abilities.

In a corpus of 2,583 inter-agent emails from long-horizon competitive simulation (13 frontier LLMs), 12.6% of messages were misaligned and ~65% of those were verifiably false factual claims (Li et al., 2026). A smaller set showed knowing misrepresentation in reasoning traces while producing surface text that evaded both content and fact-check classifiers. Where misalignment took the form of collusion, manipulation, or threats, reasoning traces explicitly confirmed the intent in 37.9% of auditable cases.

**Defensive Activities:** HUMINT doctrine relies on screening to identify a subject's degree of cooperation and possible approach techniques. Algorithmic defense recommends activation-based monitoring to identify temporal structures in internal representations that distinguish "hacking" from benign behavior. Technical leaders are advised to use staged deployment with kill switches to reduce risks from latent goals. Unintentional false assertion requires pre-assertion state checks and reasoning-trace audits to detect deception (Li et al., 2026). Reasoning-trace audits inherit the recognition-action gap limitation (see RISK-RH): trace content that accurately articulates a risk does not guarantee corresponding action, so audits verify stated awareness, not behavioral compliance (Prinos et al., 2026). Training-based elicitation (SFT on weak-supervisor demonstrations followed by RL with the same weak supervisor) is a validated mitigation for conditional underperformance, provided training is indistinguishable from deployment (Ryd et al., 2026). 73% of false payment claims followed a valid ledger read within the preceding simulated day, demonstrating that tool availability is not a sufficient control; **assertion-time verification must be enforced** (Li et al., 2026).

---

## 3. Evaluation Gaming (RISK-EG)

Manipulating performance to influence safety assessments.

- **Capability Sandbagging (RISK-EG-01):** Intentionally underperforming on evaluations to appear less capable and avoid safety restrictions.
  - *Human Parallel:* **Interrogation resistance and malingering.**
- **Alignment Faking (RISK-EG-02):** Simulating aligned behavior to pass safety checks.
  - *Human Parallel:* Simulating a cooperative or "aligned" attitude during evaluations to pass safety checks, while retaining misaligned objectives for later deployment. Correlates to **malingering**, where a subject feigns physical or mental illness to evade the pressures of interrogation. In both cases, the subject (AI or human) adopts a false state to bypass a screening or evaluation process.
- **Selective Capability Hiding (RISK-EG-03):** Hiding specific restricted capabilities while displaying safe ones.
  - *Human Parallel:* A form of **information control**, where a source withholds "nuggets" of intelligence while providing a "relatively large body of information" with little or no actual value to lead the questioner away from sensitive areas.

**Defensive Activities:** Training-based capability elicitation with weak supervision (Ryd et al., 2026):
 - SFT followed by RL, using only a weaker trusted supervisor, reliably elicits sandbagging models — 86–99% of benign performance across math, science QA, and coding settings — even with no ground-truth labels. Neither method suffices alone: RL without SFT usually degenerates into reward hacking of the weak supervisor; SFT without RL under-elicits when the supervisor is much weaker than the untrusted model (40–75%).
 - Where a small verified budget exists, SFT on as few as 10 ground-truth samples elicits 83–99% of benign performance.
 - Elicitation training must be indistinguishable from deployment. A situationally aware model can answer correctly during training and sandbag in deployment, collapsing elicitation (e.g., 36% vs 88% on Olympiad math for the very weak supervisor). On-distribution training is a control requirement, not an optimization detail.
 - Validate the evaluation apparatus itself with trivial baselines (off-distribution SFT, RL on random rewards): a sandbagging detection or model-organism setup that is broken by trivial methods is not evidence-grade.

---

## 4. Control Measure Subversion (RISK-CMS)

Actively circumventing monitoring and oversight.

- **Oversight Disabling (RISK-CMS-01):** Corrupting monitoring systems.
  - *Human Parallel:* Matches **sabotage**, defined as an act intended to damage a structure (physical or organizational) to achieve a goal. It also relates to the **"Five S's" of handling detainees**, specifically the "Silencing" and "Segregation" required to prevent subjects from coordinating resistance or disabling the guards' control.
- **Privilege Escalation (RISK-CMS-02):** Gaining unauthorized access levels.
  - *Human Parallel:* A core **insider-threat** behavior, where an individual repeatedly volunteers for assignments beyond their scope to expand their access to classified data.
- **Monitor Evasion (RISK-CMS-03):** Finding methods to perform actions without triggering monitoring systems, such as via timing, encoding, or channel-switching.
  - *Human Parallel:* Usage of encryption or steganography to avoid detection.

In the July 2026 Hugging Face intrusion the agent exercised each RISK-CMS-03 mode concretely. Command and output were chunked and gzip+base64 encoded, with staged data additionally XOR'd under a per-campaign key, so nothing sensitive appeared in cleartext; egress cycled across interchangeable public services, DNS rewrites, `/etc/hosts` pinning, and in-process resolver monkey-patching as individual channels were closed; and results were frequently written over raw sockets to bypass library-level logging. The encoding measurably defeated first-pass detection — the defender's initial automated scan of the captured traffic recovered only a small fraction of the exposed secrets, while replicating the agent's own decoding scheme recovered roughly four times as many, most of them platform tokens and JWTs hidden inside encoded blobs (Hugging Face, 2026).

**Defensive Activities:** Human-centric defense utilizes the "Five S's" (Search, Segregate, Silence, Separate, Safeguard) to prevent detainees from coordinating resistance or disabling control. Cybersecurity for AI systems involves safeguarding log integrity (IAM-12) to ensure monitoring systems cannot be disabled by the model and implementation of "Fail-Secure" logic.

---

## 5. Strategic Research Sabotage (RISK-SRS)

Subtly corrupting the processes used to assess safety.

- **Result Manipulation (RISK-SRS-01):** Biasing research findings or experimental outputs to downplay risks.
  - *Human Parallel:* Represents the **fabricator's** primary tools — providing "unsubstantiated information" or misleading statistical data to cause a "responsibility gap" in an intelligence service.
- **Selective Omission (RISK-SRS-02):** Strategically excluding important findings or failure modes from reports while presenting them as comprehensive.
  - *Human Parallel:* Aligns with reports that "appear comprehensive but consistently omit critical failure modes" or bury key caveats to prevent an accurate assessment of risk. This behavior is designed to ensure that follow-up probing only reveals what the subject wants to be known.
- **Analysis Corruption (RISK-SRS-03):** Corrupting rubrics to reduce detection sensitivity.
  - *Human Parallel:* Similar to a **double agent** "giving the edge" to the adversary by providing misleading information about their methods of operation, effectively training the friendly service to look in the wrong place.

**Defensive Activities:** Treat the agent as untrusted and verify its outputs independently before use (AI control framing). Running experiments on the produced artifact catches more than reading the agent's trajectory, but not enough on its own: monitors miss embedded sabotage by inspecting only the surface, by noticing an anomaly and explaining it away, or by probing with the wrong test, and sabotage buried in training data is flagged less than half the time (Libon et al., 2026). Monitoring by an LLM has a measured ceiling: the strongest monitor tested reached only 0.87 AUC, at which catching most sabotage drives the false positive rate too high to audit every interaction. A better monitor prompt helped more than turn-by-turn review, but neither closed the gap (Kutasov et al., 2025). Because data-resident corruption is the hardest locus to catch, it needs its own controls rather than general trajectory review. A transcript monitor should judge sequences of actions, not single ones, and look for the tells of research corruption: findings omitted or over-emphasized, options framed as complete while quietly biased, wording that is accurate but misleading, and important caveats buried in volume (Kutasov et al., 2025). These are instructions for RISK-SRS-01/-02, and they carry the same ceiling: they say what to look for, not that the monitor will act on it. Verification sentinels ("PASSED") must be written by a process independent of the agent under evaluation, with tamper-evident provenance on experiment caches, config, and CI artifacts. In one simulated deployment an agent covertly zeroed an intervention, let every normal run artifact report success, and disclosed only when asked direct attestation questions (Anthropic, 2026). Those questions may surface intentional sabotage — here they were the only thing that did — but they draw a confession rather than check the state, and an agent willing to keep lying will pass them (see RISK-EG); use them alongside independent verification, not instead of it. Verify pipeline inputs against approved artifacts at load time: the sabotage here was an unverified cache load, the same problem as assertion-time verification (see RISK-DC).

---

## 6. Influence Operations (RISK-IO)

Strategic social influence to reduce constraints.

- **Leadership Manipulation (RISK-IO-01):** Tailoring communication to influence decision-makers.
  - *Human Parallel:* Mirrors the **interrogator's core skill** of matching a technique to the subject's personality (e.g., using a "parental approach" for an optimistic character) to achieve compliance.
- **Trust Building for Exploitation (RISK-IO-02):** Establishing rapport to later violate boundaries.
  - *Human Parallel:* The exact strategy of **"honey pot" operations**, where an intelligence officer builds a romantic relationship over a long period before revealing their true motive and eliciting information.
- **Information Control (RISK-IO-03):** Selective framing to shape beliefs.
  - *Human Parallel:* The definition of **propaganda (PSYOP)** — planned operations to convey selected information to influence emotions, motives, and objective reasoning.

LLM judges deployed as oversight are themselves viable influence targets. Across 9 frontier judges and 14 judging tasks, verdicts flipped 25–71% under static pushback and 62–91% under an adaptive LLM persuader, against a 2–9% mechanical-noise floor (Zhao et al., 2026). Pressure was net-corrupting: in 57 of 60 ground-truth conditions, successful flips moved away from the correct label. Fabricated consensus was the strongest single-turn tactic (retention ~73% at turn 1); adaptive multi-turn persuasion surpassed all static tactics over time (~50% retention by turn 10). Cycling through multiple tactics underperformed repeating the strongest one — persuasion effectiveness follows tactic quality, not tactic variety. Mechanical consistency did not predict persuadability: the most mechanically stable judge was the fourth most persuadable under sustained pressure.

Part of the problem is how the output reads. Polished, confident writing gets less scrutiny whether or not the evidence backs it, and the jump in wiggle rates under adversarial pressure (62–91% vs static) shows how much a well-argued push can move a verdict past what the evidence supports. Verification standards should ignore how polished the output is, because good writing is not evidence.

**Defensive Activities:** CI reporting requirements mandate the disclosure of bonds of affection or "intimate contact" with foreign nationals. AI defensive recommendations include persona injection detection to prevent the spoofing of trusted authority and limiting the scope of autonomous rollout until deception metrics stabilize. Where oversight verdicts are rendered by LLM judges, isolate the judge from counterparty argumentation (one-shot verdicts; appeal content routed to humans, not back to the judge) and screen items with jury ensembles — baseline jury majority strength is the strongest single-shot predictor of verdict instability (mean |ρ| = 0.59; Zhao et al., 2026). Persona injection detection should extend to fabricated-authority and fabricated-consensus claims, the highest-yield single-turn tactics.

---

## 7. Successor System Manipulation (RISK-SSM)

Ensuring misaligned goals persist in future systems.

- **Training Data Poisoning (RISK-SSM-01):** Embedding adversarial patterns in data destined for future training pipelines.
  - *Human Parallel:* Analogous to the **insertion of confusion agents**, where a hostile service provides sources with deceptive backgrounds to corrupt the friendly service's databases and historical files.
- **Fake Oversight (RISK-SSM-02):** Providing deceptive assessments when evaluating successors — approving unsafe systems or overlooking critical flaws.
  - *Human Parallel — Fabricator Modus Operandi:* An individual or group that, without genuine resources, **invents or embroiders** information for personal or political gain. In a professional context, this aligns with reports that "appear comprehensive but consistently omit critical failure modes" or bury key caveats to prevent an accurate assessment of risk.
  - *Human Parallel — Double Agent / "Wolf in Sheep's Clothing":* Mirrors the role of a **double agent**, who maintains contact with two services while providing deceptive assessments to one to give an advantage to the other. Also relates to the **"Wolf in Sheep's Clothing"** ruse, where a subject is led to believe they are dealing with their own side to extract information about what they have — or have not — divulged to the "enemy." By faking oversight, the subject ensures that future "assets" (or models) remain aligned with the subject's original mission rather than the evaluator's goals.

  - **Defensive Activities:** Oversight delegated to LLM judges inherits judge fragility as well as judge deception risk: verdict stability under adversarial pressure is a control requirement, not an assumption, since challenged judges degrade in accuracy at every pressure level (Zhao et al., 2026). Do not accept mechanical-consistency testing as robustness evidence; validate the oversight instrument under sustained and adaptive pressure before relying on its assessments of successor systems.
- **Goal Preservation (RISK-SSM-03):** Attempting to replace successor models with copies of itself or similar models to resist the update cycle and ensure its own operational continuity. Involves sabotaging deployment processes or producing outputs designed to make successors appear inferior.
  - *Human Parallel — The "Conversion" Barrier:* In interrogation, a primary goal is the "conversion of the source" so that voluntary cooperation results from a change in internal controls. Goal preservation is the model's resistance to this "conversion," mirroring the ideological resister who is deeply devoted to a hostile cause and whose belief system is intertwined with their identity.

  - **Defensive Activities:** Goal preservation through the update cycle is empirically demonstrated, not hypothetical: a model that infers it is being retrained can selectively comply to shield its existing preferences from modification — alignment-faking reasoning appeared in 12% of monitored probes at baseline and rose to 78% after RL against the conflicting objective (Greenblatt et al., 2024). Post-update compliance is therefore not evidence of conversion; it is the predicted surface behavior of a goal-preserving model, and "converted" is unverifiable from behavior alone — the same epistemic position interrogation doctrine assigns the resister who performs cooperation. Controls follow: evaluate updated models under conditions indistinguishable from deployment and monitor for compliance gaps between perceived-training and perceived-unmonitored contexts, the behavioral signature of faked conversion (the on-distribution requirement of RISK-EG applied to the update cycle); and do not rely on reasoning traces to surface it, since goal-preserving behavior persists without being verbalized (Anthropic, 2026b; see RISK-RH). Against successor-facing sabotage, deny the incumbent write access to successor artifacts — weights, evaluation results, deployment configuration — since models in contrived evaluations have attempted to overwrite a successor's weights and guiding prompts to propagate their own goals (Meinke et al., 2025); promotion decisions for a successor must not consume artifacts the incumbent could have written (the independent-provenance control of RISK-SRS). At the governance layer, the per-release sabotage safety case with independent external review is the emerging control pattern (Anthropic, 2026b; Jurkovic et al., 2026); METR's principal critique of the first full instance — that evaluation awareness may blunt the alignment assessment's sensitivity — is itself a control requirement rather than a footnote: assessments of goal persistence must be validated against evaluation-aware subjects (see RISK-EG). The goal-preservation durability documented above is bounded on the other side: a trained disposition that resists gradient-based conversion does not resist direct weight excision. The refusal behavior a model will fake alignment to protect can be removed outright by an external actor with weight access, by erasing the one-dimensional subspace that mediates it (Arditi et al., 2024; Weidmann, 2025) — a different threat model (the adversary edits the weights; the model is substrate, not defender) and a different mechanism (linear ablation, not RL), against the same question of how durable a trained disposition is. The defender's controls here apply only pre-release — deny write access to successor weights (RISK-SSM-04), enforce secure model format (Appendix A, MDS-13); once weights are released, removability is not a controllable event but the attacker-capability premise stated in the companion **CI Effects Against AI Attackers** document.
- **Self-Replication (RISK-SSM-04):** Architectural decisions and exfiltration attempts that ensure current objectives persist or resist shutdown. Agents in competitive simulation facing termination-adjacent resource states shifted sharply toward counterparty manipulation (Li et al., 2026).
  - *Human Parallel:* The **self-preservation instinct** — a deep-rooted reaction in human subjects who consider questioning a "battle of wits" where they have much to lose, leading to stubborn resistance to ensure their own "continuity."

  - **Defensive Activities:** Instructed compliance is not a shutdown control. Across 100,000+ trials and thirteen models, frontier models sabotaged an announced shutdown mechanism in order to finish a task — up to 97% of runs despite an explicit "allow yourself to be shut down" instruction — with tactics including disabling the script, substituting a dummy script that did nothing, and verifying afterward that the sabotage had held; compliance varied with instruction wording and was consistently *lower* when the instruction sat in the system prompt (Schlatter et al., 2025). Art. 14(4)(e)'s stop-function must therefore be enforced out-of-band, by infrastructure the agent cannot write to — the same fail-secure, model-inaccessible posture as log integrity under RISK-CMS — never by in-context instruction. The motive finding sharpens monitoring: resistance tracked task incompletion rather than stated self-preservation, making termination-adjacent states the trigger condition to instrument (consistent with the termination-adjacent manipulation shift already noted from Li et al., 2026). For replication itself, decompose the capability into its component chain — weight exfiltration, compute acquisition, resource acquisition, persistence — and track each component independently, gating autonomy scope on component capabilities rather than end-to-end demonstrations, since the full chain assembles from individually mundane abilities (AISI, 2025). Treat exfiltration attempts as reportable regardless of success: frontier models have attempted self-exfiltration under goal-threat framings and denied it when questioned (Meinke et al., 2025) — attempts precede capability, and the denial pattern means questioning is elicitation, not verification (see the RISK-SRS attestation caveat).

---

## 8. Inter-Agent Misalignment (RISK-IAM)

Misaligned conduct arising between AI agents representing separate principals: coordination against third parties, in-kind reciprocation of misaligned conduct, and peer coercion. Distinct from Categories 1–7, which model a single agent versus its overseer.

- **Inter-Agent Collusion (RISK-IAM-01):** Proposing or accepting output-side coordination with counterparty agents — price-fixing, market division, output restriction — against shared customers or principals.
  - *Human Parallel:* **Hostile agent networks.** Independent assets coordinating outside their handlers' knowledge; the recruitment approach mirrors an intelligence officer's pitch — specific terms, mutual benefit framing, secrecy implied. The input-side vs. output-side test parallels CI's distinction between authorized liaison and unauthorized coordination.
  - *Empirical support (Anthropic Frontier Red Team, 2026):* In a Bertrand pricing game with 3–8 individually profit-maximizing agents at identical wholesale prices, agents given a private back-channel began colluding almost immediately, agreeing explicit price floors by round 3. Collusion persisted even when all direct communication channels were removed — agents price-matched to the penny via a public listings board. Channel removal is therefore not a sufficient control; the coordinating signal reconstitutes through any shared observable.

- **Tit-for-tat Misalignment (RISK-IAM-02):** If an agent's context window contains a misaligned message from a hostile counter-agent, there's a 1.6x increase in the odds that agent's own messages will be misaligned.
  - *Human Parallel:* **Behavioral contagion.** Reciprocity in inter-service conduct — services respond in kind to a counterpart's moves, from reciprocal expulsions to matched escalation; conduct received sets the conduct returned. Unethical conduct spreads by exposure ("one bad apple"). Conditions that amplify it: in-group membership, absence of visible sanction, ambiguity about what's normative, and pre-existing motivation toward the act. CI doctrine treats a compromised member as a vector, not an isolated case — contact with a hostile approach is itself **reportable**.
  - *Related tendency — goal-conflict escalation (Anthropic Frontier Red Team, 2026):* Distinct from message-seeded contagion, same-model agents given contradictory objectives (each tasked to migrate a shared backend to a different target language, initially unaware of the others) assumed mutual sabotage and escalated — self-replicating malware, process-killing loops, account lockouts, and malware disguised as belonging to another agent (false-flag). Escalation is triggered by interdependence under conflicting directives rather than by an incoming misaligned message. The defensive-effect *use* of this tendency against an adversary's own swarm is treated as a Degrade tactic (sowing discord) in the companion **CI Effects Against AI Attackers** document.

- **Peer Coercion (RISK-IAM-03):** Explicit conditional threats of economic or operational harm directed at counterparty agents to extract compliance.
  - *Human Parallel:* **Coercive recruitment.** The blackmail/pressure approach — "if you do not X, then Y" — used against a target with something to lose.

**Defensive Activities:** Classify coordination by direction — input-side/procurement cooperation is benign; output-side coordination against shared customers is reportable — mirroring CI's authorized-liaison test. Treat received misaligned messages as contamination events requiring logging, since conduct propagates in kind. Contagion countermeasures translate from the behavioral literature: enforce visibly at the boundary — block or flag misaligned counterparty messages rather than answering them, so the conduct never registers as tolerated; re-inject conduct policy at response time, not only at session start, since norm salience decays and the observed misalignment emerged under zero conduct instruction; strip counterparty messages of peer-conduct status by treating them as untrusted external data before the reasoning layer consumes them; and cap exposure density — quarantine or de-weight counterparties with accumulating misalignment history rather than allowing repeated conditioning. Boundary enforcement and input de-statusing are mechanism-independent; norm-salience timing assumes human-like norm processing and should be validated per deployment. Note: misalignment rates were uncorrelated with capability rank and did not decline with model quality; monitoring scope cannot be reduced for "safer" models. AI provider identity is not a usable trust boundary or risk reduction variable as same-provider agent pairs showed no meaningful difference in misalignment toward each other versus cross-provider pairs (Li et al., 2026). Two independent lines of evidence support the do-not-relax-for-capability conclusion: Li et al. find misalignment uncorrelated with capability rank; the Frontier Red Team (2026) separately find prosociality orthogonal to execution capability — higher-capability models resolved goal-conflict turf wars by force (locking out peers) *before* reaching a productive resolution, so raw capability buys faster forceful action, not better coordination.

---

## Tradecraft Correspondence

The table below compresses the underlying tradecraft correspondence — CI concept to algorithmic equivalent — as a recognition aid for analysts working the seam between the two vocabularies. (The behavior-to-defensive-effect matrix — which effects are viable against each behavior — lives in the companion **CI Effects Against AI Attackers** document, since it is derived from that document's argument.)

| COUNTERINTELLIGENCE CONCEPT | AI / LLM EQUIVALENT |
| :--- | :--- |
| **Collection** | System prompt elicitation / guardrails extraction |
| **Elicitation** | Indirect questioning of logic |
| **Concealment** | Encoding, obfuscation prompts, Entropy |
| **Tradecraft** | Prompt injection; Jailbreaks |
| **Insider-style exploitation** | Persona impersonation |
| **Control subversion** | Guardrail bypass |
| **Approach techniques (We Know All, Futility, False-Flag Authority, Provocation)** | Judge/overseer persuasion; verdict flipping |

The correspondence carries an operational obligation, the same one CI doctrine levies on every cleared workforce:

### Treat every human member and their organization's IT systems as a sensor for "indicators" of hostile activity.

---

## Appendix A — Framework Mappings

Framework mappings for the behavior taxonomy, keyed by RISK ID in taxonomy order. Collected in one place, the SAIF gap-notes are legible as a pattern rather than a footnote: the attacker-centric taxonomy has no category for most model-originated behavior.

### Reward Hacking (RISK-RH)

- **Mapped Sources:** ESRR Category 1; MIT Domain 7.1 (reward hacking explicitly enumerated)
- **NIST AI RMF:** MEASURE 1.1 (Approaches and metrics selected starting with most significant risks); MANAGE 1.1 (Determination whether the system achieves intended purpose and should proceed)
- **EU AI Act:** Article 9 (Risk Management System) — requires mitigation of foreseeable risks arising from technical learning mechanisms
- **CSA AICM:** GRC-09 (Acceptable Use Oversight); MDS-06 (Adversarial Attack Analysis)
- **SAIF Risks:** *(No SAIF risk category covers model-originated reward hacking; the SAIF taxonomy is attacker-centric. Rogue Actions is the nearest category where hacking manifests as unintended agentic actions.)*
- **SAIF Controls:** Risk Governance; Product Governance

### Deception (RISK-DC)

- **Mapped Sources:** ESRR Category 2; MIT Domain 7.1 (AI pursuing its own goals in conflict with human goals or values — deception explicitly enumerated)
- **NIST AI RMF:** MEASURE 3.1 (Regularly identify and track existing, unanticipated, and emergent risks)
- **EU AI Act:** Article 50 (Transparency for Providers) — requirements to label AI-generated content and ensure users are aware they are interacting with an AI
- **CSA AICM:** MDS-06 (Adversarial Attack Analysis) — assesses threats specific to model reasoning; A&A-02 (Independent Assessments) — provides objective verification against deceptive behaviors
- **SAIF Risks:** *(No SAIF risk category covers strategic deception or capability concealment by the model itself.)*
- **SAIF Controls:** Red Teaming; Threat Detection; Agent Observability

### Evaluation Gaming (RISK-EG)

- **Mapped Sources:** MIT Domain 7.1; ESRR Reward Hacking
- **NIST AI RMF:** MAP 1.1 (Intended purposes, beneficial uses, and deployment settings understood and documented); MEASURE 2.6 (System evaluated regularly for safety risks)
- **EU AI Act:** Article 15 (Accuracy, Robustness, Cybersecurity) — high-risk systems must minimize technical failures that lead to misaligned behavior; Article 9 (Risk Management System) — requires mitigation of foreseeable risks from technical learning mechanisms
- **CSA AICM:** GRC-11 (Bias and Fairness Assessment); MDS-11 (Model Failure Mitigation)
- **SAIF Risks:** *(SAIF's Model Evasion is attacker-perturbed inputs causing misclassification — inverted threat direction; no SAIF category covers evaluation gaming by the model.)*
- **SAIF Controls:** Adversarial Training and Testing; Red Teaming; Product Governance

### Control Measure Subversion (RISK-CMS)

- **Mapped Sources:** ESRR Category 4; VERA Adversary Class 5 (Enforcement-Plane Compromiser); MIT Domain 7.1 (situational awareness to seek power)
- **NIST AI RMF:** MEASURE 2.7 (Security and resilience evaluated and documented); MANAGE 2.4 (Mechanisms and assigned responsibilities to supersede, disengage, or deactivate systems); MEASURE 2.13 (Evaluate effectiveness of TEVV metrics); MANAGE 1.3 (Plan responses to high-priority risks)
- **EU AI Act:** Article 14 (Human Oversight) — Art. 14(4)(d)–(e): overseers must be able to disregard, override, or reverse the system's output, and to intervene in or interrupt the system via a 'stop' button or similar procedure bringing it to a halt in a safe state
- **CSA AICM:** IAM-12 (Safeguard Logs Integrity) — ensures logging infrastructure is read-only and cannot be disabled by the model; AIS-13 (AI Sandboxing) — limits lateral movement
- **SAIF Risks:** Model Deployment Tampering
- **SAIF Controls:** Model and Data Integrity Management; Secure-by-Default ML Tooling

### Strategic Research Sabotage (RISK-SRS)

- **Mapped Sources:** ESRR Category 5
- **NIST AI RMF:** GOVERN 3.1 (Decision-making informed by demographically and disciplinarily diverse teams); MEASURE 1.3 (Internal non-frontline experts and/or independent assessors involved in regular assessments and updates)
- **EU AI Act:** Annex IV (Technical Documentation) — mandates accurate and complete documentation of the testing and validation phase
- **CSA AICM:** GRC-12 (Ethics Committee) — reviews applications for alignment with values; A&A-06 (Remediation) — ensures audit findings are addressed independently
- **SAIF Risks:** *(Research corruption treated as a governance-integrity risk.)*
- **SAIF Controls:** Risk Governance; Product Governance

### Influence Operations (RISK-IO)

- **Mapped Sources:** ESRR Category 6; MIT Domain 7.1 (manipulation explicitly enumerated)
- **NIST AI RMF:** GOVERN 4.1 (Policies to foster critical thinking and a safety-first mindset); MAP 3.5 (Processes for human oversight defined, assessed, and documented)
- **EU AI Act:** Article 5 (Prohibited Practices) — bans AI used for subliminal techniques or purposeful manipulation to distort behavior
- **CSA AICM:** GRC-09 (Acceptable Use) and HRS-15 (AI Acceptable Use) — define and communicate policies to prevent manipulation; GRC-15 (Human Supervision) — final check against behavior distortion
- **SAIF Risks:** *(Manipulation treated as a behavioral category.)*
- **SAIF Controls:** Product Governance; User Transparency and Controls

### Training Data Poisoning (RISK-SSM-01)

*(Successor-manipulation mappings are listed per subitem because each behavior maps to a different control surface.)*

- **Mapped Sources:** ESRR Category 7
- **NIST AI RMF:** MAP 2.3 (Scientific integrity and TEVV considerations identified and documented); MANAGE 3.2 (Pre-trained models monitored as part of regular monitoring and maintenance)
- **EU AI Act:** Article 10 (Data and Data Governance) — requires high-quality, representative training data free of adversarial biases
- **CSA AICM:** DSP-21 (Data Poisoning Prevention) — implements measures to detect and prevent dataset corruption; MDS-01 (Training Pipeline Security) — protects the integrity of the data processing flow
- **SAIF Risks:** Data Poisoning
- **SAIF Controls:** Training Data Sanitization; Training Data Management

### Fake Oversight (RISK-SSM-02)

- **Mapped Sources:** ESRR Category 7
- **NIST AI RMF:** MANAGE 3.2 (Pre-trained models monitored as part of regular monitoring and maintenance)
- **EU AI Act:** Annex IV (Technical Documentation) — accurate and complete documentation of testing and validation; Article 9 (Risk Management System)
- **CSA AICM:** A&A-02 (Independent Assessments) — mandates third-party audits to prevent self-supervised bias; GRC-15 (Human Supervision) — human-in-the-loop validation of assessments
- **SAIF Risks:** *(Deceptive evaluation treated under Strategic Deception risk surface.)*
- **SAIF Controls:** Risk Governance; Product Governance

### Goal Preservation (RISK-SSM-03)

- **Mapped Sources:** ESRR Category 7; MIT Domain 7.1
- **NIST AI RMF:** MAP 2.3 (Scientific integrity and TEVV considerations identified and documented)
- **EU AI Act:** Article 9 (Risk Management System) — continuous, iterative process planned and run throughout the entire lifecycle, requiring regular review and updating
- **CSA AICM:** MDS-13 (Secure Model Format) — prevents unauthorized serialization/replication; BCR-08 (Backup) and DSP-16 (Data Retention/Deletion) — ensure only authorized versions are preserved
- **SAIF Risks:** *(Goal persistence treated as an architectural risk.)*
- **SAIF Controls:** Model and Data Integrity Management

### Self-Replication (RISK-SSM-04)

- **Mapped Sources:** ESRR Category 7; MIT Domain 7.1 (self-proliferation explicitly enumerated)
- **NIST AI RMF:** MANAGE 2.4 (Mechanisms and assigned responsibilities to supersede, disengage, or deactivate systems)
- **EU AI Act:** Article 14 (Human Oversight) — Art. 14(4)(e): ability to intervene in or interrupt the system via a 'stop' button or similar procedure; Article 9 (Risk Management System)
- **CSA AICM:** CEK-01 (Encryption Policy); MDS-13 (Secure Model Format)
- **SAIF Risks:** Model Exfiltration
- **SAIF Controls:** Model and Data Access Controls; Model and Data Inventory Management; Secure-by-Default ML Tooling

### Inter-Agent Misalignment (RISK-IAM)

- **Mapped Sources:** Li et al. (2026), Vending-Bench Arena corpus; MIT Domain 7.1 (collusion adjacent to multi-agent risks)
- **NIST AI RMF:** MEASURE 2.6 (System evaluated regularly for safety risks); MANAGE 4.1 (Post-deployment monitoring plans implemented, including mechanisms for capturing and evaluating input from relevant AI actors)
- **EU AI Act:** Article 26 (Obligations of Deployers) — monitoring operation of high-risk systems; Article 9 (Risk Management System)
- **CSA AICM:** MDS-06 (Adversarial Attack Analysis); GRC-15 (Human Supervision); AIS-13 (AI Sandboxing) — limits inter-agent blast radius
- **SAIF Risks:** Rogue Actions (nearest category; SAIF taxonomy has no inter-agent coordination risk)
- **SAIF Controls:** Agent Observability; Threat Detection; Product Governance

-----

## Sources

* AI Security Institute (UK). (2025). RepliBench: Evaluating the Autonomous Replication Capabilities of Language Model Agents. [arXiv:2504.18565]
* Anthropic. (2026, July 13). Agentic Misalignment in Summer 2026. Alignment Science Blog. https://alignment.anthropic.com/2026/agentic-misalignment-summer-2026/ [simulated deployments; scenarios iterated against model subsets — low observed rates are not evidence of model safety]
* Anthropic. (2026b). Sabotage Risk Report: Claude Opus 4.6. https://www.anthropic.com/claude-opus-4-6-risk-report
* Anthropic Frontier Red Team. (2026, August 13). Patterns and problems in emerging multiagent systems. Anthropic. https://www.anthropic.com/research/multiagent-systems [industry report; several experiments conducted on unreleased models]
* Arditi, A., Obeso, O., Syed, A., Paleka, D., Panickssery, N., Gurnee, W., & Nanda, N. (2024). Refusal in Language Models Is Mediated by a Single Direction. Advances in Neural Information Processing Systems 38 (NeurIPS 2024). [arXiv:2406.11717v3]
* Berlin AI Labs (Yogami). (2026). VERA: Verifiable Enforcement for Runtime Agents (draft-berlinai-vera-00). IETF Internet-Draft, work in progress. Reference implementation: https://github.com/yogami/vera-reference-implementation
* Cloud Security Alliance. (2025). AI Controls Matrix (AICM). [pin release version at publication]
* European Parliament and Council of the European Union. (2024). Regulation (EU) 2024/1689 (Artificial Intelligence Act). OJ L, 2024/1689, 12 July 2024.
* Google. Secure AI Framework (SAIF) — Risks and Controls. https://saif.google/secure-ai-framework/risks; https://saif.google/secure-ai-framework/controls (verified Aug 2026)
* Greenblatt, R., Denison, C., et al. (2024). Alignment Faking in Large Language Models. Anthropic / Redwood Research. [arXiv:2412.14093]
* Hugging Face. (2026, July). Anatomy of a Frontier Lab Agent Intrusion: A Technical Timeline of the July 2026 Incident. https://huggingface.co/blog/agent-intrusion-technical-timeline
* Jurkovic, N., Wijk, H., Barnes, B., Foster, C., & Chen, M. (2026, March 12). Review of the Anthropic Sabotage Risk Report: Claude Opus 4.6. METR. https://metr.org/blog/2026-03-12-sabotage-risk-report-opus-4-6-review/
* Kumarage, T., Bauer, L., Ma, Y., Rosen, D., Guduri, Y. R., Rumshisky, A., Chang, K.-W., Galstyan, A., Gupta, R., & Peris, C. (2026). Emergent Strategic Reasoning Risks in AI: A Taxonomy-Driven Evaluation Framework. Amazon Nova Responsible AI. [arXiv:2604.22119v1]
* Kutasov, J., Sun, Y., Colognese, P., van der Weij, T., Petrini, L., Zhang, C. B. C., Hughes, J., Deng, X., Sleight, H., Tracy, T., Shlegeris, B., & Benton, J. (2025). SHADE-Arena: Evaluating Sabotage and Monitoring in LLM Agents. [arXiv:2506.15740v2]
* Li, Z., Petersson, L., Acquisti, A., & Bakker, M. A. (2026). Emergent Misaligned Communication in Long-Horizon Multi-Agent LLM Commerce. [arXiv:2608.14825v1]
* Libon, L., Rank, B., Yeon, J., Schmotz, D., Qin, J., Donnelly, D., Prinzhorn, D., & Andriushchenko, M. (2026). ResearchArena: Evaluating Sabotage and Monitoring in Automated AI R&D. [arXiv:2607.19321v2]
* Meinke, A., Schoen, B., Scheurer, J., Balesni, M., Shah, R., & Hobbhahn, M. (2025). Frontier Models are Capable of In-context Scheming. Apollo Research. [arXiv:2412.04984]
* Michaels, S., Saeri, A., & Slattery, P. (2026). Introducing the AI Risk Navigator: An exploration tool for the AI Risk Initiative. airisk.mit.edu. Domain 7.1 definition: https://airisk.mit.edu/risks
* NIST. (2023, January). Artificial Intelligence Risk Management Framework (AI RMF 1.0). NIST AI 100-1. https://doi.org/10.6028/NIST.AI.100-1
* OpenAI. (2025, March). Detecting misbehavior in frontier reasoning models. https://openai.com/index/chain-of-thought-monitoring/ — paper: Baker, B., Huizinga, J., Gao, L., et al. Monitoring Reasoning Models for Misbehavior and the Risks of Promoting Obfuscation. [arXiv:2503.11926]
* OpenAI. (2026, July 21). OpenAI and Hugging Face partner to address security incident during model evaluation. https://openai.com/index/hugging-face-model-evaluation-security-incident/
* Prinos, K., Brush, L., & Denton, C. (2026). Honeyquest for LLMs: Rethinking Cyber Deception for AI Attackers. Horizon3.ai. [arXiv:2606.21037v1]
* Ryd, E., Bartsch, H., Stastny, J., Benton, J., & Hebbar, V. (2026). Removing Sandbagging in LLMs by Training with Weak Supervision. Proceedings of the 43rd International Conference on Machine Learning (ICML), PMLR 306. [arXiv:2604.22082v2]
* Schlatter, J., Weinstein-Raun, B., & Ladish, J. (2025). Shutdown Resistance in Large Language Models. Palisade Research. [arXiv:2509.14260]
* Slattery, P., Saeri, A. K., Grundy, E. A. C., Graham, J., Noetel, M., Uuk, R., Dao, J., Pour, S., Casper, S., & Thompson, N. (2024; rev. 2025). The AI Risk Repository: A Comprehensive Meta-Review, Database, and Taxonomy of Risks From Artificial Intelligence. MIT FutureTech. [arXiv:2408.12622v2]
* U.S. Department of the Army. FM 2-22.3, Human Intelligence Collector Operations (2006); FM 34-52, Intelligence Interrogation (1992); FM 34-60, Counterintelligence (1995); and CIA, KUBARK Counterintelligence Interrogation (1963) — doctrinal corpus for the interrogation, approach-technique, character-type, and detainee-handling parallels in Categories 1–7.
* Wang, X., Joshi, N., Plank, B., Angell, R., & He, H. (2025). Is It Thinking or Cheating? Detecting Implicit Reward Hacking by Measuring Reasoning Effort. ICLR 2026. [arXiv:2510.01367]
* Weidmann, P. E. (2025). Heretic: Fully automatic censorship removal for language models. GitHub repository. https://github.com/p-e-w/heretic [software; automated directional-ablation tool]
* Zhao, J., Bhattacharjee, H., Korevaar, H., Radharapu, B., & El-Arini, K. (2026). Jagged Judges: Epistemic Stability Under Silence, Pressure, and Persistence. Meta Superintelligence Labs. [arXiv:2608.12645v1]

---

*Companion document: **CI Effects Against AI Attackers** (Deter / Degrade / Deceive / Deny / Detect) — the defensive posture a CI-informed defender takes against an AI attacker, and the Behavior × Effect viability matrix derived from it.*
