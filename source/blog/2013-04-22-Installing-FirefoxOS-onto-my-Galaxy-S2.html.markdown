---
title: Installing FirefoxOS onto my Galaxy S2
date: '2013-04-22'
tags: brain-dribble
category: brain-dribble
status: draft
---

Hackintosh

I have a spare Samsung Galaxy s2 - battery has gone etc...

MacBookPro - running Mac OSX version 10.7.5

Back up ALL THE THINGS - I will not be held responsible for loss of any data - you are just about to flash your phone, you are just about to wipe ALL data - also this : http://support.mozilla.org/en-US/questions/947298

Following this: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox_OS/Firefox_OS_build_prerequisites?redirectlocale=en-US&redirectslug=Firefox_OS%2FFirefox_OS_build_prerequisites

Upgrade xcode
Make sure I have Command Line Tools installed by opening xCode, going to Preferences and the Download tab. Command Line Tools should be listed there to be installed (or indicated it's already installed).

Make sure I have the right Galaxy s2. <quote>The only model that works is the i9100; no other variants are officially compatible. (i9100P might work, since the only change is a NFC chip added)</quote> You can check by going into Setting -> About Phone. This will tell you the android version you are running as well, which needs to be above 4 (Ice Cream Sandwich).

Strangely (cos I'm not really that lucky) I do have a i9100 and am running android v4.0.3. So I guess I'm good to go.

Right next up is the Firefox OS Mac Bootstrap script, just to make sure I have all the things installed. So Terminal -> 

This took some time on my pooter. There's no ticker when you run the script, and for me it seemed like it had hung after downloading gcc.

I had to uninstall Samsung Kies before I could do anything with the phone, which I had to do via the uninstall program on the install disk image (.dmg). As it's a Samsung Galaxy I had to install Heimdall to flash it. To start with I installed version 1.3.1 as per recommendation on the Heimdall website.

I already have Android SDK installed, but I opened the GUI anyways and made sure the Platform tools was updated.

Created file -> added line

Made sure phone developer mode usb thing was on

Cloned repo - at this point I thought it was a good time to plug into my LAN rather than use the wireless, as it was being pretty flacky and from experience with my network I knew LAN worked faster. It seemed like it was going to be a long process.

ran config galaxy-s2 - said yes to the colour question. Went and got a cup of tea. I ran the config command at 18:52... by around midnight when I went to bed the code still hadn't finished running.

It had however when I woke up in the morning. Everything hunky dory so far.

Now I had to start building by running ./build.sh. This failed. I had two errors. One was 'No 10.6 or 10.5 SDK found, do you have Xcode installed?' and the other 'gcc is linked to llvm-gcc which will not create a useable emulator.'

Let's tackle the first one. Starting from the first page on MDN, it appears a dependancy is SDK 10.6 or 10.5. After looking in /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/ it appears I only have 10.7 and 10.8. Maybe I shouldn't have been so quick to upgrade :S

So long windedly I downloaded xCode 4.3, mounted the dmg (open/double click), viewed in finder, right click -> show package contents -> go to /Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/ grab the MacOSX10.6.sdk folder and copy it into /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/ - you'll most likely have to enter your password.

I thought this might fix the second error, obviously wishfully. That was no the case. Might have something to do with bug in android. Also phone is encrypted and without sim card so reset it to factory settings - and got a cheap pay as you go sim.

Re downloading and installing gcc fixed the second bug, it seemed to get stuck on the 'make bootstrap' command again, but I just left it and this time it finished. Use command brew install https://raw.github.com/mozilla-b2g/B2G/master/scripts/homebrew/gcc-4.6.rb

Now when I run ./build.sh I have no errors. However the build fails because 'Your device has unknown firmware'. The list of supported firmware is UHLPE
XXLPQ
ZSLPF
XWLP7
BGLP8
BGLP9
ZSLPG
XWLPD
XWLPI

You can find out what firmware you are running by going to Applications -> About phone. You're looking for the last 5 letters and numbers of the 'Build number'.

So my firmware version is not in that list - which means I have to get on my phone a firmware version which is. Firstly I checked to see if the phone was rooted, by downloading a route checker on the phone. 'Root Checker Basic'

Administrator user - can update firmware, delete stuf etc... in Linux world this is root. Most firmware prevents you from this user - which means you can't change firmware. I'm not root.

Now i need to root...
