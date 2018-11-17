# Tools

## Create a Linux VM

The tools we'll be using today are very usable in macOS or Windows. However, for the sake of maintaining a bit of a "hackerbox", we're going to use them within the virtual machine image you received by email. This also helps us avoid dependency and set-up issues across various OS versions.

The instructions for installing these tools are included below, *just* in case you'd like to set up your own Android hacking machine at home. 

**★ Download the `BlackHoodie Kali` image [here](http://cdimage.ubuntu.com/lubuntu/releases/18.04/release/lubuntu-18.04.1-desktop-amd64.iso),**

**★ Install VirtualBox for macOS or Windows by clicking [here](https://download.virtualbox.org)**.  

**★ Create a new virtual machine, setting the `type` to `Linux` and the Version to `Debian`**

![](/img/Create_VM.png)

**★ Bump up the memory size to allocate to the VM from the suggested 1024MB to ~8192MB.** Allocating too little RAM will result in a corrupted display when you try to install the image.

![](/img/Set_VM_Memory.png)

**★ Create a virtual hard disk with a minimum of 10 GB of space.** I tend to add a bit more, since I never know what else I may do with the VM in the future.

![](/img/Create_VM_HDD.png)

I also tend to select `Fixed size` hard disk file settings for my VMs because I care more about speed than being able to dynamically allocate additional space in the future.

![](/img/Fixed_Size_HDD.png)

**★ Select _Create_**

**Important!** Before opening the new VM, we have to update settings in its display. The latest Lubuntu release requires that you bump up the processing power of the VM before you can access a display that isn't wildly corrupted (ie, the same issue you'd experience with allocating too little RAM).

**★ Right-click on the VM and open settings.** Navigate to _System_ and update your settings as shown below:

![](/img/Right_Click_New_VM.png)

![](/img/Set_4_cores.png)

**★ Hit okay, and your settings will save.**

**★ Double click the new VM in the left-hand column.** Select your `Lubutunu` ISO and continue with the installation process.

![](/img/Lubuntu_startup.png)

##### Congratulations! You now have a virtual machine 🎉

## Setting Up Our Reversing Environment

### Install [Apktool](https://ibotpeaches.github.io/Apktool/install/)
 
Apktool is a handy application that allows us to decompile an APK and view the _SMALI_ files packaged within. Decompiling the app with Apktool will also allow us to view `AndroidManifest.xml` for a basic understanding of what an app is doing, as well as areas where permissions may be over-granted.

If you want to make changes to a decompiled application, you can use Apktool to re-build the app as well. We won't be doing that in today's workshop, but it's useful for future reversing projects. 

**★ Download a wrapper script & rename** 

```shell
wget https://raw.githubusercontent.com/iBotPeaches/Apktool/master/scripts/linux/apktool.bat
```

**★ Download the latest Apktool**
```shell
wget https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.3.3.jar
mv apktool_2.3.3.jar apktool
```

**★ Move downloaded files to `bin`**
```shell
sudo mv apktool.jar /usr/local/bin
sudo mv apktool /usr/local/bin
sudo chmod +x /usr/local/bin/apktool.jar
sudo chmod +x /usr/local/bin/apktool
```

### Install [dex2jar](https://github.com/pxb1988/dex2jar)

Dex2Jar will allow us to convert `classes.dex`, the Dalvik Executable, to readable `.class` files. For ART apps where the dex files are converted to OAT files, we can still extract the `.dex` files and convert to `.class`. Once we have `.class` files for each of the, well, classes in the app, we'll use JD-GUI to view them.

```shell
git clone https://github.com/pxb1988/dex2jar.git
```

### Install [jd-gui](http://jd.benow.ca/)

As mentioned, JD-GUI will display the Java source code of our `.class` files. 

```shell
wget https://github.com/java-decompiler/jd-gui/releases/download/v1.4.0/jd-gui_1.4.0-0_all.deb
sudo dpkg -i jd-gui_x.x.x-x_all.deb 
```

## You already have these installed, so let's talk about some handy command line functions: [Next](https://github.com/chmodxx/BlackHoodie2018/blob/master/lab/CLI_Kung_Fu.markdown)
