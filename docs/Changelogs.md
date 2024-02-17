# CHANGELOGS

This page is a list of all of the changelogs for each version of RetroPie. For a complete list of all commits to the source code see [here:](https://github.com/RetroPie/RetroPie-Setup/commits/master)  

### Version 4.8: (Mar 14, 2022)

Changes since 4.7.1

* On screen keyboard for entering WiFi password in RetroPie-Setup
* Improved joystick support in RetroPie-Setup dialogs.
* Improvement to RetroPie package management and updating.
* retroarch - updated to v1.10.0
* Updates to many libretro cores - in depth details about libretro changes can be found on their site - [https://www.libretro.com](https://www.libretro.com)
* EmulationStation updated to v2.10.2
   * Better Random: Perfect shuffle of systems, games and screensaver items
   * Fixes for event handling so startup events are cleared
   * Pixel positioning/sizing support for themes
   * Added a progress bar during loading + threaded loading for systems (threaded loading is disabled by default currently)
   * Added a cache for stat checks (performance)
   * Support for new scripting events - switching systems/selecting games/screensaver videos and image switching/etc.
   * Improvements to text wrapping for CJK glyphs
   * Updated Arcade resource lists (used to hide MAME devices/bioses and to provide friendly names for zip archives)
   * Ability to use full screen paging with LB/RB
* hatari - updated to v2.3.1
* xpadneo (Xbox One Bluetooth driver) - updated to v0.9
* zesarux - updated to v9.1
* lzdoom - updated to 3.87c
* xroar - updated to 1.0.9
* srb2 - updated to 2.2.9
* ags - switch to v3.5.1 release branch
* eduke32 - fix for gameplay bug in E1L4
* scummvm - updated to 2.5.1, first release since the ResidualVM merge includes bug-fixes and new games.
* cgenius - updated to the latest stable version (Added Cosmos engine, GUI, sound and controller improvements)
* tyrquake - updated to 0.69
* yquake2 - updated to v8.00 and added add-ons game source
* vice - switch to v3.5 branch
* advmame - fixes for building on GCC 10+
* audiosettings - add PulseAudio configuration support
* esthemes - support branches, to allow multiple themes on a single repo and many new EmulationStation themes added
* bluetooth - various fixes and improvements
* kodi - scriptmodule compatibility improvements on Ubuntu
* Improvements to handling of dkms drivers.
* New modules
   * lr-stella - added upstream / current Stella libretro core (Atari 2600 emulator)
   * lr-tic80 - TIC-80 is a free and open source fantasy computer for making, playing and sharing tiny games (see [https://tic80.com](https://tic80.com))
   * lr-retro8 - retro8 is an open source re-implementation of the PICO-8 fantasy console.
   * yabasanshiro - standalone Saturn emulator based on Yabause (RPi4 only)
   * hypseus - Hyseus Singe (Daphne) SDL2 Laserdisc emulator
   * ppsspp-1.5.4 - Added old ppsspp module (performs better for some users)
   * dosbox-staging - an enhanced and modernized DosBox fork
   * lr-uae4arm - libretro core of the uae4arm Amiga emulator.

### Version 4.7.1: (Nov 4, 2020))

Changes since 4.7

* Fixed performance issue with EmulationStation on Raspberry PI 0/1/2/3 with legacy drivers (Switch back to GLESv1 for now until issues with ES GLESv2 renderer are sorted)
* Fixed ES scraper.

### Version 4.7: (Nov 2, 2020)

Changes since 4.6

* Updated to the latest Raspberry Pi OS Buster image, with support for USB boot on the Pi4. The RetroPie 4.7 image can be flashed directly to an USB drive and booted directly, the Pi4 boot EEPROM should be updated first using Raspberry Pi Imager as detailed in https://github.com/raspberrypi/documentation/blob/master/hardware/raspberrypi/booteeprom.md.
* Added xpadneo - linux driver for xbox one wireless gamepad.
* retroarch - updated to v1.8.8.
* Added mame - standalone MAME emulator building from latest code.
* srb2 (Sonic Robo Blast 2) - updated to v2.2.2.
* cgenius - updated to 2.4.4.1.
* hatari (Atari ST emulator) - updated to v2.2.1.
* amiberry (Amiga emulator) - updated to v3.3.
* scummvm -  updated to 2.2.0
* xroar (Dragon 32 / CoCo emulator) - updated to v0.36
* ti99sim -  update to version 0.16.0 and switch to SDL2.
* Added ti99sim-sdl1 for older distros as new code requires GCC 8
* sdltrs -  switch to the SDL2 version, enable for KMS
* attractmode - now supports RPI4/KMS.
* lr-vecx - now includes GPU rendering support for smooth vector output.
* sdl1 / runcommand - fix aspect ratio using the dispmanx backend with sdl1 on fkms (this affects various sdl1 emulators such as dosbox, * daphne, openbor and others).
* lr-gpsp - fixed crash on RaspberryPi OS Buster.
* opentyrian - updated to latest code which now uses SDL2 backend.
* darkplaces-quake - added optional gles version for RPI4 with better performance.
* gemrb - updated to v0.8.6 and switched to SDL2 backend.
* lr-bnses - updated to the current BSNES version of the libretro fork.
* vice - updated to latest version, and re-enable fastsid which got disabled by default upstream.
* Improved Aarch64 support (64bit Arm) - can be manually installed on the beta 64bit Raspberry Pi OS, but is not officially supported.
* lzdoom -  update to 3.86a (This was announced as the final lzdoom release to support GL2 rendering.)
* mupen64plus - reworking of module logic - now enabled on mali targets.
* Added recognition for Jetson Nano and Tegra X1
* Added gpg signing for pre-built binaries.
* Improvements to runcommand and RPI4 videomode detection.
* Updates to Skyscraper (Metadata scraper).
* usbromservice - fixed bug with mounting ext3/ext4 partitions.
* audiosettings -  updates for Pi4 and support for discrete internal ALSA devices.
* New esthemes added.
* Various other bug fixes and improvements.
* Added new experimental modules:
  * lr-mesen - Mesen NES/Famicom emulator.
  * lr-theodore - Thomson MO/TO system emulator.
  * lr-smsplus-gx -  Sega Master System/Game Gear emulator.
  * lr-gearsystem -  Sega Master System/Game Gear/SG-1000 emulator.

### Version 4.6: (April 28, 2020)

Changes since 4.5

* Raspberry Pi 4 support! Support is labelled as beta currently as there are still things to improve, but most emulators now run well.
* The RetroPie images are now based on Raspbian Buster - Stretch is no longer supported by Raspberry Pi (Trading) ltd. RetroPie will stop updating pre-built binaries for Stretch later in the year.
* Improvements to RetroPie packaging system and core RetroPie-Setup code so package state is remembered and binary updates will only be done if an updated binary is available. Source installs won’t be overwritten by a pre-built binary when updating also. We started providing pre-built binaries for the packages in the experimental section for the supported platforms.
* RetroArch updated to v1.8.5.
  * New notification system with cheevos badges support.
  * RGUI can be themed.
  * Support for real CD ROM, with the ability to dump the disc image.
  * Improved disk control system, with support for labeling disks in .m3u files.
  * RetroAchievements support for PS1/Sega CD/PCEngine CD.
* EmulationStation updated to v2.9.1.
  * Scraper fixes for the TheGameDBNet.
  * Grid view improvements and bugfixes.
  * Theming improvements.
  * New options for "disable system name on custom collections" and "save gamelist metadata after each modification".
* Added videomode switching support to runcommand for KMS and X11 targets. SDL2 applications only.
* Added ioquake3 module for platforms other than Raspberry Pi 1-3.
* Replaced zdoom with lzdoom as zdoom is no longer maintained.
* amiberry - updated to 3.1.3 including ipf support.
* stella - updated to 6.0.1.
* SDL updated to 2.0.10 with rpi4/kms fixes.
* solarus - lots of updates to modernise the port.
* eduke32 - major overhaul including adding package for IonFury.
* zesarux - updated to v8.0.
* cgenius - updated to v2.3.6.
* drastic -  update to 2.5.0.4 with RPI4 compatibility.
* scummvm - updated to v2.1.1.
* atari800 - updated to v4.2.0 (lr-atari800 config has been moved to lr-atari800.cfg to avoid conflicting)
* lr-mupen64plus / lr-mupen64plus-next - enable GLES3 support on rpi4.
* lr-opera - renamed from lr-4do.
* Sonic Robo Blast - updated to 2.2.
* Lots of other fixes and improvements.
* Added new experimental modules.
  * vvvvvv - Port of the popular platform / puzzle game VVVVVV.
  * lr-neocd - Neo Geo CD emulator.
  * redream - Dreamcast emulator for the Raspberry Pi 4.

### Version 4.5.1: (July 17, 2019)

Changes since 4.5

* Downgraded to 4.14 kernel to resolve some 4.19 kernel/firmware issues

### Version 4.5: (July 3, 2019)

Changes since 4.4

* Dropped Raspbian/Debian Jessie support
* Raspberry Pi 3 A+ support (via Stretch firmware update)
* Many new es themes added
* Added Skyscraper (Scraper for Emulation Station game lists) 
* RetroArch updated to v1.7.6
* Amiberry (Amiga emulator) updated to v2.25, including support for launching whdload and CD32 titles from ES.
* Jzintv (Intellivision emulator) updated to 20181225 release
* atari800 - updated to v4.0.0
* Mupen64plus - updated to latest version (GlideN64 stability and compatibility improved), as well as other changes.
* Fuse (ZX Spectrum emulator) updated to v1.5.7
* ZEsarUX (ZX Spectrum emulator) updated to v7
* advmame (Advance MAME arcade emulator) - updated to v3.9
* Fixed building of quake3 for RPI.
* Added love-0.10.2 (2d Game Engine) for compatibility with older games.
* Dosbox updated to SVN r4194 including joystick fix for 360 controllers.
* CGenius - updated to v2.3.1 
* lr-flycast (libretro Dreamcast emulator) - renamed from lr-reicast and enabled for arm platforms including the RPI. 
* reicast - Switched to updated upstream repository - the latest code includes bugfixes and improvements including better game compatibility as well as our RPI fixes.
* lr-ppsspp - switched to upstream repository for latest version
* lr-fbneo  (Arcade and console emulator) - renamed from lr-fblpha - lots of improvements including neo geo cd support, and optional cyclone 68k core for better performance on slower devices for some games.The emulator can now be selected as an alternate emulator for Sega Genesis/Mastersystem/SG-1000, PC-Engine, MSX, ColecoVision and ZXSpectrum.
* Fixes and updates to many libretro cores
* Kodi updated to the 18 “Leia” release (only available in Raspbian Stretch)
* Improvements/fixes to joystick control in runcommand launch menu
* Fixes / Improvements to bluetooth pairing
* Added sixaxis driver - better DualShock 3 controller support with full bluetooth coexistence
* Third-party (Shanwan/Gasia) controller support via customhidsony & custombluez drivers
* lr-mame2014 renamed to lr-mame2015
* Emulationstation - updated to v2.8.4 which includes:
  * 2 new scrapers added for the TheGamesDB and ScreenScraper. Also many bugfixes and improvements including:
  * Gridview support now in main version
  * Hide MAME bios files by default
  * Graphical / rendering fixes
  * Loading progress
  * Allow using analog sticks for navigation
  * More flexible audio configuration
  * Lots of code refactoring, bugfixes and performance improvements, including removing boost libraries making compilation faster (and code smaller).
  * Search and load artwork based on ROM name (image and video)
  * Experimental scripting support, triggered by events.
* Added new experimental modules
  * moonlight - NVIDIA GameStream client
  * steamlink - Steam Link streaming client for Raspberry Pi 3
  * jumpnbump - multiplayer platform game
  * mysticmine - open source indie game
  * bombermaaan - Classic bomberman game
  * lr-superflappybirds - Multiplayer Flappy Bird Clone
  * lr-scummvm - libretro version of scummvm (Allows playing of many classic point and click adventures)
  * lr-x1 - Sharp X1 libretro core
  * lr-redream - Dreamcast emulator
  * lr-pokemini - Pokemon Mini emulator
  * lr-81 - Sinclair ZX81 emulator
  * lr-quasi88 - NEC PC-8801 emulator
  * splitwolf - 2-4 player split-screen Wolfenstein 3D / Spear of Destiny port
  * lr-mupen64plus-next - a new WIP Libretro core which aims to be improve upon the existing lr-mupen64plus core.

### Version 4.4: (April 14, 2018)

Changes since 4.3

* Added support for Raspbian Stretch, and switched to it for our main images, as Raspbian Jessie is no longer receiving kernel/firmware updates. Many changes were needed around the codebase to work correctly with Raspbian Stretch.
* Added basic support for the ASUS Tinker Board.
* RetroArch updated to v1.7.1 (built with video recording support via ffmpeg on Raspbian Stretch).
* AdvanceMAME updated to v3.7
* ScummVM - updated to v2.0. This fixes the controller issues and adds support for additional games.
* Stella (Atari 2600 emulator) updated to v5.0.2
* Fuse (ZX Spectrum emulator) updated to v1.4.1
* SDL2 - updated to 2.0.8
* Dosbox - Updated to latest code, implemented software MIDI synth support, and launching via .conf files directly.
* lr-freeintv libretro Intellivision emulator
* AGS - enable DIGMID support for MIDI playback on devices with no hardware MIDI Support.
* Fixes for xarcade2jstick.
* Added customhidsony, a custom hid-sony dkms driver module patched to fix the eternal vibrate bug with third-party Shanwan controllers.
* wolf4sdl - fix spear of destiny mission support.
* Zdoom - add support for launching Hexen 1 Series, Heretic, Strife and Chex 3.
* cgenius - updated to v2.2.0.
* Amiberry - update to the new SDL2 release (still using SDL1 on the Raspberry Pi due to performance reasons).
* Emulation Station improvements including Kiosk mode, and a new experimental module emulationstation-dev for those wanting to try our the very latest Emulation Station code.
* Various mupen64plus (N64 emulator) fixes.
* Removed lr-armsnes as it’s no longer developed and has only minor changes over lr-snes9x2002.
* Fix non working xm7 (Fujitsu FM-7) emulator.
* Joy2key - input mapping improvements and fixes.
* Identify and allow installing on Linux Mint Debian Edition and Deepin.
*Added various new Emulation Station themes, installable from RetroPie-Setup.
* Added new experimental modules:
  * lr-dosbox (Dosbox port for libretro)
  * dosbox-sdl2 (DOSBox port with SDL2 & FluidSynth support)
  * mame2003-plus-libretro (mame2003 with backported fixes)
  * Update lr-desmume and split 2015 version off to lr-desume2015.
  * digger - digger remastered.
  * yquake2 - Supports Quake II and both official mission packs.
  * Abuse - port of run and gun game.

### Version 4.3: (September 21, 2017)

Changes since 4.2

* Many updates to Emulation Station including:
* Collections support including Favourite, All, Recently Played and custom collections.
  * Video and Image Screensaver support.
  * Power saving modes.
  * Many theming fixes and improvements.
  * Configuration of RetroArch hotkey enable button.
  * Allow using OMXPlayer for video playback on the RPI.
  * Many other fixes and improvements. Full changelog can be found here – https://retropie.org.uk/docs/EmulationStation-Changelog/
* Added basic Odroid-XU3/4 support.
* RetroArch updated to v1.6.7. Include minimal retroarch assets for the xmb interface by default.
* AdvanceMAME updated to v3.5
* fuse updated to v1.4.0
* zesarux updated to v5.0
* lr-fbalpha updated to 0.2.97.42
* lr-imame4all renamed to lr-imame2000 to match upstream name.
* lr-bluemsx updated to add Colecovision support.
* lr-mame2003 updated with fixed audio for the Mortal Kombat series.
* Added SDL1 version of scummvm – scummvm-sdl1 – for those with joypad and MT32 issues with the standard SDL2 version.
* gamecon_gpio_rpi and db9_gpio_rpi updated for Kernel 4.9 compatibility.
* Workaround for using PCSX2 on 64bit without our custom SDL library.
* Updates/improvements to mupen64plus and the GLideN64 plugin.
* Improved controller button mapping in the RetroPie-Setup menus.
* esthemes – Many new themes available to install from esthemes configuration. Ability to update all installed themes.
* Runcommand – user menu support.
* usbromservice – fix BIOS and configuration folders not copying.
* Enabled some additional packages on Odroid boards – hatari, zdoom, openblok, alephone and lr-ppsspp.
* Bluetooth configuration – improved interoperability with the ps3 controller driver.
* New configuration tool to change terminal font size
* New packages added to experimental section:
  * pegasus-fe – Pegasus Frontend – new launcher/frontend in development.
  * lr-vice (C64 Emulator).
  * srb2 – Sonic Robo Blast 2 port.
  * cdogs-sdl – C-Dogs SDL – Classic overhead run-and-gun game.
  * lr-px68k (x68000 emulator).
* Many other fixes and improvements.


### Version 4.2: (March 19, 2017)

Changes since 4.1

- EmulationStation Improvements
    - Video Support
    - White Screen of Death Fix
- Support for the ODroid-C2  (on top of the Ubuntu 16.04 minimal image).
- Kodi 17 now installable from optional packages.
- AdvanceMame has been updated and split into three separate packages -  0.94, 1.4 and v3.3.
- Updated to RetroArch v1.5.0
- To match upstream changes, lr-mupen64plus has been renamed to lr-parallel-n64, and lr-glupen64 has been renamed to lr-mupen64plus.
- Fixed launching Pixel desktop and other X11 apps from Emulation Station.
- Fixed problems building Zdoom, ResidualVM and Mupen64Plus and PPSSPP.
- Doom ports will automatically add launch scripts if it finds doom1.wad, doom2.wad, tnt.wad, or plutonia.wad.
- lr-snes9x emulator added - a libretro port of the current snes9x codebase.
- Added Amiberry (an Amiga emulator), which is an updated fork of uae4arm, with more features.
- Multi disk zip support for Vice (C64 emulator), fs-uae, uae4arm and Amiberry (Amiga). You can now launch Amiga disk images directly from Emulation Station with uae4arm and Amiberry.
- Standalone version of Stella (Atari 2600 emulator) updated to v4.7.3.
- usbromservice - support mounting of usb stick over ~/RetroPie to keep roms on USB.
- Ability to set custom ES themes in configs/all/platforms.cfg (can override any setting in RetroPie-Setup/platforms.cfg).
- SDL2 updated to 2.0.5. Our patched SDL2 is now used on the PC version of RetroPie, which should resolve an issue with ps3 controller mapping.
- Sselph’s scraper updated to the latest version, and new options added. Scraper has been moved to optional packages and need to be installed before it will show up in configuration / tools.
- Include PowerBlock and ControlBlock driver packages.
- Input configuration script for Daphne.
- RetroPie-Setup menus now works with all connected joysticks (mapping is still hardcoded).
- Updated RPI detection code to support BRANCH=next firmware/kernel.
- Overhaul of the runcommand launch script.
- Raspbian Wheezy support removed.
- Support Xbian on RPI,  and Devuan, Elementary OS, and Neon on X86.
- Added emulationstation themes: fundamental, futura, and flat.
- New packages added to experimental section:
    - lr-mrboom (an 8 player bomberman clone).
    - lr-mame2016 (Arcade emulator).
    - lr-mess2016 (Multiple omputers/console emulator).
    - DraStic (Nintendo DS Emulator - RPI only).
    - lr-beetle-saturn (Sega Saturn emulator - x86_64 only).
    - Minivmac (Macintosh Plus Emulator).
    - Quasi88 (NEC PC-8801 emulator).
    - np2pi (NEC PC-9801 emulator).
    - Xm7 (FM-7 / Fujitsu Micro 7 emulator).
    - Mehstation and Attract-Mode Frontends.
    - launchingimages (a script from Meleu to generate system launch images based on installed Emulation Station themes).
- Many other code changes and bugfixes.


### Version 4.1: (November 5, 2016)

Changes since 4.0.2:

* Updated RetroArch and many libretro cores to the latest versions.
* Some libretro packages have been renamed to match the upstream core names:
 * lr-fba to lr-fbalpha2012
 * lr-fba-next to lr-fbalpha
 * lr-pocketsnes to lr-snes9x2002
 * lr-catsfc to lr-snes9x2005
 * lr-snes9x-next to lr-snes9x2010
* Updated Vice (C64 emulator) to the latest version.
* Fixed PPSSPP building on the RPI and updated it to the latest version.
* lr-fba-next updated to fbalpha v0.2.97.39 including fixes for Irem hardware on arm (rtype / rtype 2 etc)
* WiFi configuration - added ability to import Wifi ssid/psk from /boot/wifikeyfile.txt for set-up without a keyboard.
* Updated Fuse (Spectrum emulator) to v1.3.0
* Updated Zesarux (Spectrum / CPC emulator) to the latest version.
* Include lr-glupen64 by default on image (moved from optional to main).
* Added darkplaces-quake to optional packages. When installing/update the Quake emulators, launch scripts for any installed mission packs will be created.
* Build ResidualVM with SDL2 + opengles support.
* Added steam controller driver from https://github.com/ynsta/steamcontroller
* Added mk_arcade_joystick_rpi driver from https://github.com/recalbox/mk_arcade_joystick_rpi
* Fixed build issues on uae4arm, and kickstart removal on upgrade of uae4arm/uae4all.
* Screensaver / Screen dimming in Emulation Station no longer stops the built in scraper.
* Compatibility with upstream plymouth changes. Image is based on the latest upstream Raspbian Lite from 2016-09-23 with all updates.
* New themes added to the theme installer - including pixel-meta, pixel-tft, luminous, minilumi from Rookervik and io and spare themes from Mattrixk
* New packages added to experimental section
 * Added emulators lr-beetle-pcfx (PCFX emulator)
 * Added retropie-manager web interface (based on recalbox-manager).
 * Added pcsx2 emulator (Playstation 2 emulator - x86 / x86_64 only).
 * Added openpht  (x86 / x86_64 only).
 * Added fs-uae (Amiga emulator - x86 / x86_64 only).
 * Added lr-bsnes (Super Nintendo emulator - x86/x86_64 only)
 * Added lr-hatari (Atari ST/STE/TT/Falcon emulator)
* Added some RetroPie-Setup function documentation to aid those contributing code - https://retropie.org.uk/retropie-setup-api/
* Various other improvements / bugfixes

### Version 4.0: (August 19, 2016)

Changes since 3.8.1:

* Setup script improvements:
  * Added the ability to install/update and remove packages.
  * Added help docs to the setup script.
* Renamed mednafen emulators to beetle to match upstream libretro repositories.
* Renaming of ES input configuration which was causing confusion for shoulder/trigger inputs.
* Much faster Emulation Station start-up in gamelist only mode.
* Updated Xpad driver included with “trigger to button” enabled, so mapping of Xbox 360 / Logitech trigger buttons is easier.
* Input configuration script to set up player 1 automatically on pifba and pisnes.
* Configuration Editor can now help you configure player gamepad order for libretro emulators.
* Updated PSP emulators ppsspp and lr-ppsspp with a fix for the pausing during play.
* Autostart improvements: boot to kodi option added - (exiting kodi will take you back to emulationstation).
* Improvements to mupen64plus Glide64 video plugin, which is now the default.
* Added new libretro emulator based on mupen64 - lr-glupen64.
* lr-mame2003 updates - support for mice/analogue joystick support. Fixed aspect ratio issues.
* Updates to various other emulators including reicast, lr-fceumm, lr-nestopia, lr-snes9x-next and the RetroArch frontend.
* SDL2 dispmanx scaling, so SDL2 software can render to a lower resolution and be scaled in hardware. This enhances performance on mupen64plus for example, without having to change the video mode.
* Improvements to the Bluetooth module, including the ability to try and reconnect to devices in the background, and an option to switch off our mapping hack for 8bitdo, so devices with a newer firmware will map correctly for RetroArch. Fix pairing with Android phones.
* Splashscreen improvements: New default splashscreen and a new splashscreen repository with additional splashscreens.
* Support for configs/all/runcommand-onstart.sh  configs/all/runcommand-onend.sh user scripts
* New experimental modules:
  * TRS-80 emulator sdltrs.
  * TI-99/4A emulator ti99sim.
  * Oric 1/Atmos emulator Oricutron.
  * Dinothawr (lr-dinothawr - standalone libretro puzzle game).
  * lr-mame2014  (Late 2014/Early 2015 version of MAME - uses 0.159 romset)
  * Alternate Virtual Gamepad by sbidolach.
 * Various other bug fixes and improvements.

### Version 3.8.1: (June 4, 2016)

 - Fix escaping in iniSet causing initial backslashes to be incorrect in ini files (Affected some +Start Scripts with spaces such as DOSBox).
 - Don’t overwrite existing configs when updating advmame.
 - SSelph’s scraper – Add option to set -append and -use_nointro_name=false flags
 - Disable binary install on Wheezy.
 - Fix building of gamecondriver.
 - Correct Emulation Station autobooting configuration due to changes in raspi-config.
 - Added missing zip dependency for Solarus.
 - Fix c&p error with mupen64plus that broke the initial config generation.
 - Added new EmulationStation theme “material” from user lilbud.
 - Lr-nxengine – no error message was shown when required data files are missing.

### Version 3.8: (May 27, 2016)
 - Raspbian package/firmware rollups that fix the lockups with the Raspberry Pi 3 internal bluetooth.
 - New SDL1 dispmanx backend from Vanfanel with triple buffering which should solve some of the performance issues on the previous code. Also some additional changes are included so you can adjust the aspect ratio with env variable SDL_DISPMANX_RATIO (eg 1.33 for 4:3). The aspect ratio will be ignored if SDL_DISPMANX_IGNORE_RATIO is set and sdl1 apps will display full screen. Vice is now set to use 4:3 ratio on the Raspberry Pi.
 - Reicast (Dreamcast emulator), now supports multiplayer.
 - lr-pcsx-rearmed (PlayStation emulator) now supports 3-8 players.
 - Updated Raspberry Pi binaries for lr-fba-next, uae4arm, mupen64plus, Reicast, lr-picodrive, lr-nestopia, lr-pcsx-rearmed, lr-mgba, lr-genesis-plus-gx, lr-mame2003, and lr-fceum.
 - Added new videocore mupen64plus video plugin.
 - Improvements to Apple2 (supports automount now).
 - Added wiki viewer.
 - Improvements to the splashscreen module (added previewer, randomiser, and no longer requires a folder to be created in the splashscreen directory).
 - Various other bugfixes and minor improvements.

### Version 3.7: (April 14, 2016)

- Added new experimental modules: 
  - The Ur Quan Masters  (Port of DOS game Star Control 2).
  - Xrick (Port of Rick Dangerous).
  - Tyrquake (Standalone, not libretro).
  - Solarus Engine (Homebrew Zelda Clone).
  - SDLPoP (Prince of Persia Port).
  - Cannonball (Outrun Engine).
  - Stratagus (Warcraft and Starcraft Engine).
  - OpenBOR (Beats of Rage 2d Sidescrolling Game Engine).
  - Commander Genius (Port of Commander Keen).
  - Micropolis (Open source version of Sim City Classic).
  - Aleph One (Open Source port of Marathon Series).
  - Giana’s Return (Fan-Made sequel to the Giana Sisters).
  - Lincity (Sim City Clone).
  - Simcoupe (SAM Coupé Emulator).
- LXDE Desktop (Option in raspi-tools to reinstall the desktop environment).
- Updated Kodi to Kodi 16 (which includes joypad support).
- Updated PS3 Module (timeout fixed).
- SDL2 PS3/Wii U Pro controller fixes.
- UAE4Arm updated.
- lr-mame2003 updated with sample/nvram support and additional core settings.
- Mupen64plus updated with fix for black screen with rice plugin.
- Scummvm Improvements (updated to 1.8 with OpenGL and partial Myst support).
- Updated Config Editor (Configuration-Editor).
- Updated Carbon and Pixel Themes and added default images to the RetroPie Menu.
- Added “Other Settings” menu to Emulationstation with “save metadata on exit” and “parse gamelists only”. These options were added to mitigate the long boot and shutdown times with large romsets.
- Various other improvements and fixes.

### Version 3.6: (March 1, 2016)

**Added Support for the Raspberry Pi 3 [Via Raspbian Firmware Update]**

- Added new experimental modules:
 - Daphne (Laserdisc Emulator)
 - Libretro-QuickNES
 - Libretro-Beetle PSX (x86 only)
 - Libretro-Beetle Lynx
 - GemRB engine (Baldur’s Gate, Icewind Dale, Planescape)
 - ResidualVM (Engine for Grim Fandango and Escape from Monkey Island)
 - Libretro-MESS (based on the most recent version of MAME)
 - Libretro-MAME (based on the most recent version of MAME)
- Added EmulationStation theme Simpler Turtle Pi to the theme installer from Omnija.
- Added version details and uninstall option to the RetroPie Setup Script.
- Fixed insert coin not working on arcade based emulators.
- Various other bugfixes and improvements.

### Version 3.5: (February 6, 2016)

After taking into consideration the feedback from the vibrant RetroPie community, we have provided a few more functions to simplify the user experience such as automatic expansion of the filesystem on boot, less terminal text, and more configuration options for the runcommand launch menu. We have also fixed up some bugs with Raspbian Jessie such as the USB ROM service and have added two new experimental modules - the Löve game engine and a ColecoVision emulator (CoolCV). 

 - Added new experimental modules, Lӧve 2D Game Engine, Colecovision (CoolCV).
 - Debian usbmount package fixed up for systemd udev compatibility, making the USB ROM service work properly again without being killed after 30 seconds. Also added ntfs support by default.
 - Added an arcade rom folder option where all arcade games can be placed. 
 - Improvements to EmulationStation (Fix crash on rom delete, direct launch, symlink support, and other bug fixes).
 - Improvements to the Runcommand Launch Menu: Cleaner dialog on launch, ability to show game artwork on launch, ability to disable joystick support as well as the ability to disable the entire runcommand launch menu.
 - PS3 Controller improvements - Add multiple gasia and shanwan controller support.
 - Updated lr-mgba emulator binaries (new upstream release of mgba 0.4.0)
 - Improvements on pre-built image - disabled screen blanking, quieter boot, and filesystem automatically expanded on first boot.
 - Various other bug fixes.

### Version 3.4: (January 19, 2016)

Mostly fixes and improvements rather than new stuff this time folks. There were some problems with our RetroArch configuration defaults in RetroPie 3.3 which should be sorted now, and we have fixed up a few things that didn’t work correctly with Raspbian Jessie. We also have added early support for using the RetroPie-Setup script on a X86/X11 desktop setup, as well as some basic support for building EmulationStation & RetroArch + cores on the ODroid-C1. For more information regarding installation on x86 see [RetroPie PC installation](Debian).

We are now using Raspbian Jessie as the base for the RetroPie image. Those using Wheezy can update RetroPie-Setup and emulators by following the instructions [here](Updating-RetroPie) - however moving to Jessie is recommended. As it takes time to pre-build binaries, in the future we will only be providing pre-built binaries for Raspbian Jessie.

Changes since 3.3:

- Now using Raspbian Jessie for the RetroPie image. 
- Fixes for controller input issues with RetroArch including improved config generation to work around problems with 8bitdo controllers.
- Fixed up Bluetooth pairing module on Jessie.
- Improvements to the Xbox userspace driver (xboxdrv) including partial support of Xbox One controller.
- Can now choose to exit or restart Emulation Station. Metadata will no longer be lost if choosing to shutdown or reboot.
- Preliminary support for using the RetroPie-Setup script on x86 + X11 on Debian/Ubuntu and Ubuntu on the Odroid-C1 (building from source only).
- $HOME/.emulationstation has relocated to /opt/retropie/configs/all/emulationstation - but is symlinked from the original location. The USB Rom Service script will backup all of /opt/retropie/configs to USB. Previously it only backed up /$HOME/.emulationstation.
- Support for choosing RetroArch shaders and overlays from the RetroPie-Setup configuration editor.
- Added pixel theme from Rookervik to theme installer.
- Wonderswan and NeoGeo Pocket separated into Wonderswan/Wonderswan Colour, NeoGeo Pocket/NeoGeo Pocket Colour. 
- Various other bugfixes and improvements.

### Version 3.3: (December 21, 2015)

- Mupen64plus controller configs (including hotkeys) and Reicast (Dreamcast) controller configs added to the autoconfiguration script in emulationstation. Mupen64plus is now the default n64 emulator due to compatibility.
- AdvanceMAME 1.4 (replaces 1.2 - still based on MAME 0.106).
- PlayStation Portable emulator ppsspp is included by default (libretro version is default, the standalone version is optional).
- Removed cpc4rpi emulator, and added CapriceRPI which has many improvements over cpc4rpi.
- Updated libretro binaries including lr-fba-next updated to v0.2.97.37, and an improved lr-caprice32 which is now moved out of experimental and is the default Amstrad CPC emulator.
- Updates to Reicast emulator, which has been moved out of experimental.
- New experimental modules: OpenTTD (open source simulation game based on Transport Tycoon Deluxe), Wolf4SDL (Port of Wolfenstein 3d), Zdoom (Enhanced Port of the official DOOM source)
- PS3 controller improvements (added Gasia PS3 clone Support).
- Updated OpenMSX emulator (to the dev version 0.12.0+).
- Beta images based on Raspbian Jessie are included. They may have bugs that are not present in the Raspbian Wheezy release.
- New themes added to the theme installer (Eudora from AmadhiX, Tronkyfran from Tronkyfran, and Retroplay Canela from InsecureSpike).
- RetroArch joy-config tool removed (custom configs are now done through the RGUI or manually).
- Various other bugfixes/improvements.


### Version 3.2.1: (October 28, 2015)

- Fixes issues with controller d-pad configurations for all RetroArch-based emulators.

### Version 3.2: (October 26, 2015)

- Fixed binaries of mupen64plus and lr-tyrquake and removed mupen64plus-testing as it is now included in the default mupen64plus.
- Updated to Hatari 1.9, and built in IPF image support.
- Binary installs are now supported for those running under Raspbian Jessie - although there still may be bugs.
- New experimental modules - ppsspp / lr-ppsspp (PlayStation Portable emulator), px68k (X68000 emulator - too slow to be usable on a rpi2 though), opentyrian (a port of the DOS shoot-em-up Tyrian), and SuperTux.
uae4arm is now moved from experimental.
- Improvements to the generic bluetooth pairing module.
- Improvements to ps3controller pairing
- Fixed SNESDev driver building (failed on first attempt).
- New Turtle Pi Emulation Station theme installable via the themes installer
- GLideN64 video plugin for mupen64plus
- Various other bugfixes.

### Version 3.1: (October 6, 2015)

* Workaround for lr-snes9x-next crashes for certain games.
* New theme installation script and excellent new theme “Carbon” which is lighter on memory than the Simple theme (no more white screen of death! - works with all systems).
* Initial bluetooth module for pairing keyboards.
* We now provide images for use with Berryboot.
* Moved Super Mario War out of experimental.
* New default lr-fba-next emulator for rpi2 owners.
* Added lr-mame2003 (based on MAME 0.78) emulator.
* Minor Emulation Station tweaks, reduced time to skip buttons, and improved parsing with brackets in gamelists.
* New experimental modules - sselph’s scraper and lr-mame2010 (based on MAME 0.139)
Improved ps3 controller pairing.
* Initial support for installing RetroPie manually on Raspbian Jessie and OSMC (via source only - consider this experimental for now).
* Splashscreen improvements- can be added from samba shares, splash videos play all the way through without emulationstation cutting them off.
* Lots of bugfixes, and improvements to the RetroPie Wiki.

### Version 3.0.0 Stable : (August 11, 2015)

* New GUI for basic WiFi configuration and Config editing
* Added Dragon 32 / TRS-80 (CoCo) emulator xroar
* Added Super Mario War to ports
* Move some emulators out of experimental – lr-bluemsx (Now default for msx), lr-mednafen-ngp, lr-mednafen-wswan, lr-mgba, lr-tgbdual, lr-vba-next
* Added virtualgamepad to experimental which allows gamepad emulation via a mobile
* Restarting setup script no longer needed after updating the setup script.
* Improved support for video splashscreens and a centralised splashscreen repo (https://github.com/RetroPie/retropie-splashscreens)

### Version 3.0.0 RC1: (July 18, 2015)

* Input configuration improvements / fixes / optimisations
* Basic joypad control in RetroPie-Setup / emulator prelaunch menus.
* Make libretro Fuse default spectrum emulator (for easier joypad control)
* Added new spectrum emulator ZEsarUX to the experimental section.
* Added launching RetroArch with RGUI from the RetroPie menu in EmulationStation.
* Various other bugfixes – you can follow changes as they happen on the GitHub site –https://github.com/RetroPie/RetroPie-Setup/commits/master

### Version 3.0.0 BETA 4: (June 18, 2015)

* Work around issue with RetroArch GUI not accepting input/freezing.
* Fixed up RetroArch control configuration via our new integrated input configuration.
* Moved RetroArch joypad cofigurations to /opt/retropie/configs/all/retroarch-joypads

### Version 3.0.0 BETA 3: (June 10, 2015)
* Integrated controls configuration for EmulationStation and RetroArch – On first start EmulationStation will ask for controls to be configured, and will then also configure RetroArch based on your choices. Note that there will be a delay after selecting OK whilst this is done – this will be improved later to give feedback so it doesn’t look as though EmulationStation has frozen.
* New experimental modules/emulators: limelight (Networked game streamer for Steam), lr-tgbdual (gameboy color emu with link support), DXX-Rebirth port (Decent 1/2), r-mednafen-wswan (Wonderswan emu), lr-mednagen-gbp (NeoGeo Pocket emu), uae4arm (Amiga emu), lr-fuse (ZX Spectrum emu), lr-caprice32 (Amstrad CPC emu), lr-gw (Game and Watch simulator). All modules prefixed with lr- are libretro cores for use with Retroarch.
* New startup picture with new RetroPie logo.
* Added additional ES theme “Color Pi”
* Dosbox bug fixes / Ability to launch custom shell scripts.
* Wifi configuration under RetroPie menu.
* PS3 controller setup improvements
* Disabled root password by default
* Various other fixes / improvements.

### Version 3.0.0 BETA 2: (April 4, 2015)

 * More launch options for Hatari
 * Resize framebuffer with video mode change (and allow framebuffer res to be changed independently for terminal/X apps)
 * Improvements to minecraft-pi launch script
 * Added some experimental modules – Adventure Game Studio engine, yabause (Sega saturn), virtualjaguar (Atari Jaguar), beetle-vb (Virtualboy), mgba (game boy advance)
 * Added ProSystem (Atari 7800 emulator)
 * Fixes to mupen64plus build
 * Various other fixes / Improvements

### Version 3.0.0 BETA (March 26, 2015)

* Overhaul of emulator selection / launching – single rom folder per platform, with the facility to change default emulator per platform or per rom on launch. Also allows launch of certain emulators with specific configurations, such as render plugin for mupen64plus, and model configuration for fuse.
* RetroArch render resolution is also configurable on launch. Video output is no longer switched by default, but can be adjusted by the user if needed.
* New retropie menu in EmulationStation with easy access to retropie-setup, file manager, audio settings, controller settings, raspi-config and so on.
* Emulationstation entries are now sorted (by name) – should mostly match alphabetical order of rom folders.
* Work to ensure user configurations are preserved. More configuration files moved to /opt/retropie/configs/ structure.
* EmulationStation restarts on exit by default unless a key is pressed. Makes it easier for those that want to quick and let it restart to pick up any new roms.
* New platforms.cfg file that contains emulator names / supported file extensions. This can be copied to /opt/retropie/configs/all to override extensions added to emulationstation (A reinstall / re-configuration of
the a related emulator is needed after to update the emulationstation configuration)
* Addition of AdvanceMAME 1.2 (based on MAME 0.106) which may be useful for rpi2 owners over the 0.94 version. Framebuffer output code adjusted to work better with the Pi.
* rpix86 is included again by default (was missing from the last image).
* Updates to the usbromservice. If you want to sync rom folders it now requires a folder in the root of the usb stick called “retropie”. The roms will be synced from a sub folder called roms. It also can backup/restore your custom emulationstation gameslists / data.
* RetroArch includes additional shaders and overlays
* Various other emulator updates and fixes.

### Version 2.6.0 (February 17, 2015)

* new uae4all emulator
* updated sdl 1.x with rpi fixes for fbcon and dispmanx backend.
* rpi2 optimisations for dosbox
* update hatari emulator
* jzintv updates
* mupen64plus/mupen64plus-libretro changes/fixes
* atari800 updates (with gles support on rpi)
* allow genesis libretro core to be used for mastersystem
* new experimental cores for gb advance (rpi2 only), and nes
* optimisation / fixes for rpi
* various other fixes / improvements

### Version 2.5.0 (February 7, 2015)

* Updated to latest firmware to support Raspberry Pi 2 (TM)
* Usb rom service should now be working
* updated all binaries
* mupen64plus is out of experimental
* added gpu_mem_1024 to config.txt
* removed overclocking settings
* simplified rom folder permissions
* removed ignore_safe_mode as safe mode is removed since march 2014

### Version 2.4.2 (January 17, 2015)

* reworked vice c64 emulator – defaults with dispmanx, but should run without now without also. Comes with a default config which is better
* suited for the pi. config now resides in /opt/retropie/configs/c64/ rather than home directory.
* retronet improvements – now can enable on game launch from runcommand menu.
* added vectrex libretro core
* always reset framebuffer even when not switching screen mode in runcommmand.sh which should help some emulators that seem to leave the framebuffer in an unusable state.
* fix for fmsx rom install
* use dispmanx sdl by default for uae4all
* use dispmanx sdl by default for dgen
* mame4all configs moved to /opt/retropie/configs/mame/ rather than mame4all (to match existing structure) 

### Version 2.4.1 (January 11, 2015)

* Minor bug fixes
* Updated RetroPie-Setup Script

### Version 2.4 (January 6, 2015)

* Update of all components, e.g., RetroArch supports ZIP files natively now
* Dispmanx can be activated or deactivated for each emulator individually now
* The screen mode is configurable for each emulator individually now
* Added Atari Lynx emulator
* Added Darkplaces Quake (experimental)
* Added Minecraft-Pi (experimental)
* Added OpenMSX (experimental)
* Enhanced integration of ScummVM
* Stripped down number of installed system packages to a minimum
* Several bug fixes
* Reorganization of the binaries
* Separation of sources and binaries

### Version 2.3 (July 20, 2014)

* Several bug fixes

### Version 2.2 (July 5, 2014)

* Added Mednafen PCE Fast
* Fixed configurations for sega32x, segacd
* Updated SAMBA configuration
* Fixed imame4all-rpi rom dir configuration
* Updated Python help scripts

### Version 2.1 (June 29, 2014)

* Fixed black screen when exiting to console
* Fixed Doom Shareware starter
* Removed hidden meta data files from FBA and Megadrive rome directory

### Version 2.0 (May 29, 2014)

* Reorganized folder structure (root dir is now /opt/retropie)
* Complete rebuild of all binaries with latest versions
* EmulationStation 2 as new front-end
* Added MSX emulator OpenMSX
* Refactored RetroPie-Setup Script with command line capabilities

### Version 1.10.1 (Dec 2, 2013)

* Updated Raspbian to the latest packages
* Updated the default splash screen
* Added x86 emulator FastDosbox

### Version 1.9.1 (November 12, 2013)

* Fixed “freezing” bug

### Version 1.9 (November 6, 2013)

* Added emulator Mame4All-RPi
* Added emulator Mupen64Plus-RPi
* Added splash screen configuration to RetroPie Setup Script
* Added configuration menu for RetroArch NetPlay to RetroPie Setup Script
* Enhanced debug log functionality of RetroPie Setup Script

### Version 1.8.1 (September 13, 2013)

* Added freezing fix for Emulation Station
* Re-added source-based installation function for PC-Engine Libretro core

### Version 1.8 (September 4, 2013)

* Added (Libretro based) Genesis emulator Picodrive
* Added emulator PiFBA
* Updated Emulation Station, x86 emulator, and RetroArch to latest release

### Version 1.7 (July 14, 2013)

* Added ES-Config
* Added Atari 2600 emulator Stella
* Updated Emulation Station, x86 emulator to latest releases

### Version 1.6.1 (June 12, 2013)

* Fixed GPSP binary

### Version 1.6 (June 5, 2013)

* Added emulator Basilisk II
* Added Dispmanx
* Updated every installable component
* Enhanced script for switching between resolutions

### Version 1.5 (May 5 2013)

* Added emulator gpSP
* Added emulator SNES9X-RPi
* Added emulator PiSNES
* Added GPIO gamepad drivers
* Updated Emulation Station
* Updated rpix86

### Version 1.4.1 (April 17, 2013)

* Updated Emulation Station
* Updated rpix86

### Version 1.4 (April 7, 2013)

* Added system-dependent change of HDMI video resolution for increased performance for RetroArch-based emulators.
* Added automatic USB ROM-copy service
* Added x86 emulator rpix86
* Added Apple ][ emulator Linapple
* Enhanced themes

### Version 1.3.1 (March 18, 2013)

* Minor changes in the file organization

### Version 1.3 (March 7, 2013)

* Added NXEngine / Cavestory
* Updated DGEN to version 1.32
* Enhanced pre-defined RetroArch input configuration

### Version 1.2.1 (February 25, 2013)

* Resized partition so that the image fits on 4 GB cards

### Version 1.2 (February 20, 2013)

* Added Intellivision emulator
* Added SAMBA share installation and configuration
* Used binaries-based setup for generating the SD-card image
* Updated themes

### Version 1.1 (February 10, 2013)

* Added AdvMAME emulator
* (Re-)added Genesis-GX RetroArch core
* Added Final Burn Alpha emulator

### Version 1.0 (July 22, 2012)

**RetroPie is Born!**