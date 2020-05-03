---
layout: post
section-type: post
title: Python and Robot Framework Installation on Windows
category: Installation
tags: [ 'Python', 'Robot Framework']
---


##### Below are the detailed steps to install Python and robot framework through PIP :-
**Step  1 – Install Python and PIP**
* Go to python.org [Python 3.7](https://www.python.org/downloads/) and download desired version (suggested – 3.7)  

![alt text](../../../../img/python_rf_install/python.jpg)  
*	Check **Add Python 3.7 to path**

![alt text](../../../../img/python_rf_install/add.jpg)

*	Click Install Now
*	Once installation was successful, Go to **cmd** and type ***Python -V***, it will display the installed version.

![alt text](../../../../img/python_rf_install/pycmd.jpg)

*	PIP will get installed with python automatically, use PIP list command in the cmd to check the installation successful or not.

**Step # 2 – Install Robot framework and Selenium library through PIP**

- Use this command ***pip install robotframework*** for robot framework library
- Use this command ***pip install robotframework-seleniumlibrary*** for selenium library
-	Use this command ***pip install robotframework-pabot*** for pabot library for parallel execution
-	Use this command ***pip install robotframework-metrics*** for metrics library
-	Use this command ***pip install -U requests*** for python requests library
-	Use this command ***pip install -U robotframework-requests*** for robotframework requests library


![alt text](../../../../img/python_rf_install/alllib.jpg)

*	Note: you can use ***pip list*** command to see your installation is successful

**Step # 3 – Install Pycharm**
*	Go to this link – [Pycharm downloads](https://www.jetbrains.com/pycharm/download/#section=windows)
*	Download and install ***Community edition***

![alt text](../../../../img/python_rf_install/pycharm.jpg)

*	Click Pycharm installation file
* Complete the Installation

**Step # 4 – Configure Pycharm - intall required plugins**
* Steps to install plug-in
    1.	Open Pycharm
    2.	Go to File –> settings –> Click plug-ins
* Install ***IntelliBot @SeleniumLibrary Patched*** Refer [IntelliBot](https://www.jetbrains.com/pycharm/download/#section=windows)
* Install ***Material Theme UI Plugin*** Refer [Material Theme](https://plugins.jetbrains.com/plugin/8006-material-theme-ui/)
* Install ***CMD Support*** Refer [CMD Support](https://plugins.jetbrains.com/plugin/5834-cmd-support/)

***Please Restart pycharm to activate all the plugins***

**Step # 5 – Download Web drivers and Configure browser settings**

***Purpose of Web Driver: Web driver is a library which helps to communicate between your test automation scripts and browsers***
* Please download [IE web driver](https://www.seleniumhq.org/download/)

![alt text](../../../../img/python_rf_install/IE.jpg)

* Please download [Chrome and Firefox web driver](https://www.seleniumhq.org/download/)

![alt text](../../../../img/python_rf_install/CF.jpg)

* Create a bin directory(**Anywhere**) and copy the downloaded web drivers to bin directory and add Path
* (C:\bin) to environmental variables (***Advanced system settings*** –> ***Environment variables*** –> ***System variables*** –> ***select Path*** –> ***click Edit*** –> ***Add C:\bin directory***)

![alt text](../../../../img/python_rf_install/env.jpg)

***Note: If you add path to Environment variables, Robot framework (SeleniumLibrary) will automatically recognize the web drivers, thereby, you don’t need to explicitly mention web driver path in your test scripts.***

***OR***

We can also add the drivers in the scripts folder of python, As python folder is already added to the Path

![alt text](../../../../img/python_rf_install/pyfolder.jpg)

### References:
[Selenium RB Ubuntu Install](https://5and3.co.uk/articles/effective-website-tests-with-robot-framework-and-selenium/)

[Generic sample implementation](https://www.blazemeter.com/blog/robot-framework-the-ultimate-guide-to-running-your-tests/)

[RF user guide](https://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html)



[RF good Test cases](https://github.com/robotframework/HowToWriteGoodTestCases/blob/master/HowToWriteGoodTestCases.rst)

[Demo app RF demo](https://github.com/robotframework/WebDemo/tree/master/login_tests)

[RF Jupyter](https://nbviewer.jupyter.org/github/robots-from-jupyter/robotkernel/tree/master/examples/)
