---
layout: post
section-type: post
title: Selenium WebDriver arcitecture
category: Category
tags: [ 'Selenium' ]
---

### The Basics

1.Selenium WebDriver is a browser automation framework that allows you to execute your tests against different browser.

2.WebDriver interacts and controls the actual browser in either locally or remotely. 

3.We can use WebDriver to automate and validate Web-Applications.

### How selenium WebDriver Works Internally
 
Let’s take a look at the below architecture:

![alt text](../../../../img/Architecture/large.jpeg)

![alt text](../../../../img/Architecture/SWebDriverArchi.png)

![alt text](../../../../img/Architecture/RPexplain.jpg)

The above picture depicts, there are four components of Selenium Architecture:
 
1.Selenium Client Library

2.JSON Wire Protocol over HTTP

3.Browser Drivers

4.Browsers
 
We will try to understand each of these four components briefly:
 
1.Selenium Client Library
 
Selenium supports multiple libraries such as Java, Ruby, Python, etc.
It means that we can write our code with any of these scripting/programming languages.
Selenium Client Library sends the request in the form of API to the Browser Driver with the help of JSON Wire Protocol over HTTP (hypertext Transfer Protocol).

2.JSON Wire Protocol over HTTP

JSON stands for JavaScript Object Notation. It is a lightweight data-interchange format which transfers the data between a server and a client on the web.
JSON Wire Protocol is a REST API that transfers the data between HTTP server .Every Browser Driver uses a HTTP server to receive HTTP requests.

3.Browser Driver

Browser Drivers are used to communicate with browsers.
Each browser has its specific Browser WebDriver.
When a browser driver is received any command then that command will be executed on the respective browser and the response will go back in the form of HTTP response.
Following are the operations performed when we run our automation script using specific Browser driver:
 
1.For each Selenium command, a HTTP () request is created and sent to the browser driver.

2.The browser driver uses a HTTP server for getting the HTTP requests.

3.HTTP Server sends all the steps to perform a function which are executed on the browser.

4.The HTTP server sends the status back to the automation script.

 
3.Browsers
 
Selenium supports multiple browsers such as Firefox, Chrome, IE, Safari etc.

4.Now, let’s see what will happen internally when you execute the above script:
 
1.Upon executing the above code, Selenium client library (java) will convert the automation script to Rest API and communicates with the Chrome Driver over JSON Wire Protocol. 

2.Once API interacts with Browser Driver, then the Browser Driver will pass that request to the browser over HTTP and then the commands in your selenium script will be executed on the browser.

3.Based on the Rest Methods Type: Get/Post/Delete, response will be generated on the browser end and it will be sent over HTTP to the browser driver and from the Browser Driver over JSON Wire Protocol sends it to the UI Console.

4.Click on this link for complete understanding of JSON Wire Protocol

Let’s try understanding this with an example:
 
Below are the API’s gets evoked when we write any operation using selenium .
For example, when we write
```
driver.get(“url”)
```

below highlighted API will be executed Internally.

![alt text](../../../../img/Architecture/APIpayload.png)