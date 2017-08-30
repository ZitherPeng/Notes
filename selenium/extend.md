# 其他扩展操作  
## 多窗口  
&emsp;&emsp;有时候我们在测试一个 web 应用的时候会出现多个浏览器窗口的情况，webdriver 提供了相应的解决方案。
&emsp;&emsp;如下： 首先要获得每一个窗口的唯一标识符号（句柄）,通过获得的句柄来区分不同的窗口，从而对不同窗口上的元素进行操作。
```Java
String defaultHandle = driver.getWindowHandle();  //获得当前标签页的句柄

Set<String> currentHandles = driver.getWindowHandles();
for (String Handle : currentHandles) {
		driver.switchTo().window(Handle);   //切换到新打开的标签页
}
```

## 调用JS
&emsp;&emsp;调用JS完成页面操作。
```Java
driver.get("http://www.oray.com/");
WebElement target = driver.findElement(By.xpath("/html/body/div[2]/div[2]/div[2]/div/ul/li[1]/div/a[1]"));
((JavascriptExecutor) driver).executeScript("arguments[0].scrollIntoView();", target);
target.click();
```

## 验证码处理
对于web应用，很多地方比如登录、发帖都需要输入验证码，类型也多种多样，解决验证码的方法如下： 
- 去掉验证码：在测试环境去掉，让开发屏蔽相关验证码代码。
- 设置万能码：只要输入这个万能码，程序就认为验证通过。
- 验证码识别技术：可以通过OCR引擎来识别图片验证码，不过不能达到100%识别。
- 记录cookie：通过向浏览器添加cookie可以绕过登录的验证码，在用户登录之前，通过addcookie()方法讲用户名和密码写入cookie,cookie可以通过getcookies()方法获得。
