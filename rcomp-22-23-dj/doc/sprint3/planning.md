RCOMP 2022-2023 Project - Sprint 3 planning
===========================================
### Sprint master: 1211128 ###
# 1. Sprint's backlog #
In this sprint, each team member will keep working on the same network simulation from the previous
sprint (concerning the same building). From the already established layer three configurations, now,
OSPF based dynamic routing will be used to replace the previously used static routing.


| Task  | Task description                                                                                                                                                                                                                                                  |
|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| T.3.1 | Update the buildingA.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building A.                                                                                                          |
| T.3.2 | Update the buildingB.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building B. <br/> Final integration of each member’s Packet Tracer simulation into a single simulation (campus.pkt). |
| T.3.3 | Update the buildingC.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building C.                                                                                                          |
| T.3.4 | Update the buildingD.pkt layer three Packet Tracer simulation from the previous sprint, to include the described features in this sprint for building D.                                                                                                          |

# 2. Technical decisions and coordination #
 ### OSPF Area IDs ###

| Building  | OSPF Area ID  |
|:---------:|:-------------:|
| Backbone  |       0       |
|     A     |       1       |
|     B     |       2       |
|     C     |       3       |
|     D     |       4       |

 ### VoIP phone numbers and prefix digits schema ###
| Building |       Prefix digit       |
|:--------:|:------------------------:|
|    A     | 1 (1001, 1002, 1003,...) |
|    B     | 2 (2001, 2002, 2003,...) |
|    C     | 3 (3001, 3002, 3003,...) |
|    D     | 4 (4001, 4002, 4003,...) |

### DNS domain names ###
| Building |               DNS Domain Name / DNS Name Servers                |
|:--------:|:---------------------------------------------------------------:|
|    A     |            rcomp-22-23-dj-g3 / ns.rcomp-22-23-dj-g3             |
|    B     | building-B.rcomp-22-23-dj-g3 / ns.building-B.rcomp-22-23-dj-g3  |
|    C     | building-C.rcomp-22-23-dj-g3 / ns.building-C.rcomp-22-23-dj-g3  |
|    D     | building-D.rcomp-22-23-dj-g3  / ns.building-D.rcomp-22-23-dj-g3 |

### DNS Name Server IPv4 of each DNS Domain ###
| Building |                         DNS Domain Name                         |  IP Address   |
|:--------:|:---------------------------------------------------------------:|:-------------:|
|    A     |            rcomp-22-23-dj-g3 / ns.rcomp-22-23-dj-g3             | 10.81.185.130 |
|    B     | building-B.rcomp-22-23-dj-g3 / ns.building-B.rcomp-22-23-dj-g3  | 10.81.186.242 |
|    C     | building-C.rcomp-22-23-dj-g3 / ns.building-C.rcomp-22-23-dj-g3  | 10.81.187.227 |
|    D     | building-D.rcomp-22-23-dj-g3  / ns.building-D.rcomp-22-23-dj-g3 | 10.81.188.242 |

 [Source Document](https://moodle.isep.ipp.pt/pluginfile.php/293043/mod_resource/content/3/RCOMP-2022-2023-project-sprint3.pdf)
# 3. Subtasks assignment #

 * 1211131 - T.3.1
 * 1211151 - T.3.2
 * 1211089 - T.3.3
 * 1211128 - T.3.4
