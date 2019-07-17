# How-to: Convert stock Chromium OS to Chrome OS

> Disclaimer: This guide assumes you to have computer skills and are comfortable to operate under Linux command-line environment. Please note that there are commands that may incur permanent data loss with incorrect usage, proceed at your own risk. If you find the below content difficult to understand, please seek help from your friends or ask in our support Telegram group.

## Introduction
Your U500 box is shipped with Chromium OS as its stock operating system. Chromium OS offers you a fast, simple and secure browsing experience with its full-fledged desktop Chromium browser. Chromium OS is built from the Chromium open-source project that powers both Google Chrome browser and Chrome OS you will find in Chromebooks / Chromeboxes. Chrome OS is proprietary to Google thus it can provide more exciting features including Android support and Play Store. We are unable to ship Chrome OS for your U500 box, however, if you wish to utilise these exciting features of Chrome OS and enjoy the identical experience of a Chromebook / Chromebox, you are able to "convert" a Chromium OS image to a Chrome OS image with the help of this guide and some DIY spirit.


## Things you will need
 - U500 box that runs stock Chromium OS, or any other Linux distribution. Keyboard and a pointer device are also needed.
 - An USB mass storage device with minimum capacity of 8GB. It would be ideal to have a fast USB 3.0 flash drive.
 - Latest "[Project Croissant](https://github.com/imperador/chromefy)" zip file dump.
 - Stock Chromium OS recovery image that is running on your U500 device, click [here](https://fydeos.cowtransfer.com/s/8346223985384d) to download.
 - Target Chrome OS recovery image that you wish to convert to. We recommend the latest version of "eve" (Recovery image of Google Pixelbook) to utilise more cool features including Google Assistant. To download the recovery image, click [here](https://cros-updates-serving.appspot.com/) to navigate to the list page of all Chrome OS recovery images and search within the web-page for "eve". Click on the link that has the largest version number. At the time when this guide was written, it was [74](https://dl.google.com/dl/edgedl/chromeos/recovery/chromeos_11895.118.0_eve_recovery_stable-channel_mp.bin.zip).
 - "Chrome OS recovery utility" Chrome App: you can obtain this from [Chrome Web Store](https://chrome.google.com/webstore/detail/chromebook-recovery-utili/jndclpdbaamdhonoechobihbbiimdgai?hl=en).


## Steps to create the Chrome OS image

### 1. Getting all the required files and prepare your environment
 - Create a folder named "chromium2chrome" in Downloads folder as the working directory.
 - Navigate to "[Project Croissant](https://github.com/imperador/chromefy)"'s page on Github and download its latest file dump in zip format, by clicking the "Clone or download" button and choose "Download ZIP".
 - Unzip the `chromefy-master.zip` file you just downloaded and place the content inside "**chromium2chrome**" folder.
 - Download the U500 stock Chromium OS recovery image from [here](https://fydeos.cowtransfer.com/s/8346223985384d), also unzip the file and place the `chromiumos_image_u500_v1.1.bin` file inside "**chromium2chrome**" folder.
 - Download the Google Chrome OS recovery image, also unzip the file and place the .bin file inside "**chromium2chrome**" folder.
 - Copy `swtpm.tar` and `croissant.sh` from "chromefy-master" folder its parent "**chromium2chrome**" folder.
 - You shall now have a working directory with all the required files, like this: ![file structure screenshot](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/file-structure.png "File Structure before executing the script")


### 2. Run the commands
 - Activate the Chromium browser and then press `Ctrl` + `Alt` + `t` together, a new tab with "Crosh" shell will be opened for you.
 - Within the "Crosh" shell, enter the command `shell` to invoke a slightly advanced "bash" shell.
 - Enter `cd ~/Downloads/chromium2chrome` to change the current directory to your working directory created in previous step.
 - Enter `ls -al` to double check all the required files are there, per the screenshot below.
 - Enter the command to execute the conversion process:

 ```
 sudo bash croissant.sh chromiumos_image_u500_v1.1.bin chromeos_11895.118.0_eve_recovery_stable-channel_mp.bin swtpm.tar
 ```
 
 ![Commands to execute for the conversion](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/commands-to-start-conversion.png "Commands to execute for the conversion")


### 3. Whilst the script is running
 - You will see a lot of output scrolling through your screen, it means the script is busy converting the image.
 - This process usually takes around 1 minutes to complete, if you have been waited for a much longer time than this, you should consider abort (just close this tab) and retry the process again.
 - Towards the end of the script, you will be asked 3 questions regarding your hardware, respond "**n**" for all of them:
  ![Questions during script](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/questions-during-script.png "Questions during script")
 - If the script has completed successfully, which it should, you will see a prompt like this:
 ![script success](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/script-success.png "script success")


### 4. Burn the image file to USB
 - Your `chromiumos_image_u500_v1.1.bin` is now modified by the script in previous step to have the necessary applications of Chrome OS. In order not to get mixed-up with the original stock image and for future reference, we shall rename it to `chromed_u500_v1.1.bin`.
 ![Rename image file](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/rename-chromed-image.png "rename image file")
 - Connect your USB storage drive to your U500 box. All your data in this USB drive will be wiped in the following step. If you need to back up please do so now.
 - Launch the "Chromebook Recovery Utility" from your app launcher. Click the gear icon from the top-right corner and choose "Use local image":
 ![Chromebook Recovery Utility](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/recovery-utility-launch.png "Chromebook Recovery Utility")
 - Choose the `chromed_u500_v1.1.bin` file and your USB device when prompted, you shall see a confirmation screen:
 ![Chromebook Recovery Utility Confirmation](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/recovery-utility-confirmation.png "Chromebook Recovery Utility Confirmation")
 - When the burning process is completed, click "Done" and you shall now have a Chrome OS image that works on your U500 box.


## Steps to boot Chrome OS and install it to your hard drive

### 1. Boot from your Chrome OS image and check if things are OK
 - Keep your USB drive connected to your U500 box and power down your system.
 - Power up your U500 box whist pressing `F7` key on the keyboard, you shall see a "boot device selection menu" as below:
 ![boot device selection menu](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/F7-boot-device-picker.jpg "boot device selection menu")
 - Choose your USB drive to boot and hit `Enter`.
 - You shall find that your U500 is now booting Google's Chrome OS. You'll be greeted with the out-of-box-experience (OOBE) screens per the first boot of your U500 box. Once you follow the screen prompts and input required information you will be landed to the desktop of your new Chrome OS.
 - Now it's a good time to "poke around" in this OS and verify if things are working as expected. Please try not to install too many apps as we will be installing it to your hard drive, where the current-state will be erased and you will begin from OOBE again.

 ### 2. Install Chrome OS to your U500 box
  - Once you are happy about the Chrome OS you've just made, you can install it to your hard drive to replace the stock Chromium OS to benefit from the added functionalities. Please note that all your data from your existing stock Chromium OS and your current Chrome OS from USB drive will be lost. You will need to back up your files before continuing.
  - Same as on Chromium OS, invoke the "**bash**" shell by activating Chrome browser, hit `Ctrl` + `Alt` + `t` and then enter `shell`.
  - Input command `sudo su -` to gain administrative privileges.
  - Input command `lsblk` to list all your block storage devices, in order to identify how Chrome OS recognises your hard drive. Typically you will see a command output like this:
  ![lsblk output](https://raw.githubusercontent.com/chromium2chrome/u500box-guide/master/images/install-chromeos-to-hdd.jpg "lsblk output")
  - In the example output above, we can identify that this U500 box is having a 119.2G SSD named **`sda`**, whilst the current Chrome OS is running on a 16G USB drive recognised as **`sdb`**.
  - Run the following command to install Chrome OS to your hard drive (**`sda`**). Noted that this will erase the entire drive and all your data will be lost:
  
  ```
  chromeos-install --dst /dev/sda
  ```
  - It will take a few minutes for the command to finish depending on the i/o speed of your USB drive. Once the command finishes, please:
  	- Shutdown your U500 box
  	- Remove the USB drive
  	- Power on again
  - By now you shall have a brand-new Chrome OS installation and it will begin from OOBE. Enjoy!


## Steps to upgrade your Chrome OS installation
TODO


## Credits
[The Chromium Projects](https://www.chromium.org/)<br>
[Project Croissant](https://github.com/imperador/chromefy/) and its authors<br>
[FydeOS](https://github.com/FydeOS/) and its team