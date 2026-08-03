# RFC-0001: ContentForge Expansion
## Next Horizon (Levels 2-4)

---

## 1. Objective
This RFC details the expansion plan for ContentForge as it transitions from **Level 1 (Short-Form Video Production)** to **Levels 2, 3, and 4**. It focuses on achieving input flexibility, enabling long-form video explainer generation, and supporting static print media output.

---

## 2. Level 2: Input Flexibility (Unified Ingestion Layer)
To move beyond YouTube transcripts, ContentForge requires a unified ingestion pipeline capable of consuming diverse input types while producing a standardized context for the Discourse Analyzer and Script Generator.

### 2.1 Refactored Ingestion Flow
```
Creator Input (URL / MD / PDF / Text / Commonwealth Feed)
  --> IngestionManager
  --> [BaseIngestor Subclasses]
  --> Normalized Ingestion Context
  --> Discourse Analyzer
```

### 2.2 Ingestion Interface (`BaseIngestor`)
A common abstract base class will enforce formatting uniformity:
```python
class BaseIngestor(ABC):
    @abstractmethod
    def can_handle(self, source: str) -> bool:
        """Evaluate if the source format/protocol is supported."""
        pass

    @abstractmethod
    def ingest(self, source: str) -> NormalizedContent:
        """Process the source into standard text and metadata."""
        pass
```

### 2.3 Input Formats & Graceful Defaults
* **Markdown & PDF Uploads:** Text parsing and key section extraction.
* **Topic-Only Ingestion:** Brave Search queries to enrich sparse inputs.
* **Intelligent Defaults:** In the absence of user input, the system selects from a library of local working-class issues (transit, housing, municipal budgets) to auto-generate content.

---

## 3. Level 3: Long-Form Video Production
While short-form video serves rapid agitation, long-form content is required for deeper structural and historical explainers.

### 3.1 Narrative Pacing & Pacing Segmenter
Long-form videos (2-10 minutes) require logical sectioning rather than standard short-form segment slices:
1. **Hook & Agitation (0% - 15%):** Present a concrete, relatable local contradiction.
2. **Structural Mapping (15% - 80%):** Detail the institutional, political, and financial networks (exposing switching points).
3. **Solidarity/Action (80% - 100%):** Direct the viewer toward mutual aid or local organizing groups.

### 3.2 Visual & Audio Transitions
* **Visual Transitions:** FFmpeg-based panning, zooming, and text title overlay transitions to avoid visual fatigue from static images.
* **Multi-Track Audio:** Dynamic crossfades for background music that shift volume and intensity based on the active narrative section.

---

## 4. Level 4: Static Media Output
Physical outreach remains a foundational element of local socialist organization. Level 4 introduces print-ready leaflet and poster generation.

### 4.1 Flyer Generation Pipeline
1. **Text Layout Design:** ScriptGenerator outputs a structured JSON representing headline, key points, local contact info, and Call to Action.
2. **Template Interpolation:** Inject text into CSS-designed HTML flyer templates.
3. **PDF Compilation:** Use lightweight rendering tools (e.g., WeasyPrint) to output print-ready, high-resolution PDFs.

---

## 5. Relationship to Other Documents
* **Commonwealth Ingestion:** Structured data feeds from Commonwealth are detailed in [RFC-0002](rfc-0002-commonwealth-overview.md).
* **Guiding Framework:** The philosophical alignment of these stages is governed by the monorepo root [PHILOSOPHY.md](file:///c:/dev/leninwareAI/PHILOSOPHY.md).
