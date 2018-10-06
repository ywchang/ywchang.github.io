---
layout: post
title:  "What is Cordova?"
date:   2018-10-06 19:50:00 +0800
categories: tools
---

#### What is Cordova?

Cordova is an open source platform, which aims at building mobile applications by using HTML, CSS and Javascript tech stacks. The former name is called `PhoneGap`, which seems making more sense, in that it tries to fill the gap between the way to develop mobile apps and the way to develop webapp.

#### Why Cordova matters? 

Imagine you are a mobile developer, and you are trying to help your company to delivery a awesome mobile app, which will definitely deliver huge business value to the end users. Now the problem is among the end users, some are using Apple phones, some using Android and some using windows phones. As you may know, to develop app to live in different phone systems, requires totally different technologies. That said you have to master three different ways to develop apps and redo three times. Not to even mention the fact that new features will keep coming all the time.

Now with Cordova, using HTML, CSS and Javascript, once you make it good look in the browser, that means through Cordova, you can already ship app to different targets, Apple, Android and Windows immediately. What an awesome tool!

#### How is it working?

There is a tool named `Cordova CLI`, which is a command line tools available in different platforms, Mac OS, Windows and Linux.

The way it works is similar with maven. Using this cli tool, you can easily create the skeleton of the codes, add platforms to support, and build a package out of the source codes. With the installation of emulator, you can actually see it in the laptop.

Looking into the skeleton of codebase, only the contents inside the folder `www` is interesting to developers because that's where the real business codes live. Typically we can have separate codebase to scaffold and once we want to get a package, we can produce a compressed output static codes and embed it within this cordova codebase.