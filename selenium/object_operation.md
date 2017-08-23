# Selenium 对象操作
&emsp;&emsp;定位到对象后，需要对对象进行操作，常见的有鼠标点击、键盘操作等，这取决于我们定位到的对象支撑哪些操作。一般来说，所有与页面交互的操 作都将通过 WebElement 接口。
## 常用方法  
```Java
clear() : 清除对象的内容
send_keys() : 在对象上模拟按键输入，注意如果是函数需要增加转义符
click() : 单击对象，强调对象的独立性
submit() : 提交表单，要求对象必须是表单，强调对象必须是表单

getSize(): 返回对象的尺寸 
driver.findElement(By.cssSelector("#J_username")).getSize().height; 
driver.findElement(By.cssSelector("#J_username")).getSize().width;

getText(): 获取对象的文本
driver.findElement(By.cssSelector("#J_username")).getText()

get_attribute("属性名")：获取对象的属性值 
driver.findElement(By.cssSelector("#J_username")).getAttribute("id");

isDisplayed()：用来判断对象是否可见，即css的display属性是否为none 
driver.findElement(By.cssSelector("#J_username")).isDisplayed()

isEnabled()：判断对象是否被禁用 
driver.findElement(By.cssSelector("#J_username")).isEnabled()

isSelected()：判断对象是否被选中 
driver.findElement(By.cssSelector("#J_username")).isSelected()

getTagName()：获取对象标签名称 
driver.findElement(By.cssSelector("#J_username")).getTagName()

getLocation()：获取元素坐标 
driver.findElement(By.cssSelector("#J_username")).getLocation()

Cookie操作
getCookies()/getCookieNamed(cookie_name)：返回当前会话中的cookies 
Set<Cookie> cookies = driver.manage().getCookies();
Cookie cookie = driver.manage().getCookieNamed(cookie_name);

根据cookie name 查找\增加cookies:
Cookie cookie = new Cookie("name", "value"); 
driver.manage().addCookie(cookie);

deleteAllCookies()/deleteCookie(cookie)/deleteCookieNamed(cookie_name)： 删除 cookie
driver.manage().deleteAllCookies(); 
driver.manage().deleteCookieNamed("CookieName"); //通过 cookie 的name 
driver.manage().deleteCookie(cookie);	//删除指定的 cookie 对象
```

## 鼠标事件
&emsp;&emsp;在实际的 web 产品测试中，对于鼠标的操作，不单单只有 click()，有时候还要用到右击、双击、拖动等操作，这些操作包含在 Actions 类中。
&emsp;&emsp;在使用ActionChains类下面的方法之前，需要将包引入
```Java
import org.openqa.selenium.interactions.Actions
Actions action=new Actions(driver); 
```
Actions 用于生成用户的行为，所有的行为都存储在 action 对象，通过perform()执行存储的行为。
perform() 执行所有 Action 存储的行为，perform()同样也是 ActionChains 类提供的方法，经常结合在一起使用。
Actions类中鼠标操作常用方法:
```Java
contextClick()    右击

doubleClick()     鼠标双击页面元素 
action.doubleClick(e1).perform();

dragAndDrop(source,target)
在源对象上按下鼠标左键，然后移动到目标 元素上释放
source：鼠标按下的源对象	target：鼠标释放的目标对象

moveToElement()   鼠标移动到一个元素上
action.moveToElement(e1).perform();

clickAndHold()    在一个对象上按住鼠标左键 
action.clickAndHold(e1).perform();
 
release()         鼠标释放 
action.click(e1).release(e1).perform();

moveToElement(toElement, xOffset, yOffset) 
鼠标移到元素 toElement 的 (xOffset, yOffset) 位置，
这里的 (xOffset, yOffset) 是以元素 toElement 的左上角为 (0,0) 开始的 (x, y) 坐标轴。

moveByOffset(xOffset, yOffset)
以鼠标当前位置或者 (0,0) 为中心开始移 动到 (xOffset, yOffset) 坐标轴，
如果 xOffset 为负数，表示横坐标向左移动，yOffset 为负数表示纵坐标向上移动。而且如果这两个值大于当前屏幕的大小，
鼠标只能移到屏幕最边界的位置同时抛出 MoveTargetOutOfBoundsExecption 的异常。
```

## 键盘事件  
&emsp;&emsp;在实际的web测试工作中，需要配合键盘按键来操作，对于键盘的模拟操作， Actions 类中有提供 keyUp(theKey)、keyDown(theKey)、sendKeys(keysToSend) 等方法来实现。键盘的操作有普通键盘和修饰键盘(Ctrl+a，Ctrl+c/v等)

- 普通键盘：
driver.findElement(By.cssSelector("input.search-query")).sendKeys(Keys.TAB);
定位到对象并按tab键 
sendKeys(Keys.BACK_SPACE)  删除键(backspace) 
sendKeys(Keys.F1)  F1键  

- 修饰键盘：
action.keyDown(Keys.CONTROL).sendKeys(“a”).perform(); 
action.keyDown(Keys.ALT).keyDown(Keys.F4).keyUp(Keys.ALT).perform();
Alt+F4 组合键 关闭窗口 
- 备注：
在 WebDriver API 中，KeyDown(Keys theKey)、KeyUp(Keys theKey) 方法的参数只能是修饰键：Keys.SHIFT、Keys.ALT、Keys.CONTROL, 否则将抛出 IllegalArgumentException 异常。 
其次对于 action.keyDown(theKey) 方法的调用， 
如果没有显示的调用 action.keyUp(theKey) 或者 action.sendKeys(Keys.NULL) 来释放的话，这个按键将一直保持按住状态。

实例：
```Java
WebDriver driver = new ChromeDriver();
driver.get("http://www.oray.com/");
driver.findElement(By.xpath("//a[text()='登录']")).click();
driver.findElement(By.cssSelector("#account")).sendKeys("123");
driver.findElement(By.cssSelector("#account")).click();
Actions actions = new Actions(driver);
actions.keyDown(Keys.CONTROL).sendKeys("a").keyUp(Keys.CONTROL).perform(); 
actions.keyDown(Keys.CONTROL).sendKeys("c").keyUp(Keys.CONTROL).perform(); 
driver.findElement(By.cssSelector("#password")).click();
actions.keyDown(Keys.CONTROL).sendKeys("v").keyUp(Keys.CONTROL).perform(); 
```
## 等待时间  
&emsp;&emsp;为了保证脚本的稳定性，有时候需要引入等待时间，等待页面加 载元素后再进行操作，selenium 提供三种等待时间设置方式。
- Thread.sleep();
固定休眠时间设置，Java的Thread类里提供了休 眠方法sleep,导入包后就能使用；
sleep()方法以毫秒为单位 Thread.sleep(3000);  

- implicitlyWait()  隐式等待;
implicitlyWait() 方法比sleep() 方法智能，sleep() 方法只能在一个固定的时间等待，而 implicitlyWait() 可以在一个时间范围内等待，称为隐式等待。
```Java
driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
WebElement e = driver.findElement(By.cssSelector("div.red_box")); 
```
&emsp;&emsp;设置等待时间10s,页面上的元素5s后出现，只等待5s。不会等待10s 隐性的等待其实就相当于设置全局的等待，在定位元素时，对所有元 素设置超时时间。

- WebDriverWait()  显示等待;
就是明确的要等到某个元素的出现或者是某个元素的可点击等条件,等不到,就一直等,除非在规定的时间之内都没找到,那么就抛出异常。
```Java
WebDriver driver = new ChromeDriver();
WebElement element = (new WebDriverWait(driver, 5)).until(new ExpectedCondition<WebElement>() {
	@Override
	public WebElement apply(WebDriver driver) {
		return driver.findElement(By.cssSelector("#kw"));
	}
});
```

## alert \ confirm \ prompt 操作
&emsp;&emsp;什么是[alert \ confirm \ prompt](./demo/alert.html)?
&emsp;&emsp;WebDriver 中处理原生 JS 的 alert 、confirm 以及 prompt 非常方便。 
&emsp;&emsp;具体思路是使用 switchTo.alert() 方法定位到当前的 alert/confirm/prompt(这里注意当前页面只能同时含有一个控件，如果多了会报错的，所以这就需要一一处理了)，然后在调用Alert 的方法进行操作，Alert提供了以下几个方法：
```Java
getText()： 返回alert/confirm/prompt中的文字内容
accept() : 点击确认按钮
dismiss() : 点击取消按钮如果有取消按钮的话 
sendKeys(value) :  向prompt中输入文字 
```
示例：
```Java
//消息框 alert
WebDriver driver = new ChromeDriver();
driver.get("file:///G:/Repositories/Notes/selenium/demo/alert.html");
driver.findElement(By.cssSelector("input[value = '消息框alert']")).click();
Alert alert = driver.switchTo().alert();
System.out.println(alert.getText());
alert.accept();
```
```Java
//对话框 confirm
WebDriver driver = new ChromeDriver();
driver.get("file:///G:/Repositories/Notes/selenium/demo/alert.html");
driver.findElement(By.cssSelector("input[value = '对话框confirm']")).click();
Alert alert = driver.switchTo().alert();
System.out.println(alert.getText());
alert.dismiss();
```
```Java
//提示框 prompt
WebDriver driver = new ChromeDriver();
driver.get("file:///G:/Repositories/Notes/selenium/demo/alert.html");
driver.findElement(By.cssSelector("input[value = '提示框prompt']")).click();
Alert alert = driver.switchTo().alert();
alert.sendKeys("zither");
alert.accept();
```

## select 菜单处理
[select 菜单](./demo/select.html)
通过 Select 类自有的方法来实现选择某一项。
```Java
WebElement selector = driver.findElement(By.id("Selector")); 
Select select = new Select(selector);
```

选择select的option有以下三种方法
selectByIndex(int index) 通过index 
selectByVisibleText(String text) 通过匹配到的可见字符 
selectByValue(String value) 通过匹配到标签里的 value

示例：
```Java
try {
	WebDriver driver = new ChromeDriver();
	driver.get("file:///G:/Repositories/Notes/selenium/demo/select.html");
	WebElement selector = driver.findElement(By.id("status"));
	Select select = new Select(selector);
	select.selectByIndex(1);
	Thread.sleep(2000);
	select.selectByValue("1");
	Thread.sleep(2000);
	select.selectByVisibleText("审核不通过");
} catch (Exception e) {
}
```
