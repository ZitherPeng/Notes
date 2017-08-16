# Selenium 安装浏览器驱动  
&emsp;&emsp;Webdriver 支持 Chrome(ChromeDriver)、FireFox(geckodriver)、IE(InternetExplorerDriver)、Opera(OperaDriver)，它还支持 AndriodDriver 和 iPhone(iPhoneDriver) 的移动应用测试。
&emsp;&emsp;这里主要介绍三大主流浏览器的浏览器驱动安装。
## FireFox  
&emsp;&emsp;FireFox在3.0以前中的 Webdriver，是火狐浏览器自带的功能，但是3.0以后是实现 geckodriver，要使用 FireFox 浏览器需要自己下载 geckodriver.exe，这个程序是由 FireFox 团队提供的，可以看做它是链接 WebDriver 和FireFox 浏览器的桥梁。 
- 优点  
geckodriver 对页面的自动化测试支持得比较好，很直观地模拟页面的操作，对 JavaScript 的支持也非常完善，基本上页面上做的所有操作 geckodriver 都可以模拟。 
- 缺点  
启动很慢，运行也比较慢，不过，启动之后 Webdriver 的操作速度虽然不快但还是可以接受的，建议不要频繁启动停止 geckodriver。  
- 实现方式
  1. 把 geckodriver.exe 放入 Java 安装的 bin 目录下，然后使用代码
		```Java
		WebDriver driver = new FirefoxDriver(); 
		```
  1. 把 geckodriver.exe 放入火狐的根目录(或者其他自定义目录)，然后写如下代码： 
		```Java
		System.setProperty("webdriver.gecko.driver", "C:\\Program Files (x86)\\Mozilla Firefox\\geckodriver.exe");
		WebDriver driver = new FirefoxDriver();
		```
## Chrome
&emsp;&emsp;Chrome 没有实现 webdriver，要使用chrome浏览器需要自己下载 chromedriver.exe，这个程序是由Chrome团队提供的。
- 优点:
启动速度快。
- 实现方式
  1. 把 chromedriver.exe 放入 Java 安装的 bin 目录下，然后使用代码
		```Java
		WebDriver driver = new ChromeDriver(); 
		```
  1. 把 chromedriver.exe 放入 Chrome 的根目录(或者其他自定义目录)，然后写如下代码： 
		```Java
		System.setProperty("webdriver.chrome.driver", "C:\\Program Files (x86)\\Google\\Chrome\\Application\\chromedriver.exe");
		WebDriver driver = new ChromeDriver();
		```
- **注意**
Chrome 版本和 chromedriver.exe 的版本映射关系需要一致。
所有chromedriver均可在下面链接中下载到：
[http://chromedriver.storage.googleapis.com/index.html](http://chromedriver.storage.googleapis.com/index.html)
PS：国内访问需要翻墙

## InternetExplorer
&emsp;&emsp;webdriver 要使用 IE 浏览器需要下载 InternetExplorerDriver.exe，根据浏览器的版本下载32位或者64位的 driver。
- 优点
直观地模拟用户的实际操作，对 JavaScript 提供完善的支持。 
- 缺点
是所有浏览器中运行速度最慢的，并且只能在 Windows下运行，对 CSS 以及 XPATH 的支持也不够好。
- 实现方式
  1. 把 InternetExplorerDriver.exe 放入 Java 安装的 bin 目录下，然后使用代码
		```Java
		WebDriver driver = new InternetExplorerDriver(); 
		```
  1. 把 InternetExplorerDriver.exe 放入 IE 的根目录(或者其他自定义目录)，然后写如下代码： 
		```Java
		System.setProperty("webdriver.IE.driver", "C:\\Program Files\\Internet Explorer\\IEDriverServer.exe");
		WebDriver driver = new InternetExplorerDriver();
		```
- **注意**
需要将 IE 浏览器各个区域的保护模式设置的一样，要么全勾选，要么全不勾选，工具-- Internet 选项--安全。还需要将页面的缩放比例设置为100%。



