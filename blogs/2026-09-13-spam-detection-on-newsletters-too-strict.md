---
title: "Spam detection on newsletters too strict"
url: "https://forum.newsblur.com/t/spam-detection-on-newsletters-too-strict/13413#post_4"
date: "2026-09-13"
author: "@samuelclay Samuel Clay"
feed_url: "https://forum.newsblur.com/posts.rss"
---
Sorry for the long wait on this. You have it right, the rejections are coming from ImprovMX, which receives mail for newsletters.newsblur.com , and their SpamAssassin scoring bounces anything at 5.0 or above before NewsBlur sees it. NewsBlur itself doesn’t filter newsletters at all, and I agree the secret token in the address should be enough.
