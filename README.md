# S3权限控制配置

参考文档：[https://docs.aws.amazon.com/zh_cn/AmazonS3/latest/userguide/walkthrough1.html](https://docs.aws.amazon.com/zh_cn/AmazonS3/latest/userguide/example-policies-s3.html)



## 配置允许 IAM 用户访问某个存储桶
### 创建存储桶对应的访问策略
* 进入IAM产品菜单，选择左侧“策略”，然后选择“创建策略”：
<img width="1541" alt="截屏2022-07-26 10 20 19" src="https://user-images.githubusercontent.com/107611866/180908576-fd82df9f-3b4a-49f3-b0ba-8152198102e8.png">

* 在编辑器界面中选中右侧json的选项
<img width="1251" alt="截屏2022-07-26 10 24 31" src="https://user-images.githubusercontent.com/107611866/180909136-37487c21-ff03-4b88-9455-00415b9bd49f.png">

* 将如下的策略贴到编辑器中

* 策略说明如下：
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

注：需将以上DOC-EXAMPLE-BUCKET1修改为目标存储桶。

* 点击下一步，可以给策略打tag标签，方便后续管理。比如DOC-EXAMPLE-BUCKET1的策略，对应的标签就是DOC-EXAMPLE-BUCKET1。




### 将策略授权给IAM用户
* 回到IAM主菜单
* 选择左侧“用户”，选中想要授权的用户，进入用户界面
* 选择添加权限
<img width="1595" alt="截屏2022-07-26 10 30 54" src="https://user-images.githubusercontent.com/107611866/180910177-23a988e5-c439-45e6-b1e0-e404c0c47f0b.png">

* 在策略列表中过滤刚刚创建的策略，即可将该策略授权给用户
<img width="1456" alt="截屏2022-07-26 10 31 59" src="https://user-images.githubusercontent.com/107611866/180910315-ffeea4c4-7fd3-4dc2-ba4a-44e9fb74598b.png">
