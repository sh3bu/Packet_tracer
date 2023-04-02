# Radius server

Step:1- First assign hostname and ip address on Router R1.

Step2:Configure RADIUS SERVER(192.168.1.2)

![image](https://user-images.githubusercontent.com/67383098/229370481-ad6f1c9a-6e76-4d8c-905c-9fbe81fc0150.png)

Step:3-Now tell the router R1 that you want to use RADIUS SERVER for Authentication.

```
Router(config-if)#
Router(config-if)#aaa new-model
Router(config)#radius-server host 192.168.1.2 key p@ss
Router(config)#aaa authentication login default group radius local
Router(config)#line vty 0 5
Router(config-line)#login authentication default
Router(config-line)#
```

Step:4- Test  access from router.

Open cli of router

user - shebu 
pass - shebu@12

![image](https://user-images.githubusercontent.com/67383098/229370986-9e2f7fd4-2b47-4ff1-b940-422855ffe672.png)

 
 When given invalid password -
 
 ![image](https://user-images.githubusercontent.com/67383098/229371026-2d253756-a6b0-42ca-9f33-9e61aedd3dda.png)

