#      元素： #
>     ID   、Name、Class Name、超链接文本 LinkText 、 缺省超链接文本 PartialLinkText、 元素Tag Name
>     get:只支持http和https开头的url
>     sendKeys：支持（"auto","test1","@163.com"）
>     支持input/textarea,不支持input type=button 和iframe、frame、其他标签
>     注意：在原来基础上追加内容


>     click： 所有元素都可点击，元素不能被遮挡
>     clear:  使用对象和sendKey相同，整体清除不是退格删除 
>     getCurrentUrl： 返回当前网站
>     getTitle：  返回浏览器Tile 
>     getText： 获取文案
>     quit：  不关闭常驻内存会导致内存溢出   
#    突显 #
>     highlight（driver,logo）突显
>      for(WebElement element :链接){
>        highlight(driver,element)

# xpath： #
>     /html/body/... 
>     模糊匹配路径：//
>     父节点：//BB/..
>     指定顺序：/aa/bbb[2]
>     选择aa的最后一个bb子元素：/aa/bb[last()] 
>     匹配bb所有：/aa/bb/*
>     匹配所有/aa下的孙节点bb元素：/aa/*/bb 
>     匹配有id属性的bb元素：//bb[@id] 
>     匹配有id=‘pwd’的bb元素：//bb[@id='pwd']
>     text ：
>     //    
>     //*[text()='']
  
 
     多个属性值定位： //input[@class='aa'  and  @value='bb']
                    //input[@class='aa'  or   @value='bb']

      starts-with():  //input[starts-with(@id,'aa')]
      ends-with():   //input[ends-with(@id,'_userName')]
      contains():    //input[contains(@id,'userName')]


# cssSelector ：
>     class=div.
>     id=div#
>     属性=div[alt='']



# ##选择有id属性且以name开始的元素 #
>     xpath：//*[start-with(@id,"name")]

# ##选择有id属性且包含name的元素 #
>     xpath: //*[contains(@id,"name"]
>     优先ID定位，其次name 需要确定唯一，定位链接LinkText，其他无法定位使用xpath


# ##浏览器窗口切换（switchTo.window） # 
>      String currentWindow = driver.getWindowHandle();
>         Set<String Handles = driver.getWindowHandles();
>         for(String s : Handles){
>         	if(s.equals(currentWindow))
>         		continue;
>         	
>         	else{
>         	 driver.switchTo().window(s);
>         	}        		
>         } 
      
       
  或者：
>         for（String winHandle：driver.getWindowHandles（））{   
>         driver.switchTo().window(winHandle);       
>         }

>         String  currentWindow =driver.getWindowHandle();
>         driver.switchTo().window(currentWindow);





# ##Frames切换（switchTo.frame） #
>     driver.switchTo().frame(0) 
>     driver.switchTo().frame("iframe")
>     driver.switchTo().frame(driver.findElement(By.xpath("//iframe[@src='http://blog.163.com/newpage/ursweb/tmpl2/loginurs.html']"))); 
>     driver.switchTo().frame(driver.findElement(By.id("x-URS-iframe")));
>     driver.switchTo().defaultContent();
>     driver.switchTo().defaultContent();


# ##浏览器弹框（switchTo.alert） #
>     Alert alert= driver.switchTo().alert();
>     alert.accept(); --确认
>     alert.dismiss(); --取消
>     出现alert弹框才可使用，消失前不能其他操作


# ##元素拖拽（dragAndDrop） #
>     WebElement element = driver.findElement(By.name("source"));
>     WebElement target = driver.findElement(By.name("target"));
>     Actions act = new Actions(driver);
>     act.dragAndDrop(element,target).perform(); ==
>     act.clickAndHold(element).build().perform();
>     act.moveToElement(target).build().perform();
>     act.release(target).build().perform();


# ##系统事件操作 #
>     Actions：
>     click（）
>     clickAndHold（）
>     release（）
>     contextClick（）
>     doubleClick() 
>     keyDown(Keys theKey)
>     keyUp(Keys theKey)
>     moveToElement(WebElement toElement) 
>     moceByOffset(int xOffset,int yOffset)

# eg:删除相册-移动鼠标到一个相册上  #
>     WebElement element = driver.findElement(By.xpath（"//div[@class='ln ln0][1]")）; 
>     Actions builder = new  Actions(driver); 
>     Action hover = builder.moveToElment(element).build();


# ##设置等待时间timeouts #
>     driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);--元素定位等待时间
>     pageLoadTimeout()---页面加载时间
>     setScriptTimeout()---脚本执行等待时间


# ##显示元素等待时间 #不要混用
>     WebDriverWait wait= new WebDriverWait(driver,time period);
>     wait.until(ExpectedConditions.presenceOfElementLocated（By.id（"id")))；


测试框架：testNG
1、注解
@Test 测试方法  groups={""}, dependsOnMethods={""}
@BeforeTest  测试方法前执行
@AfterTest   测试方法后执行
 

测试验证点
org.testng.Assert
fail
assertTrue
assertNull
assertEquals

String RealName = driver.findElement(By.className("extra-menu")).findElement(By.tagName("span")).getText();
Assert.assertEquals(Name,RealName);

用例集的组织:testng.xml
分组测试：
<groups>
  <run>
     <include name=""/>

测试报告：Test-output


测试用例设计：
测试准备-@BeforeClass
System.out.println(albumElement.getText))
albumElement.click（）

System.out.println(driver.getCurrentUrl())
System.out.println(driver.getTitle())  --获取浏览页面title


测试退出-@AfterClass(alwaysRun= true)

测试内容-验证点唯一
String albumName = String.valueOf(System.currentTimeMillis()) ;时间戳
WebElement element  = driver.findElement(By.)
Assert.assertEquals(element.getTitle(),"","") 
Assert.assertEquals(element.getAttribute("href"),"","")

测试内容-数据清理（@AfterMethod）
测试内容-数据驱动(@DataProvider)


可维护性封装
HomePage hp = new HomePage(driver);
hp.login(username,password);

通用性封装 web，Android，ios共同执行
持续集成