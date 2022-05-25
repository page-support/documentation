---
layout: default
title: Customizing
nav_order: 8 
parent: Version 2.0.0
---

## Adding User Analytics to your Bot
To configure event tracking set the `settings.trackUserReplies` property in your markdown to 'true'. For instance, at the end of your markdown, add

```
<!--
settings.trackUserReplies: true
-->
```

When set to true, bot will call a global javascript function called  `pageSupportBotTracker()` and pass in user events to that function. See the [web-client documentation](https://github.com/page-support/web-client#user-engagement-tracking-and-website-analytics) for how to setup your website and integrate these events with your existing user analytics service.
