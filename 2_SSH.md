# Remote Access Configuration using SSH

### Edge Router: Huawei NetEngine AR6140E-9G-2AC

![images](./images/AR6140E-9G-2AC_Router.png)
> Yellow - Layer 3 Routed Port  
> Blue - Layer 2 Switch Port  
> Red - Management (MGMT) Port  

*Төмендегі топологияда көрсетілгендей, A1 Switch пен EdgeR1 Router-ды Copper кабелмен байланыстырып қосамыз!*
![images](images/AR6140E-9G-2AC_topology.png)

```shell
display interface brief
```
![images](images/AR6140E-9G-2AC_display_int_brief.png)

```shell
display ip interface brief
```
![images](images/AR6140E-9G-2AC_display_ip_int_brief.png)

**Configure Local User Authentication and Authorization**
```shell
aaa
 local-user student password irreversible-cipher P@s$w0rd_&1234
 local-user student privilege level 15
 local-user student service-type terminal ssh
```

> *жеке (individual) құқық (privilege) - student қолданушыға ғана тиесілі*  
> aaa  
> local-user student privilege level 15  

> жалпы (Global) құқық (privilege) - барлық қолданушыға қатысты  
> user-interface vty 0 4  
> user privilege level 15  

**Configure VTY Lines**
```shell
user-interface vty 0 4
 authentication-mode aaa
 protocol inbound ssh
```
