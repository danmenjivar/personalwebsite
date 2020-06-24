---
layout: blog
title: Basic Linux Networking Guide
date: 2020-06-24T15:14:35.258Z
toc: true
featured_image: /uploads/networking.jpg
featured_image_caption: "A Beginner's Guide to Networking on Linux"
---

## Internet 101

In very basic terms, your computer or mobile device is connected to a router or modem which connects to your ISP (Internet Service Provider; e.g. Charter, Comcast, etc.) which connects to many devices across the world forming a network of networks that we call the internet. When you open a browser and request `google.com`, your web browser sends a request for `google.com` through your router to your ISP. Your ISP routes your request to a DNS server. A DNS server takes a domain name (URL) and translates it to an IP address. Similar to how every home has a mailing address, every device on the internet has a network address (e.g. 172.16.254.1 is an IPv4 network address). This IP address is used to route your device to the corresponding web server that hosts `google.com`. The web server (running something like Apache or nginx) receives the request (along with cookies and things of that nature) and uses the URI (that's basically everything after the .com/ of a URL) to figure out what page to send you back.  

## Local Area Networks (LAN) 101

From the last section, you should know that the internet is an interconnected network of networks. All these smaller networks that make up the internet, including the one in your home are called LANs (Local Area Network). In your home, you probably have more than one device connected to your router which in turn connects to the internet. Your ISP assigns your home a single IP address (e.g. 24.244.91.19) which your router shares across all your local devices. This is referred to as NATing (Network Address Translation). Most routers are configured to assign local IP addresses that begin with 192.168, assigning itself (the router) 192.168.0.1, and the first device on the LAN 192.168.0.19. Subsequent devices tend to be assigned subsequent local IP addresses, so your second device would be assigned 192.168.0.20 and the third 192.168.0.21, and so on. This means that if device 192.168.0.21 makes a request, this request gets routed to the router at 192.168.0.1 which then uses the WAN IP address assigned by your ISP (that's the 24.244.91.19 in this example) to send the request across the internet. The response to the request happens in the reverse order, with the router accepting the response and then routing it back to the device that initiated the request. Lastly, it is important to know that every computer has a self-identifying IP address (127.0.0.1) that is often referred to as the localhost. This 127.0.0.1 serves an important purpose, it is the loopback IP protocol that allows a computer to establish an IP connection to itself.

## Practical Linux Network Commands
| cmd | description|
|-----|------------|
|ping \<domain or ip address>| test the reachability of a host|
|ifconfig| returns network configuration info|
|tcpdump | packet sniffer |
|netstat | returns network statistics

**Notes:**
* `ping` 
    * useful to test if your web browser isn't working or your entire internet isn't working by pinging a reliable host like `google.com`
    * tells you how long it takes for each response to come back
    * also gives you the exact IP address
    * can also troubleshoot packet loss from a faulty network card
* `ifconfig`
    * interfaces 
        * `eth0` wired ethernet
        * `lo` loopback (localhost)
        * `wlo1` wireless ethernet
    * details
        * `inet addr` IPv4 address
        * `inet6 addr` IPv6 address
    * stats
        * `RX` received
        * `TX` transmitted (sent)
* `tcpdump`
    * columns are read from left to right: timestamp, IP address sending from, IP address sending to, domain packet resolves to
    * alternative options:
        * to limit the amount of packets captured you can run `tcpdump -c <number>` where `<number>` is how many packets you want
        * to limit to a particular interface `tcpdump -i <name>` where `<name>` is the name of the network interface
        * to limit to a particular port `tcpdump port <number>` where `<number>` is the port number
        * to print the packets contents in ASCII run `tcpdump -A`
        * to print the packets contents in Hex run `tcpdump -XX`
* `netsat` flag options
    * `-nr`, the `-r` flag displays the kernel routing table and `-n` flag prints addresses as dotted IP addresses rather than symbolic host network names
    * `-i`, displays network interface statistics per network interface
    * `-ta`, displays connections to your machine (`-tan` to display IP addresses and not host names)

