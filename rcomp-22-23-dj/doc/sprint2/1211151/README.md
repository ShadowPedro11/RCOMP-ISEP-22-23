RCOMP 2022-2023 Project - Sprint 2 Member 1211151 folder
===========================================

## Building B and Backbone nodes required

| Network                                                                        | Required Nodes |
|:-------------------------------------------------------------------------------|:--------------:|
| End user outlets on the ground floor                                           |       25       |
| End user outlets on floor one                                                  |       60       |
| Wi-Fi network                                                                  |      110       |
| DMZ (Servers, administration workstations, and network infrastructure devices) |       10       |
| VoIP (IP-phones):                                                              |       13       |
| Backbone                                                                       |      100       |
| Total:                                                                         |      318       |

---

## Devices naming

| Device                                | Packet Tracer  - Host Name | Packet Tracer  - Display Name |
|:--------------------------------------|:---------------------------|:------------------------------|
| Building A Intermediate Cross-Connect | Switch-PT-Empty            | IC-A                          |
| Building B Intermediate Cross-Connect | Switch-PT-Empty            | IC-B                          |
| Building C Intermediate Cross-Connect | Switch-PT-Empty            | IC-C                          |
| Building D Intermediate Cross-Connect | Switch-PT-Empty            | IC-D                          |
| Horizontal Cross-Connect Floor 0      | Switch-PT-Empty            | HC-Floor 0                    |
| Horizontal Cross-Connect Floor 1      | Switch-PT-Empty            | HC-Floor 1                    |
| Consolidation Point of Room B.0.8     | Switch-PT-Empty            | CP-Room B.0.8                 |
| Consolidation Point of Room B.0.7     | Switch-PT-Empty            | CP-Room B.0.7                 |
| Consolidation Point of Room B.0.4     | Switch-PT-Empty            | CP-Room B.0.4                 |
| Consolidation Point of Room B.1.10    | Switch-PT-Empty            | CP-Room B.1.10                |
| Consolidation Point of Room B.1.8     | Switch-PT-Empty            | CP-Room B.1.8                 |
| Consolidation Point of Room B.1.7     | Switch-PT-Empty            | CP-Room B.1.7                 |
| Consolidation Point of Room B.1.5     | Switch-PT-Empty            | CP-Room B.1.5                 |
| Consolidation Point of Room B.1.2     | Switch-PT-Empty            | CP-Room B.1.2                 |
| Consolidation Point of Room B.1.14    | Switch-PT-Empty            | CP-Room B.1.14                |
| PC of Room B.0.8                      | PC-PT                      | PC-Room B.0.8                 |
| PC of Room B.0.6                      | PC-PT                      | PC-Room B.0.6                 |
| PC of Room B.1.1                      | PC-PT                      | PC-Room B.1.1                 |
| Access Point Floor 0                  | AccessPoint-PT             | BldgB_Floor0_AP               |
| Access Point Floor 1                  | AccessPoint-PT             | BldgB_Floor1_AP               |
| Laptop Floor 0                        | Laptop-PT                  | BldgB_Floor0_Laptop           |
| Laptop Floor 1                        | Laptop-PT                  | BldgB_Floor1_Laptop           |
| Building phone                        | IP Phone - 7960            | BldgB_Phone                   |
| Building server                       | Server-PT                  | BldgB_Server                  |
| Building A Router                     | 2811                       | RouterA                       |
| Building B Router                     | 2811                       | RouterB                       |
| Building C Router                     | 2811                       | RouterC                       |
| Building D Router                     | 2811                       | RouterD                       |
| Modem                                 | DSL-Modem-PT               | BldgA_DSL_Modem               |


---

## Layer two configuration

### Virtual LANs
* All VLAN's presented on "The VLAN database" were added to IC-B (Building B Intermediate Cross-Connect).
  Further, forward they will be added to other switches.

### Spanning tree protocol
* Not disable STP

### VLAN Trucking Protocol (VTP)
* In this point we need to ensure that all switches have the same complete VLAN database.
* To do this we need to configure the VTP domain described on "VTP domain".
* The switch - BldgA_IC are set as vtp server.
* Other switches are set with client mode.
* Before we change the connections between switches to trunk mode to ensure that VLAN database established by the servers is propagated.

### The VLAN database

| VLAN Name        | VLAN ID |
|------------------|:-------:|
| Backbone         |   575   |
| BuildingA_Floor0 |   576   |
| BuildingA_Floor1 |   577   |
| BuildingA_WiFI   |   578   |
| BuildingA_DMZ    |   579   |
| BuildingA_VoIP   |   580   |
| BuildingB_Floor0 |   581   |
| BuildingB_Floor1 |   582   |
| BuildingB_WiFI   |   583   |
| BuildingB_DMZ    |   584   |
| BuildingB_VoIP   |   585   |
| BuildingC_Floor0 |   586   |
| BuildingC_Floor1 |   587   |
| BuildingC_WiFI   |   588   |
| BuildingC_DMZ    |   589   |
| BuildingC_VoIP   |   590   |
| BuildingD_Floor0 |   591   |
| BuildingD_Floor1 |   592   |
| BuildingD_WiFI   |   593   |
| BuildingD_DMZ    |   594   |
| BuildingD_VoIP   |   595   |

### VTP domain
* VTP domain to be used : **rc23dj3**
---

## Layer three configuration

### IPv4 networks

| VLAN NAME        | VLAN ID | Required Nodes | Sub Network Address |      MASK       |
|:-----------------|:-------:|:--------------:|:-------------------:|:---------------:|
| BuildingB_Floor0 |   581   |       25       |  10.81.186.192/27   | 255.255.255.224 |
| BuildingB_Floor1 |   582   |       60       |  10.81.186.128/26   | 255.255.255.192 |
| BuildingB_WiFI   |   583   |      110       |   10.81.186.0/25    | 255.255.255.128 |
| BuildingB_DMZ    |   584   |       10       |  10.81.186.240/28   | 255.255.255.240 |
| BuildingB_VoIP   |   585   |       13       |  10.81.186.224/28   | 255.255.255.240 |
| Backbone         |   575   |      218       |   10.81.189.2/25    | 255.255.255.128 |

### IPv4 networks - Document detailing
* Building B needs 218 nodes.
* The IP address space for this building is : 10.81.186.0/24
* First network required 25 nodes (32)->10.81.186.192/27
* Second network required 60 nodes (64)->10.81.186.128/26
* Third network required 110 nodes (128)->10.81.186.0/25
* Fourth network required 10 nodes (16)->10.81.186.240/28
* Fifth network required 13 nodes (16)->10.81.186.224/28

### Routers and static routing

|   NETWORK   |     MASK      |  NEXT-HOP   |
|:-----------:|:-------------:|:-----------:|
| 10.81.184.0 | 255.255.254.0 | 10.81.189.1 |
| 10.81.187.0 | 255.255.255.0 | 10.81.189.3 |
| 10.81.188.0 | 255.255.255.0 | 10.81.189.4 |

### Routers and static routing - Document detailing

##### Building A
NETWORK: 10.81.184.0 <br>
MASK: 255.255.254.0<br>
NEXT-HOP: 10.81.189.1<br><br>

The Building A entry indicates that any traffic destined for the network 10.81.184.0 (Building A IP address space) with a
subnet mask of 255.255.254.0 should be forwarded to the next-hop IP address 10.81.189.1(Building A backbone IP).
##### Building C
NETWORK: 10.81.187.0<br>
MASK: 255.255.255.0<br>
NEXT-HOP: 10.81.189.3<br><br>

The Building C entry indicates that any traffic destined for the network 10.81.187.0 (Building C IP address space) with a
subnet mask of 255.255.255.0 should be forwarded to the next-hop IP address 10.81.189.3(Building C backbone IP).
##### Building D
NETWORK: 10.81.188.0<br>
MASK: 255.255.255.0<br>
NEXT-HOP: 10.81.189.4<br><br>

The Building D entry indicates that any traffic destined for the network 10.81.188.0 (Building D IP address space) with a
subnet mask of 255.255.255.0 should be forwarded to the next-hop IP address 10.81.189.4(Building D backbone IP).


---