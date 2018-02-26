注：appium安装到C盘，node.js安装到C盘

一、安装node.js
1、到官网下载node.js：https://nodejs.org/en/download/

2、获取到安装文件后，直接双击安装文件，根据程序的提示，完成nodejs的安装。

3、安装完成后，运行cmd，输入node –v，如果安装成功，会输出如下版本信息：



二、配置Android sdk环境

1、sdk环境配置：http://www.cnblogs.com/puresoul/p/4597211.html

2、确保安装了 Level 17 或以上的版本 api

3、设置 ANDROID_HOME 系统变量为你的 Android SDK 路径

     F:\Program Files (x86)\Android\android-sdk

4、把 tools 和 platform-tools 两个目录加入到系统的 Path 路径里

    ;F:\Program Files (x86)\Android\android-sdk\platform-tools;F:\Program Files (x86)\Android\android-sdk\tools



三、安装手机驱动并测试连接真机

完成上述步骤以后，为了能够让手机连接到PC端进行真机测试。还需要安装测试手机对应的驱动程序。根据手机型号提前下载相应的离线驱动并安装，之后将手机与PC通过usb线相连。在cmd中输入以下命令，如果能够看到设备，则表示安装成功。




四、安装Appium 

1.下载安装文件：https://bitbucket.org/appium/appium.app/downloads/

2.直接双击appium-installer.exe文件安装就好，桌面会生成一个appium的图标

3.把node_modules的bin目录放到系统的Path路径里

          C:\Program Files (x86)\Appium\node_modules\.bin

4.检查appium所需的环境是否OK：

进入cmd命令行，输入appium-doctor ，出现以下提示，All Checks were successful ,说明环境成功。


 

二、Appium入门实例（Java）

一、使用Eclipse直接创建案例工程

1、打开Eclipse，【File】-->【New】-->【Project】

2、选择【Java Project】-->【Next】

3、输入工程名称Appium_demo，点击【Finish】

4、右键点击工程 New-Folder，新建两个文件夹：apps和libs，目录结构如下：



 

二、导入测试的类库

1、导入Selenum类库：http://docs.seleniumhq.org/download/

　　　　1) selenium-server-standalone-2.44.0.jar

　　　　2) selenium-java-2.44.0.zip

2、导入Appium类库：

　　　　1) java-client-1.2.1.jar 

3、右键点击工程空白处，选择【Build Path】-->【Configure Build Path】 

三、下载测试APK 

　　1、下载测试的文件ContactManager.apk：https://github.com/appium/sample-code/tree/master/sample-code/apps/ContactManager

　　2、将下载的apk放到项目的apps目录下 

四、建立package包和案例文件

　　1、在src文件夹上右键单击，【New】-->【package】,输入包名:com.dan.demo，点击【Finish】

　　2、在package下新建类：ContactsTest.java，如下：　　

　　下载地址：https://github.com/appium/samplecode/tree/master/samplecode/examples/java/junit/src/test/java/com/saucelabs/appium