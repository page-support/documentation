---
layout: default
title: Answers
parent: Patterns 
grand_parent: Version 2.0.0
nav_order: 3
---

## Answers, images, recommendations, referrals

Later on in the dialog, the bot provides guidance on what to do given the answers the user gave to various symptom questions. This is also built by combining a say with a trigger. In this case the 'say' might actually be advice, but we can use the same pattern as above. For instance, given a certain combination of user replies to symptom questions like 'coughing' and 'lackOfSmell' questions, the bot ends the dialog with this guidance:

```
<!-- 
say.trigger: (same('coughing' ,[0])) and same('lackOfSmell' ,[0]))
say.type: answer
-->
It is likely that your symptoms are caused by COVID-19. You are advised to seek emergency care immediately by calling emergency services on 911 or your healthcare provider. You should follow this advice to protect others:
- Avoid contact with others. Discuss your work situation with your employer.
- Do not take public transportation, taxis, or ride-shares during the time you are practicing social distancing.
- Avoid crowded places (such as shopping centers and movie theaters) and limit your activities in public.
[Learn more about COVID-19](https://www.sutterhealth.org/for-patients/health-alerts/2019-novel-coronavirus)
[Restart assessment](https://covid-19.ada.com/sutter/index.html)
```

Here you don't need to give the say a name since the bot isn't expecting an reply from the user so we'll never need to refer to a user answer in a later trigger. After an 'answer' type, the bot assumes this user query /topic is done, and subsequent things the user might say are sent to the router and interpreted as queries rather than slot fills. The bot will ask the user if there's anything else it can help with after processing an 'answer' type. We can include links and images in the say so the user can get more information on their own, but the bot isn't going to do anything when the user clicks on those links other than display the content like any other web page would on a new tab.  

If this bot was recommending hiking shoes we'd want to include links and pictures of several hiking shoes so the user can pick one and buy it online.  

```
<!-- 
say.trigger: (same('useCase', [2]) and same('shoeType', [1]))
say.type: answer
-->
![Paris lifestyle image](https://images.unsplash.com/photo-1518556991616-b220cd5df12e?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80)
### Women's walking shoes
Here are some recommendations for casual day hiking shoes based on your responses:
- ![Keen City Tripper image](https://images.unsplash.com/photo-1511556532299-8f662fc26c06?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80) The [Keen Womens City Tripper](https://google.com) is a good looking shoe that your friends will be envious of.
- ![Merrell Day Hiker image](https://images.unsplash.com/photo-1551107696-a4b0c5a0d9a2?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1300&q=80) If you want something more sporty, try the [Merrell Women's Day Hiker](https://google.com) which will make you look like sporty spice.
```


Above we see the use of images in both the body of the ask, as well as in following list items. The bot will display the images inline vertically, in the same order they appear in the markdown - same behavior as standard markdown. The only difference is the bot UI will remove bullets when it detects an image in the list item, and add some additional spacing between list items. This helps the reader distinguish individual list items despite the length created by the image.

To maintain the readability of your bot, we recommend using only image per say tag in the heading and paragraph. In addition, use no more than one image per list item. Despite having three images in it, the above example conforms to this advice, displaying a lifestle image above the list. Then, for each product list item, it shows an image, descripion and link to the porduct - just like online web listings typicaly display them.

The preceeding type of static recommendation will work if the recommendations are drawing from a small, static set of products - allowing you to curate results in markdown for each user reply. What if you have an online store with many items that change frequently? You'll want to do a query to a backend product search/recommendation service and show the user the results. The bot can collect attributes that are important to the user, then submit those as parameters to a search. The bot can integrate in that experience by including a link with the search parameters it collected from the user in markdown. The bot will launch a new browser tab and show the results of the search in the URL you provide:

```
<!-- 
say.type: newTabAnswer
say.trigger: true
say.link: [results](https://exampleshoestore.com/search?q=shoes&gender=${gender}&type=${activity}) 
-->
```

The bot will interpolate the `${gender}` and `${activity}` parameters, setting them to values the bot asked earlier in questions name 'gender' and 'activity'.  The URL can be in any format - defined by your search service's requirements. By putting the link inside the HTML comment, it won't be shown the user.  

You can use this pattern for other types of referrals too, for example you might want to send the user to a place in your website that has a pdf, a workflow, or a webpage bootstrapped with the answers the user gave the bot. You could also [pre-fill a web form](https://stackoverflow.com/a/43980063) on another page with the params and let the user check and submit it. 
