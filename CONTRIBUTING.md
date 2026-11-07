# Contributing

Corrections and additions are welcome from buyers, security reviewers and vendors.

## Vendor corrections

If you work for a vendor listed in [`comparison.md`](comparison.md) and an entry is wrong, out of date or marked "Not published" when you do publish it, please open a pull request.

1. Change only the cells for your own product.
2. Every changed cell must link to a **public page on your own domain** (docs, trust center, DPA, terms, pricing, changelog). Pages behind a login, NDA or sales call cannot be cited, because readers cannot check them.
3. Update the "Checked" date for your row to the date you made the change.
4. Say in the PR description that you work for the vendor.
5. Keep the wording factual. Describe what the page says, not why your product is better. Superlatives and comparisons with other vendors will be removed.

We will merge corrections that are supported by the linked source, including corrections that make the maintainer's own product look worse by comparison.

## Adding a vendor

Open an issue first with the vendor name and its public security, privacy and DPA pages. New rows follow the same rule: only facts from the vendor's own public pages, and "Not published" where nothing is published.

## Questionnaire changes

`questionnaire.md` and `questionnaire.csv` hold the same questions. If you change one, change the other, and keep question IDs stable (add new IDs at the end of a section instead of renumbering) so that people who reference IDs in contracts and tickets are not broken.

Good questions are:
- answerable by a vendor in writing,
- verifiable with a document or setting,
- specific to LLM gateways or AI APIs, or a general question with a gateway-specific twist.

## Conflicts of interest

This repository is maintained by the Standard Compute team, which sells an LLM gateway. If you think an entry or question favors any vendor, including ours, open an issue. Neutrality reports get priority.

## License

By contributing you agree that your contribution is licensed under the MIT License in [`LICENSE`](LICENSE).
