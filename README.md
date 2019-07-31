# AWS-lightsail-Part2-Update
最后一次更新于 `2019/07/03`
针对油管博主 BIGDONGDONG 的第 96 期视频 part 2 命令的一次更新, 原链接: https://github.com/bigdongdongCLUB/GoodGoodStudyDayDayUp/issues/2
#### 由于原命令部分已经失效，为了方便后人操作，会将所有步骤再列一次：
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
查看是否安装成功
```
aws --version
```
##### 第三步：手动配置 AWS CLI 的文件
感谢网友的提醒，之前这部分在 `./aws/` 下操作的文件似乎过一阵子就会消失掉，可能跟重启清空有关系。<br>
不过没关系，官网更新了更方便的操作，感兴趣的朋友可访问: https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/cli-chap-configure.html<br>
简单来说，现在配置 `credentials` 和 `config` 可以通过输入以下命令一步到位:
```
aws configure
```
只有确定了服务器安装了 AWS CLI 这步命令就一定会成功。运行结果如下所示:
```
$ aws configure
AWS Access Key ID [None]: 你的 Access Key ID
AWS Secret Access Key [None]: 你的 Secret Access Key
Default region name [None]: 你的服务器所在区域(比如 us-west-2)
Default output format [None]: json
```
注意：每输入一行按一次 `Enter` 键，并不是运行命令以后一下子显示 4 行的。

##### 第四步：写重启文件
输入
```
nano renewip.sh
```
以下命令和东东给的方法一致，比如我想重启的服务器的名字是Oregon，那么就填写成以下形式后保存
```
aws lightsail stop-instance --instance-name Oregon
sleep 30
aws lightsail start-instance --instance-name Oregon
```
##### 第五步：编辑重写配置
输入
```
crontab -e
```
将以下命令复制到最后一行。注意，命令前面不要加#
```
0 3 * * * bash /root/renewip.sh
```
最后调整一下时区
```
timedatectl set-timezone Asia/Hong_Kong
```
