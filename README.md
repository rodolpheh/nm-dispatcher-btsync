## nm-dispatcher-btsync
#### A dispatcher script for NetworkManager and Bittorrent Sync

This script, used with NetworkManager-dispatcher service, manage the Bittorrent Sync in order to avoid disconnections.

### What does he do ?

This script:
* Start Bittorrent Sync service when connection is up
* Stop Bittorrent Sync service when connection is down
* Restart Bittorrent Sync service when VPN connection change

### How to install ?

First of all, this script works only with systemd because it's using systemd services.

You must have, installed in your system:
* systemd
* network-manager
* btsync

In root, copy the script to the NetworkManager dispatcher folder and add executable rights to the script:
```
# cp /source/to/50-btsync /etc/NetworkManager/dispatcher.d/50-btsync
# chmod +x /etc/NetworkManager/dispatcher.d/50-btsync
```
Replace */source/to/50-btsync* with the path to the 50-btsync file downloaded from this page.

Be sure NetworkManager-dispatcher.service is enabled at startup:
```
# systemctl enable NetworkManager-dispatcher
```

In order to start Bittorrent Sync service for your users, you must (in root):
* Add the "btsync-users" group to your system:
```
# groupadd btsync-users
```
* Add users to the btsync-users group:
```
# gpasswd -a youruser btsync-users
```
Replace *youruser* with the name of the user you want to add to the btsync-users group

Reboot your computer. Now NetworkManager should takes care of Bittorrent Sync and starts the Bittorrent Sync sessions for every users you add in btsync-users group.
