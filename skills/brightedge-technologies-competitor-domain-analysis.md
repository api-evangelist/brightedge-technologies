---
name: Analyze competitors and compare domains in BrightEdge
description: Discover an account, list its tracked competitors and domains, and compare domain performance.
api: openapi/brightedge-technologies-platform-openapi-original.json
operations:
  - get_all_accounts_5_0_objects_accounts_get
  - get_account_competitors_5_0_objects_competitors__account_id__get
  - get_account_domain_5_0_objects_domains__account_id__get
  - compare_domains_5_0_chrome_extension_keywords_compare_domains_post
---

# Competitor & domain analysis

Base URL `https://api.brightedge.com`. Auth per `authentication/brightedge-technologies-authentication.yml`.

## Steps
1. **List accounts** — `GET /5.0/objects/accounts` (`get_all_accounts_5_0_objects_accounts_get`).
2. **List competitors** — `GET /5.0/objects/competitors/{account_id}` (`get_account_competitors_5_0_objects_competitors__account_id__get`).
3. **List account domains** — `GET /5.0/objects/domains/{account_id}` (`get_account_domain_5_0_objects_domains__account_id__get`).
4. **Compare domains** — `POST /5.0/chrome_extension/keywords/compare_domains` (`compare_domains_5_0_chrome_extension_keywords_compare_domains_post`) with the target and competitor domains in the JSON body.

## Rules
- Many read operations are POST with a JSON filter body (account_id, date range) — send `Content-Type: application/json`.
- 422 = validation error with `detail[]`. 403 = the user lacks API permission for that account.
