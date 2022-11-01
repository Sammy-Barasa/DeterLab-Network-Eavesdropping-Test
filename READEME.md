# USING DETERLAB
### This is my documentation while learning how to use Deter Lab for networking service for networking experiments. The experiments include:
- Eaves Dropping

## Logging in to DeterLab Account Via SSH

Use `ssh` comand and your user name. as below:
From command prompt

```
ssh yourusername@users.deterlab.net
```
for putty

```
users.isi.deterlab.net
```
followed by your username

````
jkuat***

```
followed by your password



## Logging on to DeterLab Experiment instance

SSH to experiment instance 

```
ssh eve.EavesDropbyBarasa.EEC2505.isi.deterlab.net
```
### Change directory


### Eaves dropping

#### **ifconfig on victim**
```
ifconfig
```
The result is as below
```
# ifconfig
eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.1.1.4  netmask 255.255.255.0  broadcast 10.1.1.255
        inet6 fe80::204:23ff:fec7:a315  prefixlen 64  scopeid 0x20<link>
        ether 00:04:23:c7:a3:15  txqueuelen 1000  (Ethernet)
        RX packets 181  bytes 44688 (44.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 186  bytes 41167 (41.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth4: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.148  netmask 255.255.252.0  broadcast 192.168.3.255
        inet6 fe80::214:22ff:fe23:8971  prefixlen 64  scopeid 0x20<link>
        ether 00:14:22:23:89:71  txqueuelen 1000  (Ethernet)
        RX packets 61874  bytes 84203890 (84.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 16382  bytes 2069538 (2.0 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth5: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 00:14:22:23:89:72  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 630  bytes 64520 (64.5 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 630  bytes 64520 (64.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

#### **Run ettercap**

```
ettercap
```
The result is as below:

```
ettercap 0.8.2 copyright 2001-2015 Ettercap Development Team


Please select an User Interface
```
#### **Change to root user**

```
sudo su -
```
or
```
sudo su root

```

#### **Select an eth from ifconfig result, not 127.XXX  or 192.XXX**
```
ettercap -C -i eth1
```
press enter


#### **Enter sniff mode** 
By selecting Unified Sniff simply pressing -U


#### **Scan for host**
Use `ctrl + s` to scan for hosts


#### **Add hosts to target**

Do this by selecting the host and press a number corresponding to the posistion in list

For instance to select host 1:

press `1`

Add both hosts



#### **Start Mitm attack on Mitm tab**

Select ***ARP Poisson ....***

Press enter to select ARP Poisson and press enter again on the parameters prompt
#### **Open another instance and use tcpdump**

Login to another session of the victim computer, eve, and switch as root 


####
```
tcpdump -i eth1 -s0 -w output.pcap 
```  

for 50 seconds
ctrl c

```
404 packets received by filter
0 packets dropped by kernel
```
#### **Read the pcap output file**
```
chaosreader output.pcap
```
Result:

```
Opening, output.pcap

Reading file contents,
 100% (63420/63420)
Reassembling packets,
 100% (361/365)

Creating files...
   Num  Session (host:port <=> host:port)              Service
  0002  10.1.1.3:54080,10.1.1.2:80                     http
  0005  10.1.1.3:54084,10.1.1.2:80                     http
  0015  10.1.1.2:35356,10.1.1.3:80                     http
  0004  10.1.1.3:46250,10.1.1.2:443                    https
  0008  10.1.1.2:35350,10.1.1.3:80                     http
  0003  10.1.1.2:35346,10.1.1.3:80                     http
  0009  10.1.1.3:46256,10.1.1.2:443                    https
  0007  10.1.1.2:35348,10.1.1.3:80                     http
  0001  10.1.1.2:35344,10.1.1.3:80                     http
  0016  10.1.1.3:46264,10.1.1.2:443                    https
  0014  10.1.1.3:54094,10.1.1.2:80                     http
  0011  10.1.1.3:54092,10.1.1.2:80                     http
  0012  10.1.1.2:35352,10.1.1.3:80                     http
  0006  10.1.1.3:46254,10.1.1.2:443                    https
  0010  10.1.1.3:46258,10.1.1.2:443                    https
  0017  10.1.1.3:54098,10.1.1.2:80                     http
  0013  10.1.1.2:35354,10.1.1.3:80                     http

index.html created.
```

#### **Install elinks**

```
sudo apt-get install elinks
```

#### **Read with elinks**


```
elinks index.html
```

Scroll and select the last as_html and get the results.


Basically, the list is a decryption on all the sessions captured on the output.pcap tcpdump resut. You can select any session and see the details in the communication 

