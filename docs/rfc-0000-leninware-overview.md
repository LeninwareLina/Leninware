# RFC-0000: Leninware Overview
## Mission, Architecture, and Context

---

## 1. Executive Summary & Context

Leftist organizations lose the media war not because they lack arguments but because they lack production capacity. A well-funded right-wing media operation can turn a news event into a polished video within hours. A socialist organizer has to write, record, edit, and distribute manually — if they have time at all. ContentForge eliminates that production gap.

Existing tools fail for a specific reason: they are politically neutral by design. ChatGPT will not tell you that corporate climate rhetoric is hegemonic stabilization for a system built on extraction. It will produce balanced, both-sides content that implicitly validates the liberal framework. Leninware is explicitly, deliberately not neutral. It starts from a materialist analysis and produces content that reflects that analysis. That is not a bug — it is the entire point.

Commonwealth exists because coordination tools embed assumptions about ownership and decision-making. A spreadsheet treats all contributors as equivalent data points. A project management tool assumes hierarchical task assignment. Commonwealth is being built to reflect how collective labor actually works — contributions without bosses, dependencies without managers, visibility without surveillance.

**Why not Discord + ChatGPT + spreadsheets?** Because the tools you use shape the politics you can practice. You cannot run a democratic collective on software designed for corporate hierarchies.

---

## 2. Problem Statement

Leftist organizations are historically bottlenecked by two main systemic factors:
1. **Media Production Asymmetry:** Commercial media and well-funded opposition operations leverage high-speed automation and massive resource pools to capture public attention. Organizers spend hours manually drafting scripts, generating assets, and stitching together video, diluting their capacity for direct organizing.
2. **Coordination Scarcity & Surveillance:** Standard collaboration tools (like Slack, spreadsheets, or corporate task trackers) assume hierarchical, surveillance-driven management styles. They fail to reflect non-monetary dependencies, mutual aid dynamics, or care work, leaving collective labor invisible and uncoordinated.

---

## 3. Architecture & Projects

Leninware is a unified ecosystem composed of two companion systems:

```
               +--------------------------------------+
               |          Leninware Ecosystem         |
               +-------------------+------------------+
                                   |
         +-------------------------+-------------------------+
         |                                                   |
+--------v------------------+                       +--------v------------------+
|       ContentForge        |                       |       Commonwealth        |
| (Media Production Engine) | <--- [Data Bridge] -- |   (Coordination Ledger)   |
+--------+------------------+                       +--------+------------------+
         |                                                   |
         |-- Intent Resolution                               |-- Labor Visibility Substrate
         |-- Discourse Analysis                              |-- Graph-Based Dependency Map
         |-- Register Selector                               |-- Stewardship Health Metrics
         `-- Media Synthesis Pipeline                        `-- Participatory Ledger
```

### 3.1 ContentForge (Python)
ContentForge is a political intelligence and media production engine. It is responsible for translating topics, transcripts, or URL inputs into polished, class-conscious media.
* **Intent Resolution:** Resolves input types and bridges contextual gaps using intelligent defaults.
* **Discourse Analysis:** Scans opposing or mainstream transcripts to identify rhetorical strategies, speaker loyalty, and ideological framing.
* **Register Selector:** Dynamically selects the emotional and rhetorical mode of communication (e.g., *exhausted analyst*, *controlled fury*, *patient educator*).
* **Media Synthesis:** Coordinates TTS audio, AI visual generation, and FFmpeg assembly into burned-caption video output.

### 3.2 Commonwealth (TypeScript/Node)
Commonwealth is a planning and resource coordination ledger designed for democratic collective management and institutional transition.
* **Labor Visibility Substrate:** Establishes a durable, shared representation of contributions, including qualitative and care-focused labor.
* **Dependency Mapping:** Computes blockers, resource constraints (such as physical materials or space hire), and task narratives in a non-hierarchical graph.
* **Stewardship Metrics:** Evaluates systemic coordination health (narrative density, flow integrity, resilience factors) rather than individual compliance.

---

## 4. Philosophical Grounding

Leninware's architecture is rooted in the **Web-and-Gravity** philosophical model. Power is viewed not as a monolith, but as a relational web of vulnerable nodes. Our software represents the physical reification of class-conscious thought into digital infrastructure.

We reject academic insularity in favor of translation and accessibility, designing all components to form an active reflex loop between material organizing coordinates (Commonwealth) and public agitative media (ContentForge).

### 4.1 Collective Intelligence and Governance

A core design intention of the Leninware federation model is that nodes influence model training not only through *what* data they contribute but through *how* they evaluate it. Outputs generated by nodes—and critically, the qualitative filters and criteria used to select those outputs—feed back into a decentralized learning loop.

The quality filter you run locally is itself a governance mechanism. In this model, federated aggregation respects filter provenance when weighting examples: a node with stricter, more explicit materialist criteria contributes examples with a higher confidence weight. The people generating the data thus participate in governing the *methodology* of what the model learns, rather than acting as passive data suppliers to a central fine-tuning authority.

The exact mechanism for this (federated fine-tuning, provenance-weighted aggregation, or another approach) is deferred to a future RFC. What is established here is the principle: training data produced by organizers belongs to the collective that produced it, and the criteria they use to evaluate it must influence the collective intelligence. This is a natural consequence of the local-first, zero-telemetry commitments described in [RFC-0003](rfc-0003-deployment-and-trust.md) and the Web-and-Gravity framework's rejection of centralized control over shared infrastructure.

For a complete breakdown of this ideological framework, refer to the root [PHILOSOPHY.md](file:///c:/dev/leninwareAI/PHILOSOPHY.md).

---

## 5. Deployment and Trust

To ensure the safety of organizers under surveillance and prevent data enclosure, Leninware is designed with a decentralized, local-first threat model. For full details on self-hosting, data ownership, local inference support, and threat mitigations, see [RFC-0003: Deployment and Trust Model](rfc-0003-deployment-and-trust.md).