---
layout: default
title: Errors
nav_order: 6
parent: Version 1.0.0
---


## Deciphering Errors
The parser will usually give you an error that lets you identify where your input is incorrect and what the problem is. Search for the given word in your text. For example 

```Error: The tag named duration is missing an ask.```

tells us to search for a tag with the name 'duration' in your text with Ctrl-F or Cmd-F on mac. Always giving your tags a name helps identify where the errors are.

Occassionally the parser may give an obtuse error like this. 

```Error: Cannot create property 'values' on string 'duration'```

This happens because the data you entered couldn't be parsed. "Cannot create property" indicates that there is something wrong with your syntax, for example you left out the "name" property in a reply:

```
reply: duration 
[reply.values]
* less than a month
* more than a month
```

Trigger errors will tell you if you have mistyped a ask name or referenced an non-existent one. Correct the typo or add a ask with the referenced name. In the below error, 'phoneTyp' is a typo that references a slot named 'phoneType'

```
Error: Trigger Missing Or Invalid: Say.name phoneTyp is not defined or possibly a typo. Correct typo or add phoneTyp to a tag so the trigger can evaluate it. in "(same('phoneTyp', [0]) or share('selectCountries', [0, 1])) and (not share('selectCountries', [2,3]))"
```

If your trigger is syntactically incorrect, for example missing a ')', you'll see an error like

```
Error: parse error [1:60]: Expected EOF in "same('phoneType', [0]) or share('selectCountries', [0, 1])) and (not share('selectCountries', [2,3]))"
```

Search for the given string, correct it, and click run.

If you are missing a single quote in a trigger, the error will look like

```
Error: Error: parse error [1:92]: Unknown character "'" in "(same(phoneType', [0])"
```

Ask names must be single quoted - above phoneType' is missing the left hand single quote.


If you are missing an argument in a formula, you may see an error like this

```
Error: Error: unexpected TPAREN: ) in "(same('phoneType', ) or share('selectCountries', [0, 1])) and (not share('selectCountries', [2,3]))"
```

The ```(same('phoneType', )``` formula must have an array as the second argument, like ```(same('phoneType', [1])```
