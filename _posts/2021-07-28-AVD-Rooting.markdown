---
  layout: post
  title: AVD ROOTING
  date: 2021-07-28 16:04:00 +0300
  image: Post1.0.png
  tags: [Android]
---

It's a pretty easy task to setup an avd device. But for a security enthusiast, a rooted android device is essential to perform dynamic assessments of android application. 

While many use genymotion (a pre-rooted Android Virtual device), Here we setup an rooted Android Studio Emulator. If you are a newbie to the android pentesting and looking for setting up an virtual device, you are at the right place. Just follow the steps i mentioned in this post.

NOTE: Enabling root is not the only task you have it is also important to maintain __Root Persistence__ in your avd devices. So make sure you read and follow till the end && su binary you are downloading must match your emulator device architecture

Let's Start -

---

## Initial Setup

Turn on your system virtualization options.

Download latest version of android studio.

Add Sdk to your path __emulator and platform-tools__ must needed to be in path for this setup 
* In __windows__ the default path when you install Android studio in Home folder is `C:\Users\username\AppData\Local\Android\Sdk`
* In __Linux__ based os the default directory is `$HOME/Android/Sdk`
You can set path in Linux using command - 
```bash 
export PATH=$PATH:$HOME/Android/Sdk/emulator:$HOME/Android/Sdk/platform-tools
```

---

## AVD Creation

1. Simply open Android Studio's __AVD Manager__. (Launch Android Studio and click on configure which gives a dropdown. Click on AVD Manager)
2. A window pops up click on __Create Virtual Device__.
3. Configure your device choose any of the listed devices.
4. Choose image. This step is important. Select desired __architecture(x86/x86-64)__ and __os-version__withTag(Google API)
5. Next you can __name__ your device and configure __Memory_and_storage__(optional)

All set your device is created.
You can launch your avd through cli by command 
<small> If path is configured </small>
```bash
Linux: emulator -avd Device Name
Windows: emulator.exe -avd Device Name
```

---

## AVD Rooting

If all good till now, we can start process of rooting it.

Download __su binary of your device's architecture__ from [here](https://github.com/0xFireball/root_avd/tree/master/SuperSU)

Start your emulator by command
```bash
$ emulator -avd testAVD -writable-system
$ adb root && adb remount
```
This opens a root shell of your android device. Now follow the commands -
```bash
# cp /sdcard/Download/su /system/xbin/su
# chmod 06755 /system/xbin/su
# su --install
# su --daemon&
# setenforce 0
```
Install [Superuser](https://supersu.en.uptodown.com/android) android application into your avd. Supersu app allows you to enable root.
Download __Root-Checker app__ [here](https://root-checker.en.uptodown.com/android)
```bash
$ adb install supersu.apk 
$ adb install root-checker.apk
```

1. Open supersu app in your emulator device.
2. It pops up an update permission click on __continue__
3. Then choose __Normal__ method.
4. CLick on __ok__ (Be sure you won't click on reboot).
5. Now pass if any prompt appears and check device root status from __root-checker app__.
This gives root grant.

---

## Root Persistance

Rebooting the device may revert all the changes you done so make sure you follow this every time you reboot your device.

From the extended controls of emulator navigate to __snapshots__ section and click on __Take Snapshot__ and rename the snapshop by clicking on pencil icon.

open AVD manager and select __settings__ > __show Advanced settings__ > __Emulated performance__ section > __Boot Options__ > select your snapshot under snapshot dropdown

This will make sure that your device always boot with the saved snapshot with root.

Always start your emulator from terminal/cmd with
```bash
Linux: emulator -avd testAVD -writable-system
Windows: emulator.exe -avd testAVD -writable-system
```

---

You are all done with rooting your avd.

If you face any issues while following the commands above

__Google is your saviour__.

Bye!

If you find it helps you, share 
