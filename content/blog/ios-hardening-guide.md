---
title: "iOS Hardening Guide"
date: 2023-06-22T19:51:46+02:00
description: "A hardening guide for iOS 16 from first boot"
toc: false
draft: true
tags: []
---

# Introduction
This originally started as a checklist for myself for when I set up an iOS device so that I don't need to try and remember all the steps I've taken/all the settings I've toggled on/off, but decided to turn it into a blog post in case it's of use to anyone else.

This post isn't going to cover specific apps or tecnhiques to reduce data collection/ be more private - that'll be for another post some time next week. For now we're only going to deal with configuring default iOS settings to secure your device as much as possible, reducing the attack surface where we can. Before we dig in, it's worth talking a little bit about threat modelling - because that's going to be the basis for a) if you care about implementing any of this at all, or b) how far you're going to take things if you decide to implement everything and more.

[Threat modelling section goes here]

# Initial boot (Part 1)

Upon first boot: 
- Select the language you'd like to use your device in and the region where you're located. 
- When presented with the "Quick Start" screen, choose "Set Up Manually". Confirm your language and keyboard settings (or change them if needed). 
- Connect to your Wi-Fi network (you can continue on just mobile data, but I wouldn't recommend it). Wait a minute or two whilst your device activates.
- Choose "Continue" when presented with the "Data & Privacy" screen. Feel free to set up Face ID - or choose "Set Up Later"

## Passcode

At the "Create a Passcode" screen choose "Passcode Options" and select "Custom Alphanumeric Code". Here you can set something longer than a 6 digit passcode. If you can't think of something specifically alphanumeric, you can set a passphrase instead - ideally the longer the better. It doesn't matter if it's part of as sentence from your favourite book or poem, or 4 or 5 random words so long as it's something you can quickly recall and isn't something that someone else would easily be able to guess.

After setting a robust passcode/phrase, you'll come to the "Apps & Data" screen. Choose "Don't Transfer Apps & Data"...

# Your Apple ID

Once you've chosen not to transfer anything you'll be asked to sign in with your Apple ID. Here, there are a few choices you can make depending on your threat model...

- Can create a new one (no point, expand on why)
- Can use an existing one (this is okay)
- Can separate the Apple IDs used for iCloud and App Store so they are independent - "Use different Apple IDs for iCloud & other Apple services?" Will be asked to enter Apple ID used for iCloud

- Will be choosing to just use an existing Apple ID (because we'll be disabling iCloud later and tweaking a few more settings)

- Agree to Terms and Conditions and wait a few minutes for your Apple ID to be set up

# Initial boot (Part 2)

- Choose whether you will enable or disable location services. I tend to deny all and then go back and change it for specific applications once I've installed things.

- Choose whether you want to set up Apple Pay (or you can do this later at any time from the Settings)

# iCloud Keychain

- Choose to not use iCloud Keychain 

Spiel: Apple allows you to chang settings about your device (such as accessing keychain etc with just your device passcode - hopefully you picked a strong alphanumeric one above). Means that anyone who gains access to your phone (e.g. if they've been sitting looking over your shoulder at a bar and watch you enter the passcode, they can lock you out of everything,take over your Apple ID for iCloud/the App Store and also have access to any passwords for applications that you happend to store in Keychain)

# Initial boot (Part 3)

- Set up Screentime (or ignore it and choose "Set Up Later in Settings)
- On the "iPhone Analytics" screen choose "Don't share"
- Choose whether you would like to use the light or dark theme on the "Appearance" screen
- Choose your Display Zoom
- Swipe up and you'll be presented with the default homescreen.

Now we can start removing applications we don't need...

# Removing default applications

[Points about reducing attack surface here]

Applications I uninstall immediately (in no particular order) because we're going to replace them with some better alternatives in the post following this:

- Remove any widgets
- Mail
- Notes
- TV
- Health
- Wallet
- Music
- Find My
- Shortcuts
- Home
- Stocks
- Translate
- Books
- iTunes Store
- Fitness
- Watch
- Tips
- Voice Memos
- Compass
- Measure
- Magnifier

Many of these applications are not actually uninstalled, just "hidden". Regardless, if we don't plan on using them, then they may as well not take up space on our device.

# Reconfiguring iCloud settings

# Changing default settings

## Notifications

## Sound and Haptics

## Focus

## General

## Siri & Search

## FaceID & Passcode

## Exposure Notifications

## Privacy & Security

## App Store

## Wallet & Apple Pay

## Passwords

## Contacts

## Calendar

## Reminders

## Messages

## FaceTime

## Safari



