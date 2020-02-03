---
layout: post
section-type: post
title: Charles Proxy Setup - iOS and Andriod
category: Installation
tags: [ 'Charles proxy', 'iOS', 'Andriod' ]
---


This article is a tutorial on how to configure Charles Proxy to inspect traffic over cellular networks, and while it’s designed with ad operations use cases in mind, it’s applicable to any front end web developer with similar needs.

There are many articles out there on how to use Charles Proxy through your phone – I’ve written two myself, in fact. All those articles assume you’re leveraging a Wifi network when connecting to the internet, however and while that’s fine for basic testing on mobile web and mobile apps, there are often reasons why you want to inspect traffic over a true cellular network instead.

Perhaps you need to debug an ad that relies on carrier targeting, or you want to measure data usage or network latency through a true cellular connection.  These are more advanced use cases to be sure, but when you can’t get by with using your phone with Charles over Wifi, or a mobile emulator in Developer Tools.  Plus, Charles Proxy offers a host of powerful features like breakpoints, which you can use to test an experience in stages, or rewrite rules to reference a local file before you update your server, or blacklisting, which can be helpful to isolate the root of various technical problems.

##### The Hardware Setup Before you start, you’ll need:

A laptop running Charles Proxy.  I’m using a Mac in this case, but you could do this with a PC as well.
Two phones, at least one which can be enabled as a mobile hotspot.  I’m using two iPhone 7 in this case, but you could do this with Android devices as well.
Yes, unfortunately you’ll need two phones to setup this rig – the first is used as a mobile hotspot, the second to actually browse the web / app you need to test.  The reason you can’t simply run the connection over a single phone is because you have to manually set the IP address and port of your network connection for Charles to inspect your traffic, and you can’t do that on your phone’s cellular connection.  Creating a mobile hotspot however gives you the ability the adjust those settings on the device connecting through it.  So you’re using one phone for its mobile network and the other phone as the client that proxies requests through Charles.

![alt text](../../../../img/CharlesProxy/CPArch.jpg)

In this configuration, Phone 2 (the client) is what you would browse your website / app on.  Phone 2 makes requests (1) to Phone 1’s hotspot network, which would normally connect directly to the internet, but in this case has its requests (2) intercepted by Charles (the proxy), which records (5) and then forwards the requests to the end server on the internet (3).  When the server responds (4), the whole process happens in reverse.  Charles intercepts the response, records it (5), sends it on to phone 1 (6), which then sends the final response to phone 2 (7).  In this case, the laptop is essentially acting as a host for Charles and Phone 1 is acting as a router.

If that all makes sense, you’re ready to start on the actual configuration.  I struggled a bit setting this up myself for the first time, so I’ve tried to document it in detail.

Add the Charles Proxy Root Certificates To Your Laptop
If this is your first time using Charles, you first need to download the Charles SSL certificate on both phones as well as your laptop. While I won’t go into how SSL communication works here, Charles needs this certificate so it can handle secure requests between your browser and web servers and decrypt the content.

If you don’t complete this step, you’ll see security warnings from your browser any time you go to a secure webpage, not to mention all the content you see in Charles will be encrypted and unreadable.  You’d be surprised how much of ad tech runs on secure protocol, so I’d highly recommended you complete this step.  To read more about what the Charles root certificate does, see the documentation here.  These steps are for Mac; you’ll follow a different process for PC which are described on the Charles website.

Step 1: Open Charles and navigate to Help > SSL Proxying > Save Charles Root Certificate.  This will add the necessary certificate to your computer, but won’t enable it just yet.

![alt text](../../../../img/CharlesProxy/Install-Charles-Root-SSL-Certificate-Laptop.png)

Step 2: From here, you may have to unlock your System Keychain so you can add the Charles Certificate and Modify its trust settings so your computer will allow the certificate to be used. You’ll likely get an error that prompts you to do this automatically.

Step 3: Click the ‘System’ folder, and then click the lock icon above. You’ll have to enter your laptop password as a security precaution.

![alt text](../../../../img/CharlesProxy/Charles-Root-Certificate-Keychain.png)

Step 4: Now, you should see the Charles root certificate listed. Right-click on it, and navigate to ‘Get Info’.

Step 5: Now, under ‘Trust Settings’, change the setting for ‘When Using this certificate’ to ‘Always Trust’.

![alt text](../../../../img/CharlesProxy/Charles-Root-Certificate-Trust-Settings.png)

Step 6: Now, you should be able to navigate to any webpage on your browser, and see that SSL connections go through and are decrypted in the Charles application.

##### Add the Charles Proxy Root Certificates To Your Phones using below references:


#### References:
[For iOS setup1](https://benoitpasquier.com/charles-ssl-proxy-ios/)

[For iOS setup2](https://www.raywenderlich.com/1827524-charles-proxy-tutorial-for-ios)

[For Andriod setup 1](https://community.tealiumiq.com/t5/Tealium-for-Android/Setting-up-Charles-to-Proxy-your-Android-Device/ta-p/5121)

[For Andriod setup 2](https://www.youtube.com/watch?v=pubDgXKUXok)

[For Andriod setup 3](https://medium.com/@hackupstate/using-charles-proxy-to-debug-android-ssl-traffic-e61fc38760f7)

[For Andriod setup 4](https://stackoverflow.com/questions/17823434/ssl-proxy-charles-and-android-trouble)

[For Andriod setup 5](https://willowtreeapps.com/ideas/a-quick-guide-to-charles-a-web-debugging-proxy-application)
 