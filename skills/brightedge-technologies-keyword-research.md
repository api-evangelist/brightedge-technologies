---
name: Run keyword research and idea discovery in BrightEdge
description: Submit keywords for idea generation, poll for async results, and research/track keywords.
api: openapi/brightedge-technologies-platform-openapi-original.json
operations:
  - submit_kw_for_ideas_5_0_instant_keywordIdeas__organization_id__post
  - get_kw_ideas_result_5_0_instant_keywordIdeas__organization_id___request_id__post
  - research_keywords_5_0_chrome_extension_keywords_research_keywords_post
  - track_keywords_5_0_chrome_extension_keywords_track_keywords_post
---

# Keyword research & idea discovery

Base URL `https://api.brightedge.com`. Auth per `authentication/brightedge-technologies-authentication.yml`.

## Steps
1. **Submit for ideas (async)** — `POST /5.0/instant/keywordIdeas/{organization_id}` (`submit_kw_for_ideas_5_0_instant_keywordIdeas__organization_id__post`). Capture the returned `request_id`.
2. **Poll results** — `POST /5.0/instant/keywordIdeas/{organization_id}/{request_id}` (`get_kw_ideas_result_5_0_instant_keywordIdeas__organization_id___request_id__post`) until the job completes. BrightEdge may call back an inbound `/instant/webhook/{provider}/kw_ideas/{request_id}` receiver on its side.
3. **Research keywords** — `POST /5.0/chrome_extension/keywords/research_keywords` (`research_keywords_5_0_chrome_extension_keywords_research_keywords_post`).
4. **Track keywords** — `POST /5.0/chrome_extension/keywords/track_keywords` (`track_keywords_5_0_chrome_extension_keywords_track_keywords_post`) to add them to tracking.

## Rules
- The idea flow is asynchronous: submit → poll by `request_id`. Poll with backoff.
- 422 validation errors carry a `detail[]` array; there is no idempotency-key contract, so de-dupe submissions client-side.
