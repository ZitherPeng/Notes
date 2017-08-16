# 浏览器API

- 浏览器中加载URL： get()	-- 首先要启动浏览器 
	```Java
	driver.get("http://www.baidu.com");
	```  
- 浏览器最大化：window().maximize()
	```Java
	driver.manage().window().maximize();
	```  	
- 刷新：refresh() 
	```Java
	driver.navigate().refresh(); 
	```
- 返回上一页：back()
	```Java
	driver.navigate().back(); 
	```
- 向前进一页：forward() 
	```Java
	driver.navigate().forward();
	```
- 截图：getScreenshotAs()
	```Java
	File screenShotFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE); 
	FileUtils.copyFile(screenShotFile, new File("D:/test.png"));
	```
- 获取当前页的URL：getCurrentUrl()
	```Java
	driver.getCurrentUrl();
	```
- 关闭当前tab页面：close() 
	```Java
	driver.close(); 
	```
- 退出当前driver：quit() 
	```Java
	driver.quit(); 
	```
- 获取当前页的title:getTitle()
	```Java
	driver.getTitle();
	```
