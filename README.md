# Multi-Area OSPF Project


## Project Overview

In this project, I wanted to get a sense of what a real-world scenario would look like when setting up Multi-Area OSPF on a network. So, I designed and implemented a network using OSPF with multiple areas in Cisco Packet Tracer to demonstrate efficient routing and network segmentation. This network consists of PC's, routers, and switches interconnected to simulate a real-world scenario the best I could.

## Features

- **Network Topology:** Detailed network diagram and description of the topology used in the project.
- **Configuration Files:** Configuration files for routers and switches in each OSPF area.
- **Documentation:** Detailed documentation explaining the project objectives, design decisions, and implementation steps.
- **Testing and Validation:** Methods used to test and validate the network configuration, including packet captures and routing table analysis.

## My Project Goals

- Understand the fundamentals of OSPF routing protocol and its advantages in large-scale networks.
- Practice network segmentation and routing optimization using OSPF areas.
- Gain hands-on experience with network simulation and configuration.

## Table of Contents
- [Setup Instructions](#setup-instructions)
- [Documentation](#documentation)
- [Challenges Faced](#challenges-faced)
- [Future Enhancements](#future-enhancements)




## Setup Instructions
1. **Requirements:** Ensure you have Cisco Packet Tracer installed on your system.
2. **Clone Repository:** Clone this repository to your local machine using `git clone https://github.com/your-username/multi-area-ospf-network.git`.
3. **Open the Project:** Open the project file in Cisco Packet Tracer.
4. **Simulate and Test:** Simulate the network and validate OSPF functionality across different areas.
5. **Explore Documentation:** Refer to the documentation folder for detailed setup instructions, network diagrams, and configuration explanations.


## Documentation 
  **Part 1: My IP Subnet Design**
  * This  first table outlines the detailed subnet design for the network, including subnet names, network addresses, prefix lengths, subnet sizes, first and last valid host IPs, and OSPF area assignments. It provides a detailed overview of the network segmentation and routing configuration.
 
| Subnet Name | Subnet Network Address | Prefix Length (/n) | Size | First Valid Host IP | Last Valid Host IP | OSPF Area (0 or 2) |
|-------------|------------------------|--------------------|------|---------------------|--------------------|---------------------|
| Subnet A    | 77.77.50.128           | /25                | 128  | 77.77.50.129        | 77.77.50.254       | 2                   |
| Subnet B    | 88.88.10.128           | /25                | 128  | 88.88.10.129        | 88.88.10.254       | 0                   |
| Subnet C    | 40.40.0.0              | /25                | 128  | 40.40.0.1           | 40.40.0.126        | 0                   |
| Link 1      | 200.10.50.0            | /30                | 4    | 200.10.50.1         | 200.10.50.2        | 2                   |
| Link 2      | 200.10.50.4            | /30                | 4    | 200.10.50.5         | 200.10.50.6        | 2                   |
| Link 3      | 200.10.50.8            | /30                | 4    | 200.10.50.9         | 200.10.50.10       | 2                   |
| R1 Lo0      | 55.0.0.1               | /32                | 1    | 55.0.0.1            | 55.0.0.1           | 2                   |
| R2 Lo0      | 55.0.0.2               | /32                | 1    | 55.0.0.2            | 55.0.0.2           | 2                   |
| R3 Lo0      | 55.0.0.3               | /32                | 1    | 55.0.0.3            | 55.0.0.3           | 0                   |
| R4 Lo0      | 55.0.0.4               | /32                | 1    | 55.0.0.4            | 55.0.0.4           | 0                   |


**Part 2: My IP Address Assignments**
* This second table shows the specific IP addresses allocated to each device and host within the network. It includes details such as device names, interface names, IP addresses, and subnet masks. This plan is essential for understanding the network topology and managing IP address assignments effectively.

| Device   | Interface  | IP Address    | Mask  |
|----------|------------|---------------|-------|
| R1       | Fa0/0      | 77.77.50.129  | /25   |
| R1       | S0/2/0     | 200.10.50.2   | /30   |
| R1       | S0/2/1     | 200.10.50.9   | /30   |
| R1       | Loopback0  | 55.0.0.1      | /32   |
| R2       | S0/2/0     | 200.10.50.6   | /30   |
| R2       | S0/2/1     | 200.10.50.10  | /30   |
| R2       | Loopback0  | 55.0.0.2      | /32   |
| R3       | Fa0/0      | 88.88.10.129  | /25   |
| R3       | S0/2/0     | 200.10.50.5   | /30   |
| R3       | S0/2/1     | 200.10.50.1   | /30   |
| R3       | Loopback0  | 55.0.0.3      | /32   |
| R4       | Fa0/0      | 40.40.0.1     | /25   |
| R4       | Fa0/1      | 88.88.10.130  | /25   |
| R4       | Loopback0  | 55.0.0.4      | /32   |
| Host #1  | LAN        | 77.77.50.150  | /25   |
| Host #2  | LAN        | 40.40.0.50    | /25   |


 **Part 3: Network Topology**
 * For my topology draft I used 4 routers, 3 switches, and 2 PC's. With 3 serial links connecting routers R1-R3, R2-R3, and R2-R1. Routers 1 and 2 also have DCE interfaces and I gave link 1 different bandwidth value. I also created two areas being Area 2 and Area 0
![image](https://github.com/SpencerPros/Multi-Area-OSPF-Project/assets/156951668/5b10cf9b-592d-4600-a532-3af6b0efc853)

**Part 4: Implementing the Network**
* First I had to create the topology I drafted into Packet Tracer itself. I color coded the areas just so i could visually see which ports and routers are in which area better.
  ![image](https://github.com/SpencerPros/Multi-Area-OSPF-Project/assets/156951668/d8aa24ca-949b-4c4a-b860-0b280aa85fb9)


* Next I had to implement the IP Addressing on all devices in the network first I started with the PC's, Host 1 and 2.
  
### Host 1

   ![image](https://github.com/SpencerPros/Multi-Area-OSPF-Project/assets/156951668/785f6b39-0ac8-445a-8b98-f20c57f8c798)
  * I made the default gateway on Host 1 the IP address of the Fa0/0 interface on R1 since thats the first interface Host 1 will hit when trying to communicate outside its subnet.


### Host 2

  ![image](https://github.com/SpencerPros/Multi-Area-OSPF-Project/assets/156951668/1cec499f-25f0-4006-8ff8-0956d6d29961)
  * I made the default gateway on Host 2 the IP address of the Fa0/0 interface on R4 since thats the first interface Host 2 will hit when trying to communicate outside its subnet.

<br>

### Routers
* For the routers I will show how I implemented the IP address on port Fa0/0 on R1 but this method can be used to apply the IP address, Area, and Subnet Mask onto each routers ports
* The DCE serial interfaces you saw marked in the toplogy I assigned to be the higher IP in it's subnet. This consistency makes network configuration and troubleshooting easier, as network administrators can predict the IP addresses of DCE devices in the subnet.

  ![Router IP Implementation](https://github.com/user-attachments/assets/89a7b74a-d868-4b1b-95a1-29db340470d0)

### DCE Interfaces
* For DCE Interfaces I configured the clock rate to match what was in the topology. In my topology I have Link 1 being 1 mbps, and Links 2 and 3 being 4 mbps.
* To assign the clock rate, first I went into the router of the specific DCE port. In the example below I will implement the clock rate on Link 1 to the serial port S0/2/0 on R1. After doing that you will assign the clock rate doing the following commands, repeat this on each routers DCE interface with the correct clock rate values (1000000 for 1mbps, 4000000 for 4mbps)

  ![image](https://github.com/user-attachments/assets/7cd33b10-44ca-4b51-bc37-305f88a8f117)

<br>

### Quick Testing
* Before moving on I made sure that I can ping from each Host to its default gateway, as well as each router to its next-hop router. For example this is me pinging Host 1 to its deault gateway do the same but for Host 2 as well. Also I double checked each routers IP and subnet. Using an example on R1 writing the command "show ip int brief" on each router and see if all the IP addressing matches my table.
  ![image](https://github.com/user-attachments/assets/df9c1de1-7bd0-4998-afec-abc7ad57960b)

<br>
 
### OSPF Configuration Instructions
* Now that all routers and interfaces are configured it is time to setup the OSPF protocol on all routers and areas. This will defenitly be the most important part of the process so I really had to make sure everything is setup right.
* Create a OSPF process with a ID of 50 on each router, I will show how in a example code below

### First, On each router, I configured OSPF process 50 and manually set the Router ID as follows:

1. **R1 Router ID is 1.1.1.1**
    ```plaintext
    R1> enable
    R1# configure terminal
    R1(config)# router ospf 50
    R1(config-router)# router-id 1.1.1.1
    R1(config-router)# end
    ```

2. **R2 Router ID is 2.2.2.2**
    ```plaintext
    R2> enable
    R2# configure terminal
    R2(config)# router ospf 50
    R2(config-router)# router-id 2.2.2.2
    R2(config-router)# end
    ```

3. **R3 Router ID is 3.3.3.3**
    ```plaintext
    R3> enable
    R3# configure terminal
    R3(config)# router ospf 50
    R3(config-router)# router-id 3.3.3.3
    R3(config-router)# end
    ```

4. **R4 Router ID is 4.4.4.4**
    ```plaintext
    R4> enable
    R4# configure terminal
    R4(config)# router ospf 50
    R4(config-router)# router-id 4.4.4.4
    R4(config-router)# end
    ```

### Next I Activated OSPF on all router interfaces including Loopbacks, FastEthernet, and Serial interfaces and make the 4 Loopback interfaces and R1 Fa0/0 and R4 Fa0/0 passive interfaces
* Interfaces I did not list above specifically I did not make them passive interfaces

 **Example of Router 1:**
   ```plaintext
   R1-SP>enable 
   R1-SP#conf t
   R1-SP(config)#router ospf 50
   R1-SP(config-router)# network 77.77.50.128 0.0.0.127 area 2
   R1-SP(config-router)# network 200.10.50.0 0.0.0.3 area 2
   R1-SP(config-router)# network 200.10.50.8 0.0.0.3 area 2
   R1-SP(config-router)# network 55.0.0.1 0.0.0.0 area 2
   R1-SP(confif-router)#passive-interface FastEthernet0/0
   R1-SP(config-router)#passive-interface Loopback0
   ```

**Example of Router 2:**
   ```plaintext
   R2-SP>enable 
   R2-SP#conf t
   R2-SP(config)#router ospf 50
   R2-SP(config-router)# network 200.10.50.4 0.0.0.3 area 2
   R2-SP(config-router)# network 200.10.50.8 0.0.0.3 area 2
   R2-SP(config-router)# network 55.0.0.2 0.0.0.0 area 2
   R2-SP(config-router)# passive-interface Loopback0
   ```

**Example of Router 3:**
   ```plaintext
   R3-SP>enable 
   R3-SP#conf t
   R3-SP(config)#router ospf 50
   R3-SP(config-router)# network 88.88.10.128 0.0.0.127 area 0
   R3-SP(config-router)# network 200.10.50.0 0.0.0.3 area 2
   R3-SP(config-router)# network 200.10.50.4 0.0.0.3 area 2
   R3-SP(config-router)# network 55.0.0.3 0.0.0.0 area 0
   R3-SP(config-router)#passive-interface Loopback0
   ```

**Example of Router 4:**
   ```plaintext
   R4-SP>enable 
   R4-SP#conf t
   R4-SP(config)#router ospf 50
   R4-SP(config-router)# network 40.40.0.0 0.0.0.127 area 0
   R4-SP(config-router)# network 88.88.10.128 0.0.0.127 area 0
   R4-SP(config-router)# network 55.0.0.4 0.0.0.0 area 0
   R4-SP(config-router)#passive-interface Loopback0
   ```


# Challenges Faced

## My Network Design

### Determining the Number of Routers and Area Boundaries:

- **Challenge:** Figuring out the optimal number of routers and defining the boundaries of each OSPF area.
- **Solution:** Analyzed different network scenarios and topologies to find a balance that ensures efficient routing and scalability. Decided on four routers as the ideal size to provide a comprehensive yet manageable network setup.

### Ensuring Proper Backbone Area (Area 0) Connectivity:

- **Challenge:** Ensuring that the backbone area (Area 0) was properly connected to all other areas to maintain OSPF hierarchy and efficiency.
- **Solution:** Verified that all areas had at least one connection to Area 0, maintaining the integrity of the OSPF design and facilitating seamless inter-area routing.

  
### Deciding on the Number of Routers:

- **Challenge:** Choosing the right number of routers to include in the network.
- **Solution:** I settled on four routers, considering it a good number to demonstrate multi-area OSPF without making the network overly complex.


## Addressing and Subnetting 

### Creating a Comprehensive Routing Table:

- **Challenge:** Creating a routing table that included multiple subnets to increase the complexity and realism of the project.
- **Solution:** I designed and implemented a detailed routing table with various subnets, ensuring each subnet was properly documented and integrated into the network.

### Ensuring Proper Interface Addressing:

- **Challenge:** Making sure that each interface was addressed correctly and placed within the appropriate subnet.
- **Solution:** Carefully assigned IP addresses to each interface, cross-referenced with the subnet design to avoid conflicts, and verified the addressing through simulations and testing.

### Managing Subnet Assignments:

- **Challenge:** Making sure that each subnet was allocated appropriately to balance network traffic and ensure efficient routing.
- **Solution:** Conducted thorough planning and analysis to assign subnets in a way that optimized network performance and minimized potential issues.

  
## Documentation and Troubleshooting

### Detailing Network Design and Configuration:

- **Challenge:** Ensuring that all aspects of the network design and configuration were accurately documented.
- **Solution:** Created detailed tables and diagrams for my subnet/network design, IP address assignments, and network topology. This helped in keeping track of the configuration and provided a clear reference for troubleshooting.


### Keeping track of changes:
- **Challenge:** Keeping documentation up-to-date.
- **Solution:** After each step I would refer back to this 'README' and update it with any change I made

### Pinging Issues Between Devices
- **Challenge:** Identifying and resolving connectivity issues between devices when initial pings failed.
- **Solution:** Used step-by-step troubleshooting techniques such as verifying physical connections, checking interface statuses, and used commands like show ip int brief and ping to isolate and resolve issues.

### Resolving OSPF Configuration Errors:

- **Challenge:** Making sure OSPF configurations were correctly configured across all routers, especially with multiple areas.
- **Solution:** Verified OSPF neighbor relationships and routing tables using commands like `show ip ospf neighbor` and `show ip route`. Adjusted configurations as needed to ensure proper OSPF operation.


# Technical Skills I gained from this project

## Network Design and Implementation
- Designing complex network topologies
- Implementing network segmentation and efficient routing strategies

## Routing Protocols
- Configuring and managing OSPF in multi-area environments
- Understanding OSPF concepts such as areas, router IDs, and passive interfaces

## Subnetting and IP Addressing
- Planning and implementing subnetting schemes
- Assigning IP addresses to devices and interfaces

## Cisco Device Configuration
- Configuring Cisco routers and switches

## Network Security
- Implementing security measures such as passive interfaces
- Understanding the importance of network security in OSPF configurations

# Future Enhancements

- Expand the network by adding more routers and OSPF areas or integrating additional networking protocols.
- Implement security measures such as Access Control Lists and Virtual Private Networks to enhance the networks protection.
- Integrate real-world scenarios and traffic patterns for more realistic simulation and testing.

