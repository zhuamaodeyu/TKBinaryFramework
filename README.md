# Binrary Framework  
是一个组件二进制化的脚本工程 

#### 主要功能及特点  
1. 自动化
	* 自动化寻找工作目录下的所有可支持的xcode 项目
	* 同过将本脚本设置为定时任务，可以在空闲时间进行定时检测，以获取到最新的公开库版本     
	* 可以开启email功能，在一次操作完成后，以开启自动通知功能，通知管理者查看构建结果原因及日志文件  
2. 可配置
	* 通过config.json 文件，可以针对脚本进行丰富的配置(__详情请查看针对 config 文件介绍__)     
	* 通过设置，可以指定不同的工作目录，及日志存放目录。  
3. 可定制化  
	* 可以针对其中代码进行定制配置，可以使用私有的二进制存储库  
	* 可以进行项目过滤，针对部分没有按照 pod 创建的标准库，进行过滤，单独处理  






#### 依赖 
1. 此脚本依赖于阿里云 OSS ， 需要安装对应的 oss2 库 
	`pip install oss2` 或者 通过 `Pycharm` 来安装对应的库  
2. 可能会依赖于 carthage 
	`brew instlal carthage`  
3. 添加spec私有源  
	__注意：__ 此处推荐使用SSH 的形式，不推荐使用HTTP 形式，否则在推送 spec文件的时候，有可能让输入密码，导致推送失败   





## 使用方式      

#### 前置条件 
> 需要根据自身配置，修改配置文件  



### 二进制化  
> main.py 和 worker.py  

#### 独立运行 
1. 设置工作目录  
	修改 `main.py` 文件中  
	` main('/Users/zhuamaodeyu/Documents/LibFramework','./config.json', '/Users/zhuamaodeyu/Documents/LibFramework/log')`  为指定目录  
	* 参数1： 工作空间路径  
	* 参数2： 配置文件路径  
	* 参数3： 日志文件保存路径  

#### 定时任务 
> 具体Mac下如何创建爱你定时任务，请自行 Google  


#### debug 模式  
通过 `PyCharm` 可以执行导入项目运行  



### 私有组件提交 
> upload.py  

##### 配置 
1. 配置二进制库存放相关  
	* `key`  
	* `secret`  
	* `bucketname` 
	* `download_host`  
2. 配置 spec  
	* 源码: `source_pod_spec`  
	* 二进制: `binary_pod_spec`  


#### 私有库中 
此种方式，需要在每个私有库中都存储一份相同的 `upload.py` 脚本。 每次提交时，执行此脚本  



#### 全局 
通过配置。支持全局操作  



## Demo 工程    
> 此工程会用到私人的OSS 秘钥，会不定期重置，请使用自己的   

1. `clone git@github.com:zhuamaodeyu/TKBinaryFrameworkDemo.git`    
2. 接下同目录下的  `LibFramework.zip` 压缩包  
2. 方式1： `Pycharm`导出  
	* 设置`python` 环境()  
		![](https://github.com/zhuamaodeyu/TKBinaryFramework/blob/master/Xnip2020-05-27_09-34-40.jpg)   
	* 运行  
		![](https://github.com/zhuamaodeyu/TKBinaryFramework/blob/master/Xnip2020-05-27_09-36-15.jpg)  
		__注意： 此处需要根据自己本地环境，修改执行脚本路径__   

3. 方式2：  
	使用命令行方式运行  
	* 进入项目目录(`TKBinaryFramework`目录下)  
	* 执行`./venv/bin/python ./main.py` 运行

4. 验证framework是否上传成功  
	默认情况下，会打印出framework的上传地址，可以根据地址下载到具体的包  
 


## Config 详解  
* `mode`  
	模式指定， 此处有默认模式`debug`， 指定 `debug`模式后，在执行过程中，会将日志输出在控制台。 推荐设置为`release`  

* `upload`  
	此处是针对阿里云OSS 的设置。其中指定了一下内容 __注意:__ 如果针对脚本进行了自定义化，此处需要根据定制进行配置    
	* `key`   
		OOS key  
	* `secret`:     
		秘钥  
	* `url`:  
		上传URL地址    
	* `bucketname`:     
		存储空间名称
	* `download_host`:       
		生成的podspec 文件中，下载地址的前缀

* `swift_version`  
	指定当前脚本编译依赖的swift 版本  __由于swift中，编译的二进制framework，会依赖swift的版本，不同的版本之间可能存在不兼容，此处需要指定版本__   

* `sdk`  
	指定二进制编译目标平台  默认是`iphoneos`  

* `mach_o_type`  
	指定编译成的framework的类型，是静态库还是动态库  

* `git`  
	针对 Git 的设置  

* `email`  
	针对 email的设置  

* `pod`    
	此处分为两部分，一部分是 debug模式的， 一部分是 release 的 (__注意： 此次部分需要与前面添加的spec源部分相同，否则可能导致失败__)

* `mapping`  
	此处是针对部分没有按照`pod lib create XXX` 命令生成的标准库的映射。 需要通过此处映射，针对此种库进行单独处理。否则可能存在编译不通过问题   
	
	





## 后续计划及说明
1.  实现二进制与源码的映射  
2. 优化编译过程， 是编译更加轻量级。 不需要针对特殊项目进行映射   

 

### 说明
1. 本脚本可能还存在部分不兼容问题， 如果在使用过程中，遇到了任何问题，请通过 github或者 下方 gmail 方式联系我    
2. 当前脚本暂不支持OSX 系统  



## 联系方式 

* Gmail: playtomandjerry@gmail.com  
