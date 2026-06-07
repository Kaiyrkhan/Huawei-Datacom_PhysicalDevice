# Huawei-Based Enterprise Network Design and Implementation / Huawei құрылғылары негізінде корпоративті желіні жобалау және конфигурациялау

> **ЕСКЕРТУ!** Бұл зертханалық жұмыс нақты физикалық құрылғыны (Physical Device) қолданып жасалған!  

### Network Topology
![Topology Enterprise Network Design](./images/Topology_EnterpriseNetworkDesign_PhysicalDevice_Huawei_v1.png)  

| Device         | Role                                   |
| ---------------| ---------------------------------------|
| ISP            | ISP (Internet Service Provider) Router |
| EdgeR1         | Edge Router                            |
| С1             | Core Layer Switch                      |
| D1, D2, D3     | Aggregation Layer Switch               |
| A1, A2         | Access Layer Switch                    |
| H1, H2, H3, H4 | End Device                             |

## Scenario
1) Configure VLAN (Create VLANs and Access/Trunk Ports)  
   Link Aggregation. Eth-Trunk  
   MSTP (Multiple Spanning Tree Protocol)  
2) VRRP (Virtual Router Redundancy Protocol)
3) Single-Area OSPF
4) DHCP
5) NAT (Easy IP)
6) Remote Access (SSH, Telnet)

## Step 1 – Configure Device Hostname

```shell
# Access Layer Switch (A1, A2)

system-view
sysname A1

commit
```

```shell
# Aggregation Layer Switch (D1, D2, D3)

system-view
sysname D1

commit
```

```shell
# Core Layer Switch (C1, C2)

system-view
sysname C1

commit
```

```shell
# Edge Router (EdgeR1)

Username: super
Password: super
Warning: The password is already expired.
The password needs to be changed. Change now? [Y/N]: Y
Please enter old password: super
Please enter new password: Huawei@123
Please confirm new password: Huawei@123
The password has been changed successfully.
<Huawei>

<Huawei> system-view
[Huawei] sysname EdgeR1
[EdgeR1]
```
