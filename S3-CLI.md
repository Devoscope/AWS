# AWS S3 CLI Commands

## 1. Configure AWS CLI
```sh
aws configure
```

## 2.List Buckets
```sh
aws s3 ls
```

## 3. Create a New Bucket

```sh
aws s3 mb s3://your-bucket-name

```

## 4.Delete a Bucket
```sh
aws s3 rb s3://your-bucket-name --force
```

## 5.List Bucket Contents
```sh
aws s3 ls s3://your-bucket-name
```

## 6.Upload a File to S3
```sh
aws s3 cp /path/to/file s3://your-bucket-name/
```

## 7.Download a File from S3
```sh
aws s3 cp s3://your-bucket-name/file /local/path/
```

## 8. Upload a Folder Recursively
```sh
aws s3 cp /local/folder s3://your-bucket-name/ --recursive
```

## 9. Download a Folder Recursively
```sh
aws s3 cp s3://your-bucket-name/folder /local/path/ --recursive
```

## 10. Sync a Local Folder with S3
```sh
aws s3 cp s3://your-bucket-name/folder /local/path/ --recursive
```

## 11. Sync a Local Folder with S3
```sh
aws s3 cp s3://your-bucket-name/folder /local/path/ --recursive
```

## 12. Sync S3 Bucket to Local Folder
```sh
aws s3 sync s3://your-bucket-name/ /local/folder
```

## 13. Delete a File from S3
```sh
aws s3 rm s3://your-bucket-name/file
```

## 14. Delete a Folder from S3
```sh
aws s3 rm s3://your-bucket-name/folder --recursive
```

## 15. Make an Object Public
```sh
aws s3 cp s3://your-bucket-name/file s3://your-bucket-name/file --acl public-read
```

## 16. Get Object URL
```sh
aws s3 presign s3://your-bucket-name/file
```
