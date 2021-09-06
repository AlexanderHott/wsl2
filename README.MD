# Table of Contents

- [Table of Contents](#table-of-contents)
- [1. Installing Windows Terminal](#1-installing-windows-terminal)
  - [From the Microsoft Store](#from-the-microsoft-store)
  - [Choco](#choco)
- [2. Enable WSL2 in Windows](#2-enable-wsl2-in-windows)
- [3. Install WSL2 Linux kernel update package for x64 machines](#3-install-wsl2-linux-kernel-update-package-for-x64-machines)
  - [Set Default WSL version](#set-default-wsl-version)
- [4. Install a Linux Distribution](#4-install-a-linux-distribution)
- [5. Configure Windows Terminal](#5-configure-windows-terminal)
  - [Appearance](#appearance)
  - [Startup Terminal and Location](#startup-terminal-and-location)
- [6. Disabling the Bell (optional)](#6-disabling-the-bell-optional)
  - [Bash](#bash)
  - [Vim](#vim)
  - [`less`](#less)
- [7. Useful tools](#7-useful-tools)
  - [Text editor](#text-editor)
  - [`htop` or `ytop`](#htop-or-ytop)
  - [`net-tools`](#net-tools)
  - [neofetch](#neofetch)
- [8. GUI support](#8-gui-support)
  - [Download & Install](#download--install)
  - [Add a rule to Windows Firewall](#add-a-rule-to-windows-firewall)
  - [Link it to WSL](#link-it-to-wsl)

# 1. Installing [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab)

## From the Microsoft Store

You can install the windows terminal from the microsoft store [here](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701?activetab=pivot:overviewtab).

## Choco

```cmd
choco install microsoft-windows-terminal
choco upgrade microsoft-windows-terminal
```

# 2. Enable WSL2 in Windows

**Run Windows Terminal as administrator.**

Enter the following commands to enable WSL2 in Windows.

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

**NOTE:** You might need to enable [virtualization capabilities](https://docs.microsoft.com/en-us/windows/wsl/troubleshooting#error-0x80370102-the-virtual-machine-could-not-be-started-because-a-required-feature-is-not-installed) to use WSL. If the installation doesn't work, try enabling it.

**Now, restart your computer.**

# 3. Install WSL2 Linux kernel update package for x64 machines

Download from https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi from https://docs.microsoft.com/en-us/windows/wsl/install-win10#step-3---enable-virtual-machine-feature

```
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
```

Run the kernel update package, the installer is very simple.

## Set Default WSL version

```
wsl --set-default-version 2
```

# 4. Install a Linux Distribution

Go to https://aka.ms/wslstore and install a distribution.

**Still as administrator**, type the name of the distribution you installed in the terminal, for example if you installed Ubuntu, type `ubuntu` and hit <kbd>Enter</kbd>.

Choose a username and password, then you are set.

# 5. Configure Windows Terminal

## Appearance

WSL has a lot of features that only affect the appearance such as colorscheme, background, ect. You can change them by clicking the down facing chevron next to the `+` and clicking `settings` or by pressing <kbd>CTRL</kbd>+<kbd>,</kbd>.

The only setting which I would suggest changing is the font. If you want [NF icons](https://www.nerdfonts.com/) or [ligature](https://practicaltypography.com/ligatures-in-programming-fonts-hell-no.html) I suggest installing a [nerd font](https://www.nerdfonts.com/). My personal favorite is JettBrains Mono with Ligature.

You can set your font from `Settings` > `(your specific profile)` (left) > `Appearance` (top) > `Font Face`.

## Startup Terminal and Location

You can change which terminal is run on startup. `Settings` > `Startup` > `Default Profile`.

You can change the folder that opens from `Settings` > `(your specific profile)` (left) > `General` (top) > `Starting Directory`. To start in a directory thats part of a wsl filesystem, use the following:

```
\\wsl$\{Distrobution}\
```

For example:

```
\\wsl$\Ubuntu-20.04\home\alex
```

# 6. Disabling the Bell (optional)

Whenever there is a failed auto completion or you reach the end of a `less` document, there is an annoying bell. You have to disable it in 3 places.

## Bash

Edit the `/etc/inputrc` with your favorite text editor.

```
sudo vim /etc/inputrc
```

Uncomment (remove the `#` from ) the `set bell-style none` line and save the file.

Navigate cursor over the `#` and press<kbd>x</kbd> to delete a character in vim.

(<kbd>ESC</kbd>, <kbd>:</kbd>, <kbd>w</kbd>, <kbd>q</kbd>, <kbd>ENTER</kbd> to save the file and quit vim)

Restart the terminal (close and reopen).

## Vim

Edit or create a `.vimrc` file.

```
vim ~/.vimrc
```

Add the line `set visualbell` and save the file.

## `less`

Edit the `.profile` document.

```
vim ~/.profile
```

At the end, add:
(<kbd>SHIFT</kbd>+<kbd>G</kbd>, <kbd>i</kbd> to start typing)

```
export LESS="$LESS -R -Q"
```

Save the file.

(<kbd>ESC</kbd>, <kbd>:</kbd>, <kbd>w</kbd>, <kbd>q</kbd>, <kbd>ENTER</kbd> to save the file and quit vim)

# 7. Useful tools

## Text editor

Using vi, vim, or nano is no where near as productive as using [NeoVim](https://neovim.io/) or [Emacs](https://www.gnu.org/software/emacs/). I will be creating a tutorial on how to set up Neovim, in the mean time [here's an article](https://code.visualstudio.com/docs/remote/wsl) on how to use VSCode in WSL2.

## `htop` or `ytop`

htop and ytop are basically text-based tast managers

```
sudo apt install htop
```

or

```
sudo apt install ytop
```

## `net-tools`

[net-tools](https://www.mankier.com/package/net-tools) allows you to run commands like `ifconfig` and `netstat`.

```
sudo apt install net-tools
```

## neofetch

[neofetch](https://github.com/dylanaraps/neofetch) is a tool that gives info about the operating system.

```
sudo apt install neofetch
```

# 8. GUI support

## Download & Install

The [VcXsrv X Server](https://sourceforge.net/projects/vcxsrv/) allows WSL to run GUI programs like Python TKinter programs or file managers.

Download and run the installer. Then run XLaunch on the windows machine.

- Multipul windows
- Set Display number to 0
- Start no client
- Select all (Clipboard, Primary Selection, Native opengl, **Disable access control**)

To add the program to starup, save the config file in your startup folder. To find your startup folder, press <kbd>Windows</kbd>+<kbd>r</kbd> and type `shell:startup`. 



## Add a rule to Windows Firewall

Open Windows Defender Firewall, Advanced settings (left) > Inbound Rules (left) > New Rule... (right)

Select

- Program
- This program path, enter `%ProgramFiles%\VcXsrv\vcxsrv.exe`
- Allow the connection
- Select all (Domain, Private, Public)
- Give it a name, e.g. `WSL VcXsrv`

Click finish and close out of windows firewall.

## Link it to WSL

Add two lines to your `.bashrc` file:

```
export DISPLAY="`grep nameserver /etc/resolv.conf | sed 's/nameserver //'`:0.0"
export LIBGL_ALWAYS_INDIRECT=1
```

Install x11-apps

```
sudo apt install x11-apps
```

Restart the terminal and run `xeyes`. There should be a pair of eyes following your mouse.

<!-- # 9. RDP

https://www.youtube.com/watch?v=IL7Jd9rjgrM

Remote Desktop Connection -->
