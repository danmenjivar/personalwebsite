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
|netstat | returns network statistics|
|traceroute \<domain>|prints the route packets take to network host|
|nmap| network vulnerability scanner & network discovery|

### ping
* useful to test if your web browser isn't working or your entire internet isn't working by pinging a reliable host like `google.com`
* tells you how long it takes for each response to come back
* also gives you the exact IP address
* can also troubleshoot packet loss from a faulty network card
### ifconfig
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
### tcpdump
* columns are read from left to right: timestamp, IP address sending from, IP address sending to, domain packet resolves to
* alternative options:
    * to limit the amount of packets captured you can run `tcpdump -c <number>` where `<number>` is how many packets you want
    * to limit to a particular interface `tcpdump -i <name>` where `<name>` is the name of the network interface
    * to limit to a particular port `tcpdump port <number>` where `<number>` is the port number
    * to print the packets contents in ASCII run `tcpdump -A`
    * to print the packets contents in Hex run `tcpdump -XX`
### netsat
* `-nr`, the `-r` flag displays the kernel routing table and `-n` flag prints addresses as dotted IP addresses rather than symbolic host network names
* `-i`, displays network interface statistics per network interface
* `-ta`, displays connections to your machine (`-tan` to display IP addresses and not hostnames)
### nmap
* scan a specific IP address `nmap <address>`
    * for more info use verbose `nmap -v <address>` 
* scan multiple IP addresses sequentially `nmap <address>,<lastByteOfAddress>, ...` (e.g `nmap 192.168.0.100,1`)
* scan a range of IP addresses `nmap <address>-<lastByteOfAddress>, ...` (e.g `nmap 192.168.0.1-100`)
* scan all IP addresses that begin with a certain address e.g. `nmap 192.168.0.*`
* scan a hostname `nmap <hostname>`
* scan a list of hostnames & IP addresses
    1. Have a list of hostnames and IP addresses delimited by \n and saved as a .txt file
    2. `nmap -iL <path>` where `<path>` is the filepath to that .txt file
* scan OS inversion detection with `-A` flag
* scan which servers & devices are up & running with `-sP` flag
* display the reason a port is in a particular state with `-reason` flag
* display all host interfaces for a machine with `--iflist`

## Local DNS Entries (/etc/hosts)

As mentioned earlier in this guide, a DNS server translates a domain into an IP address. The linux hosts file (located at /etc/hosts) works similarly albeit at a local level. Whenever you request a domain, the first place Linux will check for a resolution is inside the hosts file. If it can't find an entry inside the hosts file, it then sends the request to your router, which goes through your ISP and is resolved on a DNS server. You can modify behavior by adding and removing entries in the hosts file. This can be useful to setup domain names for your localhost. 

### Changing Your Hostname (with the terminal)

A hostname is basically the name of your machine. You can use your hostname as a domain for your localhost and you can change it.
1. In a terminal, run `sudo hostnamectl set-hostname <name>` where `<name>` is the new hostname for you machine.
2. If you're using your hostname as a localhost, edit the DNS entry for `/etc/hosts`, else you're done.
3. Restart your hostname service by running `sudo service hostname restart`.

## Access Command Line of Remote Host (ssh)

| cmd | description|
|-----|------------|
| ssh \<connection string>| access the command line of a remote host|
| exit| close secure shell connection|

where `<connection string>` is either:
1. `<username>@<remotehost>`
2. `<domain_name>` or
3. `<ip_address>`

### Setup ssh host on your local machine

1. Install openssh-server if you haven't already
2. Optionally, change the default port & authentication
    - edit `/etc/ssh/sshd_config`
        - change default `Port 22`
        - change `PermitRootLogin without-password` to `PermitRootLogin no` to disable remote root access
        - add `AllowUsers <name(s)>` to limit who can access remotely
    - upon these changes, save, & `systemctl restart ssh`

## Transfer Files Between 2 Computers (sftp)

| cmd | description|
|-----|------------|
| sftp \<connection string>| transfer files securely|
| ls | remotehost directory listing|
|lls | localhost directory listing|
| put <path>| transfer file from local to remote host|
| get <path>| transfer file from remote to local host
| exit| close secure file transfer protocol|

where `<connection string>` is either:
1. `<username>@<remotehost>`
2. `<domain_name>` or
3. `<ip_address>`


## Useful Networking Websites

* [ipchicken.com](https://www.ipchicken.com/) What is my public IP address?
* [network-tools.com](https://network-tools.com/) Free network tools for webmasters, IT technicians, & geeks



