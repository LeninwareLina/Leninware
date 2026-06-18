# RFC-0002: Commonwealth Overview
## Commonwealth Bridge and Resource Coordination

---

## 1. Context
Commonwealth is the planning and resource coordination ledger designed to map local exploitation and distribute mutual aid/provisioning resources. The "Commonwealth Bridge" is the data exchange protocol that feeds direct material conditions into ContentForge's intelligence pipeline.

---

## 2. Scope of Commonwealth
Commonwealth serves three core logistical needs:
* **Financial Organization:** Establishing community ledgers and mutual aid tracking outside capitalist banking networks.
* **Resource Planning:** Logistical mapping of local community assets, tenant unions, food supplies, and eviction notices.
* **Collective Provisioning:** Managing shared resources and distribution routes to maximize mutual support.

---

## 3. The Commonwealth Bridge Protocol
To drive ContentForge media with live local data, we establish a standardized payload definition. This allows local chapters using Commonwealth to instantly output targeted agitation and educational media.

### 3.1 JSON Payload Schema
Commonwealth sends structured snapshots to ContentForge:
```json
{
  "source_system": "commonwealth",
  "data_type": "material_conditions",
  "payload": {
    "location": {
      "city": "Los Angeles",
      "neighborhood": "Koreatown"
    },
    "exploitation_type": "eviction_filing",
    "metrics": {
      "corporate_landlord": "Veritas Investments",
      "evictions_filed_this_month": 42,
      "average_rent_increase_percentage": 18.5
    },
    "action_outlets": [
      {
        "name": "Koreatown Tenants Network",
        "contact": "https://koreatowntenants.org"
      }
    ]
  }
}
```

---

## 4. Ingestion & Content Generation
When ContentForge receives a Commonwealth payload:
1. **Intent Resolution:** Bypasses standard web search/summarization and classifies input as `commonwealth_data`.
2. **Discourse Analysis:** Identifies the target audience (e.g., local tenants facing rent increases) and selects the optimal register (e.g., `controlled_fury` or `patient_educator`).
3. **Script Generation:** Translates raw rent and landlord metrics into materialist script analyses. Crucially, the script details structural incentives (the logic of real estate finance) and points viewers directly to the local organizing resource (Koreatown Tenants Network).
