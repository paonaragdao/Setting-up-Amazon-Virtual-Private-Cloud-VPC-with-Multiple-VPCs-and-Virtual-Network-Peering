# Setting up Amazon Virtual Private Cloud (VPC) with Multiple VPCs and Virtual Network Peering

In this user documentation, we will guide you through the process of setting up three VPCs (VPC A, VPC B, and VPC C) using Amazon Virtual Private Cloud. Each VPC will have private subnets in two Availability Zones within the chosen region. We will also deploy one EC2 instance per VPC. Additionally, we will establish VPC peering links between VPC A and VPC B, as well as between VPC A and VPC C. This guide assumes basic knowledge of AWS services and networking concepts.

## Diagram

![Network Peering](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/91071643-0dfc-4337-a1dd-7cb570507be3)


## Step 1: Designing the Virtual Network Before starting the setup

Let's design the virtual network based on the networking and business requirements. Identify the IP ranges to be used for each VPC and subnet. Ensure that they do not overlap.

VPC A:
•	VPC CIDR: 10.0.0.0/16 
•	Subnet A1 (Availability Zone 1): 10.0.0.0/24
•	Subnet A2 (Availability Zone 2): 10.0.1.0/24
VPC B:
•	VPC CIDR: 10.1.0.0/16
•	Subnet B1 (Availability Zone 1): 10.1.0.0/24
•	Subnet B2 (Availability Zone 2): 10.1.1.0/24
VPC C:
•	VPC CIDR: 10.2.0.0/16
•	Subnet C1 (Availability Zone 1): 10.2.0.0/24
•	Subnet C2 (Availability Zone 2): 10.2.1.0/24



## Step 2: Creating VPCs and Subnets 

Let's create the VPCs and subnets based on the designed network.

1.	Go to the AWS Management Console and navigate to the VPC service.
2.	Click on "Create VPC" and provide the necessary details for VPC A. Repeat this step for VPC B and VPC C.
3.	Once the VPCs are created, create the subnets within each VPC, ensuring they are placed in the correct Availability Zones.

![VPC](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/a9fc115e-f013-4336-a18b-b4ce5b29bca2)
![Subnets](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/df2ba427-73f7-4e7f-863b-53cb6df66436)


## Step 3: Enabling Network Gateways To enable communication between the VPCs and the internet

We need to set up network gateways.

1.	Create an Internet Gateway (IGW) in the VPC service.
2.	Attach the IGW to each VPC.
3.	Update the route tables of each subnet to route internet-bound traffic to the IGW.



## Step 4: Configuring Route Tables To control the traffic flow within and between the VPCs

We need to configure route tables.

1.	Create a route table for each subnet within the VPC service.
2.	Associate the appropriate subnets with their respective route tables.
3.	Add the necessary routes to ensure connectivity between subnets and VPCs.

![Route Tables](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/a0a12b9f-b987-46dd-803d-21cc82a97e14)


## Step 5: Configuring Security Controls To support the test environment

1.	Set up Security Groups to define the allowed inbound and outbound traffic for the EC2 instances within each VPC.

![SGs](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/92cf86b6-4c19-4640-8c90-156c758c504f)


## Step 6: Testing Network Traffic

After setting up the VPCs, subnets, gateways, route tables, and security controls, it's time to test the network traffic.

1.	Access the EC2 instances deployed in each VPC using SSH/RDP.
2.	Verify if the expected network traffic is permitted into, through, and out of each VPC.
3.	Test external connectivity to a resource within each VPC and ensure that only permitted traffic reaches the resource.



## Step 7: Step 7: Troubleshooting and Error Fixing 

If you encounter any errors or issues during the setup or testing, follow these troubleshooting steps:

1.	Check the configuration of VPCs, subnets, gateways, route tables, security groups, and NACLs for any misconfigurations.
2.	Review the AWS documentation and search for specific error messages to identify potential solutions.



## Step 8: Configuring Virtual Network Peering

In addition to the previous steps, we will now configure virtual network peering between the VPCs.

1.	Go to the VPC service in the AWS Management Console.
2.	Establish peering connections between VPC A and VPC B, as well as between VPC A and VPC C.
3.	Adjust the routing tables for each VPC to direct traffic between the peered networks.
4.	Test network connectivity between hosts in each network and troubleshoot any issues if encountered.

![Peering Connections](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/76a141e2-6c9e-4030-8a0b-052c5edb492c)


## Step 9: Verifying connections

1.	In the EC2 instance within VPC A, open a terminal or command prompt.
2.	Ping the private IP address of the EC2 instance in VPC B.
3.	Example command: ping 10.1.0.10
4.	Verify that you receive a response, indicating successful network connectivity.
5.	Repeat the above steps to test network connectivity between EC2 instances in VPC C.


![VPC A - VPC B](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/e7e4a023-edee-4625-9932-103ae4fec53c)
![VPC A - VPC C](https://github.com/paonaragdao/Setting-up-Amazon-Virtual-Private-Cloud-VPC-with-Multiple-VPCs-and-Virtual-Network-Peering/assets/48607496/28283a3d-cb26-48d8-8586-44bd55a6f4e2)


