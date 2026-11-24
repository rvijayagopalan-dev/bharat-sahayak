# BharatSahayak — Product & Technical Development Specification

**Document ID:** BS-DEV-SPEC-001  
**Version:** 1.0  
**Status:** Proposed development baseline  
**Repository:** `rvijayagopalan-dev/bharat-sahayak`  
**Audience:** Product, architecture, engineering, UX, data, AI, security, governance, operations and institutional stakeholders

---

## 1. Purpose

This specification defines the product, architecture, engineering, governance and delivery requirements for developing BharatSahayak from a static concept demonstrator into a modular, secure, accessible and institutionally governed national ecosystem.

BharatSahayak is a proposed federated ecosystem of specialized domain platforms called **Sahayaks**. It is intended to help citizens, communities, businesses, researchers, public institutions and service providers discover information, navigate services, collaborate and understand outcomes across domains.

The platform is a concept and development proposal. It is **not an official Government of India system**, does not represent government endorsement and must not imply access to live public-sector services or data unless a future, duly authorized institutional agreement establishes that access.

This document is a development baseline, not a statement of legal authority, institutional commitment, production readiness or government policy.

## 2. Product vision and outcomes

### 2.1 Vision

Create a trusted, interoperable and inclusive ecosystem in which specialized domain experiences can work together through shared standards, federated integration and governed intelligence—without requiring every institution to surrender ownership of its systems or data.

### 2.2 Product outcomes

1. Make relevant information and services easier to discover.
2. Support connected, multi-domain user journeys.
3. Enable institutions and approved partners to interoperate through governed interfaces.
4. Improve access to domain knowledge and evidence.
5. Support accountable AI-assisted guidance and workflow coordination.
6. Make service quality, inclusion and public outcomes measurable.
7. Provide a reusable platform foundation rather than building every domain capability independently.

### 2.3 Non-goals

The initial product is not intended to:

- Replace existing government portals, statutory authorities or institutional systems.
- Become a centralized repository of all citizen or government data.
- Make statutory, medical, financial, legal, employment or other consequential decisions autonomously.
- Issue official identity credentials, approvals, benefits or entitlements.
- Provide emergency response or defence command functionality.
- Bypass institutional authorization, procurement, security accreditation or applicable law.
- Claim real-time national coverage or impact based on illustrative demo data.

## 3. Product organization

### 3.1 Portfolio model

The portfolio is organized into seven mission clusters:

| Cluster | Domain focus | Current intended platform count |
|---|---|---:|
| Citizen & Human Development | Citizen services, health, education, skills, inclusion and legal awareness | 10 |
| Agriculture & Rural Prosperity | Agriculture, water, livestock and rural development | 4 |
| Economy, Industry & Innovation | Enterprise, trade, financial inclusion, startups and research | 5 |
| National Security & Resilience | Resilience, cyber awareness and disaster preparedness | 3 |
| Infrastructure, Environment & Mobility | Mobility, energy, environment, housing, infrastructure and urban services | 6 |
| Governance, Justice & Work | Governance, labour and civic participation | 3 |
| Culture, Tourism & Global India | Culture, tourism and diaspora engagement | 1 |
| **Portfolio target** |  | **32** |

### 3.2 Portfolio reconciliation — release blocker

The current `demo/index.html` contains **33 Sahayak records**, including both `SanskritiSahayak` and `PravasiSahayak` in the Culture & Global India cluster, while the dashboard and README describe 32 platforms and the cluster table allocates one platform to that cluster.

This discrepancy must be resolved before the next release:

- Product owner approves the canonical portfolio and cluster allocation.
- A version-controlled portfolio data file becomes the single source of truth.
- Directory cards, dashboard totals, cluster counts, search filters, documentation and tests derive from that source.
- Add a CI validation that fails when declared totals and actual records differ.
- Do not silently delete or rename a platform to make a count match; record the product decision and update all artifacts consistently.

Until resolved, treat the total as **TBD (32 target / 33 currently represented)** in implementation planning.

### 3.3 Sahayak product contract

Each Sahayak must have a standard metadata contract:

- Stable machine identifier.
- Display name and short description.
- Mission cluster and domain.
- Intended users and institutional stakeholders.
- User problems and intended outcomes.
- Capabilities and service catalogue.
- Workflows and supported journeys.
- Knowledge sources and data classifications.
- Integration dependencies and API contracts.
- Agent capabilities, if any, and their authorization boundaries.
- Human escalation and support model.
- Owner, steward, lifecycle status and version.
- Accessibility, localization, privacy and security requirements.

A Sahayak is a domain product boundary, not necessarily a separate application, database, cloud account or autonomous agent.

## 4. User groups and access model

| User group | Primary needs | Access principle |
|---|---|---|
| Citizens and families | Discover information and navigate services | Public information by default; protected services require appropriate authentication |
| Community and assisted-service workers | Help users navigate approved journeys | Delegated, scoped and auditable access |
| Businesses and employers | Discover programs, guidance and opportunities | Organization-aware access where required |
| Researchers and educators | Discover knowledge and collaboration opportunities | Source attribution, licensing and institutional permissions |
| Public officials and institutional staff | Review authorized workflows and information | Strong authentication, least privilege and institutional role controls |
| Domain administrators | Manage domain configuration and content | Segregated administrative privileges |
| Platform operators | Operate shared services and integrations | Just-in-time, audited operational access |
| Auditors and oversight roles | Review controls and evidence | Read-only, purpose-limited access |

### 4.1 Identity and authorization

- Support anonymous access to approved public information.
- Support federated identity for participating organizations where approved.
- Separate authentication from authorization.
- Apply role-based access control (RBAC), with attribute- or relationship-based controls where required.
- Represent delegated access explicitly, including the delegator, delegate, purpose, scope and expiry.
- Require step-up authentication for sensitive actions.
- Never infer identity, eligibility, consent or legal authority from conversational context.
- Provide session expiry, revocation and account recovery controls appropriate to the service.

## 5. Functional requirements

Priority definitions: **P0** release-critical; **P1** required for a usable pilot; **P2** later enhancement.

### 5.1 Experience and discovery

| ID | Requirement | Priority | Acceptance evidence |
|---|---|---|---|
| UX-001 | Provide a responsive national overview with clear ecosystem purpose and limitations. | P0 | Layout works at supported desktop, tablet and mobile breakpoints. |
| UX-002 | Provide searchable Sahayak directory with cluster filters. | P0 | Search matches names, descriptions, capabilities and domain metadata. |
| UX-003 | Provide a profile page for every approved Sahayak. | P0 | Profile displays owner, mission, users, capabilities, workflows and status. |
| UX-004 | Provide mission-cluster pages and portfolio counts. | P0 | Counts are derived from canonical data and reconcile automatically. |
| UX-005 | Provide accessible navigation, keyboard operation and visible focus. | P0 | Keyboard-only journey is testable; automated and manual accessibility checks pass. |
| UX-006 | Support Indian language localization and locale-aware content. | P1 | Language framework supports translated labels and content without layout breakage. |
| UX-007 | Support assisted-access patterns and low-bandwidth experience. | P1 | Core discovery flows remain usable on constrained connections. |

### 5.2 Connected journeys

| ID | Requirement | Priority | Acceptance evidence |
|---|---|---|---|
| JRN-001 | Define journeys as versioned workflow specifications across Sahayaks. | P0 | Journey metadata identifies stages, owners, dependencies and outcomes. |
| JRN-002 | Show participating platforms and user-visible progress. | P1 | User can identify current stage, next action and responsible institution. |
| JRN-003 | Preserve each institution's authority and system of record. | P0 | No workflow step writes to an external system without an approved integration and authorization. |
| JRN-004 | Support human review, rejection, correction and escalation. | P0 | Each consequential step has an accountable human or institution. |
| JRN-005 | Record workflow events and provenance. | P1 | Authorized reviewers can trace state transitions and source systems. |

### 5.3 Knowledge and content

| ID | Requirement | Priority | Acceptance evidence |
|---|---|---|---|
| KNO-001 | Maintain a governed content catalogue with owner, source, version and review date. | P0 | Content without provenance cannot be published as authoritative guidance. |
| KNO-002 | Support search across approved public and institutionally authorized sources. | P1 | Search results show source and freshness metadata. |
| KNO-003 | Support domain taxonomies, ontology mappings and common identifiers. | P1 | Domain terms can be mapped to shared concepts with version history. |
| KNO-004 | Support corrections, expiry, withdrawal and content review workflows. | P1 | Superseded or withdrawn content is no longer presented as current guidance. |
| KNO-005 | Apply licensing and redistribution restrictions to source content. | P0 | Restricted content is not exposed to unauthorized users or channels. |

### 5.4 AI-assisted capabilities

| ID | Requirement | Priority | Acceptance evidence |
|---|---|---|---|
| AI-001 | AI responses must distinguish sourced facts, interpretation and uncertainty. | P0 | Evaluations verify citations and uncertainty handling. |
| AI-002 | Retrieval-augmented responses must enforce source access controls. | P0 | Unauthorized source content cannot be retrieved through prompts or tools. |
| AI-003 | Agents must have explicit identity, purpose, tools, scopes and owner. | P0 | Agent registry and policy checks are mandatory before deployment. |
| AI-004 | Tool execution must be allowlisted and policy-enforced. | P0 | Unauthorized tool calls are denied and audited. |
| AI-005 | Consequential actions require explicit human authorization. | P0 | No autonomous approval, denial, entitlement determination or statutory decision. |
| AI-006 | Provide evaluation for quality, groundedness, safety, bias and robustness. | P0 | Versioned evaluation reports gate production promotion. |
| AI-007 | Provide agent observability, traceability and incident controls. | P1 | Authorized operators can inspect agent runs, tool calls and policy outcomes. |
| AI-008 | Support model and provider portability through an abstraction boundary. | P2 | Domain logic is not tightly coupled to one model provider. |

AI is an assistive capability. It must not be presented as an authority or substitute for professional, statutory or institutional judgment.

### 5.5 Command centre and outcomes

| ID | Requirement | Priority | Acceptance evidence |
|---|---|---|---|
| CMD-001 | Display clearly defined portfolio and service metrics. | P1 | Every metric has definition, owner, source, time window and freshness. |
| CMD-002 | Separate illustrative, synthetic, pilot and verified operational data. | P0 | UI visibly labels data status and never blends categories without disclosure. |
| CMD-003 | Support drill-down by mission, service, geography and time where authorized. | P2 | Access policies apply consistently to aggregate and detail views. |
| CMD-004 | Provide data-quality and metric lineage information. | P1 | Metric values can be traced to approved source records and transformations. |

## 6. Logical reference architecture

The architecture is federated and layered. It does not prescribe a single cloud vendor or mandate centralization of institutional data.

### 6.1 Layers

1. **Experience and access**
   - Responsive web and mobile experiences.
   - Assisted-service and institutional workspaces.
   - Accessibility, localization and notification preferences.

2. **Sahayak domain products**
   - Domain-specific experience, service catalogue and workflows.
   - Domain configuration and content.
   - Domain ownership, lifecycle and service-level objectives.

3. **Bharat Intelligence Fabric**
   - Common identity and trust integration.
   - Knowledge graph and ontology services.
   - Search, geospatial and policy knowledge.
   - Data exchange, workflow and outcome intelligence.

4. **AI agent and workflow mesh**
   - Agent registry and lifecycle.
   - Orchestration and workflow runtime.
   - Retrieval and tool gateways.
   - Evaluation, policy enforcement and human approval.

5. **Shared digital services**
   - Notification, document, consent or preference services where legally and operationally appropriate.
   - API and event catalogues.
   - Configuration, feature flags and service registry.

6. **Federated integration**
   - API gateway and service-to-service identity.
   - Event-driven integration and managed connectors.
   - Schema validation, rate limits, retries and dead-letter handling.

7. **Institutional systems and data owners**
   - Existing government, state, district, research, business and civil-society systems.
   - Systems of record remain under their respective owners.
   - Integrations require agreements, security review and explicit purpose.

### 6.2 Cross-cutting trust plane

Apply across all layers:

- Identity federation and access management.
- Privacy, purpose limitation and data minimization.
- Data classification, retention and residency controls.
- Encryption in transit and at rest.
- API, network and workload security.
- AI safety, model risk and agent policy.
- Audit, observability and incident response.
- Accessibility and inclusive design.
- Human accountability and independent assurance.

### 6.3 Deployment principles

- Prefer modular services with clear domain boundaries.
- Use stateless services where practical; persist state in managed, governed stores.
- Isolate environments and sensitive workloads.
- Use infrastructure as code and repeatable deployment pipelines.
- Support deployment across approved cloud, hybrid or institutional environments where justified.
- Avoid cross-domain data replication unless there is a defined purpose, authority, retention policy and owner.
- Design for graceful degradation when an external institution or connector is unavailable.

## 7. Core platform services

| Service | Responsibilities | Key controls |
|---|---|---|
| API and integration gateway | Routing, authentication enforcement, quotas and API lifecycle | mTLS where appropriate, OAuth/OIDC, schema checks, rate limits |
| Identity and access service | Federation, session, role and delegated access integration | MFA, least privilege, token audience/scope, revocation |
| Service and capability registry | Discovery of Sahayaks, APIs, agents and workflows | Ownership, version, lifecycle, approval |
| Knowledge services | Search, retrieval, ontology and graph access | Provenance, ACL filtering, freshness, licensing |
| Workflow orchestration | Long-running journeys, state transitions and human tasks | Idempotency, authorization, audit, timeout and compensation |
| Event backbone | Asynchronous domain events | Schema registry, access policy, retention, replay control |
| Agent runtime | Governed execution of agent tasks and tools | Agent identity, sandboxing, tool policy, budgets, traces |
| Observability | Logs, metrics, traces and service health | Sensitive-data redaction, access controls, retention |
| Analytics and outcomes | Aggregation and approved reporting | Metric definitions, lineage, aggregation and disclosure control |

## 8. Data architecture and governance

### 8.1 Data principles

1. Data remains with its authoritative owner wherever feasible.
2. Collect and exchange the minimum data necessary for a stated purpose.
3. Treat personal, sensitive, confidential and classified data according to applicable law and institutional policy.
4. Use synthetic or anonymized data for development and demonstrations.
5. Do not use production personal data in development or model evaluation without explicit authorization and safeguards.
6. Preserve provenance, lineage, quality and retention metadata.
7. Provide correction, deletion, archival and access-review mechanisms where applicable.
8. Define data residency and cross-border transfer requirements before selecting deployment topology.

### 8.2 Data classification

Each dataset and content source must be assigned an owner-approved classification, such as:

- Public.
- Internal.
- Confidential.
- Sensitive personal or regulated.
- Restricted or classified (handled only in separately authorized environments).

These labels are a proposed taxonomy and must be mapped to each participating institution's official classification policy. The platform must not assume that a common label automatically grants access.

### 8.3 Canonical metadata

Minimum dataset metadata:

- Dataset or source identifier and version.
- Data owner and steward.
- Description and business purpose.
- Classification and permitted use.
- Legal or institutional authority and agreement reference.
- Data subjects and sensitivity, where applicable.
- Source system and provenance.
- Schema and quality profile.
- Geographic and temporal scope.
- Retention and deletion schedule.
- Residency and transfer restrictions.
- Access policy and audit requirements.

### 8.4 Knowledge graph and ontology

- Maintain versioned domain ontologies and mappings.
- Record source and confidence for graph assertions.
- Distinguish authoritative identifiers from inferred entity matches.
- Support provenance and temporal validity.
- Require review before inferred relationships become authoritative.
- Provide APIs for controlled graph traversal and query.
- Avoid creating a universal person graph or identity resolution service without a separately approved purpose and legal basis.

## 9. API and interoperability standards

### 9.1 API design

- Use documented, versioned HTTP APIs for synchronous interactions.
- Use asynchronous events for suitable cross-domain state notifications.
- Publish machine-readable OpenAPI contracts for HTTP APIs.
- Define event schemas and compatibility rules.
- Use stable resource identifiers and explicit pagination.
- Standardize error envelopes, correlation IDs and idempotency keys.
- Define timeouts, retry policy, rate limits and service quotas.
- Use backward-compatible changes where possible; publish deprecation timelines.
- Never place secrets, access tokens or sensitive personal data in URLs.

### 9.2 Illustrative resource groups

- `/api/v1/mission-clusters`
- `/api/v1/sahayaks`
- `/api/v1/services`
- `/api/v1/journeys`
- `/api/v1/knowledge-sources`
- `/api/v1/agents`
- `/api/v1/organizations`
- `/api/v1/metrics`

These are candidate resource names, not approved production APIs. Final contracts require domain ownership, security review and versioning decisions.

### 9.3 Interoperability

Prefer open, documented standards and established protocols where suitable, including HTTP/REST, OpenAPI, OAuth 2.0, OpenID Connect, JSON Schema, CloudEvents and W3C-aligned accessibility guidance. Protocol adoption must be based on threat models, institutional compatibility and operational needs—not novelty.

## 10. AI and agent governance

### 10.1 Agent specification

Every agent must have:

- Stable agent ID and version.
- Business owner and technical owner.
- Purpose and approved use cases.
- Model/provider and configuration record.
- Input and output data classifications.
- System prompt and policy version under change control.
- Retrieval sources and source permissions.
- Tool list, schemas and authorization scopes.
- Execution environment and network egress policy.
- Human approval and escalation conditions.
- Budget, rate and runtime limits.
- Evaluation results and release approval.
- Monitoring, incident and rollback plan.

### 10.2 Agent lifecycle

1. Register proposed agent and owner.
2. Complete use-case, data and risk assessment.
3. Define tools and minimum permissions.
4. Build in isolated development environment.
5. Run functional, adversarial, privacy and security evaluations.
6. Obtain domain and AI assurance approval.
7. Deploy with monitoring and rate limits.
8. Review performance, incidents and drift.
9. Re-certify, update or retire.

### 10.3 Prohibited default behaviors

Unless separately authorized under a specific legal and institutional framework, agents must not:

- Make final statutory or eligibility determinations.
- Approve or deny benefits, loans, licenses, legal claims or medical treatment.
- Execute payments or financial transactions.
- Change official records or submit binding applications without explicit user and institutional authorization.
- Access unrelated domain data because it is technically reachable.
- Use prompt content as proof of identity, consent or authorization.
- Conceal uncertainty, fabricated sources or tool failures.
- Self-expand permissions or create unreviewed agents and tools.

### 10.4 AI evaluation

Evaluation suites must include:

- Task success and domain correctness.
- Groundedness and citation validity.
- Retrieval precision and recall.
- Hallucination and uncertainty behavior.
- Prompt injection and tool misuse resistance.
- Privacy leakage and access-control bypass attempts.
- Bias, accessibility and language performance.
- Robustness under malformed, ambiguous and adversarial inputs.
- Human escalation correctness.
- Latency, cost and resource consumption.

## 11. Security, privacy and compliance

Security and privacy requirements must be validated against applicable law, contracts, institutional policies and deployment context by qualified legal, privacy and security stakeholders. This specification does not provide a legal determination.

### 11.1 Minimum security controls

- Threat modelling for each product and integration.
- Secure software development lifecycle and peer review.
- Strong identity, MFA for privileged access and least privilege.
- Secrets management and key rotation.
- Encryption in transit and at rest.
- Network segmentation and controlled egress.
- WAF/API protection and abuse prevention as appropriate.
- Secure configuration baselines and vulnerability management.
- Dependency, container and infrastructure scanning.
- Software bill of materials (SBOM) for released artifacts.
- Centralized, tamper-resistant security audit trails.
- Backup, recovery and tested incident response.
- Independent penetration testing before production launch.

### 11.2 Privacy controls

- Purpose and lawful authority documented before personal data processing.
- Privacy impact assessment where required.
- Data minimization and privacy-by-design review.
- Clear notices and consent flows where consent is the appropriate legal basis.
- Retention and deletion schedules.
- Access, correction and grievance processes where applicable.
- Processor and subprocessor governance.
- Restrictions on secondary use and model training.
- Redaction and minimization in telemetry and support tooling.

### 11.3 Secure development environments

- Separate development, test, staging and production.
- Synthetic data by default outside production.
- No secrets in source control.
- Branch protection, code review and signed release artifacts where appropriate.
- CI checks for static analysis, dependencies, secrets, IaC and container images.
- Production access through approved, time-bound workflows.

## 12. Non-functional requirements

The values below are initial targets for engineering validation, not service-level commitments. Final SLOs must be set per service tier and institutional agreement.

| ID | Quality attribute | Initial target / requirement |
|---|---|---|
| NFR-001 | Availability | Define tiered SLOs; pilot target proposed at 99.5% monthly for critical shared discovery services, excluding agreed maintenance and external dependencies. |
| NFR-002 | Performance | Target p95 under 2.5 seconds for cached/read-only discovery APIs under agreed pilot load. |
| NFR-003 | Scalability | Stateless application tier and horizontal scaling; capacity tested against documented traffic profiles. |
| NFR-004 | Resilience | Timeouts, retries with backoff, circuit breakers and graceful degradation for remote dependencies. |
| NFR-005 | Recovery | Define RTO/RPO per data and service criticality; verify through recovery exercises. |
| NFR-006 | Accessibility | Target WCAG 2.2 AA for web experiences, subject to formal accessibility assessment. |
| NFR-007 | Localization | Unicode-first design, locale-aware dates/numbers and translation-ready content model. |
| NFR-008 | Security | Threat-modelled, least-privilege, auditable and independently tested before production. |
| NFR-009 | Privacy | Purpose limitation, data minimization, retention controls and privacy review. |
| NFR-010 | Observability | Correlated logs, metrics and traces with sensitive-data redaction. |
| NFR-011 | Portability | Infrastructure and deployment configuration expressed as code; avoid unnecessary vendor lock-in. |
| NFR-012 | Maintainability | Modular boundaries, documented contracts, automated tests and ownership metadata. |
| NFR-013 | Interoperability | Versioned APIs and event schemas with compatibility testing. |
| NFR-014 | Cost governance | Per-service budgets, usage attribution, anomaly detection and cost reporting. |

## 13. UX, accessibility and localization

- Design mobile-first and responsive layouts.
- Support keyboard-only navigation and visible focus states.
- Use semantic HTML, accessible names, headings and landmarks.
- Provide sufficient color contrast and avoid color-only status communication.
- Support screen readers, zoom and reduced-motion preferences.
- Provide clear language, explain technical terms and communicate uncertainty.
- Plan for Indian language content and translation workflows.
- Support low-bandwidth modes and graceful degradation.
- Make assisted-service flows transparent about who is acting and on whose behalf.
- Test with people representing diverse abilities, languages, devices and connectivity conditions.

## 14. Engineering standards and repository structure

### 14.1 Proposed target structure

```text
bharat-sahayak/
├── README.md
├── docs/
│   ├── DEVELOPMENT_SPEC.md
│   ├── PRODUCT_VISION.md
│   ├── ARCHITECTURE.md
│   ├── SECURITY_AND_PRIVACY.md
│   ├── DATA_GOVERNANCE.md
│   ├── AI_AGENT_GOVERNANCE.md
│   ├── API_STANDARDS.md
│   ├── ADR/
│   └── diagrams/
├── demo/
│   └── index.html
├── apps/
│   ├── web/
│   └── admin/
├── services/
│   ├── portfolio/
│   ├── journey/
│   ├── knowledge/
│   ├── identity-integration/
│   └── agent-orchestration/
├── packages/
│   ├── design-system/
│   ├── contracts/
│   ├── domain-models/
│   └── observability/
├── data/
│   ├── portfolio/
│   ├── taxonomies/
│   └── synthetic/
├── infrastructure/
│   ├── modules/
│   └── environments/
├── tests/
│   ├── contract/
│   ├── integration/
│   ├── e2e/
│   ├── security/
│   └── accessibility/
└── .github/
    └── workflows/
```

This is a target structure for staged evolution, not a requirement to create empty services immediately. Start with the smallest maintainable implementation and add modules when there is a concrete owner and use case.

### 14.2 Code quality

- Adopt a documented language and framework baseline per component.
- Enforce formatting, linting, type checks and static analysis.
- Require pull-request review and traceability to issues or requirements.
- Keep business logic out of UI rendering where practical.
- Use typed contracts and schema validation at boundaries.
- Keep configuration external to source code.
- Maintain developer setup and operational runbooks.
- Record material architectural decisions as ADRs.

### 14.3 CI/CD

Every pull request should run applicable checks:

1. Formatting and lint.
2. Type and schema validation.
3. Unit tests.
4. Contract and integration tests.
5. Dependency and license checks.
6. Secret scanning.
7. SAST and IaC scanning.
8. Accessibility checks for changed UI.
9. Build and artifact verification.
10. Portfolio data consistency checks.

Production deployment must require environment approval, immutable artifacts, change traceability, rollback capability and operational readiness review.

## 15. Testing and quality strategy

| Test level | Coverage |
|---|---|
| Unit | Domain logic, validation, authorization policy and transformations |
| Component | UI states, error states, forms and accessibility semantics |
| Contract | API schemas, event schemas and provider/consumer compatibility |
| Integration | Identity, workflow, search, knowledge and approved connectors |
| End-to-end | Directory discovery, profile exploration and approved user journeys |
| Security | Authentication, authorization, injection, SSRF, secrets, dependency and access-boundary tests |
| AI evaluation | Groundedness, safety, retrieval permissions, prompt injection and tool policy |
| Performance | Load, stress, endurance and dependency degradation |
| Resilience | Retry, timeout, failover, backup and restore |
| Accessibility | Automated checks plus manual assistive-technology testing |
| Data quality | Schema, provenance, freshness, classification and portfolio reconciliation |

### 15.1 Release acceptance baseline

A release candidate is acceptable only when:

- All P0 requirements for the release are met.
- No unresolved critical or high-severity security finding remains without formally approved risk treatment.
- All required tests pass and failures are triaged.
- Data and content provenance are visible where relevant.
- Authorization tests demonstrate tenant, role and source-level isolation.
- AI evaluation gates pass for the approved use case.
- Accessibility findings are reviewed and blocking issues remediated.
- Monitoring, support ownership, rollback and incident runbooks are ready.
- Product, domain, security and operational owners approve release.

## 16. Delivery roadmap

### Phase 0 — Product and portfolio baseline

- Resolve the 32-versus-33 portfolio discrepancy.
- Approve product taxonomy, Sahayak metadata and ownership model.
- Define target user journeys and pilot selection criteria.
- Establish threat model, data classification and governance principles.
- Create ADR process and engineering conventions.

**Exit:** Approved portfolio baseline, product scope, architecture decisions and prioritized backlog.

### Phase 1 — Foundation and demonstrator hardening

- Move portfolio data into a canonical structured source.
- Generate directory, clusters and counts from the source.
- Improve responsive UX, accessibility and localization readiness.
- Add automated validation and CI.
- Add profile metadata, content provenance fields and error states.

**Exit:** Consistent, tested and maintainable portfolio demonstrator.

### Phase 2 — Pilot-ready platform foundation

- Implement identity integration and authorization boundaries.
- Implement service catalogue and versioned API contracts.
- Implement governed knowledge ingestion and search.
- Implement workflow state and human task patterns.
- Implement audit, logs, metrics and traces.
- Establish security, privacy and operational readiness reviews.

**Exit:** A non-production pilot foundation using synthetic or explicitly approved data.

### Phase 3 — Controlled domain pilots

- Select a small number of Sahayaks with accountable institutional sponsors.
- Deliver a limited set of measurable, low-risk journeys.
- Integrate only approved systems and datasets.
- Evaluate usability, inclusion, reliability, safety and outcomes.
- Complete independent security and privacy assessments.

**Exit:** Pilot evaluation, risk register, evidence and go/no-go recommendation.

### Phase 4 — Federated expansion

- Expand to additional mission clusters based on evidence and sponsorship.
- Add governed agent capabilities where they demonstrably improve outcomes.
- Introduce cross-domain outcome reporting with lineage and access controls.
- Improve platform engineering, SRE, FinOps and partner onboarding.

**Exit:** Approved expansion plan with funding, ownership, controls and measurable service outcomes.

## 17. Product and operational metrics

Metrics must have a definition, owner, source, collection method, reporting cadence and limitations.

Potential measures include:

- Service discovery completion rate.
- Journey completion and abandonment rate.
- Time to find relevant information.
- Content freshness and source coverage.
- Accessibility task completion.
- Search relevance and grounded answer rate.
- Human escalation and correction rate.
- API availability and latency.
- Integration failure and recovery rate.
- Security and privacy incident trends.
- Cost per completed journey.
- User-reported usefulness and trust.

Do not equate platform registrations, page views, agent calls or generated answers with public impact. Impact claims require a defensible methodology and appropriate evaluation.

## 18. Key risks and mitigations

| Risk | Potential impact | Mitigation |
|---|---|---|
| Unclear institutional ownership | Unusable integrations and unaccountable service | Require named sponsor, owner, steward and agreement for each pilot |
| Centralization pressure | Privacy, sovereignty and adoption concerns | Federated data ownership and purpose-bound exchange |
| Inaccurate AI guidance | User harm and loss of trust | Grounding, evaluation, disclaimers, escalation and human review |
| Inconsistent portfolio definitions | Confusing UX and unreliable reporting | Canonical portfolio registry and CI count validation |
| Unauthorized data access | Privacy and security incidents | Source-level authorization, least privilege and adversarial testing |
| Legacy system dependency | Fragile journeys | Versioned adapters, resilience patterns and graceful degradation |
| Digital exclusion | Unequal access | Accessibility, language, assisted access and low-bandwidth design |
| Metric misuse | Misleading impact claims | Metric governance, lineage and independent evaluation |
| Vendor lock-in | Cost and portability constraints | Open contracts, abstraction and exit planning |
| Scope expansion | Delivery delays and weak quality | Phase gates, explicit non-goals and outcome-based prioritization |

## 19. Decisions required before implementation

The product and architecture owners must record decisions for:

1. Canonical list and count of Sahayaks, including the current 32/33 discrepancy.
2. Pilot mission clusters, journeys and institutional sponsors.
3. Legal and operating entity, product ownership and accountability.
4. Hosting model, data residency and institutional deployment constraints.
5. Identity federation and delegated access model.
6. Data-sharing, consent, retention and grievance processes.
7. Approved AI use cases, model providers and risk classification.
8. Service tiers, SLOs, RTO and RPO.
9. Languages, accessibility research and assisted-service model.
10. Funding, support, incident response and long-term operating model.
11. Open-source or proprietary licensing and contribution policy.

Record each decision in `docs/ADR/` with context, options, decision, consequences, owner and date.

## 20. Definition of Done

A feature is complete when:

- Its user problem, owner and acceptance criteria are documented.
- UX and content meet accessibility and localization requirements for the release.
- API and data contracts are versioned and reviewed.
- Authorization and privacy implications are assessed.
- Unit, integration and relevant end-to-end tests pass.
- Observability and failure behavior are implemented.
- Documentation and operational ownership are updated.
- Security and AI assurance requirements are satisfied where applicable.
- Product owner accepts the behavior against the stated criteria.

A platform is not production-ready merely because its UI or AI demonstration works. Production readiness requires institutional authority, approved data access, security and privacy assurance, operational ownership and evidence from testing.

---

## Appendix A — Current V1 demonstrator baseline

The repository's current V1 is a standalone HTML concept demonstrator in `demo/index.html`. It currently includes:

- National overview dashboard.
- Sahayak directory with search and mission-cluster filter.
- Mission cluster explorer.
- Sahayak profile modal.
- Six illustrative cross-platform journeys.
- Bharat Intelligence Fabric capability cards.
- AI Agent Mesh concept cards.
- National Impact Command Centre placeholders.
- Layered reference architecture.
- Roadmap and governance concepts.
- Responsive CSS and client-side JavaScript.

The V1 is static and illustrative. It does not implement production authentication, APIs, persistence, live integrations, operational agent execution, verified impact analytics or institutional workflows.

## Appendix B — Glossary

| Term | Definition |
|---|---|
| Sahayak | A specialized domain platform within the BharatSahayak portfolio |
| Mission cluster | A grouping of Sahayaks around a broad domain or public outcome |
| Bharat Intelligence Fabric | Shared governed knowledge, semantic, data and intelligence capabilities |
| AI Agent Mesh | Governed discovery and orchestration of specialized AI agents |
| Connected journey | A user-centered workflow spanning one or more Sahayak platforms |
| Federated integration | Controlled interaction among systems that retain separate ownership |
| System of record | Authoritative source responsible for maintaining a particular record |
| Data steward | Accountable role for data definitions, quality, access and lifecycle |
| ADR | Architecture Decision Record |
| SLO | Service Level Objective |
| RTO / RPO | Recovery Time Objective / Recovery Point Objective |

---

**Document control:** This specification should be reviewed at each major product or architecture milestone. Changes to scope, risk, standards or requirements must be versioned and approved by the relevant owners.
