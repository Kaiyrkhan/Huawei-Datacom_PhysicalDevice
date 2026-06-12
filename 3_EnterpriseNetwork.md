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

## Step 1 – Configure VLAN (Create VLANs and Access/Trunk Ports)

**A1 and A2 Switch**

```shell
# Create VLANs

vlan batch 50 111 112

vlan 50
 name MGMT
 quit
vlan 111
 name Service
 quit
vlan 112
 name Service
 quit

display vlan
```

```shell
# Configure Access Port

interface g1/0/5
 port link-type access
 port default vlan 111
 quit

...

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

vlan 111
 name Service
 quit
vlan 112
 name Service
 quit

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

**D3 Switch - Huawei VRP**

```shell
# Create VLANs

vlan batch 10 20

vlan 10
 name VMs
 quit
vlan 20
 name ESXi
 quit

display vlan
```

```shell
# Configure Trunk Port and Allowed VLANs

interface g0/0/11
 port link-type trunk
 port trunk allow-pass vlan 10 20
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

## Step 3 – Configure MSTP (Multiple Spanning Tree Protocol)

```shell
stp region-configuration
 region-name HQ
 revision-level 1
 instance 1 vlan 111
 instance 2 vlan 112
```

## Step 4 - VRRP (Virtual Router Redundancy Protocol)

**D1 and D2 Switch**

```shell
interface Vlanif111
 ip address 172.16.111.1 255.255.255.0
 vrrp vrid 1 virtual-ip 172.16.111.254
 vrrp vrid 1 priority 110
 dhcp select relay
 dhcp relay server-ip 10.10.10.67

interface Vlanif112
 ip address 172.16.112.1 255.255.255.0
 vrrp vrid 2 virtual-ip 172.16.112.254
 dhcp select relay
 dhcp relay server-ip 10.10.10.67
```

```shell
# Verify Configuration

display vrrp brief
```

## Step 4 - Single-Area OSPF

**D1 Switch**

```shell
ospf 1 router-id 50.7.7.7
 area 0.0.0.0
  network 10.1.1.104 0.0.0.3
  network 10.1.50.0 0.0.0.255
  network 172.16.111.0 0.0.0.255
  network 172.16.112.0 0.0.0.255
```

**D2 Switch**

```shell
ospf 1 router-id 50.8.8.8
 area 0.0.0.0
  network 10.1.1.108 0.0.0.3
  network 10.1.50.0 0.0.0.255
  network 172.16.111.0 0.0.0.255
  network 172.16.112.0 0.0.0.255
```

**C1 Switch**

```shell
ospf 1 router-id 50.3.3.3
 area 0.0.0.0
  network 10.1.1.100 0.0.0.3
  network 10.1.1.104 0.0.0.3
  network 10.1.1.108 0.0.0.3
  network 10.1.1.112 0.0.0.3
```

**EdgeR1 Router**

```shell
ospf 1 router-id 50.1.1.1
 default-route-advertise
 area 0.0.0.0
  network 10.1.1.100 0.0.0.3
```

## Step 5 - NAT (Easy IP)

**EdgeR1 Router**

```shell
acl number 2000
 rule 5 permit source 172.16.111.0 0.0.0.255
 rule 10 permit source 172.16.112.0 0.0.0.255
 rule 15 permit source 172.20.20.0 0.0.0.255
 rule 20 permit source 10.10.10.0 0.0.0.255

interface GigabitEthernet0/0/2
 nat outbound 2000
 ip address dhcp-alloc

ip route-static 0.0.0.0 0.0.0.0 172.21.0.1
```

**D3 Switch - Cisco IOS**

```shell
# Create VLANs

vlan 10
 name VMs
 exit
vlan 20
 name ESXi
 exit

show vlan brief

interface Vlan10
 ip address 10.10.10.1 255.255.255.0

interface Vlan20
 ip address 172.20.20.1 255.255.255.0
```

```shell
# Configure Trunk Port and Allowed VLANs

interface GigabitEthernet0/2
 description "Connected to SRV-01 NIC1"
 switchport mode trunk
 switchport trunk encapsulation dot1q
 switchport trunk allowed vlan 10,20
 exit

show vlan brief
show int status
show
```

```shell
interface GigabitEthernet0/1
 description "Uplink to C1 GE0/0/4"
 no switchport
 ip address 10.1.1.114 255.255.255.252
 no shutdown
 exit

show ip int brief
```
