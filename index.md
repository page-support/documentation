---
layout: default
title: Home
nav_order: 1
description: "Page.support is a fast no code solution for automating support"
permalink: /
---
# Page.support documentation

## Why page.support
Page.support is a SaaS for customer support. Our goal is to dramatically simplify and accelerate building good customer experiences for customer support. With this acceleration comes the ability to iterate and experiment, ultimately delivering better customer experiences.

Page.support lets you build chatbots and workflow-enabled websites quickly, without writing code. Instead of code you use the same [markdown](https://www.markdownguide.org/) commonly used to create documentation websites. We add some annotations that describe the dialog with the customer to make the experience interactive and add workflow. The simplification is possible because page.support incorporates the conversational patterns that commonly appear in support conversations. You don't need to define the detail behind them. Page.support currently supports embedding in a website or mobile webview. Additional integrations will come in the future.

Unlike most other customer support interfaces, the logic behind the page.support web experience  runs entirely in the user's browser - without interacting with a server. This makes it easier to achieve a high degree of privacy and compliance. For example you can return nothing to the server and get HIPAA compliance by default. You can select what to return to your server based on your application's requirements.

## How it works  
Our [publisher interface](https://publisher.page.support) takes markdown and our custom tags as input. You can author the markdown there or in any editor then paste it in. Clicking the Run button will run the bot so you can test it and iterate internally until you're satisfied with the experience. Next you click Download which downloads a file to add to our open source [web client](https://github.com/page-support/testBot). The README at that link describes two ways to integrate with your website.

## Background and Concepts
Publishers create markdown files that define all the content needed to define a bot.  One bot per file.  A bot is a unit of deployment confined to one page on the client.  To turn a standard web page into an interactive bot, you write key:value pairs inside HTML comments that define the bot's behavior. Otherwise its standard markdown. Here's an example that defines when the bot will ask the user to do a set of steps that are specific to specific set of devices. The markdown after the HTML comment is shown to the user if the trigger evaluates to true.

```
<!-- say.trigger: device == reply('deviceType', 3) 
     say.type: diagnostic
-->
### How to see or cancel subscriptions on your device
0. Open the Settings app. 
1. Tap your name. 
2. Tap Subscriptions. (If you don't see "Subscriptions," tap "App Store" instead. Then tap your ID, tap View ID, sign in, scroll down to Subscriptions, and tap Subscriptions.)
3. Tap the subscription that you want to manage. Don't see the subscription that you're looking for?
4. Tap Cancel Subscription. If you don't see Cancel Subscription, the subscription is already canceled and won't renew.
```

Inside the HTML comment, the parser looks for [ArchieML](http://archieml.org/) key: value notation. If it doesn't find something that looks like a key:value it will ignore it. Each key: value pair must be placed on its own line.

We'll refer to the notation inside the HTML comment as a comment tag or just "tag".  Comment tags define how the bot behaves. Regular markdown content outside HTML comments is used to define what the bot says in voice interfaces, and what it shows the user in GUI interfaces. Tags also define inputs accepted from the user. Tags add interactivity and workflow to what would otherwise be a static web page. For instance they add slot filing (asking questions) and the ability to present content dependent on the user's answers to previous questions - standard parts of a chatbot or web app workflow.

See the detailed documentation under the appropriate version link in the sidebar.
