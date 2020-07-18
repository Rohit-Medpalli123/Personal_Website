---
layout: post
section-type: post
title: Mastering ADB Commands
category: Mobile
tags: [ 'ADB', 'Android','Commands' ]
---

### What is ADB?

![alt text](../../../../img/ADB/adb1.png)

ADB stands for `Android Debug Bridge` and it is a command line tool that is used to communicate with a smartphone, tablet, smartwatch, set-top box, or any other device that can run the Android operating system (even an emulator). Specific commands are built into the ADB binary and while some of them work on their own, most are commands we send to the connected device.

ADB uses USB or TCP as its transport layer to communicate with an Android-powered device.

This tool allows you to perform many development tasks, including:

* Deploying apps to a device.
* Debugging apps.
* Viewing device and app logs.
* Profiling apps.

### ADB Basics
* adb devices (lists connected devices)
* adb root (restarts adbd with root permissions)
* adb start-server (starts the adb server)
* adb kill-server (kills the adb server)
* adb reboot (reboots the device)
* adb devices -l (list of devices by product/model)
* adb shell (starts the backround terminal)
exit (exits the background terminal)
* adb help (list all commands)
* adb -s <deviceName> <command> (redirect command to specific device)
* adb –d <command> (directs command to only attached USB device)
* adb –e <command> (directs command to only attached emulator)

If your device is not listed, try reconnecting the device and restarting the adb server via the following:

```
# Kill the server first.
$ adb kill-server
# The server will start again when running adb commands.
$ adb devices
```
💡 Tip: The kill-server command is generally useful for stopping the adb server when encountering issues such as when adb is not responding to a command or when it can’t connect to the device.

### Package Installation
* adb shell install <apk> (install app)
* adb shell install <path> (install app from phone path)
* adb shell install -r <path> (install app from phone path)
* adb shell uninstall <name> (remove the app)

### Applications Management
adb can install and uninstall applications:

```
# Install APK files.
$ adb install path_to_apk_file

# Uninstall application by its package name.
$ adb uninstall application_package
```

### Paths
* /data/data/<package>/databases (app databases)
* /data/data/<package>/shared_prefs/ (shared preferences)
* /data/app (apk installed by user)
* /system/app (pre-installed APK files)
* /mmt/asec (encrypted apps) (App2SD)
* /mmt/emmc (internal SD Card)
* /mmt/adcard (external/Internal SD Card)
* /mmt/adcard/external_sd (external SD Card)

* adb shell ls (list directory contents)
* adb shell ls -s (print size of each file)
* adb shell ls -R (list subdirectories recursively)

### File Operations
* adb push <local> <remote> (copy file/dir to device)
* adb pull <remote> <local> (copy file/dir from device)
* run-as <package> cat <file> (access the private package files)

```
# Copies file or directory with its sub-directories to the device.
$ adb push local_path device_path

# Copies file or directory with its sub-directories from the device.
$ adb pull device_path local_path
```

### Phone Info
* adb get-statе (print device state)
* adb get-serialno (get the serial number)
* adb shell dumpsys iphonesybinfo (get the IMEI)
* adb shell netstat (list TCP connectivity)
* adb shell pwd (print current working directory)
* adb shell dumpsys battery (battery status)
* adb shell pm list features (list phone features)
* adb shell service list (list all services)
* adb shell dumpsys activity <package>/<activity> (activity info)
* adb shell ps (print process status)
* adb shell wm size (displays the current screen resolution)
* dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp' (print current app's opened activity)

```
adb shell dumpsys window windows | grep Focus
```

### Package Info
* adb shell list packages (list package names)
* adb shell list packages -r (list package name + path to apks)
* adb shell list packages -3 (list third party package names)
* adb shell list packages -s (list only system packages)
* adb shell list packages -u (list package names + uninstalled)
* adb shell dumpsys package packages (list info on all apps)
* adb shell dump <name> (list info on one package)
* adb shell path <package> (path to the apk file)

### Configure Settings Commands
* adb shell dumpsys battery set level <n> (change the level from 0 to 100)
* adb shell dumpsys battery set status<n> (change the level to unknown, charging, discharging, not charging or full)
* adb shell dumpsys battery reset (reset the battery)
* adb shell dumpsys battery set usb <n> (change the status of USB connection. ON or OFF)
* adb shell wm size WxH (sets the resolution to WxH)

### Device Related Commands
* adb reboot-recovery (reboot device into recovery mode)
* adb reboot fastboot (reboot device into recovery mode)
* adb shell screencap -p "/path/to/screenshot.png" (capture screenshot)
* adb shell screenrecord "/sdcard/recording.mp4" (record device screen)
* adb backup -apk -all -f backup.ab (backup settings and apps)
* adb backup -apk -shared -all -f backup.ab (backup settings, apps and shared storage)
* adb backup -apk -nosystem -all -f backup.ab (backup only non-system apps)
* adb restore backup.ab (restore a previous backup)
* adb shell am start|startservice|broadcast <INTENT>[<COMPONENT>]
-a <ACTION> e.g. android.intent.action.VIEW
-c <CATEGORY> e.g. android.intent.category.LAUNCHER (start activity intent)

* adb shell am start -a android.intent.action.VIEW -d URL (open URL)
* adb shell am start -t image/* -a android.intent.action.VIEW (opens gallery)

### Shell Commands Execution
adb supports the shell command that allows for the execution of Unix shell commands on the device.

You can enter a remote shell on a device via the following:

```
$ adb shell
```

💡 Tip: You can exit the remote shell by typing Ctrl + D or by typing exit.

You can also execute single shell commands via the following:

```
adb shell command_to_execute
```

Android devices support most basic Unix shell commands such as ls, cat, cd, and rm. There are also a few commands for interacting with Android services. The most useful ones are:

`am` — provides access to ActivityManager. This allows you to start activities, stop processes, broadcast intents, and more.

`pm `— provides access to application packages on the device. This allows you to list all installed packages, manage installed packages, work with application permissions, and more.

💡 `Tip`: You can run these commands without any parameters to print their usage, i.e. 
adb shell am and adb shell pm.

### Logs
* adb logcat [options] [filter] [filter] (view device log)
* adb bugreport (print bug reports)

I would like to quickly mention one additional tool that works around the limitations of the default logcat command — namely its inability to filter output by application package (logcat only supports filtering based on process IDs). 

[PID Cat](https://github.com/JakeWharton/pidcat) provides simple filtering for an application package together with enhanced formatting and coloring for the logcat messages:

```
$ pidcat com.pspdfkit.viewer
```

### Permissions
* adb shell permissions groups (list permission groups definitions)
* adb shell list permissions -g -r (list permissions details)

### Connecting to Multiple Devices
adb can connect to multiple devices at the same time. You must specify the target device when issuing adb commands when multiple devices are connected.

To do this, you’ll need to know the `serial number` of the target device. You can get the serial by using the devices command:

```
$ adb devices
List of devices attached
042531501315900588da	device
913a5739	device
```
Then use the -s option to specify the serial number of the target device:

```
$ adb -s 913a5739 install app.apk
```
If only a `single` emulator or a single hardware device is connected, use `-e` to target the emulator or `-d` to target the hardware device.


### Connecting to a Device via Wi-Fi
So far, we’ve only assumed that adb connects to a device over USB, but you can also configure adb to work over Wi-Fi. The setup consists of multiple steps, outlined below.

1.Connect your device and your computer to the same Wi-Fi network.

2.Connect the device to your computer via a USB cable.

3.Find the IP address of your device. For example, you can execute the ifconfig command on the device:


```
$ adb shell ifconfig wlan0
wlan0     Link encap:UNSPEC    Driver icnss
          inet addr:192.168.1.49  Bcast:192.168.1.255  Mask:255.255.255.0
```

4.Make the target device’s adb daemon listen for TCP/IP connections on port 5555 (the default port used by adb connect below):

```
$ adb tcpip 5555
```
5.Disconnect the USB cable from the device.

6.Connect to the device using its IP address:

```
$ adb connect 192.168.1.49
```
7.Verify that the connection works:
```
$ adb devices
List of devices attached
192.168.1.49:5555	device
```
You can now use adb commands remotely. Having a wireless adb connection is nice for decreasing your dependence on wires. The underlying TCP/IP transport is also super useful for building more advanced use cases. For example, you can tunnel adb connections on your CI server to your remote computer.

`Note:` Enabling ADB over Wi-Fi on a device opens it for anybody on the same network be able to execute commands. This includes being able to install or delete packages, view data and add or delete users.
If you’re on a public network, make sure your device doesn’t have any sensitive data. If you’re on a private network with a device that has sensitive data, remote ADB will be enabled on any network you join until you restart your device.



### References:
[ADB -Commands and how to use it - Cheatsheet](https://www.notion.so/ADB-Commands-and-how-to-use-it-cba29872f803415882c858975cd98f5c)

[ADB tips](https://pspdfkit.com/blog/2019/android-debug-bridge-tips-and-tricks/)

[Exploiting andriod through ADB - youtube](https://youtu.be/ONHxcGMdkM0)

[Phonespoilt](https://youtu.be/EBgh3Ue2qNo)

[ADB tutorial](https://youtu.be/3wMlCucwGvE)

[ADB short youtube](https://youtu.be/45PcU2HIlYI)

[Android Debug Bridge (ADB): Beyond the Basics](https://www.raywenderlich.com/621437-android-debug-bridge-adb-beyond-the-basics#toc-anchor-001)
