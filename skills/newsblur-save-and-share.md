---
name: Save and share a story to your blurblog
description: Star a story for later and share it to your NewsBlur blurblog with a comment.
api: openapi/newsblur-openapi.yml
operations: [getFeedStories, markStoryHashAsStarred, shareStory, getPublicComments]
---

# Save and share a story to your blurblog

Use this skill to save a story and publish it to the user's social blurblog.

## Auth
Session cookie (`login`) or `Authorization: Bearer <token>`. See `authentication/newsblur-authentication.yml`.

## Steps
1. `getFeedStories` (GET /reader/feed/{id}) — fetch stories from a feed and pick the one to act on; capture its `story_hash`.
2. `markStoryHashAsStarred` (POST /reader/mark_story_hash_as_starred) — save (star) the story for later.
3. `shareStory` (POST /social/share_story) — share the story to the user's blurblog, optionally with a comment.
4. Optionally `getPublicComments` (GET /social/public_comments) — read the public discussion on the shared story.

## Conventions
- Stories are addressed by `story_hash` (`<feed_id>:<story_id>`).
- Starring and sharing are naturally idempotent, but NewsBlur documents no Idempotency-Key header — re-issuing is safe by state, not by contract. See `conventions/newsblur-conventions.yml`.
