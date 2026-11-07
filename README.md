# LLM gateway security questionnaire

A vendor-neutral security and procurement questionnaire for evaluating **LLM gateways and AI API providers**: routers, proxies, model marketplaces and the cloud AI platforms they compete with.

Generic SaaS questionnaires (SIG, CAIQ) miss the questions that matter for AI traffic: where inference actually runs, whether the model provider behind the gateway keeps your prompts, whether fallbacks respect your rules, and whether your request logs can support EU AI Act record-keeping. This questionnaire covers those, in plain language, with guidance for the reviewer on each question.

**Maintained by the Standard Compute team.** Standard Compute sells an LLM gateway, so we have a commercial interest in this topic. We have tried to write questions that any vendor, including us, can be held to, and the comparison uses the same sourcing rules for every vendor. Corrections are welcome, especially where you think we got it wrong in our own favor. See [CONTRIBUTING.md](CONTRIBUTING.md).

## What's in the repo

| File | What it is |
|---|---|
| [`questionnaire.md`](questionnaire.md) | 44 questions in 12 sections. For each: why it matters, what a good answer looks like, red flags, and what evidence to request. |
| [`questionnaire.csv`](questionnaire.csv) | The same questions as a spreadsheet, with empty columns for the vendor's answer, evidence link, score and notes. Opens in Excel, Google Sheets and Numbers. |
| [`comparison.md`](comparison.md) | How eight vendors answer the core questions on their own public pages, with links, checked on 2026-11-07. "Not published" where we could not find an answer. |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How vendors and reviewers can submit corrections. |

Sections: data residency and regional processing · retention and zero data retention · training and secondary use · sub-processors · SSO and SCIM · audit logs and request records · spend controls · model and provider governance · incidents, availability and assurance · EU AI Act deployer support · exit and portability · contract and DPA.

Vendors in the comparison: Standard Compute, OpenRouter, Portkey, LiteLLM, Azure OpenAI (Microsoft Foundry), Amazon Bedrock, Claude Enterprise, Cloudflare AI Gateway.

## How to use it in a vendor review

1. **Pick your must-pass questions first.** Before contacting vendors, mark the questions that are deal-breakers for your use case (for example DR-01 and RT-02 if you process personal data of EU residents, or AU-03 if you deploy a high-risk AI system). Deciding afterwards invites rationalizing a favorite.
2. **Pre-fill from public sources.** Use [`comparison.md`](comparison.md) as a starting point, then open each linked page to confirm it is still current. This shortens the questionnaire you send and shows the vendor you have done the reading.
3. **Send the CSV.** Ask vendors to fill in the "Vendor answer" and "Evidence link" columns. Ask for links to documents or settings, not prose. An answer without evidence scores at most 1.
4. **Score consistently.** 2 = good answer with evidence, 1 = partial or unverified, 0 = no answer or a red flag. Score each vendor against the "good answer" column, not against each other.
5. **Ask about the whole chain.** For gateways, every question about retention, training, residency and sub-processors applies twice: to the gateway and to the model providers it forwards to. Ask how the gateway enforces your requirement downstream, not just what its own policy is.
6. **Put the answers in the contract.** Answers that matter should end up in the DPA or order form. Question IDs (for example SP-02) make it easy to reference them in redlines.
7. **Re-check yearly** or when the vendor changes its sub-processor list, plans or terms.

## What this is not

- Not legal advice. Check obligations, especially EU AI Act dates, with your counsel.
- Not a ranking. The comparison records what vendors publish, which is not the same as what they do. A vendor with many "Not published" cells may still have good answers on request.
- Not a replacement for a full information security questionnaire. Use it alongside SIG, CAIQ or your own standard questionnaire.

## License

MIT. See [LICENSE](LICENSE). Use it, fork it, put it in your procurement templates.
