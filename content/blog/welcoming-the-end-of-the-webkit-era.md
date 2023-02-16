---
title: "Welcoming the end of the WebKit era (maybe)"
date: 2023-02-16T17:42:17+01:00
description: "Test"
draft: false
tags: [app, ios, webkit]
---
### Apple considers dropping the iOS WebKit requirement

For many years, since the first release of iOS, one of the rules of being in the App Store as a browser has menat that what Apple says goes - and this includes all web browsers being required to use Apple's WebKit rendering engine.

#### Why exactly has Apple insisted on this requirement?

To put things into context, it would be worthwile to take a step back and examine the reasons why Apple has this WebKit requirement for iOS based browsers. As [part of their response to the US House Judiciary Subcommittee on Antitrust back in July 2019](https://www.congress.gov/116/meeting/house/109793/documents/HHRG-116-JU05-20190716-SD036.pdf), they were rather open with their reasoning;

> ... "4. Does Apple restrict, in any way, the ability of competing web browsers to deploy
their own web browsing engines when running on Apple’s operating system? If yes,
please describe any restrictions that Apple imposes and all the reasons for doing so.
If no, please explain why not.
>
> All iOS apps that browse the web are required to use “the appropriate WebKit framework
and WebKit Javascript” pursuant to Section 2.5.6 of the App Store Review Guidelines
<https://developer.apple.com/app-store/review/guidelines/#software-requirements> ..."

At this point, we might think "Well, it is their App Store after all - their house, their rules. All seems fair enough" Apple expands on their justifcation, specifically citing privacy and security as the main drivers (paragraphs are mine, to improve readability):

>The purpose of this rule is to protect user privacy and security. Nefarious websites have analyzed other web browser engines and found flaws that have not been disclosed, and exploit those flaws when a user goes to a particular website to silently violate user privacy or security. This presents an acute danger to users, considering the vast amount of private and sensitive data that is typically accessed on a mobile device.
> 
>By requiring apps to use WebKit, Apple can rapidly and accurately address exploits across our entire user base and most effectively secure their privacy and security. Also, allowing other web browser engines could put users at risk if developers abandon their apps or fail to address a security flaw quickly. By requiring use of WebKit, Apple can provide security updates to all our users quickly and accurately, no matter which browser they decide to download from the App Store.

#### That all sounds pretty reasonable, doesn't it? So why might Apple get rid of the requirement?

Although the development teams of both Chrome and Firefox have [been complaining for a number of years now](#) 

_**But what does this mean exactly? And what would dropping the requirement mean for the future?**_

In practice it means that any browser on iOS devices is essentially Safari with a different look. Chrome, Firefox, and Brave are simply Safari by any other name, for the most part (we'll get to the exceptions later).



