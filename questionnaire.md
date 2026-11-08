# LLM gateway security and procurement questionnaire

44 questions in 12 sections. Each question has an ID you can reference in tickets and contract redlines. The same content is in [`questionnaire.csv`](questionnaire.csv) with empty columns for vendor answers and scoring.

Scoring suggestion: 2 = good answer with evidence, 1 = partial or unverified, 0 = no answer or red flag. Decide which questions are must-pass for your use case before you send the questionnaire, not after.

## Sections

- [DR: Data residency and regional processing](#dr-data-residency-and-regional-processing) (4)
- [RT: Retention and zero data retention](#rt-retention-and-zero-data-retention) (4)
- [TR: Training and secondary use](#tr-training-and-secondary-use) (3)
- [SP: Sub-processors](#sp-sub-processors) (3)
- [ID: Identity: SSO and SCIM](#id-identity-sso-and-scim) (4)
- [AU: Audit logs and request records](#au-audit-logs-and-request-records) (4)
- [SC: Spend controls](#sc-spend-controls) (3)
- [GV: Model and provider governance](#gv-model-and-provider-governance) (4)
- [IN: Incidents, availability and assurance](#in-incidents-availability-and-assurance) (4)
- [AI: EU AI Act deployer support](#ai-eu-ai-act-deployer-support) (4)
- [EX: Exit and portability](#ex-exit-and-portability) (4)
- [CT: Contract and DPA](#ct-contract-and-dpa) (3)

## DR: Data residency and regional processing

### DR-01. Where are prompts and completions processed (inference), and can processing be restricted to a named region such as the EU/EEA?

**Why it matters.** Under GDPR and many sector rules, the location of processing matters as much as the location of storage. A gateway can be hosted in one region and still forward prompts to model endpoints anywhere.

**Good answer.** Names the regions or countries for each hop (ingress, gateway, inference). Offers a per-workspace or per-key rule that pins inference to approved endpoints, and refuses the request when no compliant endpoint is available.

**Red flags.** "Data is stored in the EU" with nothing said about inference. A region setting that silently falls back to another region on errors or capacity limits.

**Evidence to request.** Architecture or data-flow diagram; region list per model; documentation of fallback behavior.

### DR-02. How does the vendor define the region? For example, does "Europe" mean EU/EEA only, or does it also include the UK, Switzerland or other countries?

**Why it matters.** "Europe" and "EU" are not the same thing legally. Your transfer assessment depends on the exact list of countries.

**Good answer.** An explicit list of countries or cloud regions, and a statement on whether that list differs per model or provider.

**Red flags.** Marketing terms ("European", "sovereign") with no country list.

**Evidence to request.** Written definition in the DPA or docs.

### DR-03. Do retries, fallbacks, classifiers, guardrails, caching and logging stay inside the same region rule as the main request?

**Why it matters.** Secondary calls (routing classifiers, moderation, embeddings for caching, observability exports) are where residency rules usually leak.

**Good answer.** Yes, with each auxiliary call named and covered by the same rule, or documented as content-free.

**Red flags.** The region rule applies "to the model call" only. Guardrail or moderation services run in a different region.

**Evidence to request.** List of auxiliary services that receive content, with their locations.

### DR-04. Where is account, billing, usage and log metadata stored, and does any of it leave the region?

**Why it matters.** Metadata such as user IDs, IP addresses and request logs can be personal data even when no prompt content is stored.

**Good answer.** Named storage locations for each data category, and a clear statement of which categories leave the region.

**Red flags.** Only the content path is described. Metadata location "may vary".

**Evidence to request.** Data inventory or records-of-processing extract.

## RT: Retention and zero data retention

### RT-01. Does the gateway itself store prompts or completions, for how long, and can storage be switched off?

**Why it matters.** Gateway logs are often the largest copy of your data. Many gateways log full payloads by default for debugging and analytics.

**Good answer.** Content logging is off by default, or can be switched off at the organization level. Retention periods are stated per data type.

**Red flags.** Full payload logging that cannot be disabled, or retention described as "as long as necessary".

**Evidence to request.** Retention schedule; screenshot or doc of the logging setting.

### RT-02. Can you require zero data retention (ZDR) from downstream model providers, and how is it enforced?

**Why it matters.** Using a gateway with no retention means little if the model provider behind it keeps prompts for 30 days for abuse monitoring.

**Good answer.** A ZDR requirement that can be set per organization, team or key, that lower levels cannot weaken, and that excludes non-ZDR providers from routing rather than just warning.

**Red flags.** ZDR offered only "on request" with no way to verify it applies. ZDR that is a label on providers rather than a routing constraint.

**Evidence to request.** Description of how the setting changes routing; list of providers that qualify.

### RT-03. What exactly does the provider's ZDR commitment cover (abuse monitoring, caching, safety classifiers, human review)?

**Why it matters.** "Zero retention" ranges from "no storage at all" to "no storage beyond 30 days except for abuse review".

**Good answer.** A precise definition, including transient in-memory caches and any exceptions for legal holds or abuse investigation.

**Red flags.** Undefined ZDR. Exceptions that are broad or discretionary.

**Evidence to request.** The contract clause or policy text.

### RT-04. What happens to your data at contract end, and how quickly is it deleted?

**Why it matters.** Deletion is a GDPR obligation for processors and a common audit finding.

**Good answer.** A stated deletion period (for example 30 days) for all copies, including backups, and a deletion confirmation on request.

**Red flags.** No stated period, or backups excluded without a time limit.

**Evidence to request.** DPA deletion clause.

## TR: Training and secondary use

### TR-01. Does the vendor use your prompts, completions or files to train or improve models, and is that the default?

**Why it matters.** Training use is the question most boards and works councils ask first.

**Good answer.** A contractual "no training" commitment that applies by default on business plans, without an opt-out step.

**Red flags.** Opt-out only. Training exclusion that applies to some products and not others under the same account.

**Evidence to request.** Contract or DPA clause, not only a FAQ.

### TR-02. Does the vendor require its sub-processors and downstream model providers not to train on your data, and does routing enforce that?

**Why it matters.** A gateway's own no-training promise does not bind the model providers it forwards to unless the gateway filters or contracts for it.

**Good answer.** Routing only to providers that commit not to train, either always or when a stated setting is on.

**Red flags.** "We don't train" with silence about downstream providers.

**Evidence to request.** Provider filtering documentation; flow-down clause.

### TR-03. Is any of your data used for analytics, benchmarking, product improvement or human review?

**Why it matters.** Secondary use other than training can still be incompatible with your purpose limitation.

**Good answer.** Only aggregated, content-free usage metrics are used, and human review of content happens only with your consent or for a narrowly defined abuse case.

**Red flags.** Broad "improve our services" language covering content.

**Evidence to request.** Privacy policy and DPA purpose clause.

## SP: Sub-processors

### SP-01. Is there a public, current list of sub-processors with purpose, data categories and location?

**Why it matters.** GDPR Art. 28 requires you to authorize sub-processors. With a gateway, the model providers themselves are usually sub-processors.

**Good answer.** A public page listing every sub-processor, including each model or inference provider, with purpose, data and location.

**Red flags.** List available only under NDA, or model providers missing from the list.

**Evidence to request.** URL of the list and its last-updated date.

### SP-02. How much advance notice do you get before a new sub-processor is added, and can you object?

**Why it matters.** Without notice, a new model provider can start receiving your data before you have assessed it.

**Good answer.** Written advance notice (commonly 14 to 30 days), a subscription mechanism, and a right to object or terminate.

**Red flags.** "We may update this list from time to time." No notice mechanism.

**Evidence to request.** DPA sub-processor clause.

### SP-03. When the gateway adds a new model provider, does your traffic start reaching it automatically?

**Why it matters.** This is the gateway-specific version of the sub-processor question: routing changes can add a processor in practice before any paperwork.

**Good answer.** New providers are never added to your routing without an admin action, or you can pin an explicit allow-list.

**Red flags.** Automatic routing to new providers for "better price or uptime" with no way to opt out.

**Evidence to request.** Routing and allow-list documentation.

## ID: Identity: SSO and SCIM

### ID-01. Which SSO protocols are supported (SAML, OIDC), with which identity providers, and on which plan?

**Why it matters.** SSO is how you enforce MFA, conditional access and joiner/leaver processes.

**Good answer.** SAML and/or OIDC with your IdP (for example Microsoft Entra ID, Okta, Google), available on the plan you are buying.

**Red flags.** SSO only on a much higher tier than the rest of the features you need.

**Evidence to request.** Setup guide for your IdP.

### ID-02. Can SSO be enforced, so password and social logins are disabled for your domain?

**Why it matters.** Optional SSO leaves a bypass: a leaver can keep a password login.

**Good answer.** Enforced SSO per domain, with a documented break-glass admin process.

**Red flags.** SSO available but not enforceable.

**Evidence to request.** Admin setting documentation.

### ID-03. Is SCIM provisioning supported, and does deprovisioning in the IdP revoke API keys and sessions?

**Why it matters.** API keys usually outlive the user session. Removing a person in the IdP should stop their keys too.

**Good answer.** SCIM for users and groups, with documented behavior for keys and active sessions on deprovisioning.

**Red flags.** No SCIM, or SCIM that removes the user but leaves their keys working.

**Evidence to request.** SCIM docs; deprovisioning behavior description.

### ID-04. Can access to AI tools (chat apps, coding agents) follow IdP groups rather than shared API keys?

**Why it matters.** Shared keys make attribution, offboarding and least privilege hard.

**Good answer.** Per-person identity or per-person keys mapped to IdP groups.

**Red flags.** One organization-wide key handed to everyone.

**Evidence to request.** Docs for tool sign-in or key-per-user.

## AU: Audit logs and request records

### AU-01. Is there an admin audit log of configuration changes (people, keys, budgets, policies), with before and after values?

**Why it matters.** Auditors will ask who changed a policy and when.

**Good answer.** An immutable or append-only admin log with actor, timestamp, target and old/new values, exportable.

**Red flags.** No admin log, or a log that records only that "settings changed".

**Evidence to request.** Sample export.

### AU-02. Is there a per-request record (model, serving provider, region, outcome, fallbacks) and can it be exported?

**Why it matters.** To prove where data went, you need to know which provider actually served each request, not just which model was requested.

**Good answer.** Per-request metadata including the actual serving provider and any fallbacks, exportable by CSV or API.

**Red flags.** Only aggregated dashboards. Requested model shown but serving provider hidden.

**Evidence to request.** Sample export; API docs.

### AU-03. How long are audit and request records kept, and can you choose a period?

**Why it matters.** Retention for audit records often has to match your own policy (for example 12 months). If you deploy a high-risk AI system, Art. 26(6) of the EU AI Act requires you to keep the logs it automatically generates, to the extent they are under your control, for at least six months, unless applicable Union or national law (in particular data protection law) provides otherwise.

**Good answer.** A stated retention period, configurable or at least long enough for your policy, with export before deletion.

**Red flags.** Unstated retention, or retention so short it cannot support an investigation.

**Evidence to request.** Retention statement.

### AU-04. Do audit records contain prompt content? If so, who can see them?

**Why it matters.** Logs that hold content become a sensitive data store of their own.

**Good answer.** Metadata-only by default, with content logging opt-in and access-controlled.

**Red flags.** Content in logs by default, visible to all admins.

**Evidence to request.** Log schema.

## SC: Spend controls

### SC-01. Can you set hard budgets per key, per user, per team and per organization?

**Why it matters.** Agentic workloads can spend a month's budget in hours. Alerts alone do not stop that.

**Good answer.** Hard limits that block or degrade at the cap, at each level you need, with alerts before the cap.

**Red flags.** Alerts only, or limits that are "best effort" and can overshoot.

**Evidence to request.** Docs for budget settings and enforcement behavior.

### SC-02. What happens when a budget is reached: hard stop, overage, or fallback to a cheaper model?

**Why it matters.** Unclear cap behavior causes either surprise bills or surprise outages.

**Good answer.** Documented behavior per setting, including the error returned to applications.

**Red flags.** Silent overage billed later.

**Evidence to request.** Docs or contract term on overage.

### SC-03. Can spend be attributed to a person, app, team, project or cost code for chargeback?

**Why it matters.** Finance teams need allocation, not just a total.

**Good answer.** Usage reports or exports broken down by key, user, team and a custom tag.

**Red flags.** Totals only.

**Evidence to request.** Sample usage export.

## GV: Model and provider governance

### GV-01. Can you restrict which models each team, key or app may use?

**Why it matters.** Approved-model lists are a basic AI governance control and often a requirement of internal AI policies.

**Good answer.** Model allow-lists at organization, team and key level, enforced at request time.

**Red flags.** Restrictions only in the UI, not enforced on the API.

**Evidence to request.** Docs for model restrictions.

### GV-02. Can you restrict which inference providers (clouds, hosts) may serve your traffic, and does the restriction also bind fallbacks?

**Why it matters.** The same open model can be served by many hosts with very different terms and locations.

**Good answer.** Provider allow-lists that fail closed (an empty list blocks everything) and apply to every retry and fallback.

**Red flags.** Fallback logic that ignores the allow-list "for reliability".

**Evidence to request.** Docs for provider allow-lists and fallback behavior.

### GV-03. Can lower levels (team, key) only narrow, never widen, the organization's policy?

**Why it matters.** Delegated administration should not let a team override company policy.

**Good answer.** Policies combine by intersection down the hierarchy.

**Red flags.** Team admins can override organization settings.

**Evidence to request.** Policy inheritance documentation.

### GV-04. Are guardrails available (PII redaction, content filters, prompt-injection checks), and where do they run?

**Why it matters.** Guardrails are useful but are themselves processors of your content.

**Good answer.** Optional guardrails with stated location and retention, configurable per team or key.

**Red flags.** Mandatory third-party guardrails with no stated location.

**Evidence to request.** Guardrail docs and data flow.

## IN: Incidents, availability and assurance

### IN-01. What is the contractual breach notification window?

**Why it matters.** GDPR gives controllers 72 hours to notify the authority, so your processor must tell you sooner or at least without undue delay.

**Good answer.** A fixed window (for example 24, 48 or 72 hours) in the DPA, with content of the notice described.

**Red flags.** "Without undue delay" only, or notification only for "confirmed" breaches with no time limit.

**Evidence to request.** DPA incident clause.

### IN-02. Is there a public status page and incident history, and an uptime SLA with credits?

**Why it matters.** Gateways sit in the critical path of every AI feature.

**Good answer.** Public status page, published post-mortems for major incidents, SLA with defined credits on the plan you buy.

**Red flags.** No status page, or SLA only for the top tier with no credits.

**Evidence to request.** Status page URL; SLA document.

### IN-03. How does failover work when a model provider is down, and does it respect your region and provider rules?

**Why it matters.** Failover that ignores policy turns an outage into a compliance incident.

**Good answer.** Automatic failover only among providers that meet your rules; otherwise a clear error.

**Red flags.** Failover to any available provider.

**Evidence to request.** Failover documentation.

### IN-04. Which independent assurance reports or certifications cover the service in scope (for example SOC 2 Type II, ISO/IEC 27001, ISO/IEC 42001)?

**Why it matters.** Certifications of the underlying cloud do not cover the vendor's own operations.

**Good answer.** Reports or certificates that name the service you are buying, with the scope and date, available under NDA if needed.

**Red flags.** Pointing to the cloud provider's certificates as if they were the vendor's.

**Evidence to request.** Report or certificate, scope statement, bridge letter.

## AI: EU AI Act deployer support

### AI-01. Can the service help you keep the logs a deployer of a high-risk AI system must keep (Art. 26(6): automatically generated logs under your control, kept for at least six months unless applicable Union or national law provides otherwise)?

**Why it matters.** If you deploy a high-risk system, keeping its automatically generated logs is your obligation, to the extent those logs are under your control. The six-month minimum applies unless applicable Union or national law, in particular on personal data protection, sets a different period. Financial institutions keep these logs as part of their documentation under Union financial services law. Your gateway is often where those logs are produced.

**Good answer.** Exportable request records with a retention period you can set to meet your policy.

**Red flags.** No export, or logs deleted after a few days.

**Evidence to request.** Log retention and export docs.

### AI-02. Does the vendor document which models it serves, who provides them, and links to provider documentation (model cards, usage policies)?

**Why it matters.** Deployers need to know which general-purpose AI model is in use and its provider's instructions for use.

**Good answer.** A model catalog naming the provider and version for each model, and linking to provider documentation.

**Red flags.** Opaque model aliases with no way to tell which underlying model or version served a request.

**Evidence to request.** Model catalog; per-request model/version field.

### AI-03. Can the service support transparency duties, for example by preserving provider watermarks or marking AI-generated output (Art. 50)?

**Why it matters.** Art. 50 splits the duties. Art. 50(2) puts the machine-readable marking duty on providers of AI systems that generate synthetic audio, image, video or text. Deployers have separate disclosure duties, for example Art. 50(4) for deep fakes. Art. 50 applies from 2 August 2026. Under Art. 111(4), providers of in-scope systems placed on the market before 2 August 2026 must comply with Art. 50(2) by 2 December 2026. A gateway is usually neither the marking provider nor the disclosing deployer, but it must not strip the provider's marking.

**Good answer.** Clear statement of whether the gateway modifies outputs, and how provider watermarks or metadata are passed through.

**Red flags.** Undocumented output rewriting.

**Evidence to request.** Docs on output handling.

### AI-04. Does the vendor provide AI literacy material or usage policy templates for your staff (Art. 4)?

**Why it matters.** AI literacy obligations already apply to deployers since 2 February 2025.

**Good answer.** Guidance or materials you can reuse, or at least clear acceptable-use documentation.

**Red flags.** None. (Not a deal-breaker on its own, but it shifts the work to you.)

**Evidence to request.** Links to materials.

## EX: Exit and portability

### EX-01. Is the API compatible with a widely used interface (for example the OpenAI or Anthropic API format), so you can switch vendors by changing a base URL?

**Why it matters.** Compatibility is the cheapest exit plan.

**Good answer.** Documented compatibility with a common API format, with known differences listed.

**Red flags.** A proprietary SDK required for basic calls.

**Evidence to request.** API reference.

### EX-02. Can you export your configuration (keys, policies, prompts, routing rules) and your logs in a standard format?

**Why it matters.** Without export, the cost of switching includes rebuilding all governance settings.

**Good answer.** Export of config and logs via API or file in JSON/CSV.

**Red flags.** Export only by support ticket, or not at all.

**Evidence to request.** Export docs.

### EX-03. Is there a self-hosted or open-source option, or a documented path to run the same setup elsewhere?

**Why it matters.** Some regulated buyers need the option to bring the gateway in-house.

**Good answer.** Open-source core or self-hosted edition, or a clear migration guide.

**Red flags.** None, and long minimum terms.

**Evidence to request.** Repository or deployment docs.

### EX-04. What are the termination terms: notice, data return, deletion, and any fees?

**Why it matters.** Exit terms are cheaper to negotiate before signature than after.

**Good answer.** Data return on request, deletion within a stated period, no exit fees.

**Red flags.** Auto-renewal with long notice, or fees to export data.

**Evidence to request.** Contract termination clause.

## CT: Contract and DPA

### CT-01. Is a Data Processing Agreement available, and can it be signed without a custom negotiation?

**Why it matters.** No DPA means you cannot lawfully use a processor for personal data under GDPR.

**Good answer.** A published DPA you can review in advance and sign on the plan you buy.

**Red flags.** DPA only on the top tier, or only on request after purchase.

**Evidence to request.** DPA URL.

### CT-02. Which transfer mechanisms cover transfers outside the EU/EEA (SCCs, UK IDTA, EU-US Data Privacy Framework)?

**Why it matters.** Even with regional processing, support, metadata or sub-processors may involve transfers.

**Good answer.** Named mechanisms per transfer, included in the DPA.

**Red flags.** No mention of transfers.

**Evidence to request.** DPA transfer clause.

### CT-03. Which law governs the contract, and where are disputes resolved?

**Why it matters.** Governing law affects enforceability and your legal team's review effort.

**Good answer.** A jurisdiction your legal team accepts, stated up front.

**Red flags.** Unstated, or changes by plan without notice.

**Evidence to request.** Terms of service.

## Legal references

- GDPR Art. 28 (processors), Art. 33 (breach notification), Chapter V (transfers): https://eur-lex.europa.eu/eli/reg/2016/679/oj
- EU AI Act, Regulation (EU) 2024/1689, including Art. 4 (AI literacy), Art. 26 (deployer obligations), Art. 50 (transparency) and Art. 113 (dates of application): https://eur-lex.europa.eu/eli/reg/2024/1689/oj

This questionnaire is not legal advice. Check obligations and dates with your counsel; the AI Act timeline in particular may be amended.
