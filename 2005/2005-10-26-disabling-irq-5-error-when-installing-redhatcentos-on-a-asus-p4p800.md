


date: 2005-10-26 21:31:48+00:00


# '"disabling IRQ 5" error when installing RedHat/CentOS on a ASUS P4P800'

categories:
- Linux


When starting the RedHat/CentOS installer, it kept giving me an error, over and over :
"disabling IRQ 5"

The installer was running very slow as well..
It seemed to me IRQ 5 was bound to the DVD drive

<!-- more -->

I had to disable the "enhanced mode" of the IDE drives under the (AMI) BIOS :
Steps :
- Boot the machine (no way !)
- Enter the BIOS
- Main menu
- IDE Configuration
- Onboard IDE Operate Mode
- Enhanced Mode --> Compatible Mode
- Save and reboot

The RedHat/CentOS was no longer giving the error after changing this setting...
Hope it helps..
