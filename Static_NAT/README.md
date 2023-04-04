# Static NAT


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
Router(config-if)#ip address 1.0.0.2 255.255.255.0
Router(config-if)#no shutdown
```

## Configuring Static NAT

#### Router 0
```
Router(config-if)#int fa 0/0
Router(config-if)#ip nat inside
Router(config-if)#exit

Router(config)#

Router(config)#int se 0/3/0
Router(config-if)#ip nat outside
```

```
Router(config)#ip nat inside source static 192.168.1.2 1.0.0.1
Router(config)#ip route  0.0.0.0 0.0.0.0 serial 0/3/0

Router(config)#ip nat inside source static 192.168.1.3 1.0.0.1
Router(config)#ip route  0.0.0.0 0.0.0.0 serial 0/3/0
```

![image](https://user-images.githubusercontent.com/67383098/229853839-40fed6b1-fde0-43f6-b2f6-d3af610e3474.png)








