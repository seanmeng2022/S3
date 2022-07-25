# S3权限控制配置

参考文档：[https://docs.aws.amazon.com/zh_cn/AmazonS3/latest/userguide/walkthrough1.html](https://docs.aws.amazon.com/zh_cn/AmazonS3/latest/userguide/example-policies-s3.html)

## 配置允许 IAM 用户访问某个存储桶
在本示例中，您需要授予您的 AWS 账户中的一个 IAM 用户访问其中一个存储桶 DOC-EXAMPLE-BUCKET1 的权限，以便该用户能够添加、更新和删除对象。
除了授予该用户 s3:PutObject、s3:GetObject 和 s3:DeleteObject 权限外，此策略还授予 s3:ListAllMyBuckets、s3:GetBucketLocation 和 s3:ListBucket 权限。这些是控制台所需的其他权限。此外，s3:PutObjectAcl 和 s3:GetObjectAcl 操作需要能够在控制台中复制、剪切和粘贴对象。
```
{
   "Version":"2012-10-17",
   "Statement":[
      {
         "Effect":"Allow",
         "Action": "s3:ListAllMyBuckets",
         "Resource":"*"
      },
      {
         "Effect":"Allow",
         "Action":["s3:ListBucket","s3:GetBucketLocation"],
         "Resource":"arn:aws:s3:::DOC-EXAMPLE-BUCKET1"
      },
      {
         "Effect":"Allow",
         "Action":[
            "s3:PutObject",
            "s3:PutObjectAcl",
            "s3:GetObject",
            "s3:GetObjectAcl",
            "s3:DeleteObject"
         ],
         "Resource":"arn:aws:s3:::DOC-EXAMPLE-BUCKET1/*"
      }
   ]
}
```

