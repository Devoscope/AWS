# What is a Subnet?

A **subnet** (short for "subnetwork") is a smaller network that is created by dividing a larger network into smaller, more manageable segments. Subnetting allows network administrators to efficiently organize and utilize IP address space, improve performance, and enhance security within a larger network.

## Key Points about Subnets:

### 1. IP Address Division
An IP address is made up of two main parts: the **network portion** (which identifies the network) and the **host portion** (which identifies a specific device or host within that network). By using subnetting, the network portion is further divided into smaller sections.

### 2. Subnet Mask
A **subnet mask** is used to determine which part of an IP address refers to the network and which part refers to the host. It defines the boundaries of the subnet. For example, a common subnet mask for IPv4 is `255.255.255.0`, which means the first three octets (the first 24 bits) represent the network, and the last octet (the last 8 bits) is used for hosts.

### 3. CIDR Notation
Instead of using a subnet mask, **CIDR** (Classless Inter-Domain Routing) notation is often used to describe subnets. This notation combines the IP address and subnet mask into a single string. For example, `192.168.1.0/24` means the IP address `192.168.1.0` with a subnet mask of `255.255.255.0` (the `/24` represents the number of bits allocated to the network).

### 4. Improved Efficiency
Subnetting allows for more efficient use of IP address space, ensuring that different departments or groups within an organization can have their own isolated networks.

### 5. Security
Subnetting can improve security by isolating traffic between subnets. Devices in one subnet may not be able to communicate directly with devices in another subnet without proper routing or access control.

### 6. Routing
Routers are used to direct traffic between different subnets. This allows for communication between devices on different subnets, but also enables the isolation of traffic when needed.

## Example:

A company has the IP range `192.168.1.0/24` (which has 256 possible addresses).

The company wants to split this range into two subnets. One option would be to use:

- `192.168.1.0/25` for the first subnet, which uses addresses `192.168.1.0` to `192.168.1.127`
- `192.168.1.128/25` for the second subnet, which uses addresses `192.168.1.128` to `192.168.1.255`

This division allows the company to manage network traffic more efficiently, reduce broadcast traffic, and segment devices based on function, department, or security needs.


# AWS Subnet Reserved IP Addresses

In AWS, the first four IP addresses and the last IP address in each subnet's CIDR block are **reserved** and not available for use. This is done for specific network-related purposes to ensure proper functionality within the VPC. Below is an explanation of why each of these IP addresses is reserved:

## 1. **First IP Address (Network Address)**
   - **Purpose**: The first IP address is reserved as the **network address** of the subnet.
   - **Why It's Reserved**: The network address identifies the entire subnet and cannot be assigned to any individual host or instance. It is used to represent the subnet itself.
   - **Example**: In a subnet with the CIDR `10.0.1.0/24`, the first IP address `10.0.1.0` is the network address.

## 2. **Second IP Address (Reserved for VPC Router)**
   - **Purpose**: The second IP address is reserved for the **VPC router**.
   - **Why It's Reserved**: AWS uses this IP address for routing traffic within the VPC and between subnets. It is the first usable IP address in the subnet but is reserved for internal routing functions.
   - **Example**: In the subnet `10.0.1.0/24`, the second IP address `10.0.1.1` is used by the VPC router.

## 3. **Third IP Address (Reserved for DNS)**
   - **Purpose**: The third IP address is often reserved for **DNS** purposes.
   - **Why It's Reserved**: This IP is used by AWS for DNS resolution services within the VPC. In certain configurations, it may be associated with **Amazon Route 53** or other internal DNS services.
   - **Example**: In the subnet `10.0.1.0/24`, the third IP address `10.0.1.2` might be reserved for DNS purposes, depending on the AWS setup.

## 4. **Fourth IP Address (Reserved for Future Use)**
   - **Purpose**: The fourth IP address is reserved for **future use** by AWS.
   - **Why It's Reserved**: This IP address is kept available for AWS’s internal use or for future network services. It is not allocated to any instance or service.
   - **Example**: In the subnet `10.0.1.0/24`, the fourth IP address `10.0.1.3` is reserved for future use by AWS.

## 5. **Last IP Address (Broadcast Address)**
   - **Purpose**: The last IP address in the subnet is reserved as the **broadcast address**.
   - **Why It's Reserved**: The broadcast address is used to send broadcast messages to all instances within the subnet. It cannot be assigned to any specific host or instance.
   - **Example**: In the subnet `10.0.1.0/24`, the last IP address `10.0.1.255` is the broadcast address.

---

## Summary:
In each subnet CIDR block in AWS, the first four IP addresses and the last IP address are reserved for specific network-related purposes such as identifying the subnet (network address), routing traffic within the VPC (VPC router), DNS resolution, future AWS network services, and the broadcast address. These addresses are critical for proper subnet functionality and cannot be assigned to instances or other resources within the subnet.


