---
layout: post
section-type: post
title: What is Appium & How it Works?
category: Appium
tags: [ 'Architecture', 'Basics' ]
---

## What is Appium?

Appium is an open source, cross-platform automation testing tool. It is used for automating test cases for native, hybrid and web applications. The tool has a major focus on both Android and iOS apps

## How Does it work?
Appium is a simple HTTP server that is written using Javascript. It follows the generic client-server architecture. The Appium server processes requests from the Appium client and forwards them to the simulator/emulator/real device where the test scripts are automated. The results of the test are communicated to the Appium client through the Appium server, in the form of a server response.

## Appium Concepts
In the below section, we are going to discuss three key concepts, that are intrinsic to Appium’s architecture.

### Appium Client-Server Architecture
Appium at its heart is a server written in node.js. The server works using a client-server architecture. According to the client-server architecture, the client connects to the server to avail any service hosted on the server. Any communication between the client and server is in the form of response and requests.
In Appium the client sends requests regarding automation to the Appium server. The server processes the request in its own unique way, which we will get to in a second,  and then responds with the test result or log files.

### Appium Sessions
Everything ‘testing’, is done encapsulated in a session. This is pretty obvious given the fact Appium is a simple client and server-based mechanism. The client sends post requests, also known as session requests to the server. These requests carry information in a JSON Object format, and communication is executed using the JSON Wire Protocol.

### Desired Capabilities
Appium works differently on iOS and Android. Now since it is a “cross-platform” tool, a mechanism must exist to differentiate between the two operating system’s session requests. This particular problem statement was also addressed with the help of JSON objects, called Desired Capabilities, as shown in the image below.

![alt text](../../../../img/Architecture/Desired-Capabilities.png)

Desired Capabilities are key-value pairs of information that distinguish the establishment of a session for the testing of an Android app to that of an iOS app. With arguments like-
```
platformName
deviceName
appPackage
appActivity
```
It becomes fairly easy for the server to distinguish between the two operating systems.

## JSON Wire Protocol
The JSON Wire Protocol is the mechanism used for communicating between client and server. It is developed by the webDriver developers. According to them, the protocol is a bunch of standardised endpoints that are exposed to the client using a RESTful API. This allows the webdriver to establish communication with a server and a client to perform automation.

Appium uses the mobile JSON Wire Protocol, which is an extension to the Selenium JSON Wire Protocol. It is used to control different mobile phone behaviours other than just setting up a communication stream. 

## Appium Architecture

![alt text](../../../../img/Architecture/Appium-Architect.png)

![alt text](../../../../img/Architecture/AppiumArchi.png)

1.Appium is an HTTP server written using node.js

2.The client communicates to the server using a session, where key elements of the communication process is sent with the help JSON objects. Communication is handled by the mobile JSON Wire Protocol.

3.The server differentiates between an iOS request and an Android request using the desiredCapabilites arguments.

4.Appium server then processes the request to the respective UI Automators as seen in the Appium architecture diagram below.

5.The UI Automator then processes the request and executes the command on a simulator/emulator/real device.

6.The results of the test session are then communicated to the server and then back to the client system in terms of logs, using the mobile JSON Wire Protocol.

# Appium on Android
Appium on Android uses the UIAutomator framework for automation. UIAutomator is a framework built by android for automation purposes. So, let’s take a look at the exact way that Appium works on Android.

1.Appium client (c/Java/Python/etc) connects with Appium Server and communicates via JSON Wire Protocol.

2.Appium Server then creates an automation session for the client and also checks the desired capabilities of the client. It then connects with the respective vendor-provided frameworks like UIAutomator.

3.UIAutomator will then communicate with bootstrap.jar which is running in simulator/emulator/real device for performing client operations.

4.Here, bootstrap.jar plays the role of a TCP server, which we can use to send the test command in order to perform the action on the Android device using UIAutomator.

5.The Appium android architecture diagram below gives a visual representation of the above steps.

![alt text](../../../../img/Architecture/AppiumArchi3.png)

# Appium on iOS

On an iOS device, Appium uses Apple’s XCUI Test API to interact with the UI elements.  XCUITest is the automation framework that ships with Apple’s XCode. 

1.Appium client (c/Java/Python/etc) connects with Appium Server and communicates via JSON Wire Protocol.

2.Appium Server then creates an automation session for the client and also checks the desired capabilities of the client and connects with the respective vendor-provided framework like XCUI Test.

3.XCUI Test will then communicate with bootstrap.js which is running in a simulator/emulator/real device for performing client operations.

4.Bootstrap.js will perform the action on our application that is being tested. After the execution of the command, the client sends back the message to the Appium server with the log details of the executed command.

![alt text](../../../../img/Architecture/AppiumArchi4.png)