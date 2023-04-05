# Dynamic NAT


![image](https://user-images.githubusercontent.com/67383098/229846860-6980a0f8-ba1d-4a19-bfb7-de1ff2cc88d5.png)

#### Router 0

```
Router(config)#int fa0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown

Router(config-if)#
%LINK-5-CHANGED: Interface FastEthernet0/0, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/0, changed state to up
```
```
Router(config-if)#exit
Router(config-if)#int se 0/3/0
Router(config-if)#ip address 1.0.0.1 255.255.255.0
Router(config-if)#no shutdown
```

#### Router 1

```
Router>en
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#int fa 0/0
Router(config-if)#ip address 172.168.1.1 255.255.255.0
Router(config-if)#no shutdown
```

```
Router(config)#exit
Router(config)#int se 0/3/0
Router(config-if)#ip address 1.0.0.2 0.255.255.255
Router(config-if)#no shutdown
```


## Configuring Dynamic NAT -

#### Router 1

```
R1(config)#access-list 1 permit 192.168.1.0 0.0.0.255  # access-list <id> permit <net-address> <wild_mask>
R1(config)#int fa0/0
R1(config-if)#ip nat inside
R1(config-if)#exit
R1(config)#int fa0/1
R1(config-if)#ip nat outside
R1(config-if)#exit
```

#### Create pool of ip address


```
R1(config)#ip nat pool shebu 1.0.0.1 1.0.0.50 netmask 0.255.255.255

R1(config)#ip nat inside source list 1 pool shebu
```

> The first command, "ip nat pool shebu 1.0.0.1 1.0.0.50 netmask 0.255.255.255", creates a NAT pool named "shebu" and specifies a range of IP addresses (1.0.0.1 to 1.0.0.50) that can be used for NAT translations. The netmask 0.255.255.255 means that all IP addresses in the range are allowed to be used.
> The second command, "ip nat inside source list 1 pool shebu", maps the NAT pool "shebu" to a NAT access list named "1". This command specifies that traffic matching the criteria in the access list will be translated using an IP address from the "shebu" NAT pool.


#### First Do routing configuration on R1 Router: 

- `R1(config)#ip route 0.0.0.0 0.0.0.0 1.0.0.2`

#### Configure Routing on Router R2:
 

-  `R2(config)#ip route 0.0.0.0 0.0.0.0 1.0.0.1`


Just when Ping Run Below command.

This **debug ip nat** command will help to see the translation process in Router.

Now watch the ip address carefully. you will see the subnetted ip address only.They can,t see the real ip address.

```
R1# debug ip nat

IP NAT debugging is on

R1#

NAT: s=192.168.1.2->1.0.0.4, d=1.0.0.2 [12]

```

The first line shows the initial translation from 192.168.1.2 to 1.0.0.2, with a debug identifier of [12].








