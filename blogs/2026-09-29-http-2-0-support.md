---
title: "HTTP 2.0 support"
url: "https://forum.newsblur.com/t/http-2-0-support/13858#post_2"
date: "2026-09-29"
author: "@samuelclay Samuel Clay"
feed_url: "https://forum.newsblur.com/posts.rss"
---
NewsBlur only spoke HTTP/1.1 when fetching feeds, and Dumbing of Age’s server started refusing HTTP/1.1 with that 426 a few days ago. The error page is misleading since it has nothing to do with SSL, and the missing Upgrade header didn’t matter because NewsBlur never looked at it. HTTP/2 works fine, so I added a fallback: when a feed answers with a 426, NewsBlur now retries it over HTTP/2.
