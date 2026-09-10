# RFC-0003: Deployment and Trust Model
## Data Ownership, Local Inference, and Threat Mitigation for Organizers

---

## 1. Introduction & Objectives

Democratic, labor, and tenant organizations frequently face corporate infiltration, state surveillance, and legal exposure. Introducing digital tools into these environments requires an explicit, robust trust and deployment model. 

Leninware is designed to operate on a **local-first, decentralized, and zero-telemetry** model. This document details the security posture, data boundaries, and threat mitigation strategies for organizers running ContentForge and Commonwealth.

---

## 2. Core Security & Trust Guarantees

* **Local Execution by Default:** The software is not delivered as a centralized Software-as-a-Service (SaaS). It runs on hardware owned and controlled directly by the organizing group.
* **100% Data Ownership:** All inputs (topics, source text, media uploads, internal narratives), intermediate representations (transcripts, script drafts, visual prompts), and final media assets are stored locally on the operator’s disk. No third-party servers act as intermediaries or store copies of your data.
* **Zero Telemetry and Tracking:** The codebase contains no analytics, reporting scripts, usage tracking, or automatic updater phone-homes. The system only reaches out to external APIs if explicitly configured to do so by the user.
* **Training Data Sovereignty & Governance:** Any future mechanism that feeds node-generated outputs back into model training must preserve the guarantees above. Nodes do not act as passive data suppliers; they influence the training methodology. Training data remains under the control of the collective that produced it, and participation in any shared training loop is opt-in, transparent, and governed by the participating nodes. The specific protocol for weighting examples based on local filter provenance is deferred to a future RFC.

---

## 3. Deployment Modes & Data Boundaries

Organizations can configure ContentForge to operate in one of three modes depending on their threat landscape and hardware constraints.

```
+-------------------------------------------------------------------------+
|                               USER DEVICE                               |
|                                                                         |
|  [ ContentForge CLI ] --(Local Filesystem)--> [ outputs/ & databases ]  |
|          |                                                              |
|          +--- (Mode A: Offline Local) ---> [ Local Ollama Engine ]      |
|          |                                                              |
|          `--- (Mode B: Private API) ------> [ External LLM Providers ]  |
+-------------------------------------------------------------------------+
```

### Mode A: Offline Local (Maximum Trust)
* **LLM Engine:** Local inference using **Ollama** (e.g., running `llama3.1` or `mistral`).
* **TTS Engine:** Neural voice generation using local synthetic engines or mock placeholders (TTS generation deferred locally).
* **Network Boundary:** The device can run entirely disconnected from the Internet. Inputs, scripts, and analysis do not leave the local machine.
* **Use Case:** High-risk campaigns, internal strategic planning, or situations where absolute privacy is required.

### Mode B: Private API (Hybrid Trust)
* **LLM Engine:** Cloud LLM providers (Anthropic, OpenAI) accessed via user-provided API keys.
* **TTS Engine:** Microsoft Edge TTS (neural quality via free network requests) or OpenAI TTS.
* **Network Boundary:** Outbound HTTPS requests to specific API endpoints. Inputs and prompts are sent to the provider.
* **Security Consideration:** Providers may log prompts according to their data retention policies. While major providers claim API inputs are not used for model training, they may still be retained for abuse monitoring (typically 30 days).

---

## 4. Threat Model & Mitigations

### Threat 1: Interception of Strategic Materials
* **Description:** An adversary intercepts drafts of agitation scripts, target lists, or organization coordinates.
* **Mitigation:**
  * Use **Mode A (Offline Local)** so data never crosses the network.
  * Encrypt the local storage volume containing ContentForge's `outputs/` directory and Commonwealth’s databases (e.g., using BitLocker, LUKS, or VeraCrypt).

### Threat 2: Surveillance via API Logs
* **Description:** State or corporate adversaries subpoena API providers (Anthropic, OpenAI, Microsoft) for request logs associated with an organizer's API key.
* **Mitigation:**
  * When utilizing API Mode, use temporary or project-specific billing accounts.
  * Prefer **Ollama** for all strategic writing and discourse analysis steps. Only use external APIs for low-risk, public-facing topics.

### Threat 3: Data Poisoning and Supply Chain Attacks
* **Description:** Compromised dependencies in Python or Node packages leak local database contents to a remote server.
* **Mitigation:**
  * Dependencies are pinned and locked using `uv.lock` (Python) and `pnpm-lock.yaml` (TypeScript).
  * Production deployments should run inside isolated containers (Docker) with restricted network access, blocklisting all outbound traffic except to authorized API domains.

---

## 5. Deployment Recommendations for Organizers

1. **For Tenant & Labor Agitation (Public Campaigns):**
   * **Mode B (Private API)** is acceptable. The speed of cloud LLMs is useful for churning out daily reactive videos. Since the campaign topic is public, API logging carries a lower risk.
2. **For Strike Planning & Internal Debates (Strategic Operations):**
   * **Mode A (Offline Local)** is mandatory. Run the pipeline on air-gapped or encrypted laptops. Turn off external LLM providers entirely in `.env` by ensuring `CONTENTFORGE_REAL_MODE` is disabled or routed to Ollama.
3. **Container Isolation:**
   * Run the CLI inside a Docker container:
     ```bash
     docker build -t contentforge .
     docker run --network=none -v $(pwd)/outputs:/app/outputs contentforge --topic "Local organizing drive"
     ```