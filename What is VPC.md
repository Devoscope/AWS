# What is a VPC in AWS?

A **VPC** (Virtual Private Cloud) in **AWS** (Amazon Web Services) is a logically isolated network within the AWS cloud that allows you to launch AWS resources in a virtual network you define. It is similar to having your own data center, but hosted in AWS's secure and scalable cloud environment.

## Key Features of VPC in AWS:

### 1. Isolation and Control
A VPC provides complete control over your virtual network, including the selection of IP address range, creation of subnets, route tables, and network gateways. You can isolate resources in your VPC from other networks in the AWS cloud, making it a private environment.

### 2. Subnetting
Within a VPC, you can create subnets, which divide the VPC into smaller network segments. You can have public subnets (for resources that need to be accessible from the internet) and private subnets (for internal resources that should not be publicly accessible).

### 3. Security
VPC provides robust security features such as:
- **Security Groups**: Virtual firewalls that control inbound and outbound traffic to your EC2 instances.
- **Network ACLs (Access Control Lists)**: Additional layer of security that controls traffic at the subnet level.
- **VPC Peering**: Allows two VPCs to connect securely and share resources.
- **VPN Connections**: You can connect your on-premises network to your VPC via a VPN (Virtual Private Network) for secure communication.

### 4. Internet Gateway
An **Internet Gateway** (IGW) allows communication between instances in your VPC and the internet. Instances in a **public subnet** can use the IGW to access the internet, while instances in a **
