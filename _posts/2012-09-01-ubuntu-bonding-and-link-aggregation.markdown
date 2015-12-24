---
layout: post
title: Ubuntu Bonding and link aggregation
tags:
- bridging
- Coding
- codingarena
- connections
- eth0
- google
- internet
- Internet
- lan
- link
- link aggregation
- Linux
- manu
- neo
- networking
- ppp0
- server
- ubuntu
- wifi
- wlan0
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'no'
  _edit_last: '1'
  _wp_old_slug: ''
  dsq_thread_id: '928566182'
---

Blog post on link aggregation in ubuntu

<!--more-->

##Installation##
ifenslave is used to attach and detach slave network interfaces to a bonding device.
    sudo apt-get install ifenslave

##Interface Configuration##
Edit your interfaces configuration:
     sudo vi /etc/network/interfaces

For example, to combine eth0 and eth1 as slaves to your bonding interface:
       auto eth0
       iface eth0 inet manual
       bond-master bond0

       auto eth1
       iface eth1 inet manual
       bond-master bond0

       auto bond0
       iface bond0 inet static
       address 192.168.1.10
       gateway 192.168.1.1
       netmask 255.255.255.0
       bond-mode 802.3ad
       bond-miimon 100
       bond-lacp-rate 1
       bond-slaves none


##Checking the bonding interface##
Link information is available under     /proc/net/bonding/.
To check bond0 for example:

    cat /proc/net/bonding/bond0
    Ethernet Channel Bonding Driver: v3.5.0 (November 4, 2008)

    Bonding Mode: IEEE 802.3ad Dynamic link aggregation
    Transmit Hash Policy: layer2 (0)
    MII Status: up
    MII Polling Interval (ms): 100
    Up Delay (ms): 0
    Down Delay (ms): 0

    802.3ad info
    LACP rate: fast
    Aggregator selection policy (ad_select): stable
    bond bond0 has no active aggregator

    Slave Interface: eth1
    MII Status: up
    Link Failure Count: 0
    Permanent HW addr: 00:0c:29:f5:b7:11
    Aggregator ID: N/A

    Slave Interface: eth2
    MII Status: up
    Link Failure Count: 0
    Permanent HW addr: 00:0c:29:f5:b7:1b
    Aggregator ID: N/A

##Bringing up/down Bounded interface##
To bring the bounded interface, run
    ifup bond0

To bring down a bounded interface, run

    ifdown bond0

##Ethernet Bonding modes##

Ethernet bonding has different modes you can use. You specify the mode for your bonding interface in /etc/network/interfaces. For example:
    bond-mode active-backup

Descriptions of bonding modes

    Mode 0
    balance-rr

Round-robin policy: Transmit packets in sequential order from the first available slave through the last. This mode provides load balancing and fault tolerance.

Mode 1
active-backup

Active-backup policy: Only one slave in the bond is active. A different slave becomes active if, and only if, the active slave fails. The bond's MAC address is externally visible on only one port (network adapter) to avoid confusing the switch. This mode provides fault tolerance. The primary option affects the behavior of this mode.

Mode 2
balance-xor

XOR policy: Transmit based on [(source MAC address XOR'd with destination MAC address) modulo slave count]. This selects the same slave for each destination MAC address. This mode provides load balancing and fault tolerance.

Mode 3
broadcast

Broadcast policy: transmits everything on all slave interfaces. This mode provides fault tolerance.

Mode 4
802.3ad

IEEE 802.3ad Dynamic link aggregation. Creates aggregation groups that share the same speed and duplex settings. Utilizes all slaves in the active aggregator according to the 802.3ad specification.

##Prerequisites:##

Ethtool support in the base drivers for retrieving the speed and duplex of each slave.
A switch that supports IEEE 802.3ad Dynamic link aggregation. Most switches will require some type of configuration to enable 802.3ad mode.
Mode 5
balance-tlb

Adaptive transmit load balancing: channel bonding that does not require any special switch support. The outgoing traffic is distributed according to the current load (computed relative to the speed) on each slave. Incoming traffic is received by the current slave. If the receiving slave fails, another slave takes over the MAC address of the failed receiving slave.

##Prerequisites:##

Ethtool support in the base drivers for retrieving the speed of each slave.
Mode 6
balance-alb

Adaptive load balancing: includes balance-tlb plus receive load balancing (rlb) for IPV4 traffic, and does not require any special switch support. The receive load balancing is achieved by ARP negotiation. The bonding driver intercepts the ARP Replies sent by the local system on their way out and overwrites the source hardware address with the unique hardware address of one of the slaves in the bond such that different peers use different hardware addresses for the server.


<a href="http://facebook.com/manusajith">Manu</a>

<a href="http://www.codingarena.in">www.codingarena.in</a>

<a href="http://twitter.com/manusajith" title="Twitter">@manusajith</a> | <a href="http://github.com/manusajith" title="Github">@github</a>