## Name - B.Shebu
## Dpt - CYS
## Topic - Dynamic Routing



1) Exactly replicate the given Figure by configuring the network using dynamic routing 
with the provided Information. 

![image](https://github.com/sh3bu/Packet_tracer/assets/67383098/8392f3b4-b7dc-426a-a2b0-2489622117ba)


2) Show that the PCs were able to ping each other. 

**Between pcs of each network **

![image](https://github.com/sh3bu/Packet_tracer/assets/67383098/b715a66a-9f78-441c-8d1f-ea10aa7fafb9)

**Between routers**

![image](https://github.com/sh3bu/Packet_tracer/assets/67383098/e79631a2-d2af-431d-bab4-a2cae0d85622)

**Between one network pc to another network**

![image](https://github.com/sh3bu/Packet_tracer/assets/67383098/7b5e6045-a829-423f-a215-5764da6b1c76)


3) Submit a report (yourrollnumber.pdf) that contains a list of commands to configure the 
network with a screenshot of your configured network. 

#### Router 0 -

```python
Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface FastEthernet0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown


Router(config)#interface Serial0/3/0
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#
```

#### Router 1 -

```python
Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface FastEthernet0/0
Router(config-if)#ip address 192.168.2.1 255.255.255.0
Router(config-if)#ip address 192.168.2.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#


Router(config)#interface Serial0/3/0
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#ip address 10.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#


Router(config)#interface Serial0/3/1
Router(config-if)#ip address 12.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#
```

#### Router 2 -

```python
Router>enable
Router#
Router#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface FastEthernet0/0
Router(config-if)#ip address 192.168.3.1 255.255.255.0
Router(config-if)#ip address 192.168.3.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#


Router(config)#interface Serial0/3/0
Router(config-if)#ip address 12.0.0.1 255.0.0.0
Router(config-if)#ip address 12.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#
```

## Dynamic routing


#### Router 2 -

```
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#router rip
Router(config-router)#network 192.168.1.0
Router(config-router)#network 10.0.0.0
```



#### Router 1 -

```
Router(config)#router rip
Router(config-router)#network 10.0.0.0
Router(config-router)#network 192.168.2.0
Router(config-router)#network 12.0.0.0
```

#### Router 2-

```
Router(config)#router rip
Router(config-router)#network 192.168.3.1
Router(config-router)#network 12.0.0.0
```





















