# Ubiquiti Unifi WiFi access point "UAP LR" vs "UAP AC Pro"

My old Linksys access-point was showing signs of weaknesses and I decided to change for something a bit more professionnal.

I went (by mistake) with an Ubiquiti "UAP LR". LR stands for long-range.

Actually Ubiquiti don't advertise UAP access-point so much anymore. Those are limited to 2.4GHz range. The one I really needed was an "UAP AC" (dual 2.4GHz and 5GHz bands) that is almost double the price.

First of all, you have to install a "controller" to install the AP. There's no embedded HTTP server or whatever on those AP's.

Controller offers interesting features like roaming and statistics, but you don't have to keep the controller up and running 24/7. You can just use it to provision your AP, and then the AP lives its life.

First word of caution: disable automatic upgrade! It appears the last two firmwares for the non-AC model was making the connection pretty unreliable.

Another word of caution: you SHOULD NOT buy the LR (long range) model for residential or even enterprise usage. LR models are for some very specific use (think industrial applications).

When you get an LR AP, it is set by default on auto transmit power, which is basically high power. It is likely that none of your device will be able to keep a stable connection with that. The AP constantly "yells" while your device answers with "whispers". That's not good communication, right?

In order to get a reliable connection with my devices I had to lower the transmit power to low. This defeats the purpose of long range.

The AP offers 4 SSID maximum.

The network configuration is a bit different to Linksys regarding VLAN's. On the Linksys I had the native VLAN set to 1 and I was tagging each SSID.

Here, you should set the native VLAN to whatever VLAN you want. SSID's that should use that VLAN shouldn't be tagged (don't define any VLAN). Other SSID should be tagged.

Interestingly you can't define the same VLAN for two SSID's.

One SSID is using Radius from my Synology NAS for authentication. I had to set "Radius-assigned VLAN" which is still a beta option:

![](/Users/sw/Syncthing/Android/NOTES/Blogs/blog.wains.be/images/ubiquiti-vlan-radius.png)

If you tag a VLAN on one SSID while the native VLAN is set to the same VLAN, you will get funky network issues. Radius was authenticating fine, DHCP was receiving request but phone was requesting IP over and over.

For a setup with VLAN's, Radius and multiple SSID's, see this:

[https://community.ubnt.com/t5/UniFi-Wireless/UniFi-multiple-SSID-s-VLAN-s-RADIUS-servers-and-subnets/td-p/703809](https://community.ubnt.com/t5/UniFi-Wireless/UniFi-multiple-SSID-s-VLAN-s-RADIUS-servers-and-subnets/td-p/703809)

After going through all those troubles I switch the "UAP LR" for an "UAP AC Pro". Note that only Pro models come with Gigabit Ethernet ports.

Out of the box, the Pro model is reliable without tweaking transmit power. Also it got provisionned with the configuration immediately, thanks to the controller already being in place.

I will test it some more in the next couple of weeks and report back in this post.