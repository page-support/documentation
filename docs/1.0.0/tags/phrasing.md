---
layout: default
title: Phrasing tags
parent: Tags 
grand_parent: Version 1.0.0
nav_order: 2
---

## Phrasing Tag

Phrasings determine when a query is triggered.  Usually you will enter multiple sentences that reflect how your customers phrase the query this bot is addressing. The [ArchieML](http://archieml.org/) array of strings syntax is used. These sentences are typically made searchable in text GUIs. In voice interfaces, they are used to match user queries to determine when to trigger this bot. The sentences appear inside the phrasing tag, and are not shown to the user in the dialog. Inside the HTML tag, we wrap the “phrasing” key in brackets like 

    [phrasing] 
    
and leave out the colon.  This is how ArchieML indicates that a list of things follows.  Each line that follows is used as one phrase, and lines must begin with a * to be interpreted as separate phrases. 

    <!-- [phrasing] 
    * I'm having a problem signing in with two factor auth
    * How do I sign in with a backup code
    * I can't sign in with two factor authentication.
    -->