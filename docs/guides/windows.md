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

1. install Windows 11 using the [media creation tool](https://www.microsoft.com/en-us/software-download/windows11)
    - format and then delete all partitions on the drive where you want Windows installed
    - then install on "unallocated space" 
2. windows Update -> advanced options -> disable: get updates from other PCs
3. run Windows Update several times until none left
4. do the same but with the Microsoft Store
5. uninstall bloat apps. See list of all from the start menu
6. correct timezone and sync with Windows time server
7. install [NVIDIA app](https://www.nvidia.com/en-us/software/nvidia-app/) and latest driver
    - disable: automatically optimize
    - custom installation
        - disable: install audio driver
        - enable: perform clean install
8. reboot
9. check for system updates until none left, then on Microsoft Store
10. windows update -> advanced options -> optional updates
    - if available, install:
        - Intel - Net
        - Intel - Bluetooth
        - C-MEDIA
11. reboot
12. [test internet speed](https://www.speedtest.net/)

## Display settings
1. open NVIDIA control panel, enable g-sync if available
2. for 4K monitor
    - resolution: 3840x2160
    - refresh rate: 120 Hz
    - scaling: 150%

## Windows settings
### Power options
1. go to `Control Panel\Hardware and Sound\Power Options`
2. show additional plans -> high performance: enabled
3. change plan settings:
    - turn off the display: 10 minutes
    - put the computer to sleep: never
    - change advanced plan settings -> USB settings
        - disable: USB selective suspend
4. "Choose what the power buttons do" -> "Change settings that are currently unavailable":
    - in "Shutdown settings":
        - disable: "Turn on fast startup"
        - disable: "Sleep"

### File explorer, start menu, taskbar
1. system -> for developers -> file explorer:
    - enable: show file extensions
    - enable: show hidden and system files
    - enable: show file extensions
    - enable: show full path in title bar
    - enable: show empty drives
2. open file explorer -> ellipsis icon -> options -> option file explorer to: "This PC"
3. disable all desktop icons
4. start menu:
    - layout: more pins
    - disable: show recently opened items in Start
    - disable: show recommendations for tips
5. taskbar:
    - disable: search, copilot, task view, widgets
    - taskbar behaviors: enable: automatically hide the taskbar
    - unpin all apps from taskbar
### Misc
1. mouse properties -> disable: enhanced pointer precision
2. disable: sticky keys keyboard shortcut
3. notifications: do not disturb
### Personalization
1. change to dark mode
2. set accent color: automatic
3. set mouse pointer color: black
4. change wallpaper from `C:\Users\<user>\Pictures\wallpapers`


## Setup microphone
1. plug in
2. in `Control Panel\Hardware and Sound`:
    - disable: unused inputs and outputs
    - set mic as default device and default communication device
    - set mic level to 100

## Setup bluetooth headphones
1. enable bluetooth, pair headphones
2. in `Control Panel\Hardware and Sound`:
    - set Speakers as default device and default communication device
    - if changed since pairing, again: set mic as default device and default communication device
### Permanently disable handsfree telephony
1. run `services.msc`
2. locate `Bluetooth Audio Gateway Service`
3. right click -> Properties -> General
    - click "Stop"
    - set Startup type: disabled
### Temporarily disable handsfree telephony
1. open Control Panel, then paste into address bar:
```
Control Panel\Hardware and Sound\Devices and Printers
```
2. right click device -> properties -> services -> disable "Handsfree Telephony"

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
4. Task Manager -> startup apps -> disable: any unneeded

