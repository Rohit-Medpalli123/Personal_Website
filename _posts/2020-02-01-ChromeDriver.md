---
layout: post
section-type: post
title: Installing ChromeDriver and xvfb on Ubuntu
category: Installation
tags: [ 'ChromeDriver', 'xvfb' ]
---

### Installing Selenium,ChromeDriver and xvfb on Ubuntu
 **xvfb** (X windows virtual framebuffer)

I recently got Selenium, Google Chrome, and ChromeDriver installed and working on a VM running 64-bit Ubuntu Here’s how:

First, install Google Chrome for Debian/Ubuntu:
```
sudo apt-get install libxss1 libappindicator1 libindicator7

wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

sudo dpkg -i google-chrome*.deb

sudo apt-get install -f
```
Now, let’s install xvfb so we can run Chrome headlessly:

```
sudo apt-get install xvfb
```

Install ChromeDriver:

```
sudo apt-get install unzip

wget -N http://chromedriver.storage.googleapis.com/2.26/chromedriver_linux64.zip

unzip chromedriver_linux64.zip

chmod +x chromedriver

sudo mv -f chromedriver /usr/local/share/chromedriver

sudo ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver

sudo ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
```
Try the above steps, if that doesn't work then try below additional steps for XVFB:
```
# Dependencies to make "headless" chrome/selenium work:

sudo apt-get -y install xvfb gtk2-engines-pixbuf

sudo apt-get -y install xfonts-cyrillic xfonts-100dpi xfonts-75dpi xfonts-base xfonts-scalable

echo "Starting X virtual framebuffer (Xvfb) in background..."

# Run Xvfb in the background and specify a display number (10 in my example) and Set the DISPLAY variable to the number you chose:
Xvfb -ac :10 -screen 0 1280x1024x16 &
export DISPLAY=:99
```
Install some Python dependencies and Selenium:
```
# Install pip:
sudo apt-get install python-pip

## (Optional) Create and enter a virtual environment:
sudo apt-get install python-virtualenv

virtualenv env

source env/bin/activate

# Install Selenium and pyvirtualdisplay:
pip install pyvirtualdisplay selenium
```
Now, we can do stuff like this with Selenium in Python:

```
from pyvirtualdisplay import Display
from selenium import webdriver

display = Display(visible=0, size=(800, 600))
display.start()
driver = webdriver.Chrome()
driver.get('http://christopher.su')
print driver.title
```

### Using XVFB with Robot framework:
Use the library mentioned Below


### Footnotes:
1: You can find all the ChromeDriver releases here. If you’re using a 32-bit system or a non-Linux OS, the ChromeDriver download used above won’t work.

### References:
1.[Ref 1](https://christopher.su/2015/selenium-chromedriver-ubuntu/)

2.[Ref 2](https://gist.github.com/keepitsimple/a0aa7a2e10ab930d741d)

3.[Ref 3](https://medium.com/@griggheo/running-selenium-webdriver-tests-using-firefox-headless-mode-on-ubuntu-d32500bb6af2)

4.[Ref 4](https://askubuntu.com/questions/79280/how-to-install-chrome-browser-properly-via-command-line)

5.[robotframework-xvfb](https://github.com/drobota/robotframework-xvfb)

6.[Xvfb-RF Article](http://laurent.bristiel.com/robot-framework-selenium-and-xvfb/)

7.[Stackoverflow-XVFB setup example](https://stackoverflow.com/questions/31045708/is-there-anyway-to-run-robot-framework-tests-without-a-display) 

8.[XVFB and RF test example](https://gitlab.com/sejuba1/security-scorecard-online-store/-/tree/master)

9.[XVFB-Installation steps](https://gist.github.com/addyosmani/5336747)