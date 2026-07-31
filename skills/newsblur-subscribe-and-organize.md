---
name: Subscribe to a feed and organize it
description: Find a feed by URL, subscribe, create a folder, and file the feed into it.
api: openapi/newsblur-openapi.yml
operations: [searchFeed, addUrl, addFolder, moveFeedToFolder, renameFeed]
---

# Subscribe to a feed and organize it

Use this skill to add a new source to NewsBlur and keep the reader tidy.

## Auth
Session cookie (`login`) or `Authorization: Bearer <token>`. See `authentication/newsblur-authentication.yml`.

## Steps
1. `searchFeed` (GET /rss_feeds/search_feed) — resolve a website or feed `address` to a NewsBlur feed. If the user already has the exact feed URL you can skip to step 2.
2. `addUrl` (POST /reader/add_url) — subscribe to the feed or website URL. NewsBlur auto-discovers the feed if a site URL is given.
3. `addFolder` (POST /reader/add_folder) — create a folder to group the subscription (skip if the target folder exists).
4. `moveFeedToFolder` (POST /reader/move_feed_to_folder) — file the new feed into the folder.
5. Optionally `renameFeed` (POST /reader/rename_feed) — give the feed a friendlier title.

## Conventions
- POST bodies are form-encoded; responses are JSON with `result: "ok" | "error"`.
- A bad or unreachable feed URL returns a 400 with an `errors` map — see `errors/newsblur-problem-types.yml`.
