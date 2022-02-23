---
layout: default
title: Customizing
nav_order: 5 
parent: Version 1.0.0
---

## Customize your bot's look and feel
Customers generally are interested in two things when they engage with support. First, getting an answer or resolution. Second, getting it fast. They don't care about what your logo looks like, the color of your background, etc. Unfortunately many companies spend more time on look and feel than on deliverin fast, accurate solutions. Page.support is for organizations that want to focus on real value, not cosmetics. That said, we don't want your bot to stand out like a sore thumb, so there are some basic color and font customizations. For this we use the style tag

```
style.primaryColor:  #6B7280
style.secondaryColor: #E5E7EB
style.hoverColor: #374151
style.containerBg: #F9FAFB
style.containerBorderBg: #D1D5DB
style.customerFont: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'
```

The colors values are [CSS RGB hex values](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value) The customerFont value is a double quoted [CSS font-family](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family) with any multiword font names in single quotes. Cosmetics are applied to the whole bot.