# Amazon EBS Volume Types

Amazon EBS offers different volume types optimized for performance and cost, divided into **SSD-backed** and **HDD-backed** categories.  

## **1. SSD-Backed Volumes (Performance-Oriented, Low Latency)**  
These are optimized for **low latency and high input/output operations per second (IOPS)**, making them ideal for databases and critical workloads.

### **a) General Purpose SSD (gp3, gp2)**
- **gp3 (Recommended)**
  - **IOPS:** Up to 16,000  
  - **Throughput:** Up to 1,000 MB/s  
  - **Performance:** Baseline 3,000 IOPS, independent of volume size  
  - **Best for:** Boot volumes, general workloads, development/testing, low-latency applications  
  - **Key Feature:** Cheaper than `gp2` with higher flexibility (you can provision IOPS and throughput separately)  

- **gp2 (Older Generation)**
  - **IOPS:** Baseline 3 IOPS per GB (scales up to 16,000)  
  - **Throughput:** Up to 250 MB/s  
  - **Best for:** General workloads, small databases  
  - **Key Feature:** Performance depends on volume size (larger volumes = more IOPS)  

### **b) Provisioned IOPS SSD (io2, io1)**
- **io2 (Recommended)**
  - **IOPS:** Up to 256,000  
  - **Throughput:** Up to 4,000 MB/s  
  - **Best for:** High-performance databases (e.g., Oracle, SQL Server, SAP HANA), latency-sensitive applications  
  - **Key Feature:** **99.999% durability** (more reliable than io1), independent IOPS scaling  

- **io1 (Older Generation)**
  - **IOPS:** Up to 256,000  
  - **Throughput:** Up to 4,000 MB/s  
  - **Best for:** Critical workloads needing high IOPS  
  - **Key Feature:** Similar to `io2` but with lower durability  

---

## **2. HDD-Backed Volumes (Throughput-Oriented, Cost-Effective)**  
Designed for workloads requiring **high sequential throughput** rather than low-latency access.

### **a) Throughput Optimized HDD (st1)**
- **IOPS:** Baseline 40-500 IOPS  
- **Throughput:** Up to 500 MB/s  
- **Best for:** Big data, data warehouses, log processing  
- **Key Feature:** Performance scales with volume size, but better for sequential reads/writes  

### **b) Cold HDD (sc1)**
- **IOPS:** Baseline 40-250 IOPS  
- **Throughput:** Up to 250 MB/s  
- **Best for:** Archive storage, infrequent access data  
- **Key Feature:** Cheapest EBS volume, ideal for cost-saving bulk storage  

---

## **Comparison Table**
| Volume Type | Use Case | IOPS (Max) | Throughput (Max) | Durability | Best for |
|------------|---------|------------|------------------|------------|----------|
| **gp3** (General SSD) | General workloads | 16,000 | 1,000 MB/s | 99.8% | Boot volumes, dev/test, web apps |
| **gp2** (Older SSD) | General workloads | 16,000 | 250 MB/s | 99.8% | Same as gp3 but less flexible |
| **io2** (High-Perf SSD) | High-performance DBs | 256,000 | 4,000 MB/s | **99.999%** | Databases, critical apps |
| **io1** (Older High-Perf SSD) | High-performance DBs | 256,000 | 4,000 MB/s | 99.8% | Similar to io2 but less durable |
| **st1** (HDD) | Streaming workloads | 500 | 500 MB/s | 99.8% | Big data, log processing |
| **sc1** (Cold HDD) | Archive storage | 250 | 250 MB/s | 99.8% | Long-term, low-cost storage |

