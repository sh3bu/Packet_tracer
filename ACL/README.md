# ACL

![image](https://user-images.githubusercontent.com/67383098/230168781-a2eb1ff2-08bc-4aed-9f14-b374ba0c20e2.png)

**NOTE**

For standard ACL , we can use - 0 to 99 as id
For extended ACL , we can use - 1000 - 1099 as id

#### Configure RIP routing 

ROUTER 1

![image](https://user-images.githubusercontent.com/67383098/230167397-5a6e82d4-2f6a-4146-a33c-4d13c1396179.png)

ROUTER 2

![image](https://user-images.githubusercontent.com/67383098/230167576-40be9842-6abb-4df0-b5b8-bba1e1c18d07.png)

###  Standard ACL

#### 1 - CONFIGURE ACL TO ALLOW OR DENY CERTAIN IP 

ROUTER 1 

```
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#access-list 1 deny 192.168.1.2
Router(config)#access-list 1 permit any
Router(config)#
```

#### 2 - APPLY  ACCESS LIST ON CORRECT INTERFACE

ROUTER 1 

All the traffic must come to router via **fa 0/0** so we have to appply the acl there




```
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#int fa 0/0
Router(config-if)#ip access-group 1 in
Router(config-if)#exit
```

> The third command "ip access-group 1 in" applies access control list 1 (ACL 1) to incoming traffic on the interface. This means that any traffic entering the 
> interface will be checked against the rules in ACL 1 to determine whether it should be allowed or denied.

![image](https://user-images.githubusercontent.com/67383098/230175644-b2c41242-f972-4181-8b1f-a1889fc2ba2b.png)

We can see PC 1 cant send packet past the router 0
