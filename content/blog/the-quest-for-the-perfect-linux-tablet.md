---
title: 'In search of the perfect Linux tablet (or close enough...)'
date: 2023-04-06T21:13:00+01:00
description:
toc: true
draft: false
tags: []
---

This post ended up being quite long, so feel free to use the Table of Contents to skip through and get to the relevant parts for you!

### Introduction

As much as I love a decently sized screen (ideally a 15" laptop), sometimes it isn't entirely practical. This is especially true when travelling or at a coffee shop when I already have my work laptop in my bag along with everything else. For that reason, I wanted something smaller that I could still use to update this blog, take notes, and do light coding with.

The obvious choice would have been some kind of traditional tablet like an iPad, or any flavour of Android ones currently on the market. But even with plenty of devices to choose from (which all would have done a fine job of media consumption or reading the occasional book or PDF), the idea of being limited by a certain file manager (iPad), giving up all my data to Google (any Android tablet), and the possibility of a not so great keyboard attachment left me wanting more.

For a while, I almost resigned myself to just buying a 13" laptop, but I had some qualms about how portable it was going to be when travelling with a work laptop, toiletries, and clothes already taking up space/weight in my rucksack. In the back of my mind, I also wanted the possibility of being able to use Linux rather than being stuck with ChromeOS or Windows. Eventually, I stumbled across an unlikely candidate - a Microsoft Surface Go 3 (the latest at the time of writing). 

I'll admit, I've owned the first version of the Surface Go (not for very long, mind you!) but at that point in time, there was no project ongoing with the sole purpose of making them run Linux. Although I loved the size and portability of it, Windows itself was always the major sticking point considering the Go devices themselves aren't exactly powerhouses... But with the [linux-surface](https://github.com/linux-surface/linux-surface) project, things were looking up!

Getting the Surface (many different types, suprisingly) running Linux is incredibly straightforward, though I did have a few hiccups along the way. So, for the sake of documenting it for myself (at least as of April 2023) and for anyone else who wants to do the same, here's how to get your Surface Go up and running with Ubuntu (22.10 being the latest version at the time of writing).

### Some prerequisites

For this to work, you're going to need a few things:

- Your Microsoft Surface device charged to at least 40% or more
- A USB stick that has a USB-C connection - **please do not skip this, save yourself some hassle instead**

### First boot

To get started, turn on your Surface Go and start going through the first time set up of Windows. To give ourselves the best chance of everything being functional when we wipe it and install Linux, unfortunately we need Windows around a little longer. 

The Wi-Fi connection option is where we hit our first roadblock - if you connect the Surface to a network and continue through the setup, you'll be in for a rude surprise when it becomes clear that you can't go further without singing into an existing Microsoft account or creating a new one. Instead, hit Fn + F10 which will bring up a command prompt and enter the following command (note the backslash rather than forward slash):

```bash
OOBE\bypassnro
```

This will then allow you to go on with creating an offline local account, which is all we need.

Once you are at the Windows desktop, hit the Windows key and type "Settings", then choose "Updates". For our purposes we don't care about Windows updates themselves (though they'll be installed regardless) - but we do care about firmware updates*. Ensure that all firmware updates for the Go are installed. It might take a while, so feel free to go and do something else whilst this is happening... 

---

*If you happen to see the message "Plug in your device to continue installing this update" even though your Surface is already plugged in to charge, it means that Windows has got itself into a bit of a pickle. To fix this issue:

- Press the Windows key, enter "Services"
- Right click on "Services" that shows up as an application and choose "Run as administrator" and accept the User Account Control (UAC) prompt
- Scroll down to "Windows update", right click and select "Properties"
- Choose "Manual" as the start up type
- Restart the service

---

### Preparing to install Ubuntu

At this point, all firmware updates should be finished, and your Surface Go will have restarted a number of times during the process. Now that we have that out of the way, we can take our USB stick (with a USB-C connection as noted above) and plug it into the Surface Go.

Next, head to the ]Canonical website to download Ubuntu}(https://ubuntu.com/download/desktop). Whilst you have your browser open, open a new tab and [download Balena Etcher along with it](https://www.balena.io/etcher). We'll use Etcher to make a bootable USB of Ubuntu so that we can install it on our Surface.

Once both files have been downloaded, open Etcher and click "Select image", Here, pick the Ubuntu iso file we just downloaded. Click "Select device" and choose the USB stick that is plugged into the Surface. Finally, click "Flash" and wait till it says the flashing process is complete.

### Installing Ubuntu

Before we install Ubuntu, there's one last thing we need to do: turn off Secure Boot. Although Ubuntu supports Secure Boot, for some reason, my Surface really didn't like it when trying to install Ubuntu for the first time. We'll turn it back on later towards the end of this post. 

To turn off Secure Boot, shut down your Surface. As you go to turn it on again (before pressing the power button), press and hold down the volume up button. With it depressed, press the power button. Let go of the volume up button once you see the loading animation appear. You should now be at the BIOS. 

In the BIOS, select the "Security" menu option and change the Secure Boot option to "None", then save and exit your changes.

You now have two ways of getting the Surface Go to boot from your newly created Ubuntu USB. Feel free to try either, but I only had luck with the option 2.

1. Press the Windows key and search for "Recovery" - you should see an option for it, which will take you to recovery options for the device, Select "Advanced" and choose "From USB stick". Your Surface should now restart from your USB stick instead of the SSD.
2. Completely shut down your Surface and boot to the BIOS (outlined above), except this time change the start up option by moving the entry for your USB stick to the top of the list (pressing and dragging should do the trick)

If you were successful, you should now see the same loading animation you've seen previously, but this time also an Ubuntu logo.

Go through the Ubuntu installation setup - either you can choose to install Ubuntu alongside Windows, or wipe Windows altogether. Personally, I prefer to get rid of Windows altogether because the Surface Go only has a 128GB SSD, meaning space is at a premium.

### Post-install

Congratulations! You've now got a tablet that you can:

- Use as a regular media consumption device
- Use to sketch/draw with if you've purchased the Surface Pen
- Read with - though it isn't as compact as a Kindle!
- Still have a full OS on and do light productivity work (coding, note taking, blogging) without being stuck with a tablet OS

If you really want to, you can stop here, but it would be worthwhile installing the linux-surface kernel to get the most out of your device. To do so, run the following commands (ignoring any line starting with "#"):

```bash
# This command is to import the keys used to sign linux-surface packages
wget -qO - https://raw.githubusercontent.com/linux-surface/linux-surface/master/pkg/keys/surface.asc \
    | gpg --dearmor | sudo dd of=/etc/apt/trusted.gpg.d/linux-surface.gpg
```

```bash
# Adding the repository configuration 
echo "deb [arch=amd64] https://pkg.surfacelinux.com/debian release main" \
  | sudo tee /etc/apt/sources.list.d/linux-surface.list
```

```bash
# Updating our packages and installing the linux-surface packages
sudo apt update && sudo apt install linux-image-surface linux-headers-surface libwacom-surface iptsd
```

### Re-enabling Secure Boot

If you want to re-enable Secure Boot, you'll need to import the linux-surface Secure Boot key:

```bash
sudo apt install linux-surface-secureboot-mok
```

Shut down your Surface entirely and press and hold the volume up and power button (to enter the BIOS, like before). Under the Secure Boot option, change "None" to "Microosft and 3rd Party CA". After exiting you'll then be presented with the the MOK enrollment screen. Choose "MOK enrollment", select "Yes", and your Surface should then boot to the Ubuntu login screen.

### Conclusion (...and fixing small annoyances)

After replacing Ubuntu with Windows, the Surface Go 3 is much snappier - as a result, I'm looking forward to being able to use this device for many years to come. Surprisingly, everything except the webcam (which I don't plan on using) works straight out of the box, so there's very little fiddling to do with settings and configuration after install. 

The only thing I did notice was that by default, scrolling with the touchpad or with a finger (if using in tablet mode) won't work by default. To fix this, open Firefox and in a new tab enter ```bash about:config```, then search for ```bash dom.w3c_touch_events.enabled``` Change 2 to 1 and close the tab. To make the change permanent, open a new terminal and enter ```bash echo "MOZ_USE_XINPUT2=1" | sudo tee /etc/environment```. Finally, log out, and log in again. 

That's it - enjoy your new Surface! In the next post I'll look at useful applications you can install for drawing/taking notes.




