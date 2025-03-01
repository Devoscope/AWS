# Amazon EBS (Elastic Block Store)

Amazon Elastic Block Store (EBS) is a **high-performance, block storage service** designed for use with Amazon EC2 instances. It provides **low-latency, durable storage** that can be attached to EC2 instances for storing data such as databases, file systems, and applications.

## **Key Features**
- **Block Storage:** Works like a virtual hard drive that attaches to EC2 instances.
- **Persistent Storage:** Data is retained even after stopping an EC2 instance.
- **Scalability:** Volumes can be resized dynamically without downtime.
- **Snapshots:** Supports backups via Amazon S3 for data protection.
- **Encryption:** Offers built-in encryption for data security.
- **High Performance:** Optimized for low-latency, high-throughput workloads.

## **EBS Volume Types**
EBS offers different volume types, categorized into **SSD-backed** and **HDD-backed** storage:

### **1. SSD-Backed Volumes (Low Latency, High Performance)**
| Volume Type | IOPS (Max) | Throughput (Max) | Use Case |
|------------|------------|------------------|----------|
| **gp3** (General Purpose SSD) | 16,000 | 1,000 MB/s | Web apps, boot volumes |
| **gp2** (General Purpose SSD) | 16,000 | 250 MB/s | General workloads |
| **io2** (Provisioned IOPS SSD) | 256,000 | 4,000 MB/s | Databases, critical apps |
| **io1** (Provisioned IOPS SSD - Older) | 256,000 | 4,000 MB/s | High-performance workloads |

### **2. HDD-Backed Volumes (High Throughput, Cost-Effective)**
| Volume Type | IOPS (Max) | Throughput (Max) | Use Case |
|------------|------------|------------------|----------|
| **st1** (Throughput Optimized HDD) | 500 | 500 MB/s | Big data, log processing |
| **sc1** (Cold HDD) | 250 | 250 MB/s | Archive storage |

## **Use Cases**
- **Databases:** MySQL, PostgreSQL, MongoDB, SAP HANA.
- **Big Data & Analytics:** Apache Hadoop, Spark.
- **Backup & Disaster Recovery:** Snapshot-based backups to S3.
- **Web Hosting:** Persistent storage for applications.

## **EBS vs. S3**
| Feature | EBS | S3 |
|---------|-----|----|
| **Storage Type** | Block Storage | Object Storage |
| **Durability** | Stored in a single AZ (snapshots in S3) | 11 nines durability across multiple AZs |
| **Performance** | Low-latency, high-speed IOPS | High scalability but higher latency |
| **Use Case** | Databases, boot volumes, transactional workloads | Backup, media storage, static content |

## **Conclusion**
Amazon EBS is ideal for **persistent, high-performance storage** that requires low-latency access. It is a great choice for applications that run on EC2 and need reliable, fast storage.

