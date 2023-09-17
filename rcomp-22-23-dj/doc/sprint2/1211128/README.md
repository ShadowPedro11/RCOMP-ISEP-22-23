RCOMP 2022-2023 Project - Sprint 2 Member 1211128 folder
===========================================

## Building D and Backbone nodes required

| Network                                                                        | Required Nodes |
|:-------------------------------------------------------------------------------|:--------------:|
| End user outlets on the ground floor                                           |       25       |
| End user outlets on floor one                                                  |       60       |
| Wi-Fi network                                                                  |       80       |
| DMZ (Servers, administration workstations, and network infrastructure devices) |       10       |
| VoIP (IP-phones):                                                              |       13       |
| Backbone                                                                       |      100       |
| Total:                                                                         |      288       |

---

## Devices naming

| Device                                        | Packet Tracer  - Host Name | Packet Tracer  - Display Name |
|:----------------------------------------------|:---------------------------|:------------------------------|
| Building A Intermediate Cross-Connect         | Switch-PT-Empty            | BldgA_IC                      |
| Building B Intermediate Cross-Connect         | Switch-PT-Empty            | BldgB_IC                      |
| Building C Intermediate Cross-Connect         | Switch-PT-Empty            | BldgC_IC                      |
| Building D Intermediate Cross-Connect         | Switch-PT-Empty            | Switch_BuildingD_IC           |
| Building D Horizontal Cross-Connect Floor 0   | Switch-PT-Empty            | Switch_Floor0_HC              |
| Building D Horizontal Cross-Connect Floor 1   | Switch-PT-Empty            | Switch_Floor1_HC              |
| Floor 0 - Consolidation Point 1 - Room D.0.11 | Switch-PT-Empty            | Switch_Floor0_CP1_D.0.11      |
| Floor 0 - Consolidation Point 2 - Room D.0.6  | Switch-PT-Empty            | Switch_Floor0_CP2_D.0.6       |
| Floor 0 - Consolidation Point 3 - Room D.0.3  | Switch-PT-Empty            | Switch_Floor0_CP3_D.0.3       |
| Floor 0 - Consolidation Point 4 - Room D.0.2  | Switch-PT-Empty            | Switch_Floor0_CP4_D.0.2       |
| Floor 1 - Consolidation Point 1 - Room D.1.9  | Switch-PT-Empty            | Switch_Floor0_CP1_D.1.9       |
| Floor 1 - Consolidation Point 2 - Room D.1.14 | Switch-PT-Empty            | Switch_Floor0_CP2_D.1.14      |
| Floor 1 - Consolidation Point 3 - Room D.1.7  | Switch-PT-Empty            | Switch_Floor0_CP3_D.1.7       |
| Floor 1 - Consolidation Point 4 - Room D.1.5  | Switch-PT-Empty            | Switch_Floor0_CP4_D.1.5       |
| PC of Room D.0.2                              | PC-PT                      | PC_RoomD.0.2                  |
| PC of Room D.0.3                              | PC-PT                      | PC_RoomD.0.3                  |
| PC of Room D.1.5                              | PC-PT                      | PC_RoomD.1.5                  |
| Access Point Floor 0                          | AccessPoint-PT             | AP3_Floor0                    |
| Laptop Floor 0                                | Laptop-PT                  | Laptop_RoomD.0.6              |
| Building phone                                | IP Phone - 7960            | IP Phone_BuildingD            |
| Building server                               | Server-PT                  | Server_BuildingD              |
| Building A Router                             | 2811                       | BldgA_Router                  |
| Building B Router                             | 2811                       | BldgB_Router                  |
| Building C Router                             | 2811                       | BldgC_Router                  |
| Building D Router                             | 2811                       | Router_BuildingD              |
| Modem                                         | DSL-Modem-PT               | BldgA_DSL_Modem               |

---

## Layer two configuration

### Virtual LANs
* All VLAN's presented on "The VLAN database" were added to BldgA_IC (Building A Intermediate Cross-Connect).
  Further, forward they will be added to other switches.

### Spanning tree protocol
* Not disable STP

### VLAN Trucking Protocol (VTP)
* In this point we need to ensure that all switches have the same complete VLAN database.
* To do this we need to configure the VTP domain described on "VTP domain".
* The switch - BldgA_IC is set as vtp server.
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

| VLAN NAME        | VLAN ID | Required Nodes | Sub Network Address |      MASK       |         Address Range          |           Usable IPs           |
|:-----------------|:-------:|:--------------:|:-------------------:|:---------------:|:------------------------------:|:------------------------------:|
| BuildingD_Floor0 |   591   |       25       |  10.81.188.192/27   | 255.255.255.224 | 10.81.188.192 - 10.81.188.223  | 10.81.188.193 - 10.81.188.222  |
| BuildingD_Floor1 |   592   |       60       |  10.81.188.128/26   | 255.255.255.240 | 10.81.188.128 - 10.81.188.191  | 10.81.188.129 - 10.81.188.190  |
| BuildingD_WiFI   |   593   |       80       |   10.81.188.0/25    | 255.255.255.128 |  10.81.188.0 -  10.81.188.127  |  10.81.188.1 -  10.81.188.126  |
| BuildingD_DMZ    |   594   |       10       |  10.81.188.240/28   | 255.255.255.240 | 10.81.188.240 - 10.81.188.255  | 10.81.188.241 - 10.81.188.254  |
| BuildingD_VoIP   |   595   |       13       |  10.81.188.224/28   | 255.255.255.240 | 10.81.188.224 -  10.81.188.239 | 10.81.188.225 -  10.81.188.238 |

Backbone VLAN with ID 575 are required  100 nodes.
Sub Network Address for VLAN : 10.81.189.0/25<br>
Address for this building : 10.81.189.4

### IPv4 networks - Document detailing
* Building D needs 188 nodes.
* So the IP address space for this building is : 10.81.188.0/24.
* 10.81.188.0/24 -> 256 of network space size.
* First network required 25 nodes (32)->10.81.188.192/27
* Second network required 60 nodes (64)->10.81.188.128/26
* Third network required 80 nodes (128)->10.81.188.0/25
* Fourth network required 10 nodes (16)->10.81.188.240/28
* Fifth network required 13 nodes (16)->10.81.188.224/28

### Routers and static routing

|   NETWORK   |      MASK      |  NEXT-HOP   |
|:-----------:|:--------------:|:-----------:|
| 10.81.184.0 | 255.255.254.0	 | 10.81.189.1 |
| 10.81.186.0 | 255.255.255.0	 | 10.81.189.2 |
| 10.81.187.0 | 255.255.255.0	 | 10.81.189.3 |

### Routers and static routing - Document detailing

##### Building A
NETWORK: 10.81.184.0<br>
MASK: 255.255.254.0<br>
NEXT-HOP: 10.81.189.1<br><br>
The Building A entry indicates that any traffic destined for the network 10.81.184.0 (Building A IP address space) with a
subnet mask of 255.255.255.0 should be forwarded to the next-hop IP address 10.81.189.1(Building A backbone IP).

##### Building B
NETWORK: 10.81.186.0 <br>
MASK: 255.255.255.0<br>
NEXT-HOP: 10.81.189.2<br><br>
The Building B entry indicates that any traffic destined for the network 10.81.186.0 (Building B IP address space) with a
subnet mask of 255.255.255.0 should be forwarded to the next-hop IP address 10.81.189.2(Building B backbone IP).

##### Building C
NETWORK: 10.81.187.0<br>
MASK: 255.255.255.0<br>
NEXT-HOP: 10.81.189.3<br><br>
The Building C entry indicates that any traffic destined for the network 10.81.187.0 (Building C IP address space) with a
subnet mask of 255.255.255.0 should be forwarded to the next-hop IP address 10.81.189.3(Building C backbone IP).

---