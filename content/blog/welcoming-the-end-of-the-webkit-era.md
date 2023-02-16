---
title: "Welcoming the end of the WebKit era (maybe)"
date: 2023-02-16T17:42:17+01:00
description: "Test"
draft: false
tags: [apple, ios, webkit]
---

### Apple considers dropping the iOS WebKit requirement

For many years (since the first release of iOS), one of the rules of being in the App Store as a browser has meant that what Apple says goes - including all web browsers being required to use Apple's WebKit rendering engine.

#### Why exactly has Apple insisted on this requirement?

To put things into context, it would be worth taking a step back and examine the reasons why Apple has this WebKit requirement for iOS based browsers. As [part of their response to the US House Judiciary Subcommittee on Antitrust back in July 2019](https://www.congress.gov/116/meeting/house/109793/documents/HHRG-116-JU05-20190716-SD036.pdf), they were rather open with their reasoning;

> ..."4. Does Apple restrict, in any way, the ability of competing web browsers to deploy their own web browsing engines when running on Apple’s operating system? If yes, please describe any restrictions that Apple imposes and all the reasons for doing so. If no, please explain why not.
>
> All iOS apps that browse the web are required to use “the appropriate WebKit framework and WebKit JavaScript” pursuant to Section 2.5.6 of the App Store Review Guidelines <https://developer.apple.com/app-store/review/guidelines/#software-requirements>..."

Alongside it simply being what you agree to in order to be seen on their App Store, Apple goes on to cite privacy and security as the main drivers (paragraphs are mine, to improve readability):

>"The purpose of this rule is to protect user privacy and security. Nefarious websites have analysed other web browser engines and found flaws that have not been disclosed, and exploit those flaws when a user goes to a particular website to silently violate user privacy or security. This presents an acute danger to users, considering the vast amount of private and sensitive data that is typically accessed on a mobile device.
>
>By requiring apps to use WebKit, Apple can rapidly and accurately address exploits across our entire user base and most effectively secure their privacy and security. Also, allowing other web browser engines could put users at risk if developers abandon their apps or fail to address a security flaw quickly. By requiring use of WebKit, Apple can provide security updates to all our users quickly and accurately, no matter which browser they decide to download from the App Store..."

#### That all sounds pretty reasonable. So, why might Apple get rid of the requirement?

Although the development teams of both Chrome and Firefox have [been complaining for a number of years now](https://9to5google.com/2021/05/03/ios-browsers-underpowered-apple/), the push that has Apple considering the decision is primarily down to the fact that it's simply a finer point in the larger on-going case to allow third-party app stores on iOS as part of the [European Commission's Digital Markets Act](https://commission.europa.eu/strategy-and-policy/priorities-2019-2024/europe-fit-digital-age/digital-markets-act-ensuring-fair-and-open-digital-markets_en) (DMA). 

A summary of what said DMA entails:

>  "...The Digital Markets Act (DMA) establishes a set of  narrowly defined objective criteria for qualifying a large online  platform as a so-called “gatekeeper”. This allows the DMA to remain well targeted to the problem that it aims to tackle as regards large,  systemic online platforms.
>
>  These criteria will be met if a company:
>
>  - has a strong economic position, significant impact on the internal market and is active in multiple EU countries
>  - has a strong intermediation position, meaning that it links a large user base to a large number of businesses
>  - has (or is about to have) an entrenched and durable position in the market, meaning that it is stable over time if the company met the two criteria above in each of the last three financial years..."

Although the criteria are somewhat broad, it does seem as though it has Apple squarely in its sights...

#### If the WebKit requirement is dropped, what exactly does that mean for my iPhone and iPad in the future?

Overall, it means that other browsers can offer new features and there will be some feature parity with Android, It also means that the development of these other browsers is not tied to the update and release cycle of WebKit itself. 

By no longer having this anchor, it might (though this is a bit might depending on how generous Apple is feeling with their API libraries) even be possible to build workarounds for features that are reserved solely for Safari on iOS itself. These include:

- the ability to choose full screen video
- install web apps (more on this below)
- use browser extensions (this is already a possibility with Chrome, Firefox and Edge on Android)
- integrate Apple Pay

**Circling back to browser extensions**

Because this blog is primarily focused on security and privacy, the browser extension point is of particular interest to me. One of the things I left out of that list above that is incredibly important from a privacy perspective <u>is the fact that non-Safari WebKit browsers in their current state are not allowed (by Apple) to implement Apple's own Intelligent Tracking Prevention (ITP) which limits the use of cookies in a first-party context</u>,

Being able to use browser extensions such as Ublock Origin, Firefox Containers, or NoScript, Chrome and Firefox would be able to improve and maintain users privacy whilst they browse the web.

**Progressive Web Apps (PWA) may gradually become first-class citizens**

If is is possible to not be reliant on Apple's APIs, then full PWAs that function exactly like apps could be a reality. I have a funny feeling this might even be the first way tested in terms of a "third-party" app store - with exactly no App Store at all. Why bother when you can immediately choose "Add to home screen" and be on your way? 

Further, if they are allowed to integrate Apple Pay into their browsers, Apple may even still be able to take a small cut of purchases for app features that are subscription based. At the end of it all, we may be in some odd middle ground.

**Your old iOS devices get a longer lease of life**

The dusty iPad sitting in a drawer. Or maybe you gave it to your child to keep them entertained for those 30 minutes of peace you've been wanting. Or maybe it ended up with an elderly relative who isn't quite savvy enough to use a computer without 2 hours of your time in the process. Whatever the scenario is, the last "proper" use of that iPad would be for web browsing - whether it's YouTube or online banking. 

With things as they are now though, that iPad has been rendered completely useless because it needs an up-to-date version of Safari. The problem is, that the version of Safari you need is tied to iOS updates - and those ran out a few years ago meaning you're stuck. 

By allowing non-WebKit browsers, assuming the iPad isn't completely ancient, it means you'll be able to install Chrome, or Edge, or Firefox instead and breathe a new lease of life into your devices.

**Google and Mozilla browser teams can consolidate some of their work**

By allowing non-WebKit browsers, Google and Mozilla can:

- use same engine as desktop (Blink, and Gecko respectively). There would no longer be a need for specific iOS WebKit target releases when you can re-use some of the code base that you've been working on for so long.
- Related to the point above, this all works towards speeding up development for getting a non-WebKit browser into the App Store should Apple actually go through with dropping the requirement. [Both Google and Mozilla have already started work on it](https://www.theregister.com/2023/02/07/mozilla_google_apple_webkit/).
- release patches for vulnerabilities quicker -  there is no need to wait on Apple to update the underlying WebKit engine before a fix can be pushed.

**Everyone gets a faster browser**

Due to the fact that all browsers are WebKit based, this rules out the possibility to build a quicker browser than Safari itself. If the requirement changes, Google and Mozilla can begin to optimise properly for iOS devices which is a win-win for everyone (except Apple of course...)