# polybar-buds

A simple short script to quickly switch between A2DB Sink and HFP, as well as disconnect/connect to a specific bluetooth headset/earbuds.

#Prequisites

##Before using this tool, please ensure that you have the following packages:

pulseaudio
pulseaudio-bluetooth
bluez
bluez-utils

##Ensure that you have already paired the bluetooth headset via bluetoothctl

A guide to do that can be found at:

https://wiki.archlinux.org/title/Bluetooth#Pairing

#Additional information

The script used to control the headset is dead simple. I use pacmd to toggle the headset's profile using the padmd "name" param which is just bluez_card.{MAC_ADDRESS}, and I use bluetoothctl to disconnect and connect based on the mac address (which)
