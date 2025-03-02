# **AWS Auto Scaling Group (ASG) - Complete Guide**
## **1. Overview**
Amazon EC2 **Auto Scaling Group (ASG)** allows automatic scaling of EC2 instances to maintain availability and optimize costs.  
It ensures the right number of instances are running based on **demand**, **health status**, and **scaling policies**.

✅ **Increases or decreases EC2 instances dynamically**  
✅ **Maintains high availability**  
✅ **Optimizes cost by scaling in/out automatically**  
✅ **Works with Elastic Load Balancers (ALB, NLB)**  

---

## **2. Key Components of Auto Scaling Group**
### **1️⃣ Launch Template / Launch Configuration**
- Defines the **AMI, instance type, key pair, security groups, and user data**.  
- **Launch Templates (LT)** are recommended over **Launch Configurations (LC)**.  

### **2️⃣ Auto Scaling Group (ASG)**
- Manages a group of EC2 instances.  
- Ensures the desired number of instances are always running.  
- **Automatically replaces unhealthy instances**.  

### **3️⃣ Scaling Policies**
- Defines how instances scale **in** or **out** based on metrics like **CPU usage, request count, or custom CloudWatch metrics**.  
- **Types of Scaling:**
  - **Dynamic Scaling**: Based on metrics (CPU, memory, etc.).
  - **Predictive Scaling**: Uses machine learning to forecast demand.
  - **Scheduled Scaling**: Predefined increase or decrease at specific times.

### **4️⃣ Health Checks**
- Determines whether an instance is healthy.  
- **Types:**
  - **EC2 Health Check**: Checks if the instance is responsive.
  - **ELB Health Check**: Ensures the instance is serving traffic properly.

### **5️⃣ Load Balancer Integration**
- ASG can work with **Application Load Balancer (ALB) or Network Load Balancer (NLB)** to distribute traffic across instances.  

---

## **3. Auto Scaling Lifecycle**
1️⃣ **Scale Out (Increase instances)**
   - ASG launches new instances when demand increases.
   
2️⃣ **Load Balancer Registers Instances**
   - New instances are added to the ELB target group.

3️⃣ **Traffic Distribution**
   - ELB routes requests to healthy instances.

4️⃣ **Health Check Monitoring**
   - ASG continuously checks instance health.

5️⃣ **Scale In (Decrease instances)**
   - ASG terminates unused instances when demand decreases.

---

## **4. Types of Scaling in ASG**
### **1️⃣ Dynamic Scaling (Metric-Based)**
- Automatically scales based on CloudWatch alarms.
- Example: If **CPU > 70%**, add instances. If **CPU < 30%**, remove instances.

### **2️⃣ Scheduled Scaling**
- Scale based on predefined schedules.
- Example: Increase instances **at 9 AM** and decrease them **at 7 PM**.

### **3️⃣ Predictive Scaling**
- Uses AWS machine learning models to predict future demand.
- AWS automatically adjusts scaling before demand spikes.

---

## **5. Auto Scaling Policies**
### **1️⃣ Target Tracking Scaling**
- Automatically adjusts capacity based on a specific metric (e.g., CPU Utilization).
- Example:
  ```json
  {
    "PredefinedMetricSpecification": {
      "PredefinedMetricType": "ASGAverageCPUUtilization"
    },
    "TargetValue": 50.0
  }
  ```

### **2️⃣ Step Scaling
Adds or removes instances in steps based on metric thresholds.
Example:
If CPU > 70%, add 2 instances.
If CPU < 30%, remove 1 instance.
### **3️⃣ Simple Scaling
Adds or removes a fixed number of instances when an alarm is triggered.

## **6. Auto Scaling Group Health Checks**
Auto Scaling Group (ASG) continuously monitors the health of EC2 instances and replaces unhealthy ones to maintain application availability.

### **Types of Health Checks**
| **Health Check Type** | **Description** |
|----------------------|----------------|
| **EC2 Health Check** | AWS performs status checks on instances (instance reachability & system status). |
| **ELB Health Check** | The Elastic Load Balancer (ALB/NLB) checks instance health and removes unhealthy instances from traffic routing. |
| **Custom Health Check** | Uses custom CloudWatch metrics, scripts, or external monitoring tools to determine instance health. |

### **How Health Checks Work in ASG**
1️⃣ **ASG continuously monitors instance health based on defined health check type.**  
2️⃣ **If an instance is marked as unhealthy, ASG terminates and replaces it automatically.**  
3️⃣ **The new instance is launched based on the configured Launch Template/Configuration.**  
4️⃣ **If using ELB, the instance must pass ELB health checks before receiving traffic.**  

### **Configuring Health Checks in ASG**
- You can set **Health Check Type** to `EC2`, `ELB`, or `EC2 + ELB` while creating an ASG.
- To configure ASG health checks via AWS CLI:
  ```bash
  aws autoscaling update-auto-scaling-group \
    --auto-scaling-group-name MyASG \
    --health-check-type ELB \
    --health-check-grace-period 300
  ```
## **9. Pricing Model**
AWS Auto Scaling itself is **free**, but you pay for the resources used, such as **EC2 instances, Load Balancers, and CloudWatch monitoring**.

### **Cost Components**
| **Service** | **Pricing Details** |
|------------|---------------------|
| **EC2 Instances** | You pay for the running instances (On-Demand, Spot, Reserved). |
| **Load Balancer (ALB/NLB)** | Charged based on the number of requests and data processed. |
| **CloudWatch Alarms** | Free basic monitoring; custom metrics/logs incur additional costs. |
| **Data Transfer** | Standard AWS data transfer charges apply. |

### **Example Cost Calculation**
Assume:
- **3 t3.medium instances** running in **On-Demand mode**.
- **Application Load Balancer** handling **1 million requests per day**.
- **CloudWatch Custom Metrics** for scaling.

#### **Estimated Monthly Cost**
| **Component** | **Cost Estimation** |
|--------------|---------------------|
| **3 EC2 instances** (t3.medium, $0.0416/hr) | ~$90 per instance ($270 total) |
| **ALB request processing** | ~$20 per million requests |
| **CloudWatch (5 custom metrics, alarms)** | ~$10 |
| **Total Estimated Cost** | **~$300 per month** |

### **Ways to Optimize Costs**
✅ **Use Spot Instances** – Up to 90% cheaper than On-Demand.  
✅ **Use Reserved Instances** – 1 to 3-year commitment for discounts.  
✅ **Enable Scheduled Scaling** – Reduce instances during off-peak hours.  
✅ **Monitor CloudWatch Metrics** – Avoid unnecessary scaling and optimize instance usage.  

📌 **More details on pricing:** [AWS Auto Scaling Pricing](https://aws.amazon.com/autoscaling/pricing/)  

####  11. Auto Scaling CLI Commands
### 1️⃣ Create a Launch Template
```bash
aws ec2 create-launch-template \
  --launch-template-name MyTemplate \
  --version-description "v1" \
  --launch-template-data '{
    "ImageId": "ami-12345678",
    "InstanceType": "t2.micro",
    "SecurityGroupIds": ["sg-0123456789abcdef"],
    "KeyName": "my-key-pair"
  }'
```


