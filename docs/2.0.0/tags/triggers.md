---
layout: default
title: Triggers
parent: Tags 
grand_parent: Version 2.0.0
nav_order: 4
---


## Triggers

Triggers define when a say/reply pair is executed by the bot. They let the bot adapt its behavior based on what the user has said in previous questions. This is a key advantage of bots over non interactive web pages.  You can turn a text-heavy website that requires lots of reading into a conversation. Your users don't like doing lots of reading, particularly on complex subjects, which is part of the reason they contact customer support. Let's face it - most of a typical support or sales website isn't relevant to the user's specific problem. Triggers get the user to the content that will solve their specific problem.  This is similar to what a human support representative or salesperson would do if they were talking to a user.  Example use cases are 

- recommending products to users by asking them about the problem they want to solve 
- answering tech support questions that require diagnostics 
- guiding users to resources like forms on your website
- directing users to the right support queue/contact for a given problem
 
Lets continue through the Apple refund example and show how triggers are used. Earlier the bot asked the user what device they are on and stored the reply. Next we have to tell the bot which (device-specific) steps to walk the user through. Apple's support page has one section for each device. If the user replied they are on an iPhone, we'd want the below section to be shown to the user:

```
<!-- say.trigger: same('device', [2])
     say.type: diagnostic
-->
### How to see or cancel subscriptions on your iPhone, iPad, or iPod touch
0. Open the Settings app. 
1. Tap your name. 
3. Tap Subscriptions. (If you don't see "Subscriptions," tap "iTunes & App Store" instead. Then tap your Apple ID, tap View Apple ID, sign in, scroll down to Subscriptions, and tap Subscriptions.)
4. Tap the subscription that you want to manage. Don't see the subscription that you're looking for?
5. Tap Cancel Subscription. If you don't see Cancel Subscription, the subscription is already canceled and won't renew.
```

The `say.trigger:` key is followed by an expression. If that expression is true, the bot executes the current question.  The bot will evaluate triggers in say tags from the top of the page downwards and run the first one that evaluates to true. After running a question once it won't run it again.  Every time the bot needs to determine which question to run next, it will evaluate all the not-yet-run triggers on the page from top to bottom.  **If you don't specify a trigger value or leave out the say.trigger tag, the bot assumes you always want to run this question.**
 
Triggers use formulas to test user's past replies against some set of replies that should trigger this question. The `same('device', [2])` formula is telling the bot to walk the user through the 'iPhone, iPad, or iPod' section if the user replied to the 'device' question with the third value in the deviceType reply. Any reply used in a trigger must have been defined earlier in the same document or be a built-in reply. The numbers inside the brackets are zero based indexes into the reply associated with the question.

There are three types of equality tests available, designed to handle both single-reply and multi-reply scenarios:

```
same('device', [0])
subset('device', [0,1,7])
share('device', [1,2,4])
```

The `same({say.name}, [ one or more comma separated reply indexes] )` formula will be true if *all* the user's replies are the same as the reply indexes listed in brackets. The `subset({say.name}, [ one or more comma separated reply indexes] )` formula will be true if all of the user's replies are contained in the listed indexes. For example, if the user replied with 0 and 1, the example would be true. If the user replied 0 and 3, it would be false. The `share({say.name}, [ one or more comma separated reply indexes] )` formula will be true if at least one index overlaps. For example if the user replied with 2 and 8, the example would return true. With all these formulas, the order of the indexes or the user replies is not important.

But you're not limited to these formulas. Trigger operators include ` ==, !=, <=, >=, <, >, in [value1, value2, ..]`.  You can write multi-part expressions with 'and', 'or' as in `(device == reply('deviceType', 2) and (subscription != reply('accountStatus', 3))`.  These are mostly useful when you're accepting free form inputs from the user.

To express "not in" use the format `not (device in reply('notAllowedDevices'))` surrounding the inner expression with parentheses. When using the `in` operator, the right hand side of the operator must be an list - either in the form of a function that returns a list, or list/array literal notation like `not (device in ['iOS', 'iPad'])`. The 'in' operator only works for testing if a single value is included in a set. For example, deviceType in the previous example must be a word or integer. Note that string comparisons are case sensitive. 

You can also apply the pre-defined functions `min(a,b,..), max(a,b,..), and random(n)` where n is a range from 0 to n. 


On the left or right side of an operator, you may use:
- An integer or floating point number.
- A word surrounded by single quotes like `'canceled'`.  Not recommended but will work. Generally we recommend using the reply function explained below.
- An Array of words or integers like `[1, 7, 2234]`.  Same caveats as with words.
- A reply function which has two forms. The array form returns an array if you omit an index as in `reply('deviceType')` which might return `['iOS', 'Android']` or whatever your document defines it as.  The single result form is `reply('deviceType', 1)` which represents the second reply inside the reply named 'deviceType'.  It returns `'Android'`.  Built-in replies like 'yes' work the same way. We encourage you to create and use these reply functions instead of string literals since they let you change the replies in one place and use them in many places. Reply functions are automatically created whenever you list reply options in a tag using `[reply.values]`, give it a name and list of replies.

- In a future release, we'll let you define your own javascript function calls like `getOrderStatus(orderNumber)`.  The function call is executed to retrieve or compute the value to be evaluated in the trigger. A use case is getting information from the user's device or the server backend, aka personalization of the interaction. For instance if a user is asking for an update on the status of a product they ordered, they might say the order number. The function could make a https request to your server to get a list of recent orders and show their status. This also means that the user might get an error if the request fails, or there might be a significant delay before the system replies to the user. 
