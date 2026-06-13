# Configure DHCP Server on Linux

  1) ISC DHCP Server
  2) Kea DHCP Server

> Linux distribution: Debian 12/13, Ubuntu 24.04.4 LTS, Rocky 9.7, openEuler 24.03 LTS SP3, Oracle 7.9  

### Network Topology
![Topology Enterprise Network Design](./images/Topology_EnterpriseNetworkDesign_PhysicalDevice_Huawei_v1.png)  


## Configure ISC DHCP Server on Debian

#### Scenario
  1) install DHCP Package
  2) Configure DHCP Server
  3) Configure DHCP Relay Agent
  4) Configure DHCP Logging
  5) Verify IP Address Assignment

#### Step 1 - install DHCP Package

```shell
$ ping 8.8.8.8
$ ping google.com
```

```shell
$ sudo apt update
$ sudo apt install -y isc-dhcp-server
```
```shell
# Verify DHCP Package Installation
$ sudo dpkg -l isc-dhcp-server

# View DHCP Package Details
$ sudo dpkg -s isc-dhcp-server
```

```shell
# Verify DHCP Listening Port
$ ss -lunp | grep 67
$ ss -ulpn | grep dhcpd
```
