# NDK开发 (如何新建项目)

### 1.新建项目

![image-20251021111229065](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021111229065.png)

##### 选择Native C++ 

![image-20251021111402138](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021111402138.png)

##### Compatible SDK 选择调试设备适配的版本 

(本次开发使用的是本地模拟器 版本：HarmonyOS 5.0.1 API13  所以选择API13以下的都可以适配  这里选择API12 )![image-20251021111535700](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021111535700.png)



### 2.更改配置

![image-20251021111857335](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021111857335.png)

##### 点开build-profile.json5

![image-20251021111925998](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021111925998.png)

##### 在 "externalNativeOptions" 下新增 

`"abiFilters": ["arm64-v8a", "x86_64"],`

##### 这个步骤的作用在于可以让程序部署在本地模拟器上( 这个模拟器CPU是x86_64)



![image-20251021112434507](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021112434507.png)

##### 选择 文件->项目结构 

![image-20251021112512045](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021112512045.png)

##### 选择Siging Configs ， 点击 Autonatically 进行签名

![image-20251021112614621](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021112614621.png)

##### 点击OK

### 3.测试运行

![image-20251021112637546](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021112637546.png)

##### 点击 绿色开始键运行代码 

##### 前提： 已经打开本地模拟器 ， 本地模拟器如何创建 (TODO)

![image-20251021113008419](C:\Users\kejm\AppData\Roaming\Typora\typora-user-images\image-20251021113008419.png)

##### 点击，日志响应正确，测试完成，可以进行后续的生成代码调试