---
layout: default
title: Conditional Questions
parent: Patterns 
grand_parent: Version 1.0.0
nav_order: 2
---

## Conditional questions
The tags we've introduced can be used to build pretty much any type of goal-driven conversation. A common pattern involves 'conditional questions' - questions which are only asked in certain circumstances. Conditional questions are common in pre-sales scenarios. For example if you're selling hiking shoes, you might build a tool to help users pick which shoe is ideal for their use case. If the customer selects 'city walking' as their use case, the bot won't subsequently ask the user how heavy of a backpack they will be carrying.

Conditional questions are used in many situations where a bot is giving advice such as

- where to find forms
- which product to buy
- which team to contact
- which diagnostic to trigger to solve a problem

For instance, there are several COVID screeners on the web created by various medical and governmental organizations.  This one by [Sutter Health](https://covid-19.ada.com/sutter/index.html) asks several preliminary questions up front, like accepting terms and conditions.  The user has to accept these before the actual screener starts. As the screener proceeds, it determines which questions to ask based on the answers to previous questions.

To build a dialog like this, we need to associate triggers with each say tag.  If the trigger evaluates to true, we run the question, otherwise we don't.  As the user answers more questions, we re-evaluate whether to ask every say based on all the answers collected so far. For example the screener asks the user their gender, since its part of the risk calculation that drives what advice the bot gives:

```
<!-- 
say.trigger: same('TOSAccepted', [0])
say.name: gender
say.type: single 
reply.name: gender
[reply.values]
* Male
* Female
-->
Are you male or female?
[Why only these two](...)

This text is not included in the ask
```

Above we've telling the bot to execute the 'gender' question only if the user has accepted a question named TOSAccepted in a previous step. We've omitted the `say.ask` value, causing the parser to include the first markdown it encounters after the tag. Make sure to include an empty line after the markdown so the parser knows to discontinue using that text for the ask. Using markdown for the ask lets us include richer text in the question we present to the user - in this case a link to an explanation.  Markdown may be included in the ask including html comments, paragraphs, lists, headings, and images. See the unsupported markdown section for what is not supported. 