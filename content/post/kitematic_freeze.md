+++
comments = true
date = 2015-07-25T00:00:00Z
tags = ["kitematic", "docker"]
title = "Kitematic freezes at 99%"
+++

There is a case when [Kitematic](https://kitematic.com/) freezes or hangs when started at 99%.
One of reasons is, there will be no route to the virtual box vm created by kitematic.

run
{{< highlight bash >}}
# netstat -rn
{{< / highlight >}}
you will not find an entry in the output for 192.168.99(kitematic docker vm), and since it times out reaching
for the vm, the launch of kitematic freezes at 99%.

Solution:

* Quit Kitematic after it freezes.

* Add a route to kitematic vm by running following commands -
{{< highlight bash >}}
$ ifconfig | grep -B 2 192.168.99
vboxnet2: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
	ether 0a:00:27:00:00:02
	inet 192.168.99.1 netmask 0xffffff00 broadcast 192.168.99.255
$ sudo route -nv add -net 192.168.99 -interface vboxnet2
{{< / highlight >}}

The output of netstat -rn after adding should be something like this -
{{< highlight bash >}}
KEHP-M-X03J:.kube keshava$ netstat -rn
Routing tables

Internet:
Destination        Gateway            Flags        Refs      Use   Netif Expire
127.0.0.1          127.0.0.1          UH              3   488828     lo0
192.168.99         link#13            UC              1        0 vboxnet
192.168.99.100     8:0:27:85:2:fe     UHLWIi          2       64 vboxnet   1146
{{< / highlight >}}

* Restart Kitematic. It should be up and running by now.
