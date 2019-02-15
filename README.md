# AWS-lightsail-Part2-Update
针对油管博主 BIGDONGDONG 的第 96 期视频 part 2 代码的一次更新, 原代码网址: https://github.com/bigdongdongCLUB/GoodGoodStudyDayDayUp/issues/2
#### 由于原代码部分已经失效，为了方便后人操作，会将所有步骤再列一次：
##### 第一步：获取 AWS AccessKeyId 和 AWS SecretKey
这一步只需要先点击 https://lightsail.aws.amazon.com/ls/webapp/account/advanced ，然后点击**转到IAM控制台**，选择**访问密钥(访问密钥ID和秘密访问密钥)**, 最后点击**创建新的访问密钥**并保存.csv格式的文件。
##### 第二步：安装AWS CLI
以ubuntu系统为例：
先检查是否安装了 Pip 和 Python
```
pip --version
python --version
```
没有的话需要安装，使用东东的执行语句安装
```
apt update -y
apt install python-pip -y
```
或者也可以使用 AWS 的用户指南进行安装，点击网址：https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/install-linux.html#install-linux-path <br>
再使用 Pip 安装 AWS CLI
```
pip install awscli --upgrade --user
```
##### 第三步：手动配置 AWS CLI 的文件
东东给的脚本已经失效了。访问原blog的文章，原来是博主自己更改了方法，自己感觉没有很好用，所以决定不用脚本，手动更改，很简单！
1. 配置credentials<br>
运行`vim ~/.aws/credentials`或者`nano ~/.aws/credentials`<br>
vim 保存的方式是 :wq!, nano保存的方式是 ctrl + x 再按Y<br>
将第一步获取的 AWS AccessKeyId 和 AWS SecretKey 复制进去即可。<br>
2. 配置config<br>运行`vim ~/.aws/config`或者`nano ~/.aws/config`<br>
根据虚拟机所在区域填写即可。注意，不需要管a,b,c区。比如你的虚拟机所在位置是`us-west-2a`，那就填写`us-west-2`。
##### 第四步：写重启文件
输入`nano renewip.sh`
以下代码和东东给的方法一致，比如我想重启的服务器的名字是Oregon，那么就填写成以下形式后保存
```
aws lightsail stop-instance --instance-name Oregon
sleep 30
aws lightsail start-instance --instance-name Oregon
```
##### 第五步：编辑重写配置
输入`crontab -e`
将以下代码复制到最后一行。注意，代码前面不要加#
```
0 3 * * * bash /root/renewip.sh
```
最后调整一下时区
```
timedatectl set-timezone Asia/Hong_Kong
```
大功告成！
