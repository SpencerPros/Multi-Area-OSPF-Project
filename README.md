# Multi-Area OSPF Project (Work in Progress)


## Project Overview

In this project, I wanted to get a sense of what a real world scenario would look like when seeting up Multi-Area OSPF on a network. So I designed and implemented a network using OSPF with multiple areas in Cisco Packet Tracer to demonstrate efficient routing and network segmentation. This network consists of PC's, routers, and switches interconnected to simulate a real-world scenario.

## Features

- **Network Topology:** Detailed network diagram and description of the topology used in the project.
- **Configuration Files:** Configuration files for routers and switches in each OSPF area.
- **Documentation:** Detailed documentation explaining the project objectives, design decisions, and implementation steps.
- **Testing and Validation:** Methods used to test and validate the network configuration, including packet captures and routing table analysis.

## My Project Goals

- Understand the fundamentals of OSPF routing protocol and its advantages in large-scale networks.
- Practice network segmentation and routing optimization using OSPF areas.
- Gain hands-on experience with network simulation and configuration.

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
| R2       | S0/2/0     | 200.10.50.5   | /30   |
| R2       | S0/2/1     | 200.10.50.10  | /30   |
| R2       | Loopback0  | 55.0.0.2      | /32   |
| R3       | Fa0/0      | 88.88.10.129  | /25   |
| R3       | S0/2/0     | 200.10.50.6   | /30   |
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
  
**Host 1**

   ![image](https://github.com/SpencerPros/Multi-Area-OSPF-Project/assets/156951668/785f6b39-0ac8-445a-8b98-f20c57f8c798)
  * I made the default gateway on Host 1 the IP address of the Fa0/0 interface on R1 since thats the first interface Host 1 will hit when trying to communicate outside its subnet.


**Host 2**

  ![image](https://github.com/SpencerPros/Multi-Area-OSPF-Project/assets/156951668/1cec499f-25f0-4006-8ff8-0956d6d29961)
  * I made the default gateway on Host 2 the IP address of the Fa0/0 interface on R4 since thats the first interface Host 2 will hit when trying to communicate outside its subnet.


**Routers**
* For the routers I will show how to implement the IP address on port Fa0/0 on R1 but this method can be used to apply the IP address, Area, and Subnet Mask onto each routers ports
* Quick tip: The DCE serial interfaces you saw marked in the toplogy need to be assigned the higher IP in it's subnet. This consistency makes network configuration and troubleshooting easier, as network administrators can predict the IP addresses of DCE devices in the subnet.




## Challenges Faced







## Future Enhancements

- Expand the network by adding more OSPF areas or integrating additional networking protocols.
- Implement security measures such as Access Control Lists (ACLs) and Virtual Private Networks (VPNs) to enhance network protection.
- Integrate real-world scenarios and traffic patterns for more realistic simulation and testing.

