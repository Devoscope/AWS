# Amazon EBS Snapshots

## **What is an EBS Snapshot?**
An **EBS Snapshot** is a **point-in-time backup** of an Amazon EBS volume. Snapshots are stored in **Amazon S3** and can be used to restore data, create new volumes, or replicate volumes across regions.

## **Key Features of EBS Snapshots**
- **Incremental Backup:** Only changes since the last snapshot are stored, reducing storage costs.
- **Durable & Reliable:** Stored in Amazon S3 with **99.999999999% (11 nines) durability**.
- **Fast Recovery:** Snapshots can be restored into a new EBS volume in minutes.
- **Cross-Region & Cross-Account Copying:** Snapshots can be copied to different AWS regions or accounts.
- **Encryption:** Supports AWS KMS encryption for data security.

---

## **How EBS Snapshots Work**
1. **Initial Snapshot:** The first snapshot is a **full copy** of the EBS volume.
2. **Incremental Snapshots:** Subsequent snapshots only save **blocks that changed** since the last snapshot.
3. **Restoring from Snapshot:** A new EBS volume can be created from a snapshot.
4. **Copying Snapshots:** Snapshots can be copied to another region for disaster recovery.
5. **Deleting Snapshots:** When a snapshot is deleted, only the blocks not referenced by other snapshots are removed.

---

## **Use Cases**
- **Disaster Recovery:** Quickly restore lost data by creating a new volume from a snapshot.
- **Data Migration:** Move EBS volumes between AWS regions or accounts.
- **Version Control:** Keep multiple snapshots for different versions of data.
- **Compliance & Backup:** Maintain long-term backups for regulatory requirements.

---

## **EBS Snapshot Lifecycle**
1. **Create a Snapshot**  
   ```bash
   aws ec2 create-snapshot --volume-id vol-1234567890abcdef0 --description "My snapshot"

2. **List Snapshots**  
   ```bash
   aws ec2 describe-snapshots --owner-id 123456789012

3. ** Copy a Snapshot to Another Region**
   ```bash
   aws ec2 copy-snapshot --source-region us-east-1 --source-snapshot-id snap-12345678 --destination-region us-west-2

4. **Delete a Snapshot**
   ```bash
   aws ec2 delete-snapshot --snapshot-id snap-12345678


6.  ** Restore a Volume from Snapshot**
   ```bash
   aws ec2 create-volume --snapshot-id snap-12345678 --availability-zone us-east-1a
