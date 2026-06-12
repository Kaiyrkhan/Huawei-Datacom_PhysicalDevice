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

## Step 1 – Configure VLAN (Create VLANs and Access/Trunk Ports)

**A1 and A2 Switch**

```shell
# Create VLANs
vlan batch 111 112

display vlan
```

```shell
# Configure Access Port

interface g1/0/5
 port link-type access
 port default vlan 111
 quit

interface g1/0/9
 port link-type access
 port default vlan 112
 quit

display vlan
display port vlan
```

```shell
# Configure Trunk Port and Allowed VLANs

interface g1/0/1
 port link-type trunk
 port trunk allow-pass vlan 111 112
 quit

interface g1/0/2
 port link-type trunk
 port trunk allow-pass vlan 111 112
 quit

display vlan
display port vlan
```

**D1 and D2 Switch**

```shell
# Create VLANs
vlan batch 111 112

display vlan
```

```shell
# Configure Trunk Port and Allowed VLANs

interface g0/0/2
 port link-type trunk
 port trunk allow-pass vlan 111 112
 quit

interface g0/0/3
 port link-type trunk
 port trunk allow-pass vlan 111 112
 quit

display vlan
display port vlan
```

**D3 Switch**

```shell
# Create VLANs
vlan 10
 quit

display vlan
```

```shell
# Configure Access Port

interface g0/0/1
 port link-type access
 port default vlan 30
 quit

interface g0/0/2
 port link-type access
 port default vlan 10
 quit

display vlan
display port vlan
```

## Step 2 – Configure Link Aggregation. Eth-Trunk

**D1 and D2 Switch**

```shell
interface Eth-Trunk 1                                          // Create Eth-Trunk interface
 port link-type trunk                                          // Trunk Port
 port trunk allow-pass vlan 111 112                            // Allowed VLANs         
 mode lacp-static                                              // Link Aggregation Mode
 quit
```

```shell
# Add a Port to the Eth-Trunk

interface g0/0/23
 eth-trunk 1
 quit
interface g0/0/24
 eth-trunk 1
 quit

display int brief
```

```shell
# Verify Configuration

display eth-trunk 1
```
