# Windows setup
How I like to setup my Windows environment

## UEFI settings
- Intel SpeedStep: enabled
- Intel Turbo Boost: enabled
- Resizable Bar: enabled
- Fast Boot: disabled

## Base install
!!! warning "Before you start"

    1. Backup all important data on the drive you'll be installing Windows to

    2. Your Wi-Fi adapter may not work correctly after a clean install, so make sure you're connected to the Internet via Ethernet or have your Wi-Fi adapter drivers ready

1. Install Windows 11 using the [media creation tool](https://www.microsoft.com/en-us/software-download/windows11)
    - Format and then delete all partitions on the drive where you want Windows installed
    - Then install on "unallocated space" 
2. Windows Update :material-arrow-right: advanced options :material-arrow-right: disable: get updates from other PCs
3. Run Windows Update several times until none left
4. Do the same but with the Microsoft Store
5. Uninstall bloat apps. See list of all from the start menu
6. Correct timezone and sync with Windows time server
7. Install [NVIDIA app](https://www.nvidia.com/en-us/software/nvidia-app/) and latest driver
    - disable: automatically optimize
    - custom installation
        - disable: install audio driver
        - enable: perform clean install
8. Reboot
9. Check for system updates until none left, then on Microsoft Store
10. windows update :material-arrow-right: advanced options :material-arrow-right: optional updates
    - if available, install:
        - Intel - Net
        - Intel - Bluetooth
        - C-MEDIA
11. Reboot
12. [test internet speed](https://www.speedtest.net/)

## Display settings
1. Open NVIDIA control panel, enable g-sync if available
2. For 4K monitor
    - resolution: 3840x2160
    - refresh rate: 120 Hz
    - scaling: 150%

## Windows settings
### Power options
1. Go to `Control Panel\Hardware and Sound\Power Options`
2. Show additional plans :material-arrow-right: high performance: enabled
3. Change plan settings:
    - turn off the display: 10 minutes
    - put the computer to sleep: never
    - change advanced plan settings :material-arrow-right: USB settings
        - disable: USB selective suspend
4. "Choose what the power buttons do" :material-arrow-right: "Change settings that are currently unavailable":
    - in "Shutdown settings":
        - disable: "Turn on fast startup"
        - disable: "Sleep"

### File explorer, start menu, taskbar
1. System :material-arrow-right: for developers :material-arrow-right: file explorer:
    - enable: show file extensions
    - enable: show hidden and system files
    - enable: show file extensions
    - enable: show full path in title bar
    - enable: show empty drives
2. Open file explorer :material-arrow-right: ellipsis icon :material-arrow-right: options :material-arrow-right: option file explorer to: "This PC"
3. Disable all desktop icons
4. Start menu:
    - layout: more pins
    - disable: show recently opened items in Start
    - disable: show recommendations for tips
5. Taskbar:
    - disable: search, copilot, task view, widgets
    - taskbar behaviors: enable: automatically hide the taskbar
    - unpin all apps from taskbar
    - system :material-arrow-right: for developers :material-arrow-right: End Task (enable end task in taskbar by right click): enabled
### Misc
1. Mouse properties :material-arrow-right: disable: enhanced pointer precision
2. Disable: sticky keys keyboard shortcut
3. Notifications: do not disturb
### Personalization
1. Change to dark mode
2. Set accent color: automatic
3. Set mouse pointer color: black
4. Change wallpaper from `C:\Users\<user>\Pictures\wallpapers`


## Setup microphone
1. Plug in
2. In `Control Panel\Hardware and Sound`:
    - disable: unused inputs and outputs
    - set mic as default device and default communication device
    - set mic level to 100

## Setup bluetooth headphones
1. Enable bluetooth, pair headphones
2. In `Control Panel\Hardware and Sound`:
    - set Speakers as default device and default communication device
    - if changed since pairing, again: set mic as default device and default communication device
### Permanently disable handsfree telephony
1. Run `services.msc`
2. Locate `Bluetooth Audio Gateway Service`
3. Right click :material-arrow-right: Properties :material-arrow-right: General
    - click "Stop"
    - set Startup type: disabled
### Temporarily disable handsfree telephony
1. Open Control Panel, then paste into address bar:
```
Control Panel\Hardware and Sound\Devices and Printers
```
2. Right click device :material-arrow-right: properties :material-arrow-right: services :material-arrow-right: disable "Handsfree Telephony"

## Applications
1. NVIDIA app
    - set recordings location: `C:\Users\<user>\Videos`
    - set temp folder: `C:\Users\<user>\Videos\temp`
    - instant replay: 30 seconds, off
    - disable: photo and filters
2. Chrome
    - on download: disable send usage stats
    - make default browser and for extensions: pdf, svg
    - `chrome://settings/adPrivacy/`
        - disable: ad topics
        - disable: site-suggested ads
        - disable: ad measurement
    - `chrome://extensions/`
        - remove any unneeded, keep Google Docs Offline to enable keyboard shortcuts on office suite
    - `chrome://settings/system`
        - disable: continue running background apps when closed
3. Spotify
    - install UWP version via Microsoft Store
    - streaming, download quality: "Very High"
    - disable: auto adjust quality
	- disable: show announcements about new releases
	- disable: startup on login
	- enable: close button should minimize the spotify window
4. Task Manager :material-arrow-right: startup apps :material-arrow-right: disable: any unneeded

