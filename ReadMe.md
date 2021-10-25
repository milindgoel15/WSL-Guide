# WSL-Guide
This is a repository for anyone who wants help in installing WSL on windows 11/10. I have covered almost common issues and detailed steps to install WSL. 


## Steps to install:

# Step 1: Installing WSL

There is now a new, extremely simplified way to get WSL2 up and running on your Windows 10 and Windows 11 PC. The only requirement is that you're running version 2004 of Windows 10 and above. If this sounds like your system, ensure you've also downloaded the optional KB5004296 update, too, as it's the one that enables this feature.

![image](https://user-images.githubusercontent.com/45682747/138655533-142ea4c1-1c7a-41da-bccc-e5f75a5820b4.png)

Once this is in place, open up PowerShell/CMD and enter this command:

`wsl --install`

That's it. The setup process will begin and you can relax until it's finished.

Alternative method for Windows 11 users is simply head to Microsoft Store and search for "Windows Subsystem for Linux" and install that. It will install everything needed to get wsl running.

# Step 2: Enabling Virtual Machine

If you don't already have this enabled, you'll need to turn it on before installing WSL2. As already stated, WSL2 is a tiny virtual machine, so Windows needs to be prepared for that. If you have this enabled already, skip and go straight to rebooting your PC to make sure you're ready to install.

The quickest way to do it is in PowerShell. Open PowerShell as administrator and enter this command:

`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

Now reboot your PC and move to the next section.

# Step 3: Installing Hyper-V (Skip this step if you have already installed and enabled it)

1. Download the hv.bat file and run it as administrator.
2. A command window will open and will start installing everything related to Hyper-V.( 0 interaction needed from user)
3. After it gets installed, Type "Y" to reboot the computer.
4. Done

Now open Settings and search for "Turn windows features on or off" and see if Hyper-V is enabled or not. If its not checked, enable it and reboot the computer.

# Step 4: Installing Linux Distribution

![image](https://user-images.githubusercontent.com/45682747/138656603-307d4f6d-3e13-4fd2-81fa-668d06c2fada.png)

Run the following commands to install the linux distribution you would like to install.

`wsl --install ubuntu-20.04`

(In my case, I am installing ubuntu so if you are installing some other distribution, replace ubuntu with the name from the list. You can check available distributions using this following command)
`wsl --list --online`

![image](https://user-images.githubusercontent.com/45682747/138657235-437a78a1-b32d-4fcb-bffe-73b03bed0fd4.png)

The process will automatically download and install the distribution. After its installed, just give the root username and password.

Thats't it!

# Step 5: Running wsl

To start wsl, use `wsl` in CMD/Powershell to start your linux distribution. If you have multiple distributions installed, use the following command:

`wsl -d <distribution name>`

Once you're done, typing exit will take you back into PowerShell/CMD.


## Common errors

# WslRegisterDistribution failed with error 0x80370114
To unblock the service, you will have to check with the antivirus or security solution. If you are using Windows Security, follow the steps as below:

1. Type Windows Security in the Start menu and press Enter to launch.
2. Click on App & Browser control available on the left side
3. Then click on Exploit protection settings at the bottom
4. Switch to the Program settings tab
5. Locate the Hyper-V Host Compute Service by going to the under mentioned path: `C:\WINDOWS\System32\vmcompute.exe`
6. Once included, select it, and then click on the Edit button
7. Locate Code flow guard (CFG) and uncheck Override system settings

![image](https://user-images.githubusercontent.com/45682747/138658062-e299f00a-7bbe-4447-b7d2-974ad7528353.png)

8. Finally, open PowerShell, and execute the following command to start the service

`net start vmcompute`

Done that you can now set the WSL version if needed using the wsl –set-version <distro name> 2 command.

NOTE: If you can't find the Hyper-V Host Compute Service in windows security, them head to [step 3](https://github.com/milindgoel15/WSL-Guide#step-3-installing-hyper-v-skip-this-step-if-you-have-already-installed-and-enabled-it) in this Guide above.
