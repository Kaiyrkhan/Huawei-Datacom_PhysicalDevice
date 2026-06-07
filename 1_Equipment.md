# Network Equipment Overview / Желілік құрал-жабдықтарға шолу

Table - Network Equipment
| Device Type       | Model             | Vendor | Operating System |
|-------------------|-------------------|--------|------------------|
| L2 Switch         | S3710-H24P4S-A    | Huawei | VRP              |
| L3 Switch         | S5731-H24T4XC     | Huawei | VRP              |
| Router            | AR6140E-9G-2AC    | Huawei | VRP              |
| Firewall          | USG6610E          | Huawei | VRP              |
| Access Controller | AC6508            | Huawei | VRP              |
| Access Point      | AirEngine 6761-21 | Huawei | VRP              |


Table - Login Authentication
| interface/port    | Username | Password (1)   | Password (2)   |
|-------------------|----------|----------------|----------------|
| Console Port      | admin    | P@s$w0rd_&1234 | Huawei@123     |
| VTY (SSH, Telnet) | student  | P@s$w0rd_&1234 | Huawei@123     |


## Access Layer Switch: Huawei S3710-H24P4S-A

![images](./images/S3710-H24P4S-A_Switch.png)

**Login authentication (Console Port)**
```shell
Password: P@s$w0rd_&1234
Confirm password: P@s$w0rd_&1234
```

```shell
display version
```
![images](./images/S3710-H24P4S-A_display_version.png)

```shell
display interface brief
```
![images](./images/S3710-H24P4S-A_display_int_brief.png)

##  Core/Aggregation Layer Switch: Huawei S5731-H24T4XC

![images](./images/S5731-H24T4XC_Switch.png)

**Login authentication (Console Port)**
```shell
Password: P@s$w0rd_&1234
Confirm password: P@s$w0rd_&1234
```

```shell
display version
```
![images](./images/S5731-H24T4XC_display_version.png)

```shell
display interface brief
```
![images](./images/S5731-H24T4XC_display_int_brief.png)

## Edge Router: AR6140E-9G-2AC

![images](./images/AR6140E-9G-2AC_Router.png)
> Yellow - Layer 3 Routed Port  
> Blue - Layer 2 Switch Port  
> Red - Management (MGMT) Port  

**Login authentication (Console Port)**  
**Warning:** *An initial username and password are required for the first login via the console. Set a username and password and keep them safe. Otherwise you will not be able to login via the console.*  
**New Username:** admin  
**Password:** P@s$w0rd_&1234  
**Confirm password:** P@s$w0rd_&1234  
**Info:** *Configuration console exit, please retry to log on*  

**Login authentication (Console Port)**  
**Username:** admin  
**Password:** P@s$w0rd_&1234  

**Warning:** *Auto-Config is working. Before configuring the device, stop Auto-Config. If you perform configurations when Auto-Config is running, the DHCP, routing, DNS, and VTY configurations will be lost. Do you want to **stop Auto-Config?** [y/n]:* **y**  
**Info:** *Auto-Config has been stopped.*  

```shell
display version
```
![images](./images/AR6140E-9G-2AC_display_version.png)

```shell
display interface brief
```
![images](./images/AR6140E-9G-2AC_display_int_brief.png)

```shell
display ip interface brief
```
![images](./images/AR6140E-9G-2AC_display_ip_int_brief.png)
