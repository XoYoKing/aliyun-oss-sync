# aliyun-oss-sync

阿里云OSS增量上传脚本

此脚本是用来发布我个人博客[Poison](https://tianshuang.me/)而编写的，因为工作中常用语言为Java，而Python仅是副业，代码如有不当之处，敬请指出。

逻辑很简单，递归遍历本地目录，然后判断每个文件在OSS里是否存在，如果不存在则直接上传，如果存在则检查Content-Md5是否相等，如果不相等则表明该文件内容已经发生变化，则上传该文件，OSS会自动覆盖同名文件。

值得注意的是检查Content-Md5的值是用的HTTP的HEAD方法，因为我们只需要header中的Content-Md5字段的值，所以并不需要使用GET方法拿到响应体，这样既加快了速度也节省了OSS流量。

关于oss_public_domain变量的值，你如果在同地域内网的ECS上使用该脚本，建议使用内网域名，速度快并且节省了流量费用，否则使用外网域名。
