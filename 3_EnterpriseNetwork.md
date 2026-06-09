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

<Huawei> system-view
[Huawei] sysname A1
[A1]
```

```shell
# Aggregation Layer Switch (D1, D2, D3)

<Huawei> system-view
[Huawei] sysname D1
[D1]
```

```shell
# Core Layer Switch (C1, C2)

<Huawei> system-view
[Huawei] sysname C1
[C1]
```

```shell
# Edge Router (EdgeR1)

<Huawei> system-view
[Huawei] sysname EdgeR1
[EdgeR1]
```
