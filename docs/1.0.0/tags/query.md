---
layout: default
title: Query tags
parent: Tags 
grand_parent: Version 1.0.0
nav_order: 1
---

## Query Tag

A query groups together a set of phrasings, questions, user replies, and conditional triggers.   An example of a query might be “walk the user through diagnostic to figure out why they can't connect their wifi router to the internet” A bot has one or more queries. The query key indicates that what follows is the name of the query. Give your query a name immediately after the key, inside the HTML comment. The name inside the comment isn't displayed to the user, its only just used as a unique reference to identify this dialog.  Each query in a bot must have a unique name. Assign a name that's meaningful to you and describes what the bot is helping the customer with.

    <!-- query: internet connectivity diagnostic  -->

Often you'll want to speak or show the user an introduction when the bot starts up. Anything that appears outside the HTML comment is interpreted as standard markdown and displayed to the user. This is useful when you want to show a title and/or paragraph to explain what will happen next or give instructions they will need in the dialog. 

    <!-- query: internet connectivity diagnostic -->
    # Problems connecting to the internet
    I'm going to ask you a few questions to identify why you are having trouble connecting your TV to the internet.

Whenever the parser encounters an empty line, it will end ingestion of the text to show with the query.  Other tags work this way too - just put an empty space in between them.

Page.support understands a subset of standard markdown including html comments, html, paragraphs, lists, headings, images and links. See the unsupported markdown section for what is not supported.