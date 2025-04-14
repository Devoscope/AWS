# 🧰 Mount S3 Bucket on EC2 (Ubuntu) Using `s3fs` with IAM Role

This guide helps you mount an Amazon S3 bucket to your EC2 instance using `s3fs` **without using access keys**, relying entirely on the **IAM role** attached to your EC2 instance.

---

## ✅ Step 1: Install `s3fs`

```bash
sudo apt update
sudo apt install -y s3fs
```

## ✅ Step 2: Create a Mount Point

```bash
sudo mkdir /mnt/mybucket
```

Replace mybucket with any directory name you want to use as the mount point.

## ✅ Step 3: Mount the S3 Bucket
```bash
s3fs your-bucket-name /mnt/mybucket -o iam_role=auto -o use_path_request_style -o url=https://s3.amazonaws.com
```
# # Explanation:
your-bucket-name: Replace with your actual bucket name.

iam_role=auto: Tells s3fs to use the IAM role assigned to the EC2 instance.

use_path_request_style: Required in some regions or for certain buckets.

url=https://s3.amazonaws.com: Optional; use it if you’re in the standard AWS region.

## ✅ Step 4: Verify
```bash
ls /mnt/mybucket
```

## 🔁 (Optional) Auto-Mount on Reboot

Edit your /etc/fstab file:

```bash
sudo nano /etc/fstab
```

Add the following line:
```bash
s3fs#your-bucket-name /mnt/mybucket fuse _netdev,iam_role=auto,use_path_request_style,url=https://s3.amazonaws.com 0 0
```

```bash
sudo mount -a
```

