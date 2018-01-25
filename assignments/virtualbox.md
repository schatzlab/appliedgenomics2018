## Development Environment
The standard development environment for this course is Lubuntu 17.04 Zesty, which is a fast and lightweight operating system based on Linux (a unix variant) and Ubuntu.  We have created a packaged version of this that you will need to import as an "appliance" through VirtualBox (instructions below). 
 
In order to install and use our environment follow these steps on your laptop:

### 1. Install VirtualBox
VirtualBox is software that allows you to create and work on virtual devices as separate instances within your machine. You can download it here: https://www.virtualbox.org/. Note you may need to set special permissions to allow it to load.

 
### 2. Download the 64-bit Lubuntu 17.04 Zesty appliance. 
Make sure to download the 64 bit version! (large file, so expect it to take a while): 
http://www.osboxes.org/lubuntu/ (666MB file, up to 8 GB required)

On mac, you will need to unpack the .7z archive using [The Unarchiver](https://theunarchiver.com/). This will create a file named `Lubuntu 17.04 (64bit).vmdk`.


### 3. Create the virtual machine
From within VirutalBox, click "New" to create a new virtual machine.

Then (1) Name your Virtual Machine and Select the Operating System as 64 bit Ubuntu <br>
![Name](https://raw.githubusercontent.com/schatzlab/appliedgenomics2018/master/assignments/virtualbox/NameVirtualMachine.png)

(2) Set the memory size to 4GB (or as much RAM as is available)<br>
![Memory](https://raw.githubusercontent.com/schatzlab/appliedgenomics2018/master/assignments/virtualbox/MemorySize.png)

(3) Select the Lubuntu image as your virtual hard disk<br>
![HardDrive](https://raw.githubusercontent.com/schatzlab/appliedgenomics2018/master/assignments/virtualbox/Hard%20Disk.png)

### 4. Launch the new virtual machine
When the install finishes, you will have a virtual machine called "Genomics" showing in the left menu of your VirtualBox device manager.  Double-click on this virtual machine to start it up (or single-click and then hit the "start" icon).  If you get an error message, read the details and follow the instructions to update as necessary.  (For example, you might have to install the Oracle VM Extension Pack from https://www.virtualbox.org/wiki/Downloads to get the USB controller to work.)

### 5. Log into your new Lubuntu virtual machine
The default username is "osboxes.org" and the default password is "osboxes.org"; feel free to create a new username or change the password

### 6. Explore your new machine-in-a-machine

Click on the left bottom start button.  Keep in mind that the files in your virtual environment can only be accessed from within that virtual environment, not from your usual laptop software.  So Lubuntu has a web browser, office-like apps, accessories, etc. The terminal can be accessed using the LXTerminal application in the "System Tools" menu.

### 7. Guest Additions
You will want to install guest additions to get cool features like access to shared folders and shared clipboard, native screen resolutions, etc. Please follow the linked documentation for how to install those extensions.  These tools will make it easier to switch back and forth between your virtual box machine and your native laptop.

From the VirtualBox Devices menu, click "Install Guest Additions CD Image..."

Then run this at the terminal:

```
$ sudo /media/osboxes/VBox_GAs_5.2.6/VBoxLinuxAdditions.run
$ /sbin/shutdown -r now
```

### 8. Essential Packages

After booting the virtual machine, there are a number of essential packages that will be needed. Install them with the following commands (just accept the defaults when prompted):

```
$ sudo do-release-upgrade
$ sudo apt-get update
$ sudo apt-get install build-essential
$ sudo apt-get install dkms
$ sudo agp-get install default-jre
```


### Help: Fixing the Display
In case you boot up the appliance and get some weird-looking graphics instead of a nice login screen: Hit "Host+F1" once, then "Host+F7" once and everything should be good. In VirtualBox the "Host" key is "Right Ctrl" (on Windows/Linux) or "Left Command" on OS X. (If you're using a Mac, you may also have to push some funky key called "fn" (bottom left corner of your keyboard) to get F1/F7 to behave as they should. And if you have a Mac without function keys, well, you should figure out for yourself where those keys are now...)
 
### Help: Powering Down
Always use the "power button" in the bottom right corner of your Lubuntu desktop to shut down your machine safely - do not simply exit the window or VirtualBox.  Running Lubuntu through VirtualBox can be a bit of a power drain on your laptop, so be prepared with a power cord.  
 
#### Help: Use Dropbox!
Note that updated versions of this appliance may be posted at a later date. Hence it's probably a Bad Idea (tm) if you keep source code you're working on only in your virtual machine instance. We highly recommend using a service such as Dropbox to maintain your files in. (Start->Internet->Dropbox to install.)  This also helps in case your laptop catches fire or some other mishap occurs.
