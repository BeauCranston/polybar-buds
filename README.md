# polybar-buds

A simple short script to quickly switch between A2DB Sink and HFP, as well as disconnect/connect to a specific bluetooth headset/earbuds.

I wanted to address the horrible support for wireless earbuds that have a microphone. The sound is fine, until you want to use the mic functionality.... HFP SUCKS.

The problem I found with having the system automatically switch between profiles is that the profiles switch whenever the system detects any sort of mic input channels open. Listening to music, and opening up discord for example would instantly kill my audio.

When you don't have automatic profile switching, you must do it manually either through cli or through pavucontrol (or whatever gui you use).

Also I hate having to connect my bluetooth microphone through a GUI or bluetoothctl, so I wanted a quick way of connecting and disconnecting.

The polybar-buds module hopefully solves all of these issues for the niche community of Arch users that use Pulse Audio, have a bluetooth headset / earbuds, and also use polybar.

## Prequisites

### Before using this tool, please ensure that you have the following packages:

pulseaudio
pulseaudio-bluetooth
bluez
bluez-utils
nerd-fonts

### Ensure that you have already paired and connected the bluetooth headset via bluetoothctl

A guide to do that can be found at:

https://wiki.archlinux.org/title/Bluetooth#Pairing

### Upon initial setup, your bluetooth headset will have to be connected so that you can grab the pacmd information for your device

## Additional information

The script used to control the headset is dead simple. I use pacmd to toggle the headset's profile using the padmd "name" param which is just bluez_card.{MAC_ADDRESS}, and I use bluetoothctl to disconnect and connect based on the mac address (which)

If you ever want to switch headsets to a different bluetooth headset, all you have to do is change the BT_HEADSET_NAME and BT_HEADSET_MAC env values to the new headset in the env.sh file (see the guide below).

## Setup Guide

1. Clone the git repo (or you can just download the project as a zip)

2. Copy the polybar-buds directory into ~/.config/polybar/scripts/

3. Copy and paste the contents of config.ini into your polybar config.ini at ~/.config/polybar/config.ini. (if your folder structure is different, you will need to manually modify path references in the config.ini contents and in the polybar-buds.sh script.)

or copy from here if you don't want to download a zip or clone the repo:

```
[module/headset]
type = custom/script
exec = source ~/.config/polybar/scripts/polybar-buds/env.sh && ~/.config/polybar/scripts/polybar-buds/polybar-buds.sh init
click-left = source ~/.config/polybar/scripts/polybar-buds/env.sh && ~/.config/polybar/scripts/polybar-buds/polybar-buds.sh toggle
click-right = source ~/.config/polybar/scripts/polybar-buds/env.sh && ~/.config/polybar/scripts/polybar-buds/polybar-buds.sh connect
env-PLAYBACK_ICON=󰋋
env-MIC_ICON=
env-DISCONNECTED_ICON=󰟎
label=" %output% "
interval=2

```

remember to register the module to your bar!

4. Open the env.sh file. You should see BT_HEADSET_NAME and BT_HEADSET_MAC as empty values.

5. run the following command: pacmd list-cards

6. search for the card that represents your bluetooth device (device must be connected at this point)

7. copy the "name" value which should look like this (ignore the angle brackets and only copy the name):
   name: <bluez_card.C4_SS_3A_FF_63_50>

   Paste the name into the BT_HEADSET_NAME value in the env.sh file

8. run: bluetoothctl devices Connected

the output will look like so : Device D8:1F:22:9E:8B:30 HUAWEI FreeBuds Pro 3

9. Copy the MAC address portion (ex: D8:1F:22:9E:8B:30)

10. Paste the MAC address into the BT_HEADSET_MAC value in the env.sh

After the above steps are completed you should be all set to use polybar-buds!

## Controls

Left-Click: will toggle from playback mode to mic mode

Right-Click: will disconnect or connect your bluetooth headset

## Font

If the icons end up being too small, create a new font inside of your bar section. You will need nerd-fonts for the icons to show at all.

For example this is my font for these icons specifically:
font-3 = "RobotoMono Nerd Font:size=14;2"

Please let me know how this all works! This is my first time creating anything like thisand if you have any suggestions on how to make this polybar script better I would also love to hear.

Thanks!
