---
layout: default
title: Say and Reply tags
parent: Tags 
grand_parent: Version 1.0.0
nav_order: 3
---

## Say and Reply tags

The say tag defines questions or requests a bot says to the user.  After the user replies, the bot can use the user's reply to decide what it will say next using a trigger.  The combination of say and reply tags are what turns a sequential (read top-to-bottom), non-interactive document into a conversation. There are generally two ways in which support web pages present “forks in the road” where the reader needs to select a path to go down based on their particular problem. We have slightly different ways to add tags for each way.

The most common way is to create several sections, each with a heading that describes a particular variation of the problem/solution.  We see that in [Apple's subscription cancelation support page](https://support.apple.com/en-us/HT202039). This page requires the reader to scan the whole page, scrolling down to find the section heading relevant to their device. We can create a better experience by asking the user what device they have up front, then showing the relevant one. To do this, we add a say tag and a reply tag to the top of the page, before each device-specific section.  Once the bot knows which device the user has, the bot walks the user through the steps in the appropriate section just like a human support agent would do.  The other sections are never shown to the user.  This means we need a trigger on each section that evaluates to the device the user is on.  

Let's add tags to that Apple support page below to make it interactive.  The “About canceling..” section is general information, so we want that shown to everyone.  We drop in a say comment tag after it because the subsequent sections are device-dependent.  We only want to show the section for the device the user is on. Here's what it would look like:

```
### About canceling a subscription
- Most subscriptions automatically renew unless you cancel them.
- If you cancel, you can keep using the subscription until the next billing date.
- If you cancel during a trial period, you might lose access to content immediately.

If you signed up for a free or discounted trial subscription and you don't want to renew it, cancel it at least 24 hours before the trial ends.

<!-- 
say.ask: What type of device are you on?
say.name: device
say.type: single
say.trigger: true
reply.name: deviceType
[reply.values]
* Mac
* AppleTV
* iPhone, iPad, or iPod touch
-->


<!-- say.trigger: same('device', [2]) 
     say.type: diagnostic
-->
### How to see or cancel subscriptions on your iPhone, iPad, or iPod touch
0. Open the Settings app.
1. Tap your name.
2. Tap Subscriptions. (If you don't see "Subscriptions," tap "iTunes & App Store" instead. Then tap your Apple ID, tap View Apple ID, sign in, scroll down to Subscriptions, and tap Subscriptions.)
3. Tap the subscription that you want to manage. Don't see the subscription that you're looking for?
4. [Tap Cancel Subscription](https://example.com) If you don't see Cancel Subscription, the subscription is already canceled and won't renew.



<!-- say.trigger: same('device', [0])
     say.type: diagnostic
-->
### See or cancel subscriptions on your Mac
1. Open the App Store app.
2. Click the sign-in button or your name at the bottom of the sidebar.
...


```
Lets explain what's going on above. Say tags define what we want the bot to ask the user. In this case, the bot asks which device they have so we can direct them to the steps appropriate to their device.  

    say.ask: What type of device do you have?
    say.name: device
    say.type: single

The `say.ask` key is followed by a sentence (all on one one line) that we want to bot to say to the user. We name this question 'device' with the `say.name` key.  This lets the bot check what the user replied with later in a trigger. Triggers
determine if/when the bot asks a specific question. We'll cover more on triggers
later. The `say.type` key defines the type of reply the bot expects. In this case the bot allows a single item to be selected in the reply. 
    
Next lets look at the reply tag:

    reply.name: deviceType
    [reply.values]
    * Mac
    * AppleTV
    * iPhone, iPad, or iPod touch

The `reply.name` key is followed by a name for the values that follow.  Naming a reply allows its use in triggers to refer to a specific value in the reply. It also allows reuse of the reply's value lists with other say tags without repeating the list of values. Reply names must be unique inside a bot - their values should 
only be defined once. Reply names are case-sensitive and can contain Unicode 
letters, $, _, and digits (0-9), but may not start with a digit. If the 
accompanying slot.name adequately and uniquely describes the reply, you can 
omit reply.name and the slot.name will be used.  

The `[reply.values]` key is followed by a list of replies the user may select from. The three device types that follow use Archieml's 'array of strings' format. When a user selects one of those items, the 'device' question will be assigned the selected value. Note that its the question that's assigned the value, not the reply - replies are just lists of possible replies.

In a different scenario, you may want the bot to accept multiple replies from a list, for example choosing which toppings to put on a pizza.  For that use `say.type: multiple` and the bot will let the user pick as many replies as they want from a list.

The system comes with a set of built in replies that can be referred to instead of specified. The reply names of built in replies include 

- yes 
- true
- done
- accept

See [here](https://github.com/page-support/web-client/blob/6d481d933ace9cfb57aee885309d343dfee30312/src/state/BuiltInReplies.js) for the full list.