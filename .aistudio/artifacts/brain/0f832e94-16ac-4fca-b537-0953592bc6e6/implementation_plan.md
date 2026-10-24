# AGENT CREATOR — Architectural Foundation & Governance Engine

An enterprise-grade, Harness-governed Agent Creator engine built with a zero-hardcoded philosophy. It enforces strict Finite State Machine (FSM) transitions, dynamic Gate-Driven validation powered by Instructor/Pydantic structured schemas, relational SQLite state persistence with an in-memory cache, and continuous architectural dissociation between the Agentic Control Plane and the Produced Software Product.

---

### User Review & Critical Decisions

> [!IMPORTANT]
> The architectural foundation and governance engine is constructed around the three core choices confirmed during the interview:
> - **Execution Mode**: Dual-mode execution engine featuring deterministic mock/schema gate sandbox testing alongside Live Gemini-powered reactive execution (`gemini-3.8-flash`) with Gate validations. Everything (documents, artifacts, knowledge, specs) is cataloged as a typed object.
> - **Persistence & Query Engine**: Relational SQLite embedded database (`agent_creator.db`) with an in-memory high-throughput cache layer for instant retrieval, assertiveness, and query pattern functions.
> - **UI & Observability Posture**: Terminal-first reactive console with dynamic schema inspection paired with a real-time interactive BPMN/Flow canvas with Gate trigger nodes.

- **Confirmed Decision 1**: Dual execution mode (deterministic schema gate sandbox + live Gemini reactive gate evaluation).
- **Confirmed Decision 2**: SQLite embedded database serving as the Single Source of Truth (SSOT) with in-memory caching for sub-millisecond query pattern execution.
- **Confirmed Decision 3**: Real-time BPMN flow observer and interactive canvas with gate trigger nodes combined with a terminal-first reactive inspector.
- **Confirmed Decision 4 (Architectural Dissociation)**: Strict separation between the **Agentic Platform Architecture** (Control Plane & Meta-Agent) and the **Target Product Architecture** (the generated agent/software product), with continuous post-determinism validation gates.

---

### 1. Overview & Core Concept

- **What It Does**: AGENT CREATOR is a meta-agentic governance and creation platform. Rather than building ad-hoc agents with hardcoded if-else logic, it operates as a strict Finite State Machine (FSM) where every transition is guarded by deterministic **Gates**. Each gate validates generated payloads against dynamic schemas (Pydantic/Instructor pattern), tracks object lifecycles in SQLite, and ensures the target agent architecture never leaks into the meta-agentic engine.
- **Target Audience / Persona**: AI System Architects, Autonomous Agent Engineers, and Enterprise Platform Operators who require verifiable, reproducible, and audit-compliant agent creation.
- **Key Value**: Zero hardcoded logic, guaranteed deterministic convergence via gate validations, full auditability of all agent artifacts as first-class objects, and absolute prevention of platform-target state pollution.

---

### 2. User Experience & Visual Design

#### Key User Flows
1. **Agent Genesis & Intent Definition**: The operator initializes a new agent specification. The system transitions into `INIT_INTENT` and validates the input specification against the initial intent gate.
2. **Interactive BPMN Flow Observation**: The operator monitors the agent lifecycle across real-time BPMN gate nodes:
   - `[01_INTENT]` ➔ `[02_DOMAIN_SPEC_GATE]` ➔ `[03_SCHEMA_MODELING]` ➔ `[04_TOOL_SYNTHESIS_GATE]` ➔ `[05_DISSOCIATION_GATE]` ➔ `[06_POST_DETERMINISM_GATE]` ➔ `[07_COMPILED_AGENT]`
3. **Gate-Driven Reactive Execution**: Clicking or triggering a gate executes the associated backend validation function. If payload validation fails, the reactive engine streams the error trace to the terminal console and triggers a self-correction synthesis loop.
4. **Dynamic Schema & Object Inspector**: The operator selects any node or cataloged object (Document, Tool, Gate Rule, State Schema) to inspect its Pydantic/Instructor-style JSON schema, validation constraints, and database record.
5. **Architectural Dissociation Audit**: A dedicated inspector verifies the clean dissociation between the Agentic Control Plane (internal SQLite state, Gemini API calls, gate runners) and the Target Agent Product (isolated target schemas, tools, and execution artifacts).

#### Visual Identity & Theme (SaaS Dashboard & Developer Console Guidelines)
- **Aesthetic Direction**: High-density, utilitarian developer console inspired by mission-critical control rooms and modern compiler toolchains.
- **Color Palette & Mood**:
  - Neutral Canvas: Deep dark slate (`#0B0F17`) and structural surface layers (`#111827`, `#1F2937`) with 1px hairline borders (`rgba(255,255,255,0.08)`).
  - Status Accents (Functional only):
    - Emerald (`#10B981`): Gate Passed / Deterministic Convergence / Active State
    - Amber (`#F59E0B`): Gate Evaluating / Self-Correction in Progress / Warning
    - Crimson (`#EF4444`): Gate Blocked / Schema Validation Error
    - Cyan (`#06B6D4`): Active BPMN Flow / Control Plane Pointer
- **Typography & Hierarchy**:
  - Display & Headings: `Plus Jakarta Sans` or `Outfit` for crisp structural hierarchy.
  - Body Prose: `Public Sans` or `DM Sans` for dense readability.
  - Data, Schemas & Telemetry: Monospace tabular numerals (`JetBrains Mono`, `tabular-nums`) with zero layout jitter.
- **Top Bar Contract**:
  - Zone 1: Single text wordmark `AGENT CREATOR` with subtle platform versioning.
  - Zone 2: Single-line navigation links (`FSM Pipeline`, `Object Catalog`, `Gate Engine`, `Dissociation Matrix`, `Terminal Logs`).
  - Zone 3: Primary Action (`Run Agent Genesis` / `Validate All Gates`).

---

### 3. Key Product Decisions & Trade-Offs

- **Decision 1: Dual Execution Engine (Deterministic Mock Sandbox + Live Gemini Gate Evaluation)**
  - *Chosen Approach*: The system provides both instant deterministic mock/replay execution (for zero-latency CI/CD testing and unit gates) and live `@google/genai` (`gemini-3.8-flash`) synthesis with schema-enforced output.
  - *Why*: Allows rapid offline gate verification, deterministic regression testing, and robust production-grade synthesis using Google AI Studio API.
  - *Alternatives Considered*: Pure LLM generation without deterministic gates was rejected due to lack of predictability and risk of unverified hallucinations.

- **Decision 2: SQLite Relational State Store with High-Speed In-Memory Cache**
  - *Chosen Approach*: An embedded SQLite database (`agent_creator.db`) backing all FSM states, objects, and gate logs, augmented with an in-memory cache map for sub-millisecond query pattern execution.
  - *Why*: Provides ACID guarantees, relational joins, and persistent state across server restarts without external network dependencies, while the cache ensures instant UI reactivity.

- **Decision 3: Instructor & Pydantic Meta-Pattern in Backend**
  - *Chosen Approach*: TypeScript schemas mirroring Pydantic `BaseModel` and Instructor validation pipelines. Every payload must satisfy a strict structural schema before any state transition is allowed.
  - *Why*: Prevents malformed agent definitions, enforces strict typing across all gates, and guarantees that every artifact (documents, tools, knowledge) is cataloged as a validated object.

- **Decision 4: Explicit Architectural Dissociation Registry**
  - *Chosen Approach*: Continuous post-determinism validation comparing the Control Plane schema against the Target Agent Product schema. Any accidental import or shared global state raises a dissociation violation gate error.
  - *Why*: Guarantees that the generated software product is standalone, reproducible, and completely decoupled from the creator engine.

---

### 4. Technical Architecture & Data Strategy

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                            AGENT CREATOR PLATFORM                           │
├─────────────────────────────────────────────────────────────────────────────┤
│  FRONTEND (React 19 + Tailwind CSS + Lucide Icons + Motion)                 │
│  ┌───────────────────────┐  ┌───────────────────────┐  ┌─────────────────┐  │
│  │ BPMN Flow Observer    │  │ Schema & Gate Studio  │  │ Terminal Console│  │
│  │ (Interactive Gates)   │  │ (Object Inspector)    │  │ (Reactive Logs) │  │
│  └───────────┬───────────┘  └───────────┬───────────┘  └────────┬────────┘  │
│              │                          │                       │           │
│              └──────────────────────────┼───────────────────────┘           │
│                                         ▼                                   │
│  HTTP / REST API Client (Vite Dev Server Proxy -> Express /api/*)           │
├─────────────────────────────────────────────────────────────────────────────┤
│  BACKEND (Node.js + Express + TypeScript)                                   │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ FSM Engine & Gate Controller (Zero Hardcoded Rules)                   │  │
│  │ - Transition Guards & Trigger Functions                               │  │
│  │ - Instructor/Pydantic Dynamic Schema Validator                        │  │
│  │ - Reactive Self-Correction & Gate Evaluation Runner                   │  │
│  └──────────────────┬─────────────────────────────────┬──────────────────┘  │
│                     │                                 │                     │
│                     ▼                                 ▼                     │
│  ┌─────────────────────────────────────┐  ┌──────────────────────────────┐  │
│  │ Dual Execution Provider             │  │ Architectural Dissociation   │  │
│  │ - Deterministic Sandbox Runner      │  │ Registry & Post-Determinism  │  │
│  │ - Live Gemini (@google/genai SDK)   │  │ Validation Gate              │  │
│  └──────────────────┬──────────────────┘  └──────────────┬───────────────┘  │
│                     │                                    │                  │
│                     ▼                                    ▼                  │
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │ Database Layer & High-Speed In-Memory Cache (SSOT)                    │  │
│  │ - SQLite: fsm_states, agent_objects, gate_evaluations, run_traces     │  │
│  │ - In-Memory Cache Map for fast query pattern retrieval               │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────┘
```

#### Database Schema & Object Catalog (SQLite)
1. `fsm_states`: `state_id`, `name`, `step_order`, `gate_rules_json`, `required_schema_id`, `created_at`
2. `agent_objects`: `object_id`, `object_type` (INTENT, KNOWLEDGE, DOCUMENT, TOOL_SPEC, GATE_RULE, SCHEMA_MODEL, ARTIFACT), `name`, `payload_json`, `validation_status`, `is_target_product`, `created_at`
3. `gate_evaluations`: `evaluation_id`, `gate_name`, `source_state`, `target_state`, `status` (PASSED, BLOCKED, REFINING), `schema_errors_json`, `evaluated_at`
4. `execution_runs`: `run_id`, `agent_name`, `current_state`, `mode` (MOCK, LIVE_GEMINI), `trace_logs_json`, `dissociation_passed`, `converged_at`

#### Interactive Component & State Mapping
- **BPMN Canvas Component**: Renders the 7-stage gate sequence. Clicking a gate triggers `/api/fsm/trigger-gate` with visual real-time feedback (evaluating ➔ passed/blocked).
- **Terminal Console Component**: Subscribes to execution events, rendering tabular timestamps, gate evaluation outputs, schema verification details, and color-coded system transitions.
- **Schema & Object Inspector Modal**: Allows viewing raw Pydantic-like JSON schemas, testing live payload validation against rules, and inspecting the database record.
- **Architectural Dissociation Auditor**: Visual matrix verifying that Control Plane variables and Target Product artifacts maintain 100% boundary isolation.
- **Agent Genesis Wizard**: Initiates new agent creation jobs with configurable domain goals, gate strictness, and execution mode (Deterministic Sandbox or Live Gemini).

---

### Step-by-Step Implementation Roadmap

1. **Backend Server & Database Foundation**:
   - Create `server.ts` with Express, SQLite database initialization (`agent_creator.db`), tables, seed FSM states, and in-memory cache layer.
   - Configure full CRUD and query pattern functions for FSM objects and gate definitions.
2. **Pydantic/Instructor Pattern & Gate Evaluation Engine**:
   - Implement dynamic schema validation engine (field types, mandatory properties, regex, post-determinism checks).
   - Integrate Dual Execution: Deterministic Sandbox Runner + Live Gemini API (`gemini-3.8-flash`) with structured schema response generation.
   - Implement Architectural Dissociation Validator verifying zero leakage between Control Plane and Target Product.
3. **Frontend Control Plane Interface**:
   - Build Top Bar following the 3-zone contract with brand mark, single-line navigation, and primary execution action.
   - Build Interactive BPMN Flow Observer with real-time gate nodes and clickable transition triggers.
   - Build Terminal-First Reactive Console streaming validation traces and FSM transitions.
   - Build Object & Schema Inspector allowing full CRUD, inspection, and live validation testing.
   - Build Dissociation Matrix visualizer showing the clean separation of architectures.
4. **Integration & Verification**:
   - Wire all endpoints, verify both mock and live Gemini execution paths, test gate self-correction on invalid payloads, ensure zero broken images or dead controls, and run `compile_applet`.
