---
layout: default
title: Customizing
nav_order: 5 
parent: Version 2.0.0
---

## Customize your bot's look and feel
Customers generally are interested in two things when they engage with support. First, getting an answer or resolution. Second, getting it fast. They don't care about what your logo looks like, the color of your background, etc. Unfortunately many companies spend more time on look and feel than on delivering fast, accurate solutions. Page.support is for organizations that want to focus on what's important to customers, not cosmetics. That said, we don't want your bot to stand out like a sore thumb, so there are some basic color and font customizations. For this we use the settings tag. Put this tag at the end of your markdown file. You only need to include the properties you want to to change - the others will use the defaults.

```

<!-- 
settings.primaryColor:  #6B7280
settings.secondaryColor: #E5E7EB
settings.hoverColor: #374151
settings.containerBg: #F9FAFB
settings.containerBorderBg: #D1D5DB
settings.customerFont: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,'Segoe UI', Roboto, 'Helvetica Neue', Arial, 'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'
-->

```

### Definitions
* primaryColor sets the color of button backgrounds and focus:ring 
* secondaryColor does nothing at the moment, held in reserve
* hoverColor sets the color while hovering over buttons - their backgrounds and ring.
* containerBg sets the background color of the outer bot container. It does not affect the color of the individual conversation round containers, those remain white. 
* containerBorderBg does nothing at the moment 

The colors values are [CSS RGB hex values](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value) The customerFont value is a double quoted [CSS font-family](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family) with any multiword font names in single quotes. Cosmetics are applied to the whole bot.