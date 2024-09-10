+++
title = "How to fix messed up internal VPN on Ubuntu"
date = 2024-09-09
+++

For legal and sanity reasons, there’s no classified stuff here. To anyone from work: Yes, I fixed it. Crisis averted, lesson learnt.  

This is mostly a note to self in case I try to fix this issue when it happens again, and I need to revert everything.

## Problem
WiFi works 10/10 on work laptop. VPN works 5/10. It connects, works for a few minutes and then it just stops working. Even after disconnecting from VPN, WiFi does not work normally and a system reboot is needed.

> "My VPN does not work. I can't take WFH."  
> "MY VPN DOES NOT WORK TOO!!"  
> \- 2 colleagues (who also happen to have Ubuntu)  

The above is a testimonial to the issue not being unique to me.

### Problem Pt. 2
Having, SOMEHOW by sheer brilliance (read: Stack Overflow), fixed the above issue, when I log in at office on the internal WiFi, I cannot access the internal services. VPN works completely fine, though.

## Cheap Fix
Restarting Network Manager and `systemd-resolved` service fixed the issue but felt like hitting a drained TV remote to juice out a few button presses. A permanent fix was needed.

## Resolution
The issue lies with the `systemd-resolved` which provides DNS resolution to applications. There's a symlink created to `/etc/resolv.conf` by the service for domain name translation through the nameservers provided.  

* Fix which worked for me was deleting the symlinked `resolv.conf` and manually adding the nameservers. Restarting systemd-resolved and NetworkManager fixed the issue and VPN and WiFi worked completely fine then, as expected.  

* Another fix I had tried to implement but did NOT work for me was replacing the line in the file ` /etc/ppp/ip-up.d/0000usepeerdns`:
```sh
cp -a "$REALRESOLVCONF" "$REALRESOLVCONF.pppd-backup.$PPP_IFACE"
```

> with

```sh
cp "$REALRESOLVCONF" "$REALRESOLVCONF.pppd-backup.$PPP_IFACE"
chmod 644 "$REALRESOLVCONF.pppd-backup.$PPP_IFACE"
```
  
This solved all my VPN and WiFi problems till I visited office on a Monday morning.

## Resolution Pt. 2
It was a frantic attempt at fixing the WiFi issue because I could ONLY connect to internal services with VPN on and even internal office WiFi did not work for it. I had to undo what I had done but I couldn't put my finger on what it was.  

* I reverted the change in the `0000usepeerdns` file but it did not solve my issue.  
* I moved back the symlinked `resolv.conf` but it STILL did not fix my issue. The symlink was gone and needed to be created again.  

The good old reinstall came in clutch.

```sh
sudo apt remove --purge systemd-resolved
sudo apt install systemd-resolved
```

A Network Manager restart right after this created the symlink again and fixed the issue.