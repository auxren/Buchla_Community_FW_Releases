# Installing 200e Bus Buccaneer on Windows (alpha)

**Not yet run on hardware.** Read [INSTALL.md](INSTALL.md) first; the warnings and the power-cycle steps there apply on Windows too. This page covers what is different on Windows.

## What you need
- Windows 10 or 11, 64-bit.
- The same hardware as in [INSTALL.md](INSTALL.md): a Xenomorpher, or a Studio H WPM, or Buchla's USB Firmware Card.

## Install
1. Download the app's `.exe` installer from this repository's releases and run it.
2. This alpha is **not code-signed**, so Windows SmartScreen shows "Windows protected your PC". Choose **More info**, then **Run anyway**.
3. The installer is per-user and does not ask for administrator rights.
4. The app needs Microsoft's WebView2 runtime. Most Windows 10 and 11 computers already have it; if yours does not, the installer downloads it (it needs the network for that).

## Where your files live
Settings, the firmware list, your library and your backups are kept in `%LOCALAPPDATA%\com.auxren.buccaneer` (paste that into the File Explorer address bar). Backups are in the `backups` folder there. When you uninstall, leave the "delete application data" box unticked, or your backups go with it. Safer still: set the Backup folder in Settings to somewhere outside the app's data folder.

## USB, MIDI and COM ports
- **Xenomorpher:** it appears as a USB MIDI device; Windows may shorten or add a number to its name, and the app finds it anyway. Only one program can use a MIDI port at a time on Windows: close any other MIDI program (a DAW, a MIDI monitor) before you start, or the app tells you the port is in use.
- **Studio H WPM over USB:** it shows up **twice**, as a MIDI device and as a serial (COM) port. Windows 10 and 11 need no driver for either. The COM number can change when the WPM switches between running and update mode; the app handles that.

## Wi-Fi (WPM)
The WPM update over Wi-Fi works as on the Mac: join the WPM's own network, BUCHLA200E, for the update. Windows usually rejoins BUCHLA200E on its own; if the app cannot reach the WPM, pick the network again from the Wi-Fi list. If your computer is also on another network (Ethernet or a second Wi-Fi adapter), turn that adapter off for the update if the app cannot reach the WPM.

## If the WPM USB update says it is in its bootloader
Double-press the WPM's reset button, wait a few seconds, and try the update again. The app carries on from the bootloader.

## Drivers
Only the official **Buchla USB Firmware Card** route needs a driver on Windows. The card's update interface (USB ID **03EB:2FF6**) must use the **WinUSB** driver for this app to talk to it. If it does not, the app says the card's USB driver is not WinUSB and points here.

**Set it to WinUSB (Zadig)**
1. Plug in the card. Download Zadig from <https://zadig.akeo.ie/> and run it.
2. Choose **Options, List All Devices**.
3. Pick the card's update interface in the list: the one whose USB ID reads **03EB 2FF6**. Check the ID before you continue; do not change any other device.
4. Choose **WinUSB** as the driver on the right, then **Replace Driver** (or **Install Driver**) and wait for it to finish.

**What this changes.** Buchla's own utility and Atmel FLIP use a different driver for the same card. While WinUSB is bound, **they cannot see the card**. Only one driver can be bound at a time.

**Switch back to Buchla's utility**
- Device Manager: find the card (under "Universal Serial Bus devices", or by its USB ID 03EB:2FF6 in Properties, Details, Hardware Ids), right-click, **Uninstall device**, tick **Delete the driver software for this device**, then unplug and replug the card. Buchla's utility and FLIP use their own driver, so after this reinstall that driver with Buchla's or Atmel's installer.
- Switching back means reinstalling that driver with Buchla's or Atmel's installer; Zadig cannot restore it for you.

Switch one way, finish what you are doing, then switch back before changing again.
