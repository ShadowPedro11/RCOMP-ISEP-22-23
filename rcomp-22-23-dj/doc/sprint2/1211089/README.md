RCOMP 2022-2023 Project - Sprint 2 - Member 1211089 folder
===========================================

## Node required by the Building C

|                                                                                | Building C (nodes) |
|--------------------------------------------------------------------------------|:------------------:|
| End user outlets on floor zero                                                 |         40         |
| End User outlets on floor one                                                  |         50         |
| Wi-Fi networks                                                                 |         55         |
| DMZ (Servers, administration workstations, and network infrastructure devices) |         20         |
| VoIP (IP-phones)                                                               |         25         |
| Total                                                                          |        190         |

## Devices naming

| Device                                      | Packet Tracer  - Host Name | Packet Tracer  - Display Name |
|:--------------------------------------------|:---------------------------|:------------------------------|
| Building A Intermediate Cross-Connect       | Switch-PT-Empty            | IC_A                          |
| Building B Intermediate Cross-Connect       | Switch-PT-Empty            | IC_B                          |
| Building C Intermediate Cross-Connect       | Switch-PT-Empty            | IC_C                          |
| Building D Intermediate Cross-Connect       | Switch-PT-Empty            | IC_D                          |
| Building A Horizontal Cross-Connect Floor 0 | Switch-PT-Empty            | HC_Floor0                     |
| Building A Horizontal Cross-Connect Floor 1 | Switch-PT-Empty            | HC_Floor1                     |
| Consolidation Point in Room c.0.2           | Switch-PT-Empty            | Switch_Floor0_c.0.2           |
| Consolidation Point in Room c.0.4           | Switch-PT-Empty            | Switch_Floor0_c.0.4           |
| Consolidation Point in Room c.0.7           | Switch-PT-Empty            | Switch_Floor0_c.0.7           |
| Consolidation Point in Room c.0.11          | Switch-PT-Empty            | Switch_Floor0_c.0.11          |
| Consolidation Point in Room c.1.1           | Switch-PT-Empty            | Switch_Floor0_c.1.1           |
| Consolidation Point in Room c.1.4           | Switch-PT-Empty            | Switch_Floor0_c.1.4           |
| Consolidation Point in Room c.1.13          | Switch-PT-Empty            | Switch_Floor0_c.1.13          |
| Consolidation Point in Room c.1.19          | Switch-PT-Empty            | Switch_Floor0_c.1.19          |
| PC of Room c.0.7                            | PC-PT                      | PC0                           |
| PC of Room A.1.19                           | PC-PT                      | PC1                           |
| Access Point Floor 0                        | AccessPoint-PT             | Access Point0                 |
| Laptop Floor 0                              | Laptop-PT                  | Laptop0                       |
| Building phone                              | IP Phone - 7960            | IP Phone 0                    |
| Building server                             | Server-PT                  | Server0                       |
| Building A Router                           | 2811                       | RouterA                       |
| Building B Router                           | 2811                       | RouterB                       |
| Building C Router                           | 2811                       | RouterC                       |
| Building D Router                           | 2811                       | RouterD                       |
| Building A modem                            | DSL-modem-PT               | BldgA_DSL_Modem               |
| Building A DSL router                       | 2811                       | Router_DSL                    |

## Layer two configuration

### Virtual LANs
* All VLAN's presented on "The VLAN database" were added to IC_C (Building C Intermediate Cross-Connect).
  Further, forward they will be added to other switches.

### Spanning tree protocol
* Not disable STP

### VLAN Trucking Protocol (VTP)
* In this point we need to ensure that all switches have the same complete VLAN database.
* To do this we need to configure the VTP domain described on "VTP domain".
* The switch - IC_C is set the vtp server.
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

## Layer three configuration

### IP for Building C  **10.81.187.0/24** 


| VLAN Name        | VLAN ID |
|------------------|:-------:|
| BuildingC_Floor0 |   586   |
| BuildingC_Floor1 |   587   |
| BuildingC_WIFI   |   588   | 
| BuildingC_DMZ    |   589   |
| BuildingC_VoIP   |   590   |
| Backbone         |   575   | 

## IP address assignation per VLAN

* For the up to 55 nodes network - a 64 address block - 26 bits prefix 
* For the up to 50 nodes network - a 64 address block - 26 bits prefix
* For the up to 40 nodes network - a 64 address block - 26 bits prefix
* For the up to 25 nodes network - a 32 address block - 27 bits prefix
* For the up to 20 nodes network - a 32 address block - 27 bits prefix


* The 55 addresses block: 10.81.187.0/26
* The 50 addresses block: 10.81.187.64/26 (0 + 64)
* The 40 addresses block: 10.81.187.128/26 (64 + 64)
* The 25 addresses block: 10.81.187.192/26 (128 + 32)
* The 20 addresses block: 10.81.187.224/26 (192 + 32)

| VLAN |     IP range     |
|:----:|:----------------:|
| 588  |  10.81.187.0/26  |
| 587  | 10.81.187.64/26  |
| 586  | 10.81.187.128/26 |
| 590  | 10.81.187.192/27 |
| 589  | 10.81.187.224/27 |


### Routers and static routing

|  Destination   |  NEXT-HOP   |
|:--------------:|:-----------:|
| 10.81.184.0/23 | 10.81.189.1 |
| 10.81.186.0/24 | 10.81.189.2 |
| 10.81.188.0/24 | 10.81.189.4 |



