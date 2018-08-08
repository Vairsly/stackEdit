
# git完整配置流程

## 一.  安装 git ,上传公钥
1.下载安装git 
		[git 下载](https://git-scm.com/downloads)
2. 跳到.ssh目录下：
>如果为windows系统.用户目录（我这里是C:\Users\admin\.ssh目录），git 默认在.ssh目录调用私钥；
3. 生成公钥
```
>$ ssh-keygen -t rsa -****C username@qq.com**
Generating public/private rsa key pair.
Enter file in which to save the key (//.ssh/id_rsa): id_rsa_yourName
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in id_rsa.
Your public key has been saved in id_rsa.pub.
The key fingerprint is: 08:0f:a3:dd:5f:33:7a:aa:67:ff:e2:c4:1a:5e:21:ac username@qq.com
```
4. 上传公钥:
> a. 复制公钥: 
```
clip < ~/.ssh/id_rsa.pub
```
> b. 添加公钥
```
在 git 服务器，找到add key，把公钥复制添加;
```
5. 下拉代码
>跳转到项目目录（D:\P-phpStudy\WWW\wechat_project）
>git init;//

						


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTA0NDEyODddfQ==
-->