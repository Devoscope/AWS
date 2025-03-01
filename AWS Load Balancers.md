# **AWS Load Balancers: ALB vs. NLB**

Amazon Web Services (AWS) provides **Elastic Load Balancing (ELB)** to distribute incoming traffic across multiple targets to ensure **high availability and fault tolerance**. The two most commonly used load balancers are:

- **Application Load Balancer (ALB)** – Operates at **Layer 7 (Application Layer)**
- **Network Load Balancer (NLB)** – Operates at **Layer 4 (Transport Layer)**

---

## **1. Application Load Balancer (ALB)**
### **Overview**
The **Application Load Balancer (ALB)** operates at **Layer 7 (HTTP/HTTPS)** and is designed for **routing web traffic** intelligently based on URL paths, hostnames, request headers, and query parameters.

### **Key Features**
✅ **Layer 7 Routing** – Routes requests based on the request URL, headers, and hostnames.  
✅ **Path-Based Routing** – Directs traffic based on the URL path (e.g., `/api/*` → API servers).  
✅ **Host-Based Routing** – Routes requests based on the domain name (e.g., `api.example.com`).  
✅ **WebSocket Support** – Supports real-time communication protocols.  
✅ **SSL Termination** – Offloads SSL/TLS encryption to the ALB.  
✅ **Sticky Sessions** – Supports session persistence using cookies.  
✅ **AWS WAF Integration** – Works with **AWS Web Application Firewall (WAF)** for security.  
✅ **Supports HTTP/2 & gRPC** – Allows for faster and more efficient web applications.  

### **Use Cases**
- Web applications using **HTTP/HTTPS**
- Microservices and containerized applications (**ECS, EKS, Fargate**)
- API Gateway alternative
- Routing traffic to multiple domains or paths

### **Example ALB Listener Rule**
```json
{
  "Conditions": [
    {
      "Field": "path-pattern",
      "Values": ["/api/*"]
    }
  ],
  "Actions": [
    {
      "Type": "forward",
      "TargetGroupArn": "arn:aws:elasticloadbalancing:region:account-id:targetgroup/my-target-group"
    }
  ]
}
```

# **Network Load Balancer (NLB) - AWS**
## **Overview**
The **Network Load Balancer (NLB)** is an AWS **Elastic Load Balancer (ELB)** that operates at **Layer 4 (Transport Layer)** of the **OSI model**. It is designed to handle **millions of requests per second** while maintaining **ultra-low latency**.

✅ **Best for high-performance applications**  
✅ **Supports TCP, UDP, and TLS protocols**  
✅ **Provides static IP addresses**  
✅ **Preserves the client IP**  

---

## **1. Key Features of NLB**
### **1️⃣ Layer 4 Load Balancing**
- Routes traffic at the **Transport Layer** based on **IP address and Port (TCP, UDP, TLS)**.  
- Does not inspect application-level traffic like HTTP headers.  

### **2️⃣ High Performance & Low Latency**
- Can handle **millions of requests per second**.  
- Suitable for real-time applications and workloads requiring **minimal latency**.  

### **3️⃣ Static IP Address**
- Unlike ALB, **each NLB has a static IP per Availability Zone (AZ)**.  
- You can associate an **Elastic IP (EIP)** with NLB.  

### **4️⃣ Preserves Client IP**
- Unlike ALB, NLB forwards the **original client IP** to the backend instances.  
- Useful for applications requiring client IP visibility for logging and security.  

### **5️⃣ TLS Passthrough**
- Does not terminate SSL/TLS but instead passes encrypted traffic directly to the backend servers.  

### **6️⃣ Cross-Zone Load Balancing**
- Disabled by default (but can be enabled).  
- When disabled, traffic is routed only within the same **Availability Zone (AZ)**.  

### **7️⃣ AWS PrivateLink Support**
- Allows exposing services to **other VPCs and AWS accounts** securely.  
- Useful for internal services without internet exposure.  

---

## **2. Use Cases of NLB**
✅ **High-performance applications** requiring **low-latency** (e.g., financial trading apps).  
✅ **Gaming, VoIP, and real-time applications** (UDP support).  
✅ **Load balancing non-HTTP traffic** such as **databases (MySQL, PostgreSQL), MQTT brokers, and messaging services**.  
✅ **Hybrid cloud scenarios** using AWS **VPN, Direct Connect, or VPC Peering**.  
✅ **Microservices with PrivateLink** for secure inter-service communication.  

---

## **3. How NLB Works**
1️⃣ **Client sends a request to NLB.**  
2️⃣ **NLB selects a healthy backend target** in the target group based on the selected routing algorithm.  
3️⃣ **NLB forwards the request** to the target **without modifying the client IP**.  
4️⃣ **The target processes the request** and **sends a response back** to the client.  

---

## **4. Target Groups Supported by NLB**
A **target group** defines where incoming traffic is directed.  
NLB supports **three types of target groups**:

| Target Type | Description |
|-------------|-------------|
| **Instance** | Routes traffic to EC2 instances using instance IDs. |
| **IP Address** | Routes traffic to IPs in AWS or on-premise networks. |
| **AWS PrivateLink** | Integrates with AWS PrivateLink for VPC-to-VPC communication. |

---

## **5. NLB Health Checks**
### **What are Health Checks?**
- Health checks determine if a target (backend instance) is **healthy** before routing traffic to it.  
- If a target is **unhealthy**, NLB stops sending traffic to it.  

### **NLB Health Check Parameters**
| Parameter | Description |
|-----------|-------------|
| **Protocol** | TCP |
| **Port** | Custom port |
| **Threshold** | Number of failed checks before marking a target as unhealthy |
| **Interval** | Time between health check attempts |

Example CLI command to set up a health check:
```bash
aws elbv2 modify-target-group-attributes \
  --target-group-arn arn:aws:elasticloadbalancing:region:account-id:targetgroup/my-target-group \
  --attributes Key=healthcheck.interval.seconds,Value=30
```
![image](https://github.com/user-attachments/assets/44ad9584-d0cc-453f-aa4a-876daa6afef8)

## 8. How to Create an NLB in AWS Console
1️⃣ Go to AWS Console → EC2 → Load Balancers → Create Load Balancer.
2️⃣ Select "Network Load Balancer".
3️⃣ Choose Internal or Internet-facing.
4️⃣ Select VPC and Availability Zones.
5️⃣ Configure Listeners (TCP/UDP).
6️⃣ Create a Target Group and Register Targets.
7️⃣ Review and Create the Load Balancer.

##9. Pricing Model
AWS NLB pricing is based on:
💰 LCU (Load Balancer Capacity Unit) – Measures usage based on new connections, active connections, and data processed.
💰 Data Processed (GBs) – The amount of inbound and outbound traffic.

##10. Conclusion
✅ Network Load Balancer (NLB) is best for high-performance, low-latency applications.
✅ Supports TCP, UDP, and TLS traffic, making it ideal for gaming, VoIP, financial apps, and real-time streaming.
✅ Provides static IPs and preserves client IP addresses, making it easy for security and firewall configurations.
✅ Works seamlessly with AWS PrivateLink for VPC-to-VPC connectivity.

🚀 Use NLB when you need ultra-fast performance with minimal latency! 🚀
