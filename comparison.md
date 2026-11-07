# How vendors answer publicly

**Checked: 2026-11-07.** Each cell summarizes what the vendor says on its **own public pages** (docs, trust center, DPA, terms, pricing, changelog), linked in the Source column. No third-party sources are used. "Not published" means we could not find the answer on the vendor's own public pages on that date. It does not mean the vendor lacks the capability: ask them, and if they publish it, send a correction (see [CONTRIBUTING.md](CONTRIBUTING.md)).

Where a page existed but could not be read (for example a trust center that renders only with JavaScript or failed with a certificate error), the cell says so.

This is a snapshot, not a recommendation. Vendors change plans, terms and features often. Always confirm against the current version of the linked page and your contract before relying on a cell.

**Conflict of interest:** this repository is maintained by the Standard Compute team. Standard Compute's row was written from its own public wording, using the same rules as every other row. If you find a cell for any vendor, including ours, that overstates or understates what the source says, please open an issue.

Vendors, in the order below: [Standard Compute](#standard-compute) · [OpenRouter](#openrouter) · [Portkey](#portkey) · [LiteLLM](#litellm) · [Azure OpenAI](#azure-openai-microsoft-foundry) · [Amazon Bedrock](#amazon-bedrock) · [Claude Enterprise](#claude-enterprise) · [Cloudflare AI Gateway](#cloudflare-ai-gateway)

## Summary

Short form of the per-vendor tables below. "NP" = Not published. Plan restrictions are in the detailed tables.

| Topic | Standard Compute | OpenRouter | Portkey | LiteLLM | Azure OpenAI | Amazon Bedrock | Claude Enterprise | Cloudflare AI Gateway |
|---|---|---|---|---|---|---|---|---|
| Regional inference option | Europe rule | EU and US in-region | Region of choice (no list) | Where you deploy | Data Zone EU, regional | Geographic inference profiles (EU, US, APAC) | US-only option; no EU option stated | Not compatible with Regional Services |
| ZDR / no content retention | Yes, per company/team/key | Yes, all plans | Logging off per request or org; no-body storage on request | Message logging off switch (self-hosted) | Modified abuse monitoring (eligibility required) | `data_retention_mode: none`, model exceptions | Claude Code only, separate enablement | Logging off; ZDR for Unified Billing only |
| No training by vendor | Yes | Yes | NP | NP | Yes | Yes | Yes (commercial default) | Yes |
| Public sub-processor list | Yes, 14 days' notice | Yes, 30 days (model providers excluded) | Exists, not readable; notice NP | NP | Yes, 30 days to 6 months | Yes, 30 days | Yes, "reasonable notice" | Yes, 30 days |
| SSO | SAML incl. Entra ID | SAML (Enterprise) | SAML, OIDC (Enterprise) | SAML, OIDC (Enterprise; free up to 5 users) | Entra ID | IAM Identity Center | SAML, OIDC, require SSO | All plans |
| SCIM | From Entra (Claude Desktop/Code sign-in) | Enterprise | Yes (plan NP) | Enterprise | NP | Via IAM Identity Center | Yes | Enterprise |
| Admin audit log | Yes, before/after values | SCIM mappings only | Enterprise | Enterprise | Diagnostic logs | CloudTrail | 180-day export; Compliance API | 18 months |
| Per-request records | Exportable, 12 months | API; retention NP | Yes; retention by plan | Spend logs (self-hosted) | Diagnostic logs | Invocation logging (opt-in) | Compliance API | Gateway logs, capped by plan |
| Hard budgets | Per key and company | Per member and key | Enterprise and select Pro | Per key, user, team | Token quotas; cost budgets alert only | Token quotas; hard spend cap NP | Org, group, user | Spend limit rules per gateway |
| Model allow-list | Per key | Guardrails | Per integration, guardrail | Per key, team, user | Azure Policy | IAM / SCP | Org-wide on/off, roles | Per-request headers, aliases |
| Provider allow-list | Company/team/key, fail-closed | Guardrails | Enterprise | NP | n/a (single provider) | n/a (single provider) | n/a (single provider) | Per-request headers |
| Breach notice window | 72 hours | 72 hours | NP | NP | 72 hours | Without undue delay | 48 hours | Without undue delay |
| EU AI Act deployer feature | NP | NP (guidance only) | NP (blog only) | Art. 5 guardrail template | Trust Center page, AI literacy guide | NP in docs (blog only) | Art. 50 page only | NP for AI Gateway |
| Self-host / open source | NP | NP | Open-source gateway | Open source | No | No | No | No |
| Certifications stated | In progress (see table) | SOC 2 Type II | ISO 27001, SOC 2 | SOC 2 Type II | Azure ISO 27001, SOC 2 (service scope in STP) | SOC (Bedrock in scope), ISO | ISO 27001, ISO 42001, SOC 2 | SOC 2 Type II, ISO 27001 |
| Public DPA | Yes, sign in dashboard | Yes | Page exists, not readable | NP | Yes | Yes | Yes | Yes |

---

## Standard Compute

Managed LLM gateway (frontier and open models). Row written by the maintainer from Standard Compute's public wording; verify against the linked pages.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | "Set a Europe rule for your company, a team or a single key, and every request, including retries and fallbacks, is served only by approved European inference endpoints. If no European endpoint can serve it, the request is refused before your prompt is sent." EU gateway terminates TLS and runs in Finland; account data stored in Frankfurt. Country list for "Europe": Not published. | https://standardcompute.com/security |
| Retention / ZDR | Zero data retention can be required for a company, team or key; requests are then routed only to inference endpoints that commit to keeping no copy, and lower levels cannot switch it off. States that prompts are processed in memory and never written to storage or logs. | https://standardcompute.com/security |
| Training use | Does not train on prompts or outputs. With a region rule or ZDR on, requests go only to providers that commit not to train on them. | https://standardcompute.com/dpa |
| Sub-processors | Public list with purpose, data and location; 14 days' notice before adding one. | https://standardcompute.com/sub-processors |
| SSO | SAML SSO, including Microsoft Entra ID, for the dashboard; users on a verified domain join the company automatically. Enforced SSO: Not published. | https://standardcompute.com/pricing |
| SCIM | Employees can sign in to Claude Desktop and Claude Code with a Microsoft work account through the EU gateway; access follows Entra groups through SCIM provisioning. | https://standardcompute.com/pricing |
| Audit logs | Admin changes recorded with before and after values. Per-request record (model, serving provider, region rule) exportable, kept for 12 months. Request records hold metadata only. | https://standardcompute.com/security · https://standardcompute.com/pricing |
| Spend controls | Fixed monthly budget per person or app that does not overrun; spending caps per key and per company; optional top-off from a prepaid company balance. Team-level budgets: Not published. | https://standardcompute.com/pricing |
| Model / provider allow-lists | Model selection per key. Provider allow-lists for company, team or key; lower levels can only narrow; new providers are not added without admin approval; fallbacks cannot route around the list. | https://standardcompute.com/security |
| Breach notification | 72 hours (DPA). | https://standardcompute.com/dpa |
| EU AI Act deployer support | Not published as a dedicated feature (see audit log row for request records). | https://standardcompute.com/security |
| Exit / portability | Request records exportable. Claude Code and Claude Desktop can be pointed at the gateway. Self-hosted option: Not published. | https://standardcompute.com/security |
| Certifications | No certificate or report published. States its security program is built on ISO 27001:2022 controls with certification in progress, and that its infrastructure providers hold ISO 27001 and SOC 2. | https://standardcompute.com/security |
| DPA | Public text; signable in the dashboard. Covers no training, no content retention and 72-hour breach notice. | https://standardcompute.com/dpa |

## OpenRouter

Managed LLM router/gateway.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | EU and US in-region routing: requests to `eu.openrouter.ai` or `us.openrouter.ai` have prompts and completions processed within that region. Business or Enterprise plan. DPA EU addendum: EU API payloads go only to EU model providers and are not transferred outside the EU/EEA. | https://openrouter.ai/docs/features/privacy-and-logging · https://openrouter.ai/pricing · https://openrouter.ai/assets/data-processing-agreement.pdf |
| Retention / ZDR | Inputs not stored by default unless prompt logging is opted into; logged data retained for a minimum of 3 months. ZDR routing available on every plan (account setting, guardrail, or per request). Enterprise accounts default to ZDR-only. CSAM screening applies to all traffic, including ZDR, from 2026-10-27. | https://openrouter.ai/terms · https://openrouter.ai/docs/guides/features/zdr · https://openrouter.ai/docs/guides/features/input-output-logging |
| Training use | Does not use inputs or outputs for training. Some downstream providers may; an account setting excludes providers that train. | https://openrouter.ai/privacy · https://openrouter.ai/docs/features/privacy-and-logging |
| Sub-processors | Public list in the Trust Center and DPA Schedule 3. 30 days' notice for subscribers; AI model providers are excluded from that notice. 30 days to object. | https://trust.openrouter.ai/ · https://openrouter.ai/assets/data-processing-agreement.pdf |
| SSO | SAML (Okta, Entra ID, Google Workspace, custom). Enterprise plan. | https://openrouter.ai/docs/guides/features/sso |
| SCIM | Supported, with group mappings to workspaces. Enterprise plan. | https://openrouter.ai/docs/guides/features/scim-mappings |
| Audit logs | Per-request logs (model, provider, cost, tokens, member) via API; aggregated activity export. Admin-action log: SCIM mappings audit log only. Request log retention: Not published. | https://openrouter.ai/docs/guides/features/logs · https://openrouter.ai/pricing |
| Spend controls | Guardrail spending caps (daily, weekly, monthly) per member and per key. Not on the Free plan. | https://openrouter.ai/docs/guides/features/guardrails |
| Model / provider allow-lists | Guardrails restrict models and providers per member or key and can enforce ZDR; managed by org admins. | https://openrouter.ai/docs/guides/features/guardrails |
| Breach notification | Without undue delay and within 72 hours, including at sub-processors (DPA). | https://openrouter.ai/assets/data-processing-agreement.pdf |
| EU AI Act deployer support | Not published as a feature. Sovereign AI guide and blog posts discuss the Act. | https://openrouter.ai/docs/guides/features/sovereign-ai |
| Exit / portability | OpenAI SDK works as a drop-in replacement; logs retrievable by API. Deletion within 30 business days of request (DPA). Self-host: Not published. | https://openrouter.ai/docs/quickstart · https://openrouter.ai/assets/data-processing-agreement.pdf |
| Certifications | SOC 2 Type II. ISO 27001: Not published. | https://trust.openrouter.ai/ |
| DPA | Incorporated into the Terms, with SCCs (updated 2026-08-26). Signed copy on request (Business); custom DPA (Enterprise). | https://openrouter.ai/assets/data-processing-agreement.pdf · https://openrouter.ai/pricing |

## Portkey

Managed and open-source AI gateway. Docs are titled "Portkey (Prisma AIRS AI Gateway) Docs" and carry the banner "Portkey is now PRISMA AIRS AI Gateway". A separate doc set exists at `portkey.ai/docs/aigw/`; this row uses the main docs.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | Changelog (July 2025): LLM data can be hosted in any region of your choice with strict isolation and no cross-border data flow. Regions and plan not listed. In hybrid deployment, prompts, responses and logs stay in the customer network. VPC/private cloud: Enterprise. | https://portkey.ai/docs/changelog/2025/july · https://portkey.ai/docs/enterprise/poc |
| Retention / ZDR | Log retention: Developer 3 days, Production 30 days, Enterprise custom. `x-portkey-debug:false` keeps content out of logs per request; org-wide "Metrics Only" mode; not storing bodies at all on request. | https://portkey.ai/docs/product/observability/logs · https://portkey.ai/pricing |
| Training use | Not published. | |
| Sub-processors | Trust Vault has a sub-processors section; page not retrievable on 2026-11-07 (certificate error). Notice period: Not published. | https://trust.portkey.ai/ |
| SSO | OIDC and SAML 2.0. Enterprise plan. | https://portkey.ai/docs/product/enterprise-offering/org-management/sso |
| SCIM | Supported for Azure AD and Okta (users and workspace groups). Plan: Not published. | https://portkey.ai/docs/product/enterprise-offering/org-management/scim/scim |
| Audit logs | Org-wide admin audit logs with API. Enterprise plan. Custom retention policies listed. | https://portkey.ai/docs/product/enterprise-offering/audit-logs |
| Spend controls | Cost or token budgets on integrations, keys and workspaces, with alerts. Enterprise and select Pro customers. | https://portkey.ai/docs/product/ai-gateway/virtual-keys/budget-limits |
| Model / provider allow-lists | Per-integration model allow-lists; "Model Rules" guardrail org-wide; provider access permissions on Enterprise. | https://portkey.ai/docs/product/model-catalog/integrations · https://portkey.ai/docs/integrations/guardrails/model-rules |
| Breach notification | Not published (security page describes "transparent communication" during incidents, no time window). | https://portkey.ai/docs/product/enterprise-offering/security-portkey |
| EU AI Act deployer support | Not published as a feature (blog post only). | https://portkey.ai/blog/ai-governance-checklist-for-2025/ |
| Exit / portability | OpenAI SDK via `base_url`. Open-source, self-hostable gateway (`github.com/portkey-ai/gateway`). Data lake export on Enterprise. | https://portkey.ai/docs/product/ai-gateway · https://github.com/portkey-ai/gateway |
| Certifications | States ISO 27001 and SOC 2 certified, GDPR and HIPAA compliant. | https://portkey.ai/docs/product/enterprise-offering/security-portkey |
| DPA | DPA page exists; its text did not render on 2026-11-07, so terms not confirmed. | https://portkey.ai/dpa |

## LiteLLM

Open-source LLM proxy, plus a self-hosted Enterprise license. No LiteLLM-hosted cloud offering was found on its pages, so this row covers self-hosting. The trust center (`trust.litellm.ai`) renders only with JavaScript and could not be read on 2026-11-07.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | Runs in your infrastructure (air-gapped available); no data or telemetry stored on LiteLLM servers when self-hosted. Region routing by tags (for example `route:region:eu`); "Multi-region" listed as Enterprise. | https://docs.litellm.ai/docs/data_security · https://docs.litellm.ai/docs/proxy/customer_routing · https://www.litellm.ai/enterprise |
| Retention / ZDR | `turn_off_message_logging` keeps prompts and responses out of logging callbacks (off by default). Configurable spend-log retention. Per-team logging off: Enterprise. | https://docs.litellm.ai/docs/proxy/logging · https://docs.litellm.ai/docs/proxy/spend_logs_deletion |
| Training use | Not published (states no personal data is sent to LiteLLM servers when self-hosting). | https://docs.litellm.ai/docs/data_security |
| Sub-processors | Not published (trust center not readable). | https://docs.litellm.ai/docs/data_security |
| SSO | OIDC and SAML 2.0 for the Admin UI. Requires an Enterprise license; free for up to 5 users from v1.76.0. | https://docs.litellm.ai/docs/proxy/admin_ui_sso |
| SCIM | Supported (Entra ID, Okta); Enterprise license. Deprovisioning blocks the user's virtual keys. | https://docs.litellm.ai/docs/tutorials/scim_litellm |
| Audit logs | Admin actions on keys, teams, users and models; exportable to S3. Enterprise license. | https://docs.litellm.ai/docs/proxy/audit_logs |
| Spend controls | `max_budget` and `budget_duration` per key, user, team and team member, plus TPM/RPM limits (open source). Per-model and tag budgets: Enterprise. | https://docs.litellm.ai/docs/proxy/users |
| Model / provider allow-lists | Per-key `models` list, plus team and user restrictions. Model access groups: Enterprise. Provider allow-list as a separate control: Not published. | https://docs.litellm.ai/docs/proxy/model_access |
| Breach notification | Not published. Incident response policy "available upon request". | https://docs.litellm.ai/docs/data_security |
| EU AI Act deployer support | Release v1.81.14 lists an "EU AI Act Article 5" guardrail policy template. Plan not stated. | https://docs.litellm.ai/release_notes/v1.81.14/v1-81-14 |
| Exit / portability | Open source, self-hosted, OpenAI-compatible proxy. | https://github.com/BerriAI/litellm |
| Certifications | SOC 2 Type II (report via trust center). | https://docs.litellm.ai/docs/data_security |
| DPA | Not published. | |

## Azure OpenAI (Microsoft Foundry)

Docs now describe Azure OpenAI as part of "Foundry Models sold by Azure" in Microsoft Foundry. Single provider, so provider allow-lists do not apply.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | Deployment types: Global (any Azure region), Data Zone (US, EU) and Standard/Regional (the chosen geography). EU Data Zone follows the EU Data Boundary, which can include EFTA countries such as Norway and Switzerland. Microsoft can add regions to a data zone without prior notice. | https://learn.microsoft.com/en-us/azure/foundry/foundry-models/concepts/deployment-types |
| Retention / ZDR | Flagged content may be stored for human review in the resource's geography (EEA reviewers for EEA deployments). Modified abuse monitoring, which removes storage and human review, requires additional Limited Access eligibility. Stateful features keep data until deleted. | https://learn.microsoft.com/en-us/azure/foundry/openai/concepts/abuse-monitoring · https://learn.microsoft.com/en-us/azure/foundry/responsible-ai/openai/data-privacy |
| Training use | Not available to OpenAI or other providers; not used to train generative AI foundation models without permission. | https://learn.microsoft.com/en-us/azure/foundry/responsible-ai/openai/data-privacy |
| Sub-processors | Public list on the Service Trust Portal. At least 6 months' notice for new Customer Data subprocessors; at least 30 days for AI-functionality subprocessors. | https://learn.microsoft.com/en-us/compliance/assurance/assurance-supplier-management |
| SSO | Microsoft Entra ID with conditional access, MFA, managed identities and RBAC; API keys can be disabled. | https://learn.microsoft.com/en-us/azure/foundry/concepts/authentication-authorization-foundry |
| SCIM | Not published in Foundry docs (access uses Entra ID identities directly). | |
| Audit logs | Diagnostic categories include Audit, Request and Response, and Request Usage, sent to Log Analytics or Storage. | https://learn.microsoft.com/en-us/azure/foundry/how-to/diagnostic-logging |
| Spend controls | TPM quotas per subscription, region and model. Cost budgets alert but cannot cap. Foundry Control Plane with AI Gateway enforces token quotas per project. | https://learn.microsoft.com/en-us/azure/foundry/concepts/manage-costs · https://learn.microsoft.com/en-us/azure/foundry/control-plane/how-to-enforce-limits-models |
| Model allow-lists | Built-in Azure Policy "only use approved models"; custom policy can block deployment types such as GlobalStandard. | https://learn.microsoft.com/en-us/azure/foundry/how-to/model-deployment-policy |
| Breach notification | Within 72 hours, per the DPA. | https://learn.microsoft.com/en-us/compliance/assurance/assurance-incident-management |
| EU AI Act deployer support | Trust Center EU AI Act page and an AI literacy guide. No Foundry-specific deployer guide. | https://www.microsoft.com/en-us/trust-center/compliance/eu-ai-act |
| Exit / portability | v1 API works with the standard OpenAI client. Data kept 90 days after termination for extraction, then deleted. | https://learn.microsoft.com/en-us/azure/foundry/openai/api-version-lifecycle · https://www.microsoft.com/en-us/trust-center/privacy/data-management |
| Certifications | Azure ISO 27001/27017/27018 and SOC 1/2/3. Per-service scope is in the Service Trust Portal appendices; not confirmed on a public page for this service. | https://learn.microsoft.com/en-us/azure/compliance/offerings/cloud-services-in-audit-scope |
| DPA | Microsoft Products and Services DPA (addendum to the Product Terms). | https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA |

## Amazon Bedrock

Single cloud provider with many models, so provider allow-lists do not apply.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | Geographic cross-Region inference profiles (for example EU, US, APAC) keep processing in that geography, though data may move outside the source Region. Global profiles route to any commercial Region. CloudTrail records the inference Region. | https://docs.aws.amazon.com/bedrock/latest/userguide/geographic-cross-region-inference.html |
| Retention / ZDR | Per-Region `data_retention_mode` (`none` for ZDR, default, others) at account or project level, enforceable by SCP. Some models require retention (for example up to 30 days for certain models), with stated exceptions. | https://docs.aws.amazon.com/bedrock/latest/userguide/data-retention.html |
| Training use | AWS and third-party model providers do not use Bedrock inputs or outputs to train models. | https://aws.amazon.com/bedrock/faqs/ |
| Sub-processors | Public list, updated at least 30 days before a new sub-processor is engaged; email subscription. | https://aws.amazon.com/compliance/sub-processors/ |
| SSO | IAM Identity Center or IAM, with MFA, recommended. | https://docs.aws.amazon.com/bedrock/latest/userguide/data-protection.html |
| SCIM | IAM Identity Center supports SCIM v2.0 provisioning from an external IdP. | https://docs.aws.amazon.com/singlesignon/latest/userguide/provision-automatically.html |
| Audit logs | CloudTrail for API calls. Model invocation logging (off by default) records full request and response bodies to CloudWatch or S3. | https://docs.aws.amazon.com/bedrock/latest/userguide/logging-using-cloudtrail.html · https://docs.aws.amazon.com/bedrock/latest/userguide/model-invocation-logging.html |
| Spend controls | Token quotas via Service Quotas; cost attribution via inference profiles, tags and Cost Explorer. Hard spend cap: Not published. | https://docs.aws.amazon.com/bedrock/latest/userguide/quotas.html · https://docs.aws.amazon.com/bedrock/latest/userguide/cost-management.html |
| Model allow-lists | IAM or SCP policies on model and inference profile ARNs; Region-deny SCPs. | https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_examples_bedrock.html |
| Breach notification | Without undue delay (DPA s.9.1); no fixed hour count. | https://d1.awsstatic.com/legal/aws-dpa/aws-dpa.pdf |
| EU AI Act deployer support | Not published in docs or compliance pages (AWS blog post only). | https://aws.amazon.com/blogs/machine-learning/building-trust-in-ai-the-aws-approach-to-the-eu-ai-act/ |
| Exit / portability | OpenAI-compatible Chat Completions and Responses APIs. Data returned or deleted on request up to 90 days after termination (DPA s.14). | https://docs.aws.amazon.com/bedrock/latest/userguide/endpoints.html |
| Certifications | Bedrock (excluding Marketplace) listed in SOC and ISO scope. | https://aws.amazon.com/compliance/services-in-scope/SOC/ · https://aws.amazon.com/compliance/iso-certified/ |
| DPA | AWS DPA, with SCCs applied automatically through the Service Terms. | https://d1.awsstatic.com/legal/aws-dpa/aws-dpa.pdf |

## Claude Enterprise

Anthropic's enterprise plan for Claude apps and Claude Code. Single provider, so provider allow-lists do not apply. Notes on the Claude API are labeled.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | Traffic may be routed to select countries in the US, Europe, Asia and Australia; data stored in the US. "US-only inference" available on usage-based Enterprise plans. EU-only option: Not published. (Claude API: `inference_geo` offers `us` and `global`.) | https://privacy.claude.com/en/articles/7996890-where-are-your-servers-located-do-you-host-your-models-on-eu-servers · https://support.claude.com/en/articles/15422948-enable-us-only-inference-for-your-organization · https://platform.claude.com/docs/en/manage-claude/data-residency |
| Retention / ZDR | Custom retention period, minimum 30 days. ZDR is available for Claude Code only, not included in the standard plan, and needs separate enablement. Flagged content may be kept up to 2 years. | https://privacy.claude.com/en/articles/10440198-configure-custom-data-retention-controls-for-enterprise-plans · https://code.claude.com/docs/en/zero-data-retention |
| Training use | No training on commercial product inputs or outputs by default; exceptions are opt-ins such as feedback. | https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training |
| Sub-processors | Public list. "Reasonable notice" before a new subprocessor; 15 days to object. | https://www.anthropic.com/subprocessors |
| SSO | SAML (and OIDC for some IdPs), domain capture, optional "Require SSO". | https://support.claude.com/en/articles/13132885-set-up-single-sign-on-sso |
| SCIM | Included, with JIT provisioning and group-to-role mapping. | https://claude.com/solutions/enterprise |
| Audit logs | Audit log export for the past 180 days (IDs, not content). Compliance API activity feed retains 6 years from enablement. | https://support.claude.com/en/articles/9970975-access-audit-logs · https://platform.claude.com/docs/en/manage-claude/compliance-faq |
| Spend controls | Spend limits for the organization, groups and users; pooled group budgets (beta). | https://support.claude.com/en/articles/14782391-claude-enterprise-consumption-guide · https://support.claude.com/en/articles/17005973-manage-pooled-group-budgets-on-enterprise-plans |
| Model allow-lists | Org-wide on/off per model; custom roles narrow access within that set. | https://support.claude.com/en/articles/15694740-manage-model-access-for-your-organization |
| Breach notification | Without undue delay, and in any event within 48 hours (DPA). | https://assets.claude.com/d16e60156ee20e9a1c5cfff5c0cabfba39b7c9bf.pdf |
| EU AI Act deployer support | Not published as deployer documentation. A page on Art. 50 content marking exists. | https://support.claude.com/en/articles/16266773-how-claude-marks-ai-generated-content |
| Exit / portability | Primary Owners can export organization data. Return or export within 30 days of termination, then deletion (DPA). | https://support.claude.com/en/articles/13346720-export-your-organization-s-data |
| Certifications | ISO 27001:2022, ISO/IEC 42001:2023, SOC 2 Type I and Type II. | https://privacy.claude.com/en/articles/10015870-what-certifications-has-anthropic-obtained |
| DPA | Public DPA incorporated into the Commercial Terms, with SCCs. | https://assets.claude.com/d16e60156ee20e9a1c5cfff5c0cabfba39b7c9bf.pdf |

## Cloudflare AI Gateway

Managed AI gateway on Cloudflare's network.

| Dimension | Public answer | Source |
|---|---|---|
| Data residency | AI Gateway listed as "Not compatible" with Regional Services and Geo Key Manager; Customer Metadata Boundary "compatible with caveats". | https://developers.cloudflare.com/data-localization/compatibility/ |
| Retention / ZDR | Logs on by default; can be turned off per gateway or per request, or limited to metadata. ZDR routes Unified Billing traffic to providers that do not retain prompts; does not cover bring-your-own-key traffic. | https://developers.cloudflare.com/ai-gateway/observability/logging/ · https://developers.cloudflare.com/ai-gateway/features/unified-billing/ |
| Training use | Does not use customer content to train LLMs. Third-party providers reached through the gateway follow their own terms. | https://www.cloudflare.com/trust-hub/responsible-ai/ |
| Sub-processors | Public list. At least 30 days' notice; 10 days to object (DPA v6.3). | https://www.cloudflare.com/gdpr/subprocessors/cloudflare-services/ |
| SSO | Dashboard SSO free on all plans. | https://developers.cloudflare.com/fundamentals/manage-members/dashboard-sso/ |
| SCIM | Enterprise customers only. | https://developers.cloudflare.com/fundamentals/account/account-security/scim-setup/ |
| Audit logs | Account audit logs retained 18 months. Gateway request logs capped by plan; Logpush export. | https://developers.cloudflare.com/fundamentals/account/account-security/audit-logs/ · https://developers.cloudflare.com/ai-gateway/reference/pricing/ |
| Spend controls | Spend limit rules per gateway, scoped by model, provider or custom metadata (max 20 rules); enforcement is eventually consistent. | https://developers.cloudflare.com/ai-gateway/features/spend-limits/ |
| Model / provider allow-lists | Auto Router headers `cf-aig-allowed-models` and `cf-aig-allowed-providers`; model aliases; "require provider credentials" blocks Cloudflare-billed fallback. Gateway-wide allow-list: Not published. | https://developers.cloudflare.com/ai-gateway/features/routing/auto-router/ |
| Breach notification | Without undue delay (DPA); no hour figure. | https://cf-assets.www.cloudflare.com/dzlvafdwdttg/4Q9t8JmVFtSrFJs1QGYngn/4b5d517abf6468ffa88627d457ee945c/DPA_2025-06-20_Version.pdf |
| EU AI Act deployer support | Not published for AI Gateway. General Responsible AI page explains deployer obligations. | https://www.cloudflare.com/trust-hub/responsible-ai/ |
| Exit / portability | OpenAI-compatible unified endpoint; log export via Logpush. Self-host: not offered. | https://developers.cloudflare.com/ai-gateway/usage/chat-completion/ |
| Certifications | SOC 2 Type II, ISO 27001:2022, ISO 27701. Whether AI Gateway is in scope: Not published. | https://www.cloudflare.com/trust-hub/compliance-resources/iso-certifications/ |
| DPA | Public Customer DPA v6.3 (2025-06-20), with SCCs. | https://cf-assets.www.cloudflare.com/dzlvafdwdttg/4Q9t8JmVFtSrFJs1QGYngn/4b5d517abf6468ffa88627d457ee945c/DPA_2025-06-20_Version.pdf |

---

## Methodology

- Sources: vendor-owned domains only (including vendor-owned GitHub repositories). Blog posts on a vendor's own domain are cited only where nothing else exists, and are labeled as such.
- One snapshot date for all rows: 2026-11-07.
- "Not published" is used when the answer could not be found on the vendor's own public pages, or the page could not be read; the latter is stated in the cell.
- Cells paraphrase closely. Where wording matters (for example breach notice windows), the source text is quoted or the number is given exactly.
- Plan names and prices change often and are mostly left out; check the vendor's pricing page.
