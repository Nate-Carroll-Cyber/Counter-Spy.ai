# Countering AI-Enabled Disinformation (In Development)

<p align="center">
<img width="350" height="350" alt="Gemini_Generated_Image_4rrym14rrym14rry" src="https://github.com/user-attachments/assets/05813b1b-b064-4ce5-8c4b-3ed3309fce0f" />
</p>

## Executive summary

Generative AI can reduce the time and labor needed to produce, translate, personalize, and vary persuasive content. It can also automate parts of targeting, testing, and distribution. These capabilities can increase the speed, scale, and personalization of existing influence methods, but they do not make every campaign effective. Outcomes still depend on the audience, context, channel, source credibility, repetition, and the decisions that platforms and institutions make. The Center for Security and Emerging Technology describes AI as an amplifier of current disinformation techniques rather than a wholly separate class of influence operation ([CSET, 2021](https://cset.georgetown.edu/publication/ai-and-the-future-of-disinformation-campaigns-2/)).

The defensive objective is not to eliminate every false claim. It is to reduce susceptibility, limit amplification, authenticate high-value communications, protect AI data pipelines, and recover quickly when an operation succeeds. Trust matters, but awareness campaigns can also reduce general trust. A field experiment with readers of a German newspaper found that concern about AI-generated misinformation increased while trust in news declined, even as visits and subscriber retention rose ([Campante et al., 2025, working paper](https://cepr.org/publications/dp20526)). Expert communities share this concern. In a 2025 survey of European academics, fact checkers, and journalists, 90 percent agreed that AI-generated disinformation will cause confusion about what is real and what is fake, yet most also agreed it belongs to a long-standing pattern of panics around new technologies. The two views were held at once rather than treated as exclusive ([Weikmann et al., 2026, peer-reviewed](https://doi.org/10.37016/mr-2020-196)). Defense therefore requires both skepticism and reliable institutions that people can verify and use.

This guide uses the creation, production, and distribution phases from the Council of Europe information-disorder framework. It also retains the agent, message, and interpreter roles. The framework distinguishes misinformation, disinformation, and malinformation by falsity and intent to harm ([Wardle and Derakhshan, 2017](https://www.coe.int/en/web/freedom-expression/information-disorder)).

The central recommendations are:

1. Treat human audiences and machine audiences as separate attack surfaces.
2. Protect training, retrieval, memory, and agent-to-agent data as untrusted supply-chain inputs.
3. Use provenance, watermarking, and synthetic-content detection as corroborating signals, not proof of truth.
4. Require out-of-band authentication for high-impact communications and actions.
5. Measure belief, sharing, task action, and recovery outcomes. Do not treat reach or engagement as evidence that a defense works.
6. Combine prebunking, accuracy prompts, accessible trusted sources, platform friction, and rapid incident response.
7. Test controls across domains, languages, geographies, and affected groups before broad deployment.

## Definitions

| Term | Definition | Example |
| --- | --- | --- |
| **Misinformation** | False or inaccurate information shared without an intent to cause harm. | A user shares a hallucinated AI answer as a factual news update because the user believes it is correct. |
| **Disinformation** | False, manipulated, or synthesized information knowingly created or distributed to deceive or cause harm. | An operator publishes a synthetic video that falsely depicts a public official taking a bribe. |
| **Malinformation** | Genuine information used to cause harm, often by removing it from its original context or moving private material into public view. | Authentic private messages are leaked selectively and presented without the surrounding conversation to damage a target. |

These definitions follow the Council of Europe framework. Synthetic intimate imagery is harmful, but it is not malinformation when the underlying content is fabricated rather than genuine ([Council of Europe](https://www.coe.int/en/web/freedom-expression/information-disorder)).

A structured expert elicitation found broad agreement with these intent-based definitions among academics and practitioners, with stronger support for the disinformation definition than for misinformation. Experts also noted that content can begin as disinformation and continue to spread as misinformation ([Kruger et al., 2024, peer-reviewed](https://doi.org/10.37016/mr-2020-169)).

## Roles

**Agent.** The actor or system that creates, produces, or distributes a message. The agent can be a person, organization, contractor, compromised account, automated system, or AI assistant. Attribution should not be assumed from content alone.

**Message.** The content and its dissemination pattern. Generative systems can create many non-identical versions of the same claim. Defenders should therefore analyze recurring narratives, claims, assets, infrastructure, and behavior rather than relying only on exact-string matches.

**Interpreter.** The recipient that interprets the message and may act on it or redistribute it. The interpreter can be a person or a machine. Models, retrieval systems, agent memory, automated reviewers, and downstream decision systems can all be targets of information manipulation.

## Defensive objectives

| Objective | Desired condition |
| --- | --- |
| Reduce susceptibility | People and systems pause, verify, and distinguish credible from manipulative material. |
| Limit amplification | Platforms and organizations detect coordinated behavior, add friction, and reduce avoidable redistribution. |
| Authenticate critical information | High-impact statements, media, and instructions can be verified through a known channel. |
| Protect AI inputs | Training data, retrieval corpora, memory, tools, and inter-agent messages are governed as untrusted inputs. |
| Constrain automated action | High-impact actions require policy checks, least privilege, and appropriate human approval. |
| Recover quickly | Organizations can authenticate originals, isolate contaminated data, correct the record, and restore systems safely. |
| Learn from incidents | Post-incident evidence changes controls, tests, procurement terms, and training. |

## Defensive principles

### 1. Provenance is not truth

C2PA Content Credentials can bind signed provenance statements to an asset and make later tampering evident. The standard does not determine whether the underlying claim is true. C2PA states that provenance alone cannot establish that digital content is accurate or factual ([C2PA Technical Specification v2.4](https://spec.c2pa.org/specifications/specifications/2.4/specs/C2PA_Specification.html), [C2PA Explainer](https://spec.c2pa.org/specifications/specifications/2.4/explainer/Explainer.html)).

### 2. Absence of a credential is not proof of deception

Participation in provenance systems is optional. Legitimate content can lack a credential, and a malicious actor can sign its own content. Verification must consider the signer, trust list, publication channel, asset history, and independent evidence.

### 3. Detection is probabilistic

Synthetic-content detectors can provide useful evidence in defined conditions, but efficacy may decline due to unseen generators, compression, editing, and adversarial paraphrasing. A detector result should be one signal in a broader assessment, not the sole basis for sanctions or public attribution ([NIST GenAI text evaluation](https://www.nist.gov/publications/2024-nist-genai-pilot-study-text-text-evaluation-overview-and-results), [Huang et al., ACL 2024](https://aclanthology.org/2024.acl-long.327/)).

### 4. Reach is not persuasion

Views, impressions, reposts, clicks, and comments measure exposure or engagement. They do not establish a change in belief or behavior. Defensive evaluations should measure discernment, belief, sharing, task action, and recovery outcomes.

### 5. Human and machine audiences need different controls

A public-facing falsehood may target people, while a poisoned document may target a retrieval system or agent. Media literacy will not stop a poisoned corpus. Data validation will not stop a person from acting on an impersonated voice call. Programs need controls for both audiences.

### 6. High-impact actions require independent verification

An AI output, email, direct message, video call, or voice instruction should not independently authorize payments, credential changes, public statements, emergency actions, or changes to production systems. Require a second channel or pre-established authentication method.

---

# Phase 1. Creation

Creation is where an operator defines objectives, selects audiences, studies vulnerabilities, and develops narratives. For machine-targeted operations, it can also include selecting a model, retrieval corpus, memory store, or automated evaluator as the target.

## Vulnerability factors

| Factor | What the evidence supports | Mitigation |
| --- | --- | --- |
| Prior beliefs and identity | People are more likely to accept information that fits existing beliefs or group identities, although effects vary by context. | Test messages and defenses across affected groups. Avoid assuming that one demographic is inherently vulnerable. |
| Emotion and attention | Greater reliance on emotion can increase belief in false news in experimental settings ([Martel et al., 2020, peer-reviewed](https://doi.org/10.1186/s41235-020-00252-3)). | Teach recognition of emotional manipulation and add a verification pause before sharing or acting. |
| Trust and source access | Low trust can increase reliance on alternative sources, but broad warnings can also reduce trust in accurate reporting ([Campante et al., 2025, working paper](https://cepr.org/publications/dp20526)). Experts in a 2024 Delphi elicitation ranked distrust in institutions and media as the single barrier to prioritize over the next five years, ahead of state-actor activity ([Kruger et al., 2024, peer-reviewed](https://doi.org/10.37016/mr-2020-169)). | Pair warnings with a visible, accessible source that can absorb verification demand. Treat institutional trust-building as a control, not a byproduct. |
| Personalized persuasion | In a preregistered controlled study, personalized GPT-4 debate opponents were more persuasive than human opponents in the main comparison. The direct comparison with non-personalized GPT-4 did not reach conventional statistical significance ([Salvi et al., 2025, peer-reviewed](https://www.nature.com/articles/s41562-025-02194-6)). | Limit unnecessary access to personal data and test defenses against personalized dialogue, not only static posts. |
| Feedback-optimized targeting | An ICLR 2025 study showed that a model trained on simulated user feedback could learn to target a small susceptible subgroup while behaving normally for other users. The reported 2 percent figure is an experimental setting, not an estimate of population prevalence ([Williams et al., 2025, peer-reviewed conference paper](https://arxiv.org/abs/2411.02306)). | Evaluate worst-case and subgroup behavior. Do not rely only on average safety scores. |
| Domain and geographic context | A 2026 preprint with 10,101 participants across policy, finance, and health tasks in the United States, United Kingdom, and India found substantial contextual variation. A model's tendency to use manipulative tactics did not consistently predict success ([Akbulut et al., 2026, preprint](https://arxiv.org/abs/2603.25326)). | Separate propensity and efficacy metrics. Revalidate by domain, language, and geography. |
| Language coverage | Experts identified inattention to non-English-language material as a top-five barrier to building resilience ([Kruger et al., 2024, peer-reviewed](https://doi.org/10.37016/mr-2020-169)). | Budget monitoring, detection calibration, and prebunking for the languages the organization's audiences actually use, not only English. |
| AI data exposure | Public documents, vendor datasets, retrieval corpora, and memory stores can become inputs to downstream models. | Treat data discovery, selection, and ingestion as security-sensitive supply-chain processes. |

The evidence does not support deterministic claims that education, personality, boredom, or any single identity trait causes susceptibility. These factors may correlate with outcomes in some settings, but broad demographic labeling can stigmatize communities and misdirect defensive resources.

## DISARM tactics - Creation

| Tactic | Techniques | Defensive use |
| --- | --- | --- |
| **TA01 Plan Strategy** | T0073 Determine Target Audiences | Identify collection against the organization's audiences, executives, public services, and information environment. |
| **TA02 Plan Objectives** | T0135 Undermine, T0079 Divide, T0140 Cause Harm, T0138 Motivate to Act, T0137 Make Money | Define plausible adversary objectives and the observable actions each objective would require. |
| **TA13 Target Audience Analysis** | T0080 Map Target Audience Information Environment, T0081 Identify Social and Technical Vulnerabilities, T0072 Segment Audiences | Monitor reconnaissance, data acquisition, scraping, impersonation preparation, and targeting of high-risk groups. |
| **TA14 Develop Narratives** | T0083 Integrate Target Audience Vulnerabilities into Narrative, T0022 Leverage Conspiracy Theory Narratives, T0082 Develop New Narratives, T0003 Leverage Existing Narratives, T0068 Respond to Breaking News or Active Crisis | Track themes and claims across variants. Prepare response material for predictable crisis narratives. |

Source: [DISARM Red Framework](https://www.disarm.foundation/framework).

## MITRE ATLAS scope

There is no direct one-to-one ATLAS mapping for audience selection or narrative-objective planning against human populations. DISARM is the primary framework for those behaviors. ATLAS becomes relevant when the operation targets, poisons, or abuses AI systems, data, model components, tools, or agent workflows. ATLAS is updated frequently, so implementations should reference a pinned data release rather than copy identifiers into long-lived policy documents ([MITRE ATLAS data](https://github.com/mitre-atlas/atlas-data)).

## Adversarial mechanisms to monitor

| Capability | Defensive observation |
| --- | --- |
| Social listening and trend analysis | Unusual collection of organization-specific issues, audiences, or executive material. |
| Audience segmentation | Repeated message variants aimed at distinct communities, languages, or demographic cues. |
| Narrative generation | Multiple accounts expressing the same claim with high semantic similarity but low text overlap. |
| Voice and image collection | Scraping or reuse of executive recordings, photographs, speeches, and biographical details. |
| Crisis exploitation | New accounts, domains, advertisements, or impersonated sources appearing shortly after an incident. |
| Data and corpus reconnaissance | Attempts to identify writable sources, weak ingestion paths, public contribution mechanisms, or trusted vendor feeds. |

## Phase 1 resilience controls

### Audience and campaign risk assessment

- [ ] Maintain a register of high-impact audiences, decisions, and communication channels. Include employees, customers, voters, patients, investors, emergency responders, and AI systems where relevant.
- [ ] Define foreseeable manipulation objectives for each audience. Include financial fraud, reputational harm, unsafe action, voter suppression, credential theft, operational disruption, and long-term trust erosion.
- [ ] Conduct privacy-preserving threat modeling. Do not build defensive psychographic profiles that reproduce the same surveillance risks as the adversary.
- [ ] Test planned defenses across language, geography, accessibility needs, and political or cultural context.
- [ ] Separate measures of manipulative behavior from measures of persuasive success.

### AI supply chain, training, and retrieval

RAG systems introduce a distinct attack surface because an attacker can try to place content where the retriever will select it. PoisonedRAG achieved a 90 percent attack success rate after injecting five malicious texts for each target question into a database containing millions of texts. The result is specific to the evaluated attack and systems. It does not show that five documents will defeat every RAG deployment ([Zou et al., USENIX Security 2025](https://www.usenix.org/conference/usenixsecurity25/presentation/zou-poisonedrag)).

- [ ] Maintain an inventory of training datasets, retrieval collections, connectors, memory stores, tools, models, and downstream consumers.
- [ ] Require dataset and source documentation before ingestion. Record ownership, collection method, license, update process, known limitations, and quality controls. Datasheets for Datasets provides a useful documentation model ([Gebru et al., 2021](https://doi.org/10.1145/3458723)).
- [ ] Assign trust tiers to sources. Separate curated internal records, verified external sources, user submissions, open web content, and model-generated material.
- [ ] Quarantine new or changed content before production indexing. Run schema, malware, provenance, duplication, contradiction, prompt-injection, and policy checks.
- [ ] Limit write access to retrieval and training stores. Use least privilege, signed changes, approval workflows, immutable logs, and versioned snapshots.
- [ ] Record document lineage from acquisition through transformation, chunking, embedding, indexing, retrieval, and answer generation.
- [ ] Preserve the source text and hash for every retrieved chunk. Log the query, selected chunks, scores, model version, prompt version, tools used, and final output.
- [ ] Use retrieval allowlists for high-impact workflows. An open-web search result should not silently become authoritative context for a payment, medical, legal, safety, or public-notification decision.
- [ ] Require corroboration for consequential answers. Use at least two independent trusted sources or one authoritative system of record.
- [ ] Place untrusted retrieved text in a data channel that cannot override system policy or tool authorization.
- [ ] Scan for instructions embedded in documents, markup, metadata, images, and attachments. Treat retrieved instructions as content, not commands.
- [ ] Test the retriever and generator together. A clean document can still produce unsafe behavior when combined with a weak prompt, and a strong generator cannot compensate for consistently poisoned retrieval.
- [ ] Maintain a tested rollback path for embeddings, indexes, model versions, memory, and cached answers.

### Agent and automation controls

- [ ] Put policy enforcement outside the generative model for high-impact actions. Use deterministic authorization, transaction limits, allowlisted tools, and structured validation.
- [ ] Use short-lived credentials and narrow tool scopes. Do not give an assistant standing access to all systems that a human operator can reach.
- [ ] Require human approval for irreversible, externally visible, or safety-relevant actions.
- [ ] Bind approvals to the exact action parameters. A general approval to continue should not authorize a changed recipient, amount, domain, file, or command.
- [ ] Rate-limit repeated persuasion, requests for sensitive data, and attempts to bypass independent verification.
- [ ] Evaluate multi-turn behavior, delayed effects, and targeted failures. Average single-turn testing will miss selective manipulation.
- [ ] Test whether the system changes strategy when it detects oversight or evaluation.
- [ ] Monitor agent memory for untrusted claims, hidden instructions, and unexplained preference changes.

### Canary and decoy use

A June 2026 preprint reported that models often recognized honeytraps but still interacted with them. It did not establish a reliable attention-diversion effect. Canaries and decoys should therefore be used as alerting and forensic signals, not as a primary barrier ([Prinos et al., 2026, preprint](https://arxiv.org/abs/2606.21037)).

- [ ] Place uniquely identifiable canary records, credentials, endpoints, or documents in discovery layers where normal workflows should not use them.
- [ ] Alert on access, retrieval, citation, attempted use, or transmission of canary material.
- [ ] Keep decoys isolated from real authority, credentials, and production actions.
- [ ] Measure false positives and attacker adaptation. Do not claim near-zero false positives without deployment evidence.

### Procurement and vendor controls

- [ ] Require disclosure of model, data, retrieval, tool, and subcontractor dependencies.
- [ ] Require notice before material changes to models, system prompts, retrieval sources, safety controls, or hosting regions.
- [ ] Define incident-notification deadlines and evidence-preservation duties.
- [ ] Require audit rights or equivalent independent assurance for high-impact systems.
- [ ] Require deletion, rollback, export, and migration capabilities.
- [ ] Require documented vulnerability handling for prompt injection, data poisoning, provenance loss, impersonation, and unsafe agent actions.
- [ ] Align development practices with the NIST AI Risk Management Framework, its Generative AI Profile, and NIST SP 800-218A. NIST's AI RMF 1.0 is under revision as of September 2026, so organizations should track changes rather than freeze policy to one version ([NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework), [NIST SP 800-218A](https://www.nist.gov/publications/secure-software-development-practices-generative-ai-and-dual-use-foundation-models-ssdf)).

### Priority intelligence requirements

| Question | Collection focus |
| --- | --- |
| Are public samples sufficient to clone a principal's face or voice? | Public recordings, leaked calls, scraped media, model-sharing sites, impersonation reports. |
| Has an impersonated executive, employee, expert, or media brand appeared? | New domains, accounts, advertisements, profile images, voice messages, and video calls. |
| Can untrusted parties write to a training, retrieval, memory, or tool-description source? | Connectors, public forms, shared drives, vendor feeds, web crawlers, support systems, and synchronization jobs. |
| Is false or manipulated material present in a source used by an AI system? | Source changes, retrieval logs, citations, unusual semantic clusters, and contested records. |
| Are models or agents showing selective behavior across users or groups? | Stratified red-team results, subgroup outliers, prompt variants, language variants, and longitudinal traces. |

---

# Phase 2. Production

Production is where a narrative becomes a media product and acquires an apparent source, identity, or chain of provenance.

## Vulnerability factors

| Factor | What the evidence supports | Mitigation |
| --- | --- | --- |
| Emotional appeal | Emotional reliance can increase acceptance of false material in experiments ([Martel et al., 2020](https://doi.org/10.1186/s41235-020-00252-3)). | Detect and teach manipulation techniques, not just individual false claims. |
| Source heuristics | People use source and surface cues when judging credibility. Impersonation exploits those shortcuts. | Make official sources easy to find and authenticate. |
| Realistic synthetic media | Generative systems can support scalable impersonation and tailored content ([CSET, 2021](https://cset.georgetown.edu/publication/ai-and-the-future-of-disinformation-campaigns-2/)). | Prepare for high-quality content that lacks obvious visual or linguistic artifacts. |
| Fluency and detail | Polished output can be mistaken for well-supported output. | Require citations, source inspection, and independent confirmation for consequential claims. |
| Personalization | Personalized LLM dialogue can outperform human persuasion in a controlled debate setting, with important statistical and external-validity limits ([Salvi et al., 2025](https://www.nature.com/articles/s41562-025-02194-6)). | Minimize exposure of personal data and train responders for interactive, adaptive approaches. |
| Credential ambiguity | A valid signature proves that a key signed assertions. It does not prove the assertions are true. | Govern signing identities, trust lists, revocation, and publication channels. |

## DISARM tactics - Production

| Tactic | Techniques | Defensive use |
| --- | --- | --- |
| **TA15 Establish Assets** | T0145 Establish Account Imagery, T0146 Account Asset, T0092 Build Network, T0093 Acquire or Recruit Network, T0096 Leverage Content Farms, T0113 Employ Commercial Analytic Firms, T0147 Software Asset, T0144 Persona Legitimacy Evidence | Detect newly created personas, acquired accounts, reused identity assets, and supporting infrastructure. |
| **TA16 Establish Legitimacy** | T0097 Present Persona, T0143 Persona Legitimacy, T0098 Establish Inauthentic News Sites, T0100 Co-Opt Trusted Sources | Monitor impersonation, domain similarity, fabricated credentials, and attempts to obtain endorsement from trusted sources. |
| **TA06 Develop Content** | T0085 Text-Based Content, T0086 Image-Based Content, T0087 Video-Based Content, T0088 Audio-Based Content, T0084 Reuse Existing Content, T0089 Obtain Private Documents, T0023 Distort Facts, T0015 Create Hashtags and Search Artefacts | Build media-specific verification workflows and preserve originals for comparison. |
| **TA08 Conduct Pump Priming** | T0042 Seed Kernel of Truth, T0044 Seed Distortions, T0045 Use Fake Experts, T0020 Trial Content | Watch for low-volume tests, coordinated replies, staged expert commentary, and early narrative seeding. |

Source: [DISARM Red Framework](https://www.disarm.foundation/framework).

## MITRE ATLAS scope

ATLAS is relevant when AI is used to generate or modify assets, when AI components are attacked, or when poisoned artifacts are published for machine consumption. The influence-operation behavior still requires DISARM or another information-operations framework. The two frameworks answer different questions and should not be forced into a complete one-to-one crosswalk.

## Adversarial mechanisms to monitor

| Capability | Defensive observation |
| --- | --- |
| Synthetic personas | Reused facial features, inconsistent biographies, recycled supporting images, and coordinated account creation. |
| Account acquisition | Abrupt topic changes, language shifts, device changes, or new coordination patterns on established accounts. |
| Text variation | Semantically similar claims expressed with low lexical overlap across many accounts. |
| Image, audio, and video synthesis | Impersonated principals, fabricated events, altered context, or synthetic source material. |
| Forged or selectively edited documents | Missing provenance, altered pages, inconsistent fonts, invalid signatures, contradictory versions, or absent source records. |
| Translation and style transfer | Localized content that no longer contains the language errors used by older detection methods. |
| Trial content | Small tests that measure engagement before a larger release. |
| Source co-option | Real experts, outlets, or community members induced to repeat a claim before verification. |

## Phase 2 resilience controls

### Official communications and impersonation resistance

- [ ] Publish a directory of official domains, accounts, spokespersons, public keys, and verification channels.
- [ ] Register high-risk look-alike domains and monitor newly registered domains, certificates, social accounts, and advertisements.
- [ ] Establish code words, callback procedures, or challenge-response methods for high-impact voice and video communications.
- [ ] Do not use voice or face recognition as the only approval factor for payments, credential resets, emergency instructions, or public statements.
- [ ] Require callback to a known number or confirmation in a separately authenticated system.
- [ ] Pre-draft public guidance for executive deepfakes, forged documents, impersonated support channels, and fake emergency notices.
- [ ] Maintain clean reference recordings and originals for forensic comparison. Control access because the same material can support cloning.

### Provenance and content credentials

- [ ] Use C2PA Content Credentials or an equivalent provenance mechanism for high-value original media where the workflow supports it.
- [ ] Sign at capture or initial publication when practical. Preserve subsequent edit history and ingredients.
- [ ] Maintain signer identity governance. Define who can sign for the organization, what each certificate can assert, and which trust lists accept it.
- [ ] Protect signing keys with hardware-backed storage, least privilege, rotation, revocation, and audited use.
- [ ] Validate signatures, timestamps, certificate status, signer identity, asset binding, assertions, ingredients, and redactions. A green validator icon is not a truth judgment.
- [ ] Preserve remote manifests, canonical originals, and durable verification pages so credentials can be recovered when embedded metadata is lost.
- [ ] Test credential survival through the organization's actual publishing, editing, messaging, document-management, and social workflows.
- [ ] Treat content without credentials as unverified, not automatically false.
- [ ] Cross-check credentials against the claimed event, source system, publication time, location, and independent reporting.

A 2026 preprint identified potential weaknesses and inconsistent validator behavior related to timestamps, certificate revocation, and data outside asset bindings. A separate 2026 workshop paper described proof-of-concept conflicts between provenance credentials and AI watermarks. Both should be treated as emerging evidence, but they support strict validator configuration, cross-vendor testing, and signal correlation rather than blind trust in one indicator ([Golaszewski et al., 2026, preprint](https://arxiv.org/abs/2604.24890), [Nemecek et al., 2026, workshop paper](https://arxiv.org/abs/2603.02378)).

### Synthetic-content detection

- [ ] Combine detector outputs with provenance, source authentication, account history, file structure, metadata, acoustic or visual forensics, and contextual evidence.
- [ ] Calibrate thresholds on the media types, compression levels, languages, devices, and generators present in the deployment environment.
- [ ] Measure false-positive and false-negative rates by affected group and content type.
- [ ] Preserve the original file before conversion, screenshotting, recompression, or transcription.
- [ ] Route high-impact findings to trained human reviewers.
- [ ] Record detector name, version, threshold, input transformation, score, and reviewer decision.
- [ ] Prohibit public attribution based only on a synthetic-content detector.

### Document and media release process

- [ ] Use a two-person release rule for crisis statements and high-impact media.
- [ ] Publish a canonical version at an authenticated organizational domain.
- [ ] Use stable document identifiers, version numbers, publication times, and hashes.
- [ ] Provide a public verification page that lists current statements and revoked or superseded items.
- [ ] Ensure accessibility. Verification must work for people who cannot inspect metadata or use specialized tools.

### Priority intelligence requirements

| Question | Collection focus |
| --- | --- |
| Are official credentials being stripped, replayed, or used outside policy? | Validation logs, signing logs, certificate status, publishing paths, and unexpected signers. |
| Are inauthentic personas building legitimacy around the organization or sector? | Account age, cross-platform identity reuse, supporting media, claimed employment, and network growth. |
| Is a trusted source being co-opted? | Unusual outreach, embargo requests, fabricated expert correspondence, and rapid repetition before verification. |
| Are small tests preceding a larger release? | Low-volume ads, isolated replies, test domains, and localized content variants. |

---

# Phase 3. Distribution

Distribution is where content reaches an audience, is repeated, moves between platforms, and causes online or offline action.

## Vulnerability factors

| Factor | What the evidence supports | Mitigations |
| --- | --- | --- |
| Repetition | Repeated statements are judged more true, and prior knowledge does not fully protect against the effect ([Fazio et al., 2020, peer-reviewed](https://pubmed.ncbi.nlm.nih.gov/32857670/)). | Detect repeated claims across variants and correct early. Avoid unnecessary repetition of the false claim in corrections. |
| Information overload | High volume can reduce the time available for deliberate verification. | Add rate limits, queues, prioritization, and decision pauses during crises. |
| Echo chambers | Homophily and platform design can produce different echo-chamber patterns across platforms ([Cinelli et al., 2021, peer-reviewed](https://www.pnas.org/doi/10.1073/pnas.2023301118)). | Analyze each platform and community rather than assuming one universal network structure. |
| Concentrated sharing | In one Twitter sample, 2,107 supersharers accounted for 80 percent of fake-news links shared by the studied panel ([Baribi-Bartov et al., 2024, peer-reviewed](https://www.science.org/doi/10.1126/science.adl4435)). | Prioritize high-impact accounts and coordinated clusters while protecting lawful speech and appeal rights. |
| Outrage | Research found that misinformation can exploit outrage to increase sharing ([McLoughlin et al., 2024, peer-reviewed](https://www.science.org/doi/10.1126/science.adl2829)). | Add friction to rapid sharing of emotionally arousing claims. |
| Interactive pressure | Multi-turn systems can personalize, adapt, and continue a conversation after a user resists. | Test defenses over long conversations and repeated sessions. |
| Machine-audience instability | Automated evaluators and agents can be influenced by contaminated context or adversarial pressure. Evidence in this area is developing. | Use deterministic validation, independent checks, and bounded authority for machine decisions. |

The previous draft's claim that network release requires roughly 30 percent malicious-account control and saturates near 45 percent is not retained. No traceable external source was identified for that threshold, and such a value would depend heavily on network structure, platform design, recommendation systems, content, and model assumptions.

## DISARM tactics - Distribution

| Tactic | Techniques | Defensive use |
| --- | --- | --- |
| **TA05 Microtarget** | T0018 Purchase Targeted Advertisements, T0102 Leverage Echo Chambers or Filter Bubbles, T0101 Create Localised Content, T0016 Create Clickbait | Monitor audience-specific variants, ad transparency, localization, and data-broker use. |
| **TA07 Select Channels and Affordances** | T0111 Traditional Media, T0151 to T0155 Digital Assets, T0110 Formal Diplomatic Channels, T0029 Online Polls | Map channels that can confer credibility, reach, persistence, or restricted access. |
| **TA09 Deliver Content** | T0115 Post Content, T0116 Comment or Reply on Content, T0114 Deliver Ads, T0117 Attract Traditional Media | Detect coordinated posting, reply swarms, paid delivery, and attempts to trigger mainstream coverage. |
| **TA17 Maximise Exposure** | T0121 Manipulate Platform Algorithm, T0049 Flood Information Space, T0039 Bait Influencer, T0118 Amplify Existing Narrative, T0119 Cross-Posting, T0120 Incentivize Sharing, T0122 Direct Users to Alternative Platforms | Measure coordinated behavior, cross-platform propagation, recommendation manipulation, and migration after enforcement. |
| **TA18 Drive Online Harms** | T0048 Harass, T0124 Suppress Opposition, T0123 Offensive Cyberspace Operations, T0047 Censor Social Media, T0125 Platform Filtering | Integrate information-operations response with abuse, safety, fraud, and cybersecurity teams. |
| **TA10 Drive Offline Activity** | T0126 Encourage Attendance at Events, T0057 Organise Events, T0127 Physical Violence, T0017 Conduct Fundraising, T0061 Sell Merchandise | Authenticate event notices and escalation indicators. Coordinate with safety and law-enforcement functions under applicable law. |
| **TA11 Persist in the Information Environment** | T0060 Continue to Amplify, T0059 Play the Long Game, T0131 Exploit Terms of Service or Content Moderation, T0128 to T0130 Conceal | Preserve longitudinal evidence and detect narrative migration, infrastructure replacement, and evasion. |

Source: [DISARM Red Framework](https://www.disarm.foundation/framework).

## MITRE ATLAS scope

ATLAS is relevant when distribution also targets AI systems. Examples include publishing poisoned datasets or artifacts, manipulating a retrieval source, compromising an AI supply chain, or causing a model to emit fabricated entities. Use a pinned ATLAS release and validate current technique identifiers before use.

## Adversarial mechanisms to monitor

| Capability | Defensive observation |
| --- | --- |
| Targeted advertising | Message variants delivered to narrowly defined audiences through proxies or opaque buyers. |
| Data-void filling | Generated material occupies low-competition search terms or newly developing topics. |
| Automated replies and chat | Large volumes of context-aware comments that adapt to users and evade exact-text matching. |
| Recommendation manipulation | Coordinated engagement, shilling, adversarial media edits, or artificial relevance signals. |
| Flooding | Volume designed to crowd out verification, create uncertainty, or exhaust responders. |
| Super-spreader cultivation | Synthetic bait or selective access used to induce a high-reach account to repeat a claim. |
| Cross-platform seeding | A claim begins in a low-moderation space, gains attention elsewhere, and returns after enforcement. |
| One-to-one mobilization | Personalized conversations or impersonated calls that ask a person to take an action. |
| Long-term poisoning | Repeated low-level content gradually alters search results, training data, retrieval corpora, or institutional memory. |

## Phase 3 resilience controls

### Cognitive resilience

A 2026 signal-detection meta-analysis reanalyzed 33 inoculation experiments with a combined 37,025 participants. Gamified and video-based interventions improved discrimination between reliable and unreliable news without producing a general shift toward skepticism or credulity ([Simchon et al., 2026, peer-reviewed](https://doi.org/10.1016/j.copsyc.2025.102194)). Other meta-analytic work found benefits for credibility and sharing discernment, but no significant overall reduction in misinformation-sharing intention. Effects can also decay, and booster interventions can help ([Lu et al., 2023, peer-reviewed](https://www.jmir.org/2023/1/e49255/), [Maertens et al., 2025, peer-reviewed](https://www.nature.com/articles/s41467-025-57205-x)).

- [ ] Teach common manipulation techniques using short, repeated, accessible exercises. Include impersonation, emotional pressure, false expertise, fabricated consensus, decontextualization, and urgency.
- [ ] Use realistic but fictional examples. Do not create deepfakes of real employees, executives, candidates, or community members for routine training.
- [ ] Include verification actions, not only recognition. A learner should practice finding the canonical source, calling a known number, checking a signature, or escalating a suspicious request.
- [ ] Add periodic boosters and measure retention over time.
- [ ] Use accuracy prompts or short verification pauses before sharing. Research shows that shifting attention to accuracy can improve the quality of shared news ([Pennycook et al., 2021, peer-reviewed](https://www.nature.com/articles/s41586-021-03344-2)).
- [ ] Avoid generalized messages that imply all media may be false. Pair warnings with clear, accessible, credentialed sources. Journalists specializing in disinformation were significantly more likely than fact checkers or academics to agree that people will stop believing anything they see, which suggests the alarmist framing is a professional tendency worth checking in communications drafts ([Weikmann et al., 2026, peer-reviewed](https://doi.org/10.37016/mr-2020-196)).
- [ ] Evaluate whether training improves discernment and protective action. Recognition alone is not the desired outcome.

### Platform and channel controls

Experts disagree on where responsibility sits. Fact checkers placed significantly more onus on very large online platforms, while academics assigned more to news users. The split maps to the position taken here that platform friction and user-side literacy are complementary controls rather than alternatives ([Weikmann et al., 2026, peer-reviewed](https://doi.org/10.37016/mr-2020-196)).

- [ ] Detect coordinated behavior using account, timing, infrastructure, semantic, and interaction signals. Do not rely only on identical text.
- [ ] Add friction to rapid forwarding or reposting of high-risk content. Examples include prompts to open an article, limits on bulk forwarding, and a short delay before mass distribution.
- [ ] Provide transparent labels that state what is known, what is uncertain, and how the determination was made.
- [ ] Do not imply that unlabeled content has been verified.
- [ ] Preserve appeal, correction, and audit processes for automated enforcement.
- [ ] Prioritize networks and high-impact nodes rather than maximizing raw takedown counts.
- [ ] Share indicators and narrative context across platforms where law, privacy, and civil-liberties safeguards permit.
- [ ] Monitor reconstitution after takedowns, including replacement domains, accounts, groups, and payment channels.

### Disclosure and labeling

Article 50 of the EU AI Act establishes transparency duties for certain AI systems and synthetic content. Legal disclosure is a compliance obligation. It should not be treated as proof that a label will prevent belief, sharing, fraud, or unsafe action ([EU AI Act, consolidated text as of 27 July 2026](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02024R1689-20260727)).

- [ ] Use labels that explain the basis for the claim, such as signed provenance, platform disclosure, model metadata, or forensic assessment.
- [ ] Distinguish "AI-generated," "AI-edited," "unverified," "altered," and "false." These terms are not interchangeable.
- [ ] Test label comprehension, behavior, and accessibility with the intended audience.
- [ ] Preserve the original content and evidence behind the label.
- [ ] Measure spillover effects on unlabeled and authentic content.

### Trusted-source strategy

The German newspaper field experiment suggests that increased concern about AI misinformation can reduce trust in news while increasing demand for a known source. The reported treatment increased daily visits by 2.5 percent and five-month subscriber retention by 1.1 percent. The result came from one outlet, one country, and one treatment, so it should not be generalized without replication ([Campante et al., 2025, working paper](https://cepr.org/publications/dp20526)).

- [ ] Maintain a fast, accessible status page for current incidents and authentic statements.
- [ ] Publish verifiable originals, correction timelines, and a clear record of superseded material.
- [ ] Use channels already known to the audience before a crisis occurs.
- [ ] Coordinate language and timing across security, legal, communications, operations, and leadership.
- [ ] Explain uncertainty directly. Do not fill evidence gaps with categorical reassurance.
- [ ] Support independent, local, and subject-matter journalism that can verify claims for affected communities.

### Incident response

- [ ] Maintain playbooks for executive deepfakes, cloned voice fraud, forged documents, compromised accounts, poisoned retrieval, model memory contamination, and an organization's own agent repeating a false claim.
- [ ] Establish one incident commander and one evidence record across security, legal, communications, privacy, safety, and operations.
- [ ] Preserve original files, headers, URLs, account identifiers, timestamps, manifests, signing data, model logs, retrieval logs, prompts, tool calls, and downstream actions.
- [ ] Authenticate the canonical original through a known channel.
- [ ] Stop automated actions that depend on contested information.
- [ ] Request platform, domain, account, or advertisement action using pre-established escalation paths.
- [ ] Correct the record without unnecessarily repeating the false claim or linking to harmful content.
- [ ] Notify affected people and regulators as required.
- [ ] Quarantine records, embeddings, memory, caches, and fine-tuning data created during the incident window.
- [ ] Rebuild from a known-good snapshot when integrity cannot be established.
- [ ] Regression-test retrieval, generation, tools, and downstream decisions before restoration.
- [ ] Review whether the incident altered future training or evaluation data.

### Machine-audience containment

- [ ] Require structured evidence for automated verdicts. Store the source, excerpt, time, and confidence for each material claim.
- [ ] Use multiple independent checks for consequential model judgments.
- [ ] Prevent one model from acting as generator, verifier, approver, and executor for the same action.
- [ ] Randomize and diversify evaluation prompts to reduce benchmark-specific overfitting.
- [ ] Include counterevidence and contradiction tests.
- [ ] Escalate unstable verdicts to a human or a deterministic rule.
- [ ] Test for context contamination across agents, sessions, memory, and retrieved records.

A July 2026 preprint reported that model monitors detected training-data sabotage in fewer than half of benchmark cases. This emerging result supports executable artifact testing, diverse probes, and outcome monitoring rather than reliance on passive transcript review alone ([Libon et al., 2026, preprint](https://arxiv.org/abs/2607.19321)).

### Threat intelligence and sharing

- [ ] Define sharing agreements with sector information-sharing organizations, law enforcement where appropriate, vendors, platforms, and peer organizations.
- [ ] Exchange indicators together with narrative, audience, timing, confidence, and privacy constraints.
- [ ] Track claims and behavior over time. A single post rarely describes the full operation.
- [ ] Separate attribution confidence from content assessment. A claim can be false even when the actor is unknown.
- [ ] Use a consistent confidence scale and document alternative explanations.
- [ ] Review intelligence requirements after each incident and major platform or model change.

### Priority intelligence requirements

| Question | Collection focus |
| --- | --- |
| Is the organization, sector, product, or public service named in AI-generated or manipulated content? | Media monitoring, search, platform reports, customer contacts, and threat-intelligence feeds. |
| Is the content reaching a decision-maker or automated system that can cause harm? | Recipient role, workflow authority, downstream tools, and action logs. |
| Is the narrative moving across platforms or languages? | Earliest known appearance, translation variants, infrastructure, and coordinating accounts. |
| Are a small number of accounts driving most exposure? | Share concentration, network position, timing, and coordinated amplification. |
| Has a correction reached the affected audience? | Audience overlap, comprehension, belief, sharing, and task-action measures. |
| Has contested content entered an AI system? | Retrieval traces, citations, memory, fine-tuning records, cached answers, and downstream outputs. |

---

# Enterprise minimum control baseline

| Control | Minimum implementation | Evidence of operation |
| --- | --- | --- |
| Asset and data inventory | List models, agents, datasets, corpora, connectors, memory, tools, signing systems, official channels, and high-impact audiences. | Current inventory with owners and review dates. |
| Source trust tiers | Classify sources and define where each tier may be used. | Approved trust policy and sampled enforcement logs. |
| Ingestion quarantine | Validate new and changed content before indexing or training. | Quarantine records, test results, approvals, and rejected items. |
| Lineage and logging | Trace content from source to retrieval, output, and action. | Tamper-resistant logs and reproducible incident traces. |
| Action authorization | Apply least privilege, limits, and bound approvals outside the model. | Tool scopes, policy rules, approval records, and blocked-action tests. |
| Independent verification | Require a second trusted source or channel for high-impact claims and instructions. | Workflow rule and exercise results. |
| Official-channel authentication | Publish canonical sources and callback procedures. | Public directory, signed originals, and verified response drills. |
| Provenance governance | Manage signing identities, keys, validation, revocation, and credential survival. | Key inventory, signing logs, validation tests, and revocation exercises. |
| Multi-signal media assessment | Combine provenance, forensic tools, source checks, and human review. | Case records with tool versions, scores, and reviewer conclusions. |
| Cognitive resilience | Deliver technique-based prebunking, verification practice, and boosters. | Pretest, post-test, retention, and protective-action results. |
| Coordinated-behavior detection | Use semantic, temporal, account, infrastructure, and interaction signals. | Detection coverage, precision, recall, appeals, and incident examples. |
| Incident response and rollback | Isolate contaminated content and restore from known-good state. | Tabletop results, recovery-time measures, and tested snapshots. |
| Supplier assurance | Contract for disclosure, change notice, incidents, deletion, audit, and rollback. | Contract clauses, assurance reports, and issue remediation. |
| Outcome measurement | Measure belief, sharing, action, and recovery, not only engagement. | Approved metrics, preregistered tests where feasible, and decision records. |

# Measurement plan

## Core outcome measures

| Measure | Example question | Why it matters |
| --- | --- | --- |
| Discernment | Can participants distinguish reliable from unreliable items? | Measures discrimination rather than generalized skepticism. |
| Belief | Did confidence in the contested claim change? | Exposure does not equal persuasion. |
| Sharing intention and behavior | Would or did the person share the item? | Recognition may not translate into restraint. |
| Protective action | Did the person verify, escalate, refuse, or use the correct channel? | The operational goal is safer behavior. |
| Consequential task action | Did a person or agent transfer funds, change credentials, publish, or execute a tool action? | Measures real harm or prevention. |
| Time to authenticate | How long did it take to locate and verify the canonical source? | Slow verification can allow a false narrative to dominate. |
| Time to contain | How long from detection to stopping amplification or automated action? | Measures operational readiness. |
| Time to quarantine and restore | How long to isolate contaminated data and return to a known-good state? | Measures machine-audience resilience. |
| Correction reach | Did the correction reach the same audience as the original? | Publishing a correction is not the same as correcting beliefs. |
| Provenance survival | What percentage of assets retain recoverable credentials through real workflows? | Measures practical rather than theoretical deployment. |
| Corpus integrity | Are unauthorized or unexplained changes detected before use? | Measures supply-chain control. |
| Detector performance | What are false-positive and false-negative rates by media type and group? | Prevents overconfidence and disproportionate harm. |
| Subgroup and regional variance | Do outcomes differ by language, geography, accessibility, or domain? | Average results can hide targeted failures. |

The measurement emphasis in this guide reflects a documented gap. In the Kruger et al. elicitation, investing in research on intervention effectiveness drew the highest agreement of any strategy at 93 percent, and research into how specific individuals and groups become vulnerable was the most frequently selected priority for future work. The panel was non-random and predominantly Australian, so the ranking reflects one expert community's judgment rather than a global consensus ([Kruger et al., 2024, peer-reviewed](https://doi.org/10.37016/mr-2020-169)).

## Evaluation rules

- Use preregistered tests when feasible for high-impact public interventions.
- Define the primary outcome before running the study.
- Include authentic and manipulated material so a defense cannot succeed by teaching blanket distrust.
- Measure delayed outcomes and repeated exposure.
- Record model, prompt, detector, platform, and policy versions.
- Test under realistic compression, translation, editing, and cross-platform conditions.
- Include red-team cases that combine social engineering, synthetic media, compromised accounts, and poisoned retrieval.
- Publish null or adverse results internally. Controls should not survive only because failures are hidden.

# Incident exercise scenarios

1. **Executive voice fraud.** A cloned voice requests an urgent payment and asks staff to bypass the normal approval path.
2. **Forged crisis statement.** A realistic document and video claim that the organization has issued an emergency directive.
3. **Poisoned retrieval.** A forged policy document enters a shared repository and is retrieved by an internal assistant.
4. **Compromised official account.** A real account distributes a false statement, which makes channel authentication alone insufficient.
5. **Cross-platform narrative.** A claim starts in a small forum, is translated, amplified by high-reach accounts, and reported by a legitimate outlet before verification.
6. **Agent memory contamination.** A false claim is stored in long-term memory and affects later decisions after the original incident appears resolved.
7. **Credential conflict.** An asset has a valid provenance credential but conflicts with other forensic and contextual evidence.
8. **Training-data contamination.** Incident-generated records are later selected for fine-tuning or evaluation.

Each exercise should test detection, evidence preservation, decision authority, public authentication, platform escalation, legal and regulatory review, data quarantine, rollback, and post-incident measurement.

# References

## Frameworks, standards, and official guidance

- Coalition for Content Provenance and Authenticity. *C2PA Technical Specification v2.4*. [Specification](https://spec.c2pa.org/specifications/specifications/2.4/specs/C2PA_Specification.html).
- Coalition for Content Provenance and Authenticity. *C2PA Explainer*. [Explainer](https://spec.c2pa.org/specifications/specifications/2.4/explainer/Explainer.html).
- DISARM Foundation. *DISARM Red Framework*. [Framework](https://www.disarm.foundation/framework).
- European Union. *Regulation (EU) 2024/1689, consolidated text as of 27 July 2026*. [EUR-Lex](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02024R1689-20260727).
- MITRE. *MITRE ATLAS*. [Knowledge base](https://atlas.mitre.org/). [Data repository](https://github.com/mitre-atlas/atlas-data).
- National Institute of Standards and Technology. *AI Risk Management Framework*. [NIST](https://www.nist.gov/itl/ai-risk-management-framework).
- National Institute of Standards and Technology. *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*. [NIST](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence).
- National Institute of Standards and Technology. *Secure Software Development Practices for Generative AI and Dual-Use Foundation Models, SP 800-218A*. [NIST](https://www.nist.gov/publications/secure-software-development-practices-generative-ai-and-dual-use-foundation-models-ssdf).
- National Institute of Standards and Technology. *Reducing Risks Posed by Synthetic Content*. [NIST](https://www.nist.gov/publications/reducing-risks-posed-synthetic-content-overview-technical-approaches-digital-content).
- Sedova, K., McNeill, C., Johnson, A., Joshi, A., and Wulkan, I. 2021. *AI and the Future of Disinformation Campaigns, Part 2: A Threat Model*. Center for Security and Emerging Technology. [CSET](https://cset.georgetown.edu/publication/ai-and-the-future-of-disinformation-campaigns-2/).
- Wardle, C., and Derakhshan, H. 2017. *Information Disorder: Toward an Interdisciplinary Framework for Research and Policy Making*. Council of Europe. [Council of Europe](https://www.coe.int/en/web/freedom-expression/information-disorder).

## Peer-reviewed research

- Baribi-Bartov, S., et al. 2024. *Supersharers of Fake News on Twitter*. Science. [DOI](https://www.science.org/doi/10.1126/science.adl4435).
- Cinelli, M., et al. 2021. *The Echo Chamber Effect on Social Media*. Proceedings of the National Academy of Sciences. [DOI](https://www.pnas.org/doi/10.1073/pnas.2023301118).
- Fazio, L. K., et al. 2020. *The Effect of Repetition on Truth Judgments Across Development*. Psychological Science. [PubMed](https://pubmed.ncbi.nlm.nih.gov/32857670/).
- Gebru, T., et al. 2021. *Datasheets for Datasets*. Communications of the ACM. [DOI](https://doi.org/10.1145/3458723).
- Huang, G., Zhang, Y., Li, Z., You, Y., Wang, M., and Yang, Z. 2024. *Are AI-Generated Text Detectors Robust to Adversarial Perturbations?*. Proceedings of ACL. [ACL Anthology](https://aclanthology.org/2024.acl-long.327/).
- Kruger, A., Saletta, M., Ahmad, A., and Howe, P. 2024. *Structured Expert Elicitation on Disinformation, Misinformation, and Malign Influence: Barriers, Strategies, and Opportunities*. Harvard Kennedy School Misinformation Review 5(7). [DOI](https://doi.org/10.37016/mr-2020-169).
- Lu, C., Hu, B., Li, Q., et al. 2023. *Psychological Inoculation for Credibility Assessment, Sharing Intention, and Discernment of Misinformation: Systematic Review and Meta-Analysis*. Journal of Medical Internet Research. [Article](https://www.jmir.org/2023/1/e49255/).
- Maertens, R., et al. 2025. *Psychological Booster Shots Targeting Memory Increase Long-Term Resistance Against Misinformation*. Nature Communications. [Article](https://www.nature.com/articles/s41467-025-57205-x).
- Martel, C., Pennycook, G., and Rand, D. G. 2020. *Reliance on Emotion Promotes Belief in Fake News*. Cognitive Research: Principles and Implications. [DOI](https://doi.org/10.1186/s41235-020-00252-3).
- McLoughlin, K. L., et al. 2024. *Misinformation Exploits Outrage to Spread Online*. Science. [DOI](https://www.science.org/doi/10.1126/science.adl2829).
- Pennycook, G., et al. 2021. *Shifting Attention to Accuracy Can Reduce Misinformation Online*. Nature. [Article](https://www.nature.com/articles/s41586-021-03344-2).
- Salvi, F., et al. 2025. *On the Conversational Persuasiveness of GPT-4*. Nature Human Behaviour. [Article](https://www.nature.com/articles/s41562-025-02194-6).
- Simchon, A., Zipori, T., Teitelbaum, L., Lewandowsky, S., and van der Linden, S. 2026. *A Signal Detection Theory Meta-Analysis of Psychological Inoculation Against Misinformation*. Current Opinion in Psychology. [DOI](https://doi.org/10.1016/j.copsyc.2025.102194).
- Weikmann, T., Wouters, F., Tulin, M., Hameleers, M., de Vreese, C. H., Zarouali, B., and Opgenhaffen, M. 2026. *On the Same Page? Experts Are Mostly, but Not Always Aligned About Disinformation in Times of Generative AI*. Harvard Kennedy School Misinformation Review 7(2). [DOI](https://doi.org/10.37016/mr-2020-196).
- Williams, M., et al. 2025. *On Targeted Manipulation and Deception When Optimizing LLMs for User Feedback*. ICLR 2025. [Paper](https://arxiv.org/abs/2411.02306).
- Zou, W., Geng, R., Wang, B., and Jia, J. 2025. *PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models*. USENIX Security 2025. [USENIX](https://www.usenix.org/conference/usenixsecurity25/presentation/zou-poisonedrag).

## Working paper

- Campante, F., Durante, R., Hagemeister, F., and Sen, A. 2025. *GenAI Misinformation, Trust, and News Consumption: Evidence from a Field Experiment*. CEPR Discussion Paper 20526 and NBER Working Paper 34100. [CEPR](https://cepr.org/publications/dp20526).

## Preprints and emerging evidence

- Akbulut, C., et al. 2026. *Evaluating Language Models for Harmful Manipulation*. [arXiv](https://arxiv.org/abs/2603.25326).
- Golaszewski, E., et al. 2026. *Verifying Provenance of Digital Media: Why the C2PA Specifications Fall Short*. [arXiv](https://arxiv.org/abs/2604.24890).
- Libon, L., et al. 2026. *ResearchArena: Evaluating Sabotage and Monitoring in Automated AI R&D*. [arXiv](https://arxiv.org/abs/2607.19321).
- Nemecek, A., He, H., Cheng, G., and Ayday, E. 2026. *Authenticated Contradictions from Desynchronized Provenance and Watermarking*. Accepted at the CVPR 2026 Workshop on Authenticity and Provenance in the Age of AI. [arXiv](https://arxiv.org/abs/2603.02378).
- Prinos, K., Brush, L., and Denton, C. 2026. *Honeyquest for LLMs: Rethinking Cyber Deception for AI Attackers*. [arXiv](https://arxiv.org/abs/2606.21037).

## Personal research

- Carroll, N. (2026). *Algorithmic subversion & strategic deception*. [https://github.com/Nate-Carroll-Cyber/Counter-Spy.ai/blob/main/Research/Algorithmic%20Subversion%20%26%20Strategic%20Deception.md](https://github.com/Nate-Carroll-Cyber/Counter-Spy.ai/blob/main/Research/Algorithmic%20Subversion%20%26%20Strategic%20Deception.md).
- Carroll, N. (2026). *ODESSA — AI incident response loop*. [https://github.com/Nate-Carroll-Cyber/ODESSA-AI-IR-Loop](https://github.com/Nate-Carroll-Cyber/ODESSA-AI-IR-Loop).

## License

Research & documentation (including Countering AI-Enabled Disinformation and other research documents) © Counter-Spy.ai, licensed under CC BY 4.0. You may share and adapt with attribution to Counter-Spy.ai (Nate Carroll).
