Pre

* Mininet
* OpenVSwitch
* Pox
* TCPdump

# 1 Create single topology at Mininet

**Topology**

h1 ---- s1 ---- h2
	|
	|
        h3


![mininetTopo](/img/topo0.png)

$ sudo mn --topo single,3 --switch ovsk --controller=remote

```
*** Creating network
*** Adding controller
Unable to contact the remote controller at 127.0.0.1:6653
Unable to contact the remote controller at 127.0.0.1:6633
Setting remote controller to 127.0.0.1:6653
*** Adding hosts:
h1 h2 h3 
*** Adding switches:
s1 
*** Adding links:
(h1, s1) (h2, s1) (h3, s1) 
*** Configuring hosts
h1 h2 h3 
*** Starting controller
c0 
*** Starting 1 switches
s1 ...
*** Starting CLI:

```

### 1.1. Test

- mininet> links

```
h1-eth0<->s1-eth1 (OK OK) 
h2-eth0<->s1-eth2 (OK OK) 
h3-eth0<->s1-eth3 (OK OK) 
```

- mininet> net

```
h1 h1-eth0:s1-eth1
h2 h2-eth0:s1-eth2
h3 h3-eth0:s1-eth3
s1 lo:  s1-eth1:h1-eth0 s1-eth2:h2-eth0 s1-eth3:h3-eth0
c0
```

- mininet> pingall

```
*** Results: 100% dropped (0/6 received)
```

- mininet> dump

```
<Host h1: h1-eth0:10.0.0.1 pid=6708> 
<Host h2: h2-eth0:10.0.0.2 pid=6710> 
<Host h3: h3-eth0:10.0.0.3 pid=6712> 
<OVSSwitch s1: lo:127.0.0.1,s1-eth1:None,s1-eth2:None,s1-eth3:None pid=6717> 
<RemoteController c0: 127.0.0.1:6653 pid=6700> 
```

# 2. Flow table (ARP)

In open another terminal, and type the folow commands

### 2.1. Show flow entry in Flow table



- sudo ovs-ofctl dump-flows s1

```
NXST_FLOW reply (xid=0x4):
```

- dpctl dump-flows tcp:127.0.0.1:6634 (on mininet terminal)

```
*** s1 ------------------------------------------------------------------------
NXST_FLOW reply (xid=0x4):
```

Switch flow table is empty and there is no controller connected to the switch
therefore the switch doesn't know that to do with the incoming traffic, leading
to ping failure.

### 2.2. Add flow


#### 2.2.1 Add flow at port 1

- sudo ovs-ofctl add-flow s1 in_port:1,action=output:2
- Show:

```
NXST_FLOW reply (xid=0x4):
 cookie=0x0, duration=4.535s, table=0, n_packets=0, n_bytes=0, idle_age=4, in_port=1 actions=output:2

```

On mininet terminal, type `xterm h1 h2` to open h1, h2 terminal

- On xterm h1:

```
tcpdump -ne -i h1-eth0
```


- On xterm h2:

```
tcpdump -ne -i h2-eth0
```

![mininet](/img/1.png)

- On mininet terminal

```
h1 ping h2
```

```
PING 10.0.0.2 (10.0.0.2) 56(84) bytes of data.
From 10.0.0.1 icmp_seq=1 Destination Host Unreachable
From 10.0.0.1 icmp_seq=2 Destination Host Unreachable
From 10.0.0.1 icmp_seq=3 Destination Host Unreachable
From 10.0.0.1 icmp_seq=4 Destination Host Unreachable
---
```

```
h1 ping h2
```

![mininet](/img/topo1.png)

```
mininet> h2 ping h1
```

![mininet](/img/topo2.png)


#### 2.2.2 Add flow at port 2

- sudo ovs-ofctl add-flow s1 in_port:2,action=output:1
- sudo ovs-ofctl dump-flows s1

```
NXST_FLOW reply (xid=0x4):
 cookie=0x0, duration=1843.332s, table=0, n_packets=111, n_bytes=4830, idle_age=628, in_port=1 actions=output:2
 cookie=0x0, duration=24.187s, table=0, n_packets=0, n_bytes=0, idle_age=24, in_port=2 actions=output:1

```

- On xterm h1:

```
tcpdump -ne -i h1-eth0
```


- On xterm h2:

```
tcpdump -ne -i h2-eth0
```
![mininet](/img/2.png)

- On mininet terminal


```
PING 10.0.0.2 (10.0.0.2) 56(84) bytes of data.
64 bytes from 10.0.0.2: icmp_seq=1 ttl=64 time=0.753 ms
64 bytes from 10.0.0.2: icmp_seq=2 ttl=64 time=0.215 ms
64 bytes from 10.0.0.2: icmp_seq=3 ttl=64 time=0.124 ms
64 bytes from 10.0.0.2: icmp_seq=4 ttl=64 time=0.144 ms
^C
--- 10.0.0.2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3069ms
rtt min/avg/max/mdev = 0.124/0.309/0.753/0.258 ms

---
```

```
mininet> h1 ping h2
```

![mininet](/img/topo3.png)

```
mininet> h2 ping h1
```

![mininet](/img/topo4.png)

# 3. Simple web server (HTTP)

Starting a simple HTTP server on `h1`, making a request from `h1`,
the shutting down the web server:

```
mininet> h1 python -m SimpleHTTPServer 80 &
mininet> h2 wget -O - h1
```


![mininet](/img/topo51.png)


![mininet](/img/topo52.png)

```

--2018-03-27 17:19:13--  http://10.0.0.1/
Connecting to 10.0.0.1:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 290 [text/html]
Saving to: ‘STDOUT’

-                     0%[                    ]       0  --.-KB/s               <!DOCTYPE html>
<!--
 - File              : index.html
 - Author            : Channith Am <amcnith@gmail.com>
 - Date              : 30.09.2017
 - Last Modified Date: 30.09.2017
 - Last Modified By  : Channith Am <amcnith@gmail.com>
-->

<html>
	<body>
		<p>
		Hello</p>
	
	</body>
</html>
-                   100%[===================>]     290  --.-KB/s    in 0s      

2018-03-27 17:19:13 (29,1 MB/s) - written to stdout [290/290]

```

```
mininet> h1 kill %python
```

```
Serving HTTP on 0.0.0.0 port 80 ...
10.0.0.2 - - [27/Mar/2018 17:19:13] "GET / HTTP/1.1" 200 -
```

Exit the CLI:
-------------

mininet> exit

Cleanup:
--------

$ sudo mn -c

# References

[1] http://mininet.org/walkthrough/

[2] https://github.com/mininet/openflow-tutorial/wiki/Learn-Development-Tools

