# Introduction
This repo contains tools to flush AMD RX580 vbios under WIN11 system.
The routine is verified under win-11 safe mode.
You can use this direction if one of your bios is incorrectly flushed and malfunctioning.

# Files
| filename | description |
| ----- | ------- |
| amdvbflash.exe | amdvbflash3.04 working on win11 and safe mode |
| insttool64.exe  | install this before using amdvbflash.exe |
| gpuz-left.rom  | left switch vbios of my rx580 sapphire nitro+ 8GB exported using gpuz, this is a working legacy vbios |
| cmd-left.rom  | left switch vbios of my rx580 sapphire nitro+ 8GB exported using amdvbflash command, this is a working legacy vbios |
| Sapphire.RX580limited.8192.170320_1.rom  | vbios that supports UEFI booting, verified to be working fine. |

# Usage
1. enter safe mode according to [Windows-Manuall](https://support.microsoft.com/zh-cn/windows/%E5%9C%A8-windows-%E4%B8%AD%E4%BB%A5%E5%AE%89%E5%85%A8%E6%A8%A1%E5%BC%8F%E5%90%AF%E5%8A%A8%E7%94%B5%E8%84%91-92c27cff-db89-8644-1ce4-b3e5e56fe234)
1. open cmd.exe
1. `cd` to this folder
1. `amdvbflash.exe -i` to inspect cards and connector ids. usually the desired AMD card id is 0.
1. `amdvbflash.exe -s 0 backup.rom` this will dump the current bios into current directory.
1. `amdvbflash.exe -unlockrom 0` unlock first to be able to flush later.
1. `amdvbflash.exe -f -p 0 Sapphire.RX580limited.8192.170320_1.rom` wait until finish and reboot.


# If one of your vbios is damaged
1. toggle vbios switch to the functioning one.
1. boot your system, and follow the [Windows-Manuall](https://support.microsoft.com/zh-cn/windows/%E5%9C%A8-windows-%E4%B8%AD%E4%BB%A5%E5%AE%89%E5%85%A8%E6%A8%A1%E5%BC%8F%E5%90%AF%E5%8A%A8%E7%94%B5%E8%84%91-92c27cff-db89-8644-1ce4-b3e5e56fe234) to enter safe mode.
1. after entering the safe mode, toggle vbios switch to the damaged one while the computer is running. this will direct vbios interaction to the damaged vbios flash-chip.
1. follow instructions in Usage chapter and reboot to verify the newly flashed vbios.
1. repeat this procedure if another vbios file should be tested.

# If you cannot access your motherboard bios interface
1. poweroff your machine.
1. unplug the 8-pin and 6-pin power supplies of your dGPU. but keep the GPU PCIE connected.
1. plug video cable in to the on-board HDMI or DP port.
1. power on and you will see bios entrace prompt after a short while.
1. enter your motherboard bios interface and find "CSM" option.
1. set CSM to `on`, and then set graphic vbios mode to `legacy` instead of auto or UEFI.
1. save and reboot and then power off.
1. replug power supplies for your dGPU, and restore your normal cable port connection.
1. power on and you will see the motherboard bios entrance normally displayed. 
