# Small Organization Secure-network-topology
## Project Overview
This project demonstrates how a small computer network can be designed, configured, and secured using Cisco Packet Tracer.

The goal was to simulate how devices in an organization communicate with each other while keeping the network organized and secure.

In this project, I created multiple Virtual Local Area Networks(VLANs), configured routers and switches, and applied Access Control Lists (ACLs) to control which devices are allowed to communicate.

The simulation helps show how real company networks are built and managed.

# Network scenerio
 The organization consists of:
* IT Department (1PC, 1 SERVER)
* Management   (2PCS)
* Staff IP  (2LAPTOPS)
* External Network  (1PC)
* 1 Router
* 1 Switch
Each department is assigned a seperate VLAN for security and trafffic management.

Each device was connected using  appropriate cables to simulate how devices would connect in a real office enviroment.

The purpose of the design was to seperate different departments into their own networks while still allowing controlled communication between them.

## Network Topology
Network Topology <img width="1440" height="900" alt="topology1" src="https://github.com/user-attachments/assets/f3a8d82c-4db0-4278-a9f1-531d7e128749" />
<img width="1440" height="900" alt="topology" src="https://github.com/user-attachments/assets/ad56a4b8-11eb-48fc-b26c-b322238894c4" />
## Technologies Used
- Cisco Packet Tracer
- VLAN Configuration
- IP Addressing
- Inter-VLAN Routing
- Ping Testing

## IP Addressing Scheme
|Device            |IP Address   |Subnet Mask    |VLAN    | 
|------------------|-------------|---------------|--------|
| IT               | 192.168.10.0|255.255.255.0  |10      |
| Management       | 192.168.20.0|255.255.255.0  |20      |
| Staff            | 192.168.30.0|255.255.255.0  |30      |
| External Network | 10.10.10.0  |255.0.0.0      |        |
## VLAN Configuration
VLAN stands for Virtual Local Area Network
Instaed of having every computer on the same neetwrok, Vlans allow devices to be grouped logically. 
This improves both security and netwrok performance.
For example,
- VLAN 10 - IT
- VLAN 20 - Management 
- VLAN 30 - Staff
  
Each VLAN acts like its own small network even though they are connected to the same switch.

VLAN Configuration<img width="1440" height="900" alt="vlan-config" src="https://github.com/user-attachments/assets/37d907d5-ec57-4ca3-8a74-11a81d080513" />
<img width="1440" height="900" alt="vlan-config2" src="https://github.com/user-attachments/assets/7b08d7fc-1e6d-4d49-b004-36680feee785" />
VLANs were configured on switches to isolate traffic between departments.

## Routing Configuration
A router was configured to allow communication between the different VLANs. 
This process is called Inteer-VLAN Routing.
Without the router, devices in different VLANs would not be able to communicate with each other.
The router acts like a traffic controller, directing data between networks.

Router config <img width="1440" height="900" alt="router-config" src="https://github.com/user-attachments/assets/09f7969c-61d0-4d00-8228-dc810ae15073" />

## Security Measures
To ensure the network remains secure and properly controlled, several security mechanismswere implimented on the switches and routers.  These configurations help protect and infrastructure from unauthorized access, prevent misuse of network resourcesm, and enforce administrative control over the devices.

- ## VLAN Segmentation for department isolation
  
The network was divided into multiple Virtual Local Area Networks. VLANs logically seperate devices into different departments even though they share the same physical switch.

This improves  netwrok organization and security because devices in one department cannot freely communicate with devices in another department explicitly allowed through routing.

For example:
- Vlan 10 - IT
- Vlan 20 - Management
- Vlan 30 - Staff

code:

- enable
- configure terminal 
- vlan 10 
- name IT 
- vlan 20
- name Management 
- Vlan 30
- name Staff

this configuration creates three Vlans and asigns them names corresponding to deprtments within the organization.

- ## Assigning Switch ports to VLANs
After creating VLANs, switch ports were assigned to specific VLANs so that devices connected to those ports sutomatically become members of the appropriate netwrok segment.
Port Assignment Example

* interface fastEthernet0/1
* switchport mode access
* switchport access vlan 10

* interface fastethernet0/2
* switchport mode access 
* switchport access vlan 20

* interface fastethernet0/3
* switchport mode access
* switchport access vlan 30

This ensures that devices connected to each port belong to their designated department network.


  
- ## Inter-vlan Routing
Since devices in different vlans cannot coomunicate directly, a router was configured to allow controlled communication between VLANs.

This process is known as Inter-vlan routing and allows departments to share resources when necessary while maintaining segmentation.

Router Configuration

* interface g0/0.10
* encapsulation dot1Q 10
* ip address 192.168.10.1 255.255.255.0

* interface g0/0.20
* encapsulation dot1Q 20
* ip address 192.168.20.1 255.255.255.0

* interface g0/0.30
* encapsualtion dot1Q 30
* ip address 192.168.30.1 255.255.255.0

Each VLAN receives its own gateway for comunication between networks.

- ## Password Protection
Basic password security was implemented on routers and switches to prevent unauthorized configuration access.
* enable
* conf t
* password 

this ensures that only authorized adminstrators can manage network devices.

- ## Banner MOTD
A message of the day (motd) banner was configured to warn users that the system is restricted.

* banner motd #

This message appears whenever someone attempts to access the device.

- ## Testing and verification
Devices within the same VLAN were tested for communication using ping commands.

- ## Connectivity Testing
Devices within the same VLAN were tested for communication using ping commands.
Example:
ping 192.168.20.2

- ## Network Validation
The following checks were performed:
- Devices within the same VLAN communicate successfully
- inter-vlan communication works through the router
- Disabled ports remain inactive
- Login authentication and MOTD banner appear correctly

- ## Port Security
Port security allows the switch to limit the number of MAC addresses that can connect to a specific port. I configured each access port to allow only one device using sticky MAC learning. If another device tries to connect, the port automatically shuts down to protect the network.

This improves internal network security and prevents unauthorized access at the access layer.

Configuration Steps used:
- interface fa0/1
- switchport mode access
- switchport port-security
- switchport port-security maximum 1
- switchport port-security mac-address sticky
- switchport port-security violation shutdown



## Conclusion
The network was Successfully implemented according to the lab scenerio.
All departments can communicate as intended, while maintaining proper isolation and security.

## Key Learnings
- VLAN creation and management
- Inter-vlan routing
- IP planning
- Network troubleshooting and testing.
- Port Security

## Lab File
You can download the Cisco Packet Tracer lab file to try it yourself
[small secure network topology.pkt.zip](https://github.com/user-attachments/files/25741494/small.secure.network.topology.pkt.zip)
