---
title: "Cannot add a custom atom feed from bugzilla"
url: "https://forum.newsblur.com/t/cannot-add-a-custom-atom-feed-from-bugzilla/13835#post_2"
date: "2026-09-17"
author: "@samuelclay Samuel Clay"
feed_url: "https://forum.newsblur.com/posts.rss"
---
The URL is fine and NewsBlur did find the feed. The fetch was what failed: bugs.kde.org refuses any request whose user agent looks like a desktop browser, and NewsBlur’s fetcher ends its user agent with one, so every fetch came back 403 and the feed sat empty with no title. I’ve changed the fetcher to retry with its plain NewsBlur user agent when a site does that, which bugs.kde.org accepts.
