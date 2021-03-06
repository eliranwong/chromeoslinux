# Android Studio + Flutter + Dart + Connecting flutter to Chromebook

We found the following way is the easiest one to setup Android Studio together with flutter and dart.  Overall, it is easier to first install Android Studio then flutter and dart.

1) Go to https://developer.android.com/studio (with a Chrome OS browser, not with a Linux browser, so that it automatically directs to a download link for the Chrome os version of Android Studio.)

2) Download Chrome OS installation file for Chrome OS

3) Open "Files" app, go to "Downloads" folder and locate the downloaded file.  In our testing, the file name is "android-studio-ide-201.7042882-cros.deb".

4) Right click and select "Install with Linux (Beta)"

5) Launch after installation is finished, via either launcher or running "/opt/android-studio/bin/studio.sh" on terminal

6) Follow the "Setup Wizard" to complete the setup.

7) On welcome screen, select "Configure > Plugins"

8) Search for "flutter" and install flutter plugin

9) Restart Android Studio after installing "flutter" plugin

10) On welcome screen, select "Create New Flutter Project" > "Flutter Application" > Next

11) On "Configure the new Flutter Application" dialog, you will note that Flutter SDK path is still empty.  Select "Install SDK", right next to the text field of "Flutter SDK path".  Write down the path you choose to install the flutter SDK.

12) AFTER "Flutter SDK" is downloaded, select "Cancel" to close the dialog first.  Yes, close it first!  You won't be able to create a new flutter project yet.

13) Open /etc/profile, e.g.:

> sudo nano /etc/profile

14) Locate the following section, add your path and save the file:

> if [ "`id -u`" -eq 0 ]; then

>   PATH="..."

> else

>   PATH="/usr/local/bin:...:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"

> fi

> export PATH

15) Make sure ADB debugging is enabled: Settings > Linux > Develop Android apps > Enable ADB debugging

16) Restart Linux virtual machine.

17) Run on terminal:

> flutter doctor

18) Select "Always allow from this computer" to authorize connect flutter to your Chromebook upon prompting "Allow USB debugging?"

<img src="screenshot_connect_chromebook.png">

19) Run on terminal the following command and accept all licenses upon prompting:

> flutter doctor --android-licenses

20) At this point, you should be able to create a new flutter project in Android Studio and test your project with your chromebook directly. To have a final check, run:

> flutter doctor

It should looks like:

<img src="flutter_doctor.png">

Please note that VS Code is optional.

[Optional]

You may encounter the following warning:

dpkg: warning: parsing file '/var/lib/dpkg/status' near line 57 package 'android-studio':
 missing 'Maintainer' field

To get rid of this warning:

1) Run

> sudo nano /var/lib/dpkg/status

2) Use "ctrl + shift + -" key combination to go to line 57

3) Enter "Maintainer: "

3) Save the file (ctrl + o + enter) and exit (ctrl + x)

# Create an alias for use in terminal

> echo "alias studio=/opt/android-studio/bin/studio.sh & disown" >> ~/.bashrc

> studio

# Trouble-shooting: integrated terminal does not have flutter path

If you lanch Android Studio by click its icon on Launch, you may find flutter command now available.  You may need to set assign further variables.  A simple solution is to launch studio from terminal you can find flutter command works directly from Android Studio's integrated terminal.

You may read the section above on creating an alias:
https://github.com/eliranwong/ChromeOSLinux/blob/main/development/AndroidStudioFlutter.md#create-an-alias-for-use-in-terminal

