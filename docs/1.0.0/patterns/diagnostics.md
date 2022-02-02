---
layout: default
title: Diagnostics
parent: Patterns 
grand_parent: Version 1.0.0
nav_order: 1
---

## Diagnostics

Lets look again at the earlier example that contained a diagnostic say tag:

```
<!-- say.trigger: same('device', [2])
     say.type: diagnostic
-->
### How to see or cancel subscriptions on your device ![phone screen](https://example.com/image.png)
0. Open the Settings app. 
1. Tap your name. 
3. Tap Subscriptions. (If you don't see "Subscriptions," tap "App Store" instead. Then tap your ID, tap View ID, sign in, scroll down to Subscriptions, and tap Subscriptions.) ![subscriptions page](https://example.com/image.png)
4. Tap the subscription that you want to manage. 
5. Tap Cancel Subscription. If you don't see Cancel Subscription, the subscription is already canceled and won't renew.
```

We want the bot to ask the user to perform a sequence of steps defined by the list beginning with `0. Open the Settings app.` Instead of showing the whole list, the bot will show one element in the list to the user and wait for the user to reply 'done' before preceeding. This is particularly useful in voice scenarios. Sequences like this are so common in tech support that we can standardize the behavior with one say.type called a diagnostic. Its a shorthand for a sequence of asks and replies typical of diagnostics.  It saves you the trouble of creating multiple asks and replies for each element in the list. The diagnostic tag must be followed by a markdown list (ordered or unordered).  The bot will end the diagnostic by asking 'Did that solve your problem?' 
