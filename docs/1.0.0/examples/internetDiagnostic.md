---
layout: default
title: Internet Diagnostic Example
parent: Examples
grand_parent: Version 1.0.0
nav_order: 2
---

A hypothetical support conversation when an ISP user calls in to ask why their internet is down. Includes a diagnostic, images, and multiple answers.

```
<!-- query: internet is down -->
## Having problems connecting to the internet?
This diagnostic will help you identify the problem and recommend a solution.

<!-- [phrasing] 
* my router doesn't work
* my internet is down
-->

<!--
say.name: attempts
say.ask: Which of the following have already tried?
say.type: multiple 
reply.name: allAttempts
[reply.values]
* Turned my computer's WiFi off then on
* Rebooted the router
* Updated router firmware
* Checked that router power is on and the lights are green
* Checked that more than once device is unable to connect to the internet
-->

<!-- 
say.name: device
say.type: single
reply.name: deviceType
[reply.values]
* Brand Alpha model A1 router
* Brand Zeta model B334 router
* Brand Beta model Z44
-->
### Router models
What type of router do you have?
![Router models](/assets/routerModels.png)

<!-- 
say.trigger: same('device',[1]) 
say.type: answer
-->
Your router may need to be upgraded, this router has a history of problems and doesn't support some new devices. We suggest one of the following routers - click the link to purchase:
- [InternetCo Router WB45](http://www.example.com)
  ![InternetCo Router WB45](/assets/router1.jpg)
- [InternetCo Router XY87](http://www.example.com) 
  ![InternetCo Router XY87](/assets/router2.jpg)
- [FancyWidgetCo Router WFFB45](http://www.example.com)
  ![FancyWidgetCo Router WFFB45](/assets/router3.jpg)


<!-- 
say.trigger: share('device',[0,2])  and (subset('attempts', [0, 1, 2])) 
say.type: diagnostic
-->
Your router may not be connected to our servers. Try the following in this precise order:
1. unplug your router's power
2. unplug your router cable
3. disconnect all devices
4. reconnect the power
5. reconnect the cable
6. reconnect your devices  

<!-- 
say.trigger: share('device',[0,2])  
say.name: isConnected
say.ask: Do you have internet connectivity after performing those steps?
say.type: single
reply.name: yes
-->

<!-- 
say.trigger: same('isConnected',[1])
say.type: answer
say.name: supportForums
-->
Please check our [community forums](http://example.com) for more information on what your problem might be.

<!-- 
say.trigger: same('isConnected',[0])
say.type: answer
say.name: done
-->
Great, thanks for contacting customer support. Goodbye.
```