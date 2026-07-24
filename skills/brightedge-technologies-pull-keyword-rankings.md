---
name: Pull keyword rankings for a BrightEdge account
description: Authenticate, discover an account, list its keyword groups and keywords, and pull ranking/time-series metrics.
api: openapi/brightedge-technologies-platform-openapi-original.json
operations:
  - get_all_accounts_5_0_objects_accounts_get
  - get_account_keywordgroups_5_0_objects_keywordgroups__account_id__get
  - get_account_keywords_5_0_objects_keywords__account_id__get
  - get_time_value_5_0_objects_time__account_id___time_frequency___day__get
---

# Pull keyword rankings

Base URL `https://api.brightedge.com`. Auth: HTTP Basic, or a token header (`X-Token` / `Bearer-Token`) — API access must be enabled for your user by a BrightEdge representative. See `authentication/brightedge-technologies-authentication.yml`.

## Steps
1. **List accounts** — `GET /5.0/objects/accounts` (`get_all_accounts_5_0_objects_accounts_get`) to get the `account_id` values you can access.
2. **List keyword groups** — `GET /5.0/objects/keywordgroups/{account_id}` (`get_account_keywordgroups_5_0_objects_keywordgroups__account_id__get`).
3. **List keywords** — `GET /5.0/objects/keywords/{account_id}` (`get_account_keywords_5_0_objects_keywords__account_id__get`).
4. **Pull time-series metrics** — `GET /5.0/objects/time/{account_id}/{time_frequency}/{day}` (`get_time_value_5_0_objects_time__account_id___time_frequency___day__get`) for ranking trends.

## Rules
- Use the pinned `/5.0` prefix for reproducibility; `/latest5` rolls to the newest v5.
- Errors: validation failures return **422** with a `detail[]` array (`errors/brightedge-technologies-problem-types.yml`). No RFC 9457 problem+json.
- No idempotency-key or documented rate-limit headers; these are read operations, safe to retry.
