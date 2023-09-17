RCOMP 2022-2023 Project - Sprint 3 Member 1211128 folder
===========================================


## OSPF dynamic routing

### OSPF Area IDs ###

* The first step was clear existing routing tables on routers.
* Then we access each router config an add the following commands using this table.
> router ospf 1 <br>
> network [network-address] [wildcard-mask] area [area-id]

|  Building  | NETWORK-ADDRESS | NETWORK-WILDCARD  | OSPF Area ID |
|:----------:|:---------------:|:-----------------:|:------------:|
| Building A |   10.81.184.0   |     0.0.1.255     |      1       |
| Building B |   10.81.186.0   |     0.0.0.255     |      2       |
| Building C |   10.81.187.0   |     0.0.0.255     |      3       |
| Building D |   10.81.188.0   |     0.0.0.255     |      4       |
|  Backbone  |   10.81.189.0   |     0.0.0.127     |      0       | 

---

## HTTP servers

* At this point we add a SERVER-PT to Building D, named **"BuildingD_HTTP_Server"**.
* The IPv4 address set is **10.81.188.243**.
* HTML page:

![httpServer](resources/httpServer.png)


---

## DHCPv4 service

* To define DHCPv4 we must exclude the sub interfaces on building router.
* Then we enter on router config DHCPv4 service for each VLAN within the building, except for DMZ.
* To set DHCPv4 we use this commands:

> ip dhcp pool [pool-name] <br>
> default-router [default-gateway] <br>
> network [network-address] [subnet-mask] <br>

* The VoIP VLAN DHCP server configuration include option 150.


---

## VoIP service

* To set the VoIP service we first add another "IP phone 7960" to building and set the telephony service on building router.

> telephony-service
max-ephones 2
max-dn 2
ip source-address [ip-address] port 2000
auto assign 1 to 2

>ephone-dn 1
number 1001
ephone-dn 2
number 1002

* To received calls from other building we add this commands
>dial-peer voice [building-vlan_id] voip
> destination-pattern[building-number]
> session target ipv4:[ip-address-of-building-VoIP-addresses]


* And on switch connection to VoIP phone we enabled the voice VLAN (switchport voice vlan VLANID) and disabled the access VLAN  (no switchport access vlan).



---

## DNS

![DNS](resources/DNS.png)

---

## NAT (Network Address Translation)

**HTTP**
>ip nat inside source static tcp 10.81.188.243 443 10.81.189.1 443
ip nat inside source static tcp 10.81.188.243 80 10.81.189.1 80

**DNS**
>ip nat inside source static tcp 10.81.188.242 53 10.81.189.1 53
ip nat inside source static udp 10.81.188.242 53 10.81.189.1 53

10.81.188.243 --> ip  Server_HTTP
10.81.188.242 --> ip  Server_DNS
10.81.189.1   --> ip da sub-interface backbone

---

## Static Firewall (ACLs)

**Configure for every Local Network except DMZ**

>no access-list [LIST-NUMBER]
access-list [LIST-NUMBER] deny ip any host [SUB-INTERFACE] -> Configure for all Local Networks (Deny connection with [SUB-INTERFACE]) <br>              
access-list [LIST-NUMBER] permit icmp any [DMZ-NETWORK] [DMZ-WILD-CARD] echo-reply -> (Allow PC communication with Server)<br>
access-list [LIST-NUMBER] permit tcp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 80 -> (All traffic to the DMZ should go to 80 )<br>
access-list [LIST-NUMBER] permit tcp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 443 -> (All traffic to the DMZ should go to 443)<br>
access-list [LIST-NUMBER] permit tcp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 53 -> (All traffic to the DMZ should go to 53 tcp)<br>
access-list [LIST-NUMBER] permit udp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 53 -> (All traffic to the DMZ should go to 53 upd)<br>
access-list [LIST-NUMBER] deny ip any [DMZ-NETWORK] [DMZ-WILD-CARD] -> (Deny communication with DMZ) <br>                      
access-list [LIST-NUMBER] permit ip [NETWORK] [NETWORK-WILD-CARD] any -> (Unblock ips of this network)   <br>                    
access-list [LIST-NUMBER] permit udp any eq bootpc any eq bootps ->  (Allow DHCP)   <br>               
interface [ROUTER-SUB-INTERFACE] <br>
ip access-group [LIST-NUMBER] in <br>

**Configure ACL external Spoofing**

>no access-list 100 <br>
access-list 100 deny ip [DMZ-NETWORK] [DMZ-WILD-CARD] any -> (Deny IP traffic originating from the [DMZ-NETWORK])<br>
access-list 100 permit tcp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 80 -> (All traffic to the DMZ should go to 80)<br>
access-list 100 permit tcp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 443 -> (All traffic to the DMZ should go to 443)<br>
access-list 100 permit tcp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 53 -> (All traffic to the DMZ should go to 53 tcp)<br>
access-list 100 permit udp any [DMZ-NETWORK] [DMZ-WILD-CARD] eq 53 -> (All traffic to the DMZ should go to 53 upd)<br>
------------------------------------------------------------------------------------------------------------------------------------------------| <br>
access-list 100 deny ip [NETWORK] [WILD-CARD] any -> (Don't allow external Spoofing) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | <br>
access-list 100 deny ip any host [SUB-INTERFACE]  -> (Deny connection with [SUB-INTERFACE]) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |-----> Configure for all Local Networks except DMZ <br>
access-list 100 permit ip any [NETWORK] [WILD-CARD] -> (Allow send to [NETWORK]) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | <br>
------------------------------------------------------------------------------------------------------------------------------------------------| <br>
access-list 100 permit ip any [BACKBONE-NETWORK] [BACKBONE-WILD-CARD] -> (Allow valid communications to [BACKBONE-NETWORK])
access-list 100 deny ip any host [DMZ-SUB-INTERFACE] -> (Deny communication with [DMZ-SUB-INTERFACE] )
access-list 100 permit icmp any [DMZ-NETWORK] [DMZ-WILD-CARD] echo-reply -> (Allow PC connection to Server)
access-list 100 permit ospf any any -> (Allow OSPF)
interface [BACKBONE-INTERFACE]
ip access-group 100 in

| LOCAL NETWORKS | LIST | SUB-INTERFACE |    NETWORK     | WILD-CARD | ROUTER-SUB-INTERFACE |
|:--------------:|:----:|:-------------:|:--------------:|:---------:|:--------------------:|
|    FLOOR 0     | 101  | 10.81.188.193 | 10.81.188.192  | 0.0.0.31  |  FastEthernet0/0.1   |
|    FLOOR 1     | 102  | 10.81.188.129 | 10.81.188.128  | 0.0.0.63  |  FastEthernet0/0.2   |
|     WI-FI      | 103  |  10.81.188.1  |  10.81.188.0   | 0.0.0.127 |  FastEthernet0/0.3   |
|      DMZ       | ---  | 10.81.188.241 | 10.81.188.240  | 0.0.0.15  |  FastEthernet0/0.4   |
|      VOIP      | 105  | 10.81.188.225 | 10.81.188.224  | 0.0.0.15  |  FastEthernet0/0.5   |

BACKBONE-NETWORK: 10.81.189.0 <br>
BACKBONE-WILD-CARD: 0.0.0.127 <br>
BACKBONE-INTERFACE: FastEthernet0/1 <br>

---