---
name: Read and triage your NewsBlur river
description: Load subscribed feeds, pull unread stories across feeds, and mark them read.
api: openapi/newsblur-openapi.yml
operations: [login, getFeeds, getRiverStories, getUnreadStoryHashes, markStoryHashesAsRead]
---

# Read and triage your NewsBlur river

Use this skill to catch up on unread stories across all subscribed feeds and clear them.

## Auth
NewsBlur accepts a session cookie or an OAuth 2.0 bearer token. Either sign in with
`login` (POST /api/login) to obtain the `newsblur_sessionid` cookie, or send an
`Authorization: Bearer <token>` header on every request. See
`authentication/newsblur-authentication.yml`.

## Steps
1. `getFeeds` (GET /reader/feeds) — list the user's subscriptions with per-feed unread counts. Note the feed ids that have unread items.
2. `getRiverStories` (GET /reader/river_stories) — pull the combined "river" of unread stories across those feeds. Pass `feeds` (feed ids) and `page` to walk pages.
3. Review each story; collect the `story_hash` values the user has finished reading.
4. `markStoryHashesAsRead` (POST /reader/mark_story_hashes_as_read) — mark that batch read in one call. Prefer this over the deprecated single-story `mark_story_as_read`.
5. Optionally `getUnreadStoryHashes` (GET /reader/unread_story_hashes) to confirm the remaining unread set.

## Conventions
- Stories are addressed by `story_hash` (`<feed_id>:<story_id>`). See `data-model/newsblur-data-model.yml`.
- Pagination is page-number based via the `page` parameter.
- Responses carry `result: "ok" | "error"`; on error inspect the `errors` map. See `errors/newsblur-problem-types.yml`.
