# DEVECO 在linux 环境下编译（未完善，已找到）



### 预置条件



#### 配置JDK

##### 1.下载JDK，支持JDK 17版本。

````
sudo apt-get install openjdk-17-jdk
````

验证安装是否成功

````
java -version
````

输出示例：

````
openjdk version "17.0.16" 2025-07-15
OpenJDK Runtime Environment (build 17.0.16+8-Ubuntu-0ubuntu122.04.1)
OpenJDK 64-Bit Server VM (build 17.0.16+8-Ubuntu-0ubuntu122.04.1, mixed mode, sharing)
````

##### 2.配置JDK环境变量。

编辑环境变量文件：

````
sudo nano /etc/environment
````

在文件末尾添加以下内容：

````
JAVA_HOME="/usr/lib/jvm/java-17-openjdk-amd64"
PATH=$PATH:$JAVA_HOME/bin
````

保存并退出后，运行以下命令使更改生效：

````
source /etc/environment
````

验证环境变量配置：

````
echo $JAVA_HOME
echo $PATH
````



### 获取命令行工具

##### 1.命令行工具获取。

前往 [下载中心]([下载中心 | 华为开发者联盟-HarmonyOS开发者官网，共建鸿蒙生态](https://developer.huawei.com/consumer/cn/download/command-line-tools-for-hmos)) 下载linux的Command Line Tools![image-20251022102628758](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251022102628758.png)



##### 2.将下载后的命令行工具解压到本地。

````
unzip commandline-tools-linux-x64-XXXX.XXX.zip
````

解压后如下：

![image-20251022103544359](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251022103544359.png)



### 配置环境变量

打开.bashrc 文件

````
vim ~/.bashrc
````

在文件末尾添加以下行：

````
export PATH=$HOME/download/command-line-tools/bin:$PATH

export NODE_HOME=$HOME/download/command-line-tools/tool/node
export PATH=$PATH:$NODE_HOME

export HDC_HOME=$HOME/download/command-line-tools/sdk/default/openharmony/toolchains
export PATH="$PATH:$HDC_HOME"


````

保存并重新加载配置

````
source ~/.bashrc
````

验证是否成功:

````
kejm@kejm-ubuntu22:~/download$ ohpm --version

5.3.2

kejm@kejm-ubuntu22:~/download$ node -v

v18.20.1

kejm@kejm-ubuntu22:~/download$ npm -v

10.5.0

kejm@kejm-ubuntu22:~/download$ which node

/home/kejm/download/command-line-tools/tool/node/bin/node

kejm@kejm-ubuntu22:~/download$ hdc -v

Ver: 3.2.0b

kejm@kejm-ubuntu22:~/download$ hvigorw -v

6.0.6
````

### 安装libGL1库

在linux系统的构建场景下，使用[纹理压缩](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile-app#section2095319147103)功能需要安装libGL1库。

执行以下命令安装libGL1库：

````
sudo apt install -y libgl1-mesa-dev
````



