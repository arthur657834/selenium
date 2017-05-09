docker-compose up -d
docker-compose scale web=2 worker=3

docker-compose.yml
```yaml
hub:
  image: selenium/hub
  ports:
    - 4444:4444
firefox:
  image: selenium/node-firefox-debug
  ports:
    - 5901:5900
  links:
    - hub
chrome:
  image: selenium/node-chrome-debug
  ports:
    - 5902:5900
  links:
    - hub
```

http://10.1.50.250:4444/grid/console
查看浏览器启动状态

open browser 后面 + remote_url=http://10.1.50.250:4444/wd/hub


vnc默认密码:secret


https://github.com/SeleniumHQ/selenium/wiki/DesiredCapabilities#webdriver-1

If you specify a value for remote you can also specify 'desired_capabilities' which is a string in the form key1:val1,key2:val2 that will be used to specify desired_capabilities to the remote server. This is useful for doing things like specify a proxy server for internet explorer or for specify browser and os if your using saucelabs.com. 'desired_capabilities' can also be a dictonary (created with 'Create Dictionary') to allow for more complex configurations.

可以在http://10.1.50.250:4444/grid/console查看

browserName="firefox"
version="22",
Platform="LINUX"

chrome设置成功，firefox不行

pen browser 后面 +  desired_capabilities=${browser_info}


{seleniumProtocol=WebDriver, browserName=firefox, maxInstances=1, version=53.0, applicationName=, platform=LINUX}]


ex1:
```python
import org.openqa.selenium.*;  
import org.openqa.selenium.remote.RemoteWebDriver;  
import org.openqa.selenium.remote.DesiredCapabilities;  
  
//test01： 只匹配Windows下的ie来执行此用例，版本不限；多个版本匹配成功时优先级暂未知  
DesiredCapabilities aDesiredcap = DesiredCapabilities();  
aDesiredcap.setBrowserName("internet explorer")  
aDesiredcap.setVersion("")  
aDesiredcap.setPlatform(Platform.WINDOWS)  
WebDriver wd = new RemoteWebDriver<span style="font-family: Arial, Helvetica, sans-serif;">("http://localhost:4444/wd/hub", aDesiredcap);</span>  
wd.doSomething()  
  
//test02： 只匹配linix下的firefox的版本为22的浏览器执行用例；    
DesiredCapabilities aDesiredcap = DesiredCapabilities("firefox", "22", Platform.LINUX);  
WebDriver wd = new RemoteWebDriver("http://localhost:4444/wd/hub", aDesiredcap);  
wd.doSomething()      
  
//test03： 只匹配MAC下的safari浏览器执行，版本不限    
DesiredCapabilities aDesiredcap = DesiredCapabilities.safari();  
aDesiredcap.setPlatform(Platform.MAC)  
WebDriver wd = new RemoteWebDriver("http://localhost:4444/wd/hub", aDesiredcap);  
wd.doSomething()      
  
//test04： 只匹配chrome浏览器，任意平台，任意版本  
DesiredCapabilities aDesiredcap = DesiredCapabilities.chrome();  
aDesiredcap.setPlatform(Platform.ANY)  
WebDriver wd = new RemoteWebDriver("http://localhost:4444/wd/hub", aDesiredcap);  
wd.doSomething()      
```
