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

