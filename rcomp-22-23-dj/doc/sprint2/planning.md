RCOMP 2022-2023 Project - Sprint 2 planning
===========================================
### Sprint master: 1211089 ###
# 1. Sprint's backlog #
The goal in this second sprint is creating a network for the development structured cabling project of hte first sprint.
In this sprint the focus is on the layer two infrastructure, and the layer three fundamentals.


| Task  | Task description                                                                                                                                                                                           |
|-------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| T.2.1 | Development of a layer two and layer three Packet Tracer simulation for building A, encompassing the campus backbone  <br> Integration of every member's Packet Tracer simulation into a single simulation |
| T.2.2 | Development of a layer two and layer three Packet Tracer simulation for Building B, encompassing the campus backbone                                                                                       |
| T.2.3 | Development of a layer two and layer three Packet Tracer simulation for Building C, encompassing the campus backbone                                                                                       |
| T.2.4 | Development of a layer two and layer three Packet Tracer simulation for Building D, encompassing the campus backbone                                                                                       |

# 2. Technical decisions and coordination #

 * Packet tracer version to be used : **8.2.0.0162**
 * **5 VLANS** per building.
 * VTP domain to be used : **rc23dj3**
 * VLAN Trucking Protocol (VTP)
 * VLAN default : **VLANID 1**
 * VLAN range : **575-605**
 * IPv4 address space to be used : **10.81.184.0/21**
 * ISP router IPv4 node address : **121.60.203.74/30**
 * For VoIp phones, the **7960 model** is to be used
 * For the router static routing use the **2811 model**

#### Building A

| VLAN Name        | VLAN ID  |
|------------------|:--------:|
| BuildingA_Floor0 |   576    |
| BuildingA_Floor1 |   577    |
| BuildingA_WIFI   |   578    |
| BuildingA_DMZ    |   579    |
| BuildingA_VoIP   |   580    |
| Backbone         |   575    |

#### Building B

| VLAN Name        |  VLAN ID  |
|------------------|:---------:|
| BuildingB_Floor0 |    581    |
| BuildingB_Floor1 |    582    |
| BuildingB_WIFI   |    583    |
| BuildingB_DMZ    |    584    |
| BuildingB_VoIP   |    585    |
| Backbone         |    575    |

#### Building C

| VLAN Name        | VLAN ID |
|------------------|:-------:|
| BuildingC_Floor0 |   586   |
| BuildingC_Floor1 |   587   |
| BuildingC_WIFI   |   588   |
| BuildingC_DMZ    |   589   |
| BuildingC_VoIP   |   590   |
| Backbone         |   575   |

#### Building D

| VLAN Name        | VLAN ID |
|------------------|:-------:|
| BuildingD_Floor0 |   591   |
| BuildingD_Floor1 |   592   |
| BuildingD_WIFI   |   593   |
| BuildingD_DMZ    |   594   |
| BuildingD_VoIP   |   595   |
| Backbone         |   575   |

## **Layer three configuration :**

|                                                                                | Building A (nodes) | Building B (nodes) | Building C (nodes) | Building D (nodes) |
|--------------------------------------------------------------------------------|:------------------:|:------------------:|:------------------:|:------------------:|
| End user outlets                                                               |         40         |         25         |         40         |         25         |
| End User outlets on floor one                                                  |         70         |         60         |         50         |         60         |
| Wi-Fi networks                                                                 |        100         |        110         |         55         |         80         |
| DMZ (Servers, administration workstations, and network infrastructure devices) |         90         |         10         |         20         |         10         |
| VoIP (IP-phones)                                                               |         35         |         13         |         25         |         13         |
| Total                                                                          |        335         |        218         |        190         |        188         |

### **Backbone: 100 nodes** 

## **IP address space per building :**

* For the up to 335 nodes network - a 512 address block - 23 bits prefix
* For the up to 218 nodes network - a 256 address block - 24 bits prefix
* For the up to 190 nodes network - a 256 address block - 24 bits prefix
* For the up to 188 nodes network - a 256 address block - 24 bits prefix
* For the up to 100 nodes network - a 128 address block - 25 bits prefix


* The 335 addresses block: 10.81.184.0/23
* The 218 addresses block: 10.81.186.0/26 (184 + 2)
* The 190 addresses block: 10.81.187.0/26 (186 + 1)
* The 188 addresses block: 10.81.188.0/26 (187 + 1)
* The 100 addresses block: 10.81.189.0/26 (188 + 1)

|  Building  |       IP       |
|:----------:|:--------------:|
| Building A | 10.81.184.0/23 |
| Building B | 10.81.186.0/24 |
| Building C | 10.81.187.0/24 |
| Building D | 10.81.188.0/24 |
|  Backbone  | 10.81.189.0/25 |

| Building Backbone |     IP      |
|:-----------------:|:-----------:|
|    Building A     | 10.81.189.1 |
|    Building B     | 10.81.189.2 |
|    Building C     | 10.81.189.3 |
|    Building D     | 10.81.189.4 |


[Source Document](https://moodle.isep.ipp.pt/pluginfile.php/289129/mod_resource/content/2/RCOMP-2022-2023-project-sprint2.pdf)


# 3. Subtasks assignment #

* 1211131 - T.2.1
* 1211151 - T.2.2
* 1211089 - T.2.3
* 1211128 - T.2.4
