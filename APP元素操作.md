锁定屏幕
driver.lockScreen(3);//锁定屏幕3秒，参数为秒

把当前应用放到后台去
driver.runAppInBackground(5);//应用放到后台5秒

注意：以上2个用于特殊功能需求

收起键盘
driver.hideKeyboard();//收起软键盘，每次sendkey的操作之后，都要带上，避免某些应用某些手机不会自动收起键盘，挡住后续要操作的控件

检查应用是否已经安装
driver.isAppInstalled("com.example.android.apis")//用于检查关联应用，比如需要在应用分享微信，那么需要先检查微信是否安装

安装应用到设备中去
driver.installApp("path/to/my.apk")//本地安装包的路径
从设备中删除一个应用
driver.removeApp("com.example.android.apis")//按照包名来删除

模拟设备摇晃
driver.shake()//摇一摇

关闭应用
driver.closeApp()//完全关闭

启动 (LAUNCH)，根据服务关键字 (desired capabilities) 启动会话 (session) ，关闭应用之后使用
driver.launchApp()

应用重置
driver.resetApp()//相当于卸载重装，清理掉所有的内容

Context,用于webview等混合应用的测试
driver.getContextHandles()//列出所有上下文
driver.getContext()//列出当前上下文
driver.context();//将上下文切换到默认上下文
driver.context("WEBVIEW")//切换到“WEBVIEW”

获取应用的字符串
driver.getAppStrings();//应用的资源里面的strin

滑动(SWIPE)
driver.swipe(75, 500, 75, 0, 1000)

捏屏幕 (双指往内移动来缩小屏幕)
driver.pinch(element);//需要控件能够缩放

放大屏幕 (双指往外移动来放大屏幕)
driver.zoom(element)

从手机中拉出文件
driver.pullFile("Library/AddressBook/AddressBook.sqlitedb");//手机中的文件位置
推送文件到设备中去
byte[] data = Base64.encodeBase64("some data for the file".getBytes());
String path = "/data/local/tmp/file.txt";
driver.pushFile(path, data)//path同pull data是要推送的内容

以下只支持android
driver对象类型必须为 AndroidDriver<AndroidElement> 不可以是AppiumDriver或IOSDriver
启动 ACTIVITY，在当前应用中打开一个 activity 或者启动一个新应用并打开一个 activity
driver.startActivity("appPackage","com.example.android.apis", null, null);//大部分用于调用其他应用时使用，调用时要考虑被调用的activity是否需要各种参数，否则容易出现错误
当前 ACTIVITY
driver.currentActivity();

打开下拉通知栏
driver.openNotifications();
给设备发送一个按键事件
driver.pressKeyCode(AndroidKeyCode.HOME);----按Home键
driver.pressKeyCode(AndroidKeyCode.BACK);----按返回键
也可以直接用键值，常用的如下
1 -->  "KEYCODE_MENU" 
2 -->  "KEYCODE_SOFT_RIGHT" 
3 -->  "KEYCODE_HOME" 
4 -->  "KEYCODE_BACK" 
5 -->  "KEYCODE_CALL" 
6 -->  "KEYCODE_ENDCALL" 
19 -->  "KEYCODE_DPAD_UP" 
20 -->  "KEYCODE_DPAD_DOWN" 
21 -->  "KEYCODE_DPAD_LEFT" 
22 -->  "KEYCODE_DPAD_RIGHT" 
23 -->  "KEYCODE_DPAD_CENTER" 
24 -->  "KEYCODE_VOLUME_UP" 
25 -->  "KEYCODE_VOLUME_DOWN" 
26 -->  "KEYCODE_POWER" 
27 -->  "KEYCODE_CAMERA" 





课程中手势方面讲了比较少，手势也是自动化测试中比较麻烦的事情，从投入产出来看，手势在自动化中也是要尽量避免，不过这里我还是要详细讲一些Appium手势的用法

Appium中有一个TouchAction类 所有的手势都是基于此，包含一些封装好的手势 比如swipe等
下面上代码：
TouchAction action = new TouchAction(driver);//初始化
action.press(el1).moveTo(el2).release();//按el1元素，移动到el2，然后释放，定义手势的内容
action.perform();//执行手势，没有则不执行

TouchAction中的所有方法在这里：http://appium.github.io/java-client/io/appium/java_client/TouchAction.html 同学们可以自己看

所有的手势变化，都在上面代码的第二行中，按照想要的操作改变方法即可，所有的action方法都是连着写下去，可以写很长。。。虽然不推荐

常用的复杂手势其实就2种：
swipe操作 其实就等于press（起始坐标）.waitaction（间隔）.moveto（目标坐标）.release
手势解锁  press（起始）.moveto.moveto.moveto.release

至于其他的就比较简单了
tap 点击 不需要release
press 短按 需要release 拿来后面接moveto
longpress 长按 默认1秒释放，可以修改时长，相对于tap就多了时间间隔，也可以接moveto

每个手势的方法，都有坐标，元素以及元素加坐标3类参数，如果是元素，那么会取元素的中心点坐标，如果是元素加坐标会去左上角加坐标，比如：
press（100,100） 就是按100,100点
press（el）  就是按el元素的中心点
press（el,100,100）  如果el左上角坐标是x，y，那么就是按x+100，y+100

接下来是我的使用经验，希望同学们少走点弯路，特别是5和6
尽量使用元素，避免坐标，除了坐标本身的缺点之外，TouchAction对于坐标支持不是很好，有些bug。。。
连续使用多个moveto坐标形式，x和y是相对坐标，只用一个，则是绝对坐标。。。。
各个手势之间根据需要加入waitaction，避免出错
手势要能够生效，如果页面拖不动，很容易出问题
Appium日志中能够看到每个action具体的类型和xy坐标，可以对照排查
android手机的开发者选项中有个指针位置，可以在屏幕上画出触摸轨迹，方便调试

至于多指操作使用MultiTouchAction 具体的见 http://appium.github.io/java-client/io/appium/java_client/MultiTouchAction.html 
其实就是把单个手势放在一起执行罢了
MultiTouchAction actions = new MultiTouchAction(driver);//初始化
actions.add(TouchAction1);
actions.add(TouchAction2);
actions.perform();
除了add和perform，其他没有方法了，此时单个TouchAction不需要perform

最后，Appium的手势比较复杂，使用过程中肯定会遇到许多问题，而且Appium的手势本身也有些奇怪的问题，所以希望同学们掌握调试的方法，解决实际遇到的问题~
其实，我常用的也就是拖动和解锁这2个手势~