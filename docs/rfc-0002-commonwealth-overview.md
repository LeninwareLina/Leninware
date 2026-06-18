# RFC-0002: Commonwealth Overview
## Commonwealth Bridge and Resource Coordination

---

## 1. Context
Commonwealth is the planning, governance, and resource coordination ledger designed for post-capitalist institutional transition. Its Level 0 capability is the **Labor Visibility Substrate** — a durable shared representation of labor, contributions, dependencies, and thermodynamic conditions. 

The "Commonwealth Bridge" is the data exchange protocol that feeds direct collective health, task narratives, and resource constraints into ContentForge's intelligence pipeline to generate targeted agitation, education, and mobilization media.

---

## 2. Core Domain Model
Commonwealth’s business logic is grounded in participatory economics (Parecon) and negotiated coordination. It rejects surveillance and audit-driven logging, prioritizing legibility and collective trust.

```
                   +-------------------+
                   |    Collective     |
                   +---------+---------+
                             |
         +-------------------+-------------------+
         |                                       |
+--------v----------+                   +--------v----------+
|      Member       |                   |     WorkItem      |
|  (Standing: Act/  |                   |  (Status: Prop/   |
|   Obs/Suspended)  |                   |   Act/Comp/Arch)  |
+--------+----------+                   +---+-------+-------+
         |                                  |       |
         |         +------------------------+       |
         |         |                                |
+--------v---------v+                       +-------v-----------+
|   Contribution    |                       |    Dependency     |
| (Context: trust/  |                       |  (Type: Blocking/ |
|  attributable to  |                       |   Informational)  |
|  indiv/collective)|                       +-------------------+
+-------------------+
```

### 2.1 Collective
The coordinating unit of organization.
* `id`: Unique identifier (UUID).
* `name`: Name of the collective.
* `description`: Purpose of the collective.
* `metadata`: Extensible context for chapter/group-specific data.

### 2.2 Member
A full domain concept representing standing within the collective, drawing from Devine's model of standing proportional to being affected by decisions.
* `id`, `collectiveId`, `name`, `contact`, `joinedAt`.
* `standing`: Active, Observer, or Suspended.

### 2.3 WorkItem
Individual tasks, projects, or campaigns.
* `id`, `collectiveId`, `title`.
* `narrative`: Description of *why* this work exists and what it unblocks (Required).
* `status`: Proposed, Active, Completed, or Archived. (Note: "Blocked" is a derived state calculated from unresolved dependencies, never a manually set status).
* `resourceConstraints`: Defines the thermodynamic reality of the task, replacing price-based scarcity:
  * `energyRequired` (e.g., "High", "10kWh")
  * `materials` (e.g., `["printing paper", "flyers"]`)
  * `infrastructureDependencies` (e.g., `["sound system", "room hire"]`)

### 2.4 Contribution
Legitimizes and makes individual and care work visible.
* `id`, `workItemId`, `description` (what was done).
* `context`: Qualitative narrative context to make labor referenceable (rather than audited proof).
* **Attribution constraint:** Contributions must have either `memberId` (individual contribution) or `collectiveId` (collective care/work that cannot be subdivided), never both and never neither.

### 2.5 Dependency
Defines graph-based relationships between tasks.
* `id`, `dependentWorkItemId` (blocked item), `dependencyWorkItemId` (prerequisite).
* `type`: Blocking (strict constraint) or Informational (general awareness).
* `justification`: Detailed narrative justifying why the dependency exists.

### 2.6 Stewardship & Graph Health
Tracks the systemic coordination health of the collective using structural and qualitative metrics:
* `narrativeDensity`: Percentage of work items explaining *why* they exist.
* `flowIntegrity`: Ratio of unblocked work items to active items.
* `resilienceFactor`: Contributor diversity across critical dependencies.
* `detectedBlindSpots`: Circular dependencies, missing narratives, or unaddressed bottlenecks.

---

## 3. The Commonwealth Bridge Protocol
Instead of feeding raw exploitation metrics, the actual Commonwealth Bridge feeds systemic logistical snapshots and resource constraints into ContentForge.

### 3.1 JSON Payload Schema
The bridge utilizes `StewardshipSnapshot` payloads to identify mobilization and agitative opportunities:
```json
{
  "source_system": "commonwealth",
  "data_type": "stewardship_snapshot",
  "payload": {
    "collective_id": "7bf3-40e1-88f9-cf5603a12a5b",
    "collective_name": "Koreatown Tenants Network",
    "health": {
      "narrative_density": 0.95,
      "flow_integrity": 0.58,
      "resilience_factor": 0.40,
      "status": "Fragile"
    },
    "detected_blind_spots": [
      "Eviction prevention door-knocking blocked by physical material constraint: 'flyers' on WorkItem 'August Agitation Blitz'"
    ],
    "capacity_forecast": "Tenant outreach is stalled due to local production material bottleneck."
  }
}
```

---

## 4. Ingestion & Agitation Logic
When ContentForge receives a Commonwealth `stewardship_snapshot` payload:
1. **Intent Resolution:** Classifies the source as `commonwealth_snapshot`.
2. **Discourse Analysis:** Identifies the target audience (local supporters, volunteers, or community members) and recommended registers (e.g., `exhausted_analyst` to point out the absurdity of local resource lockups, or `patient_educator` to request mutual aid).
3. **Script Generation:** Translates the logistical blockages (e.g., Veritas Investments' evictions increasing while KTN is blocked on door-knocking flyers) into a call for material mobilization. 

The resulting video script directs the working class not to abstract charity, but to step in and directly resolve the thermodynamic constraints of the local organizing graph.
