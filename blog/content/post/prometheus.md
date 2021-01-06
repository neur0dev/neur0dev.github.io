+++
title = "Prometheus"
description = "Monitoramento"
date = 2019-07-19T18:30:33-03:00
tags = ["monitoring"]
draft = true
weight = 1
+++

From a technology perspective, monitoring is the tools and processes by which you measure and manage yout technology systems. But monitoring is much more than that. Monitoring provides the translation to business value from metrics generated by your systems and applications. 

Your monitoring system translates those metrics into a measure of user experience. That measure provides feedback to the business to help ensure it's deelivering what define below, to indicate what isn't working and what's delivering an insufficient quality of service. 

A monitoring system has two customers:

* Technology
* The business

### Technology as a customer

The first customer of your monitoring system is Technology. That's you, your team, and the other folks who manage and maintain your technology environment (you might also be called Engineering or Operations or DevOps or Site Reliability Engineering). You rely on monitoring to let you know the state of your technology environment. You also use monitoring quite heavily to detect, diagnose, and help resolve faults and other issues in your technology environment, preferably before it impacts your users.

Monitoring contributes much of the data that informs your critical product and technology decisions, and measures the success of those projects. It's a foundation of your product management life cycle and your relationship with your internal customers, and it helps demonstrate that the business's money is being well spent.

Without monitoring you're winging it at best and at worst being negligent.

**Note**: There's **[a great diagram from Google SRE book](https://landing.google.com/sre/sre-book/chapters/part3/#fig_part-practices_reliability-hierarchy)** that show how monitoring is the foundation of the hierarchy of building and managing applications.

### The business as a customer

The business is the second customer of your monitoring. Your monitoring exists to supporte the business and to make sure it continues to do business. Monitoring provides the reporting that allows the bisness to make good product and technology investments. Monitoring also helps the business measure the value that technology delivers.

### Monitoring fundamentals

Monitoring should be a core tool for managing infrastructure and your business. Monitoring should also be mandatory, built, and deployed with your applications. Without it you will not be able to understand the state of your world, readily diagnose problems, capacity plan, or provide information to your organization about performance, costs, or status.

An excellent exposition of this foundation is the Google service hierarchy chart we mentioned earlier.

![]()
Service hierarchy

But monitoring can be hard to implement well, and it can very easily be bad if you're monitoring the wrong things or int the wrong way. There are some key monitoring anti-patterns and mitigation:

### Monitoring as afterthought

In any good application development methodology, it's a good idea to identify what you want to build vefore you build it. Sadly, there's a common anti-pattern of considering monitoring,and other operrational functions like security, as value-add components of your application rather than core features.

Monitoring, like security, is a core feature of your applications. If you're building a specification or user stories for your application, include metrics and monitoring for each component of your application. Don't wiat until the end of a project or just before deployment. I guarantee you'll miss something that needs to be monitored.

### Monitoring by rote

Many environments create **[cargo cult](https://en.wikipedia.org/wiki/Cargo_cult)** monitoring checks for all your applications. A team reuses the checks they have built in the past rather than envolving those checks for a new system or application. A common example is to monitor CPU, memory and disk on every host, but not the key services that indicate the application tha runs on the host is functional. If an application can go down without you noticing, even with monitoring in place, then you need to reconsider what you are monitoring.

A good approach to your monitoring is to design a top-down monitoring plan based on value. Identify the parts of the application that delivere value and monitor those first, working your way down the stack.

![]()
Monitoring design

Start with business logic and business outputs, move down to application logic, and finally into infrastructure. This doesn't mean you shouldn't collect infrastructure or operating system metrics they provide value in diagnostics and capacity planning but you're unlikely to need them to report the value of your applications.

**Note**: If you can't start with business metrics, then start monitoring close to the user. They are the ultimate customer and their experience is what driver your business. Understanding what their experience is and detecting when they have issues is valuable in its own right.

### Not monitoring for correctness

Another common variant of this anti-pattern is to monitor the status of services on a host but not the correctness. For example, you may monitor if a web application is running by checking for an HTTP 200 response code. THis tells you the application is responding to connections, but not if it's returning the correct data in response to those requests.

A better aproach is monitoring for the correctness of a service first for example, monitor the content or rates of a business transaction rather than the uptime of the web server it runs on. This allows you to get the value of both: if the content of a service ins't correct because it is misconfigured, buggy, or broken you'll see that. If the content isn't correct because underlying web service goes down, you'll also know that.

### Monitoring statically

A further check anti-pattern is the use of static thresholds for example, alerting if CPU usage on a host exceeds 80 percents. Checks are often inflexible Boolean logic or abitrary static in time thresholds. They generally rely on a specific result or ranage being matched. The checks don't consider the dynamism of most complex systems. A match or a breach in a threshold may be important or could have been triggered by an exceptional event or could even be a natural consequence of growth.

Arbitrary static threshold are almost always wrong. Baron Schwartz, CEO of database performance analysis vendor **[VividCortex, put it well]()**:

They're worse than a broken clock, which is a least right twice a day. A threshold is wrong for any given system, because all systems are slightly different, and it's wrong for any given moment during the day, because systems experience constantly changing load and other circumstances.

To monitor well we need to look at windows of data, not static points in time, and we need to use smarter techniques to calculate values and thresholds.








 






















































