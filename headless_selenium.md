yum install -y Xvfb
pip install selenium
pip install pyvirtualdisplay
Xvfb :10 -ac
-ac代表关闭xvfb的访问控制
export DISPLAY=:10


pip install xvfbwrapper

```python
#!/usr/bin/env python
from selenium import webdriver
from xvfbwrapper import Xvfb
xvfb = Xvfb(width=1280,height=720)
xvfb.start()
print('Start...')
browser = webdriver.Firefox()
browser.get('http://52sox.com')
title = browser.title
print(title)
print("Clean...")
browser.close()
xvfb.stop()
```