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

##Guide

Go to the polybar-buds-env.sh file and enter the name of the bluetooth headset into the BLUETOOTH_HEADSET_NAME value.

To find the "name" of the bluetooth device run the following command: pacmd ls

All of the pulse audio channels will be listed. You just need to find the channel for your device. The name that you are looking for will look something like this

    name: <bluez_card.C4_SS_3A_FF_63_50>

ignore the angle braces and copy the name inside of them.
