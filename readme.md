
# 基于 selenium 模拟浏览器进行登录枚举 -- by NOVASEC   

由于 selenium 依赖问题 该项目不再进行维护

开发及使用细节参考:

Python实现简约的 selenium 登录爆破框架

https://mp.weixin.qq.com/s/qLmEp8KXmYYyGaPkLWGwAw



关于如何使用CSS选择器

谷歌浏览器--F12--Crtl+C选择元素--右键复制--复制Selector



# 重点注意

```
由于脚本依赖Chrome和ChromeDriver运行环境，导致新人环境经常配置错误。

因此考虑上次Chrome程序及对应驱动，但是github无法上传超过100M的数据。

并且考虑到程序依赖环境的便携，因此存入chromePortable (Chrome便携版,可更新)

注意：

chromePortable内仅仅包含便携版的启动器和下载器，不包含实际可执行的Chrome程序。

因此，使用前请 联网打开 [chromePortable目录下的Chrome.vbs或Chrome.exe] 下载对应的chrome浏览器版本。

如果有安全环境需求，建议自己在setting.py内设置自己的Chrome.exe路径。


不能使用最新版的selenium，建议使用：selenium=4.2.0（感谢wolvez反馈
pip3 install -r requirements.txt
pip3 uninstall selenium
pip3 install selenium==4.2.0

```



# 更新记录

20220321 添加配置文件功能,记录命令有一些不友好。[已添加]

20220321 不小心删除了整个项目,需要重新积累Star啦

20220323 增加css选择器（find_element_by_css_selector）处理其他三个选择器无法匹配到空格关键字的问题

20220402 增加chromedriver驱动和chromePortable文件夹。内置chromedriver驱动和Chrome便携版本vbs下载器。

```
Selenium之find_element_by_css_selector()的使用方法参考:
https://blog.csdn.net/qq_35861801/article/details/108125082
```

20220727 支持USER:PASS格式的字典,当参数设置时,用户名字典和密码字典相同时,自动调用。

```
if user_dict == pass_dict:
    user_pass_list = f_user.readlines()
    for user_pass in user_pass_list:
        user = user_pass.split(":", 1)[0].strip()
        pwd = user_pass.split(":", 1)[-1].strip()
```



# Todo

2. 考虑扩展为注入JS来进行登陆参数匹配,便于用户在浏览器调试(概率)。

3. 对接验证码识别方案(概率)。

   


# 必备

1. 你需要一个Chrome浏览器

   ```
   已内置便携Chrome版本下载器，使用前请打开ChromePortable/Chrome.vbs下载对应的chrome浏览器版本。
   ```

2. 你需要一个chromedriver驱动程序

   ```
   已内置chromedriver_win32_100.0.4896.60.exe,如需替换请修改setting.py中的chromedriver路径。
   
   Chrome与Chromedriver版本对应表:
   https://blog.csdn.net/weixin_45532870/article/details/106327359
   ```

   

# 命令示例:

```
方式1：使用setting.py配置启动参数后 
python3 browser-brute.py
当前版本推荐在setting.py中配置启动参数


方式2：命令行制定启动参数
python3 browser-brute.py 
-lu http://xxxxx/login.html 
--user_[class|name|id|CSS]    帐号表单[class|name|id|CSS]属性  
--pass_[class|name|id|CSS]    密码表单[class|name|id|CSS]属性 
--button_[class|name|id|CSS]  登录按钮[class|name|id|CSS]属性 
-bcp "path-of-chrome.exe" 
-bdp "path-of-chromedriver.exe"  
-ud username.txt -pd password.txt 
```



# 使用方法

```
Python3 was used !!! This program supports Python2 and Python3

usage: browser-brute.py [-h] [-lu LOGIN_URL] [-t1 TIME_1] [-t2 TIME_2] [-ui USER_ID] [-un USER_NAME] [-uc USER_CLASS] [-us USER_CSS_SELECTOR] [-pi PASS_ID] [-pn PASS_NAME] [-pc PASS_CLASS] [-ps PASS_CSS_SELECTOR]
                         [-bi BUTTON_ID] [-bn BUTTON_NAME] [-bc BUTTON_CLASS] [-bs BUTTON_CSS_SELECTOR] [-ud USER_DICT] [-pd PASS_DICT] [-k KEYWORD] [-bh BROWSER_HEADLESS] [-bp BROWSER_PROXY] [-bua BROWSER_USERAGENT]
                         [-bud BROWSER_USER_DIR] [-bcp BROWSER_CHROME_PATH] [-bdp BROWSER_DRIVER_PATH] [-v]

optional arguments:
  -h, --help            show this help message and exit
  -lu LOGIN_URL, --login_url LOGIN_URL
                        The login address, eg: http://192.168.1.1/login.aspx
  -t1 TIME_1, --time_1 TIME_1
                        Specifies the pause time (s) before access , eg: 1
  -t2 TIME_2, --time_2 TIME_2
                        Specifies the pause time (s) after access , eg: 1
  -ui USER_ID, --user_id USER_ID
                        Specify the username attribute by id
  -un USER_NAME, --user_name USER_NAME
                        Specify the username attribute by name
  -uc USER_CLASS, --user_class USER_CLASS
                        Specify the username attribute by class, No Spaces
  -us USER_CSS_SELECTOR, --user_css_selector USER_CSS_SELECTOR
                        Specify the username attribute by css selector, handle Spaces
  -pi PASS_ID, --pass_id PASS_ID
                        Specify the password attribute by id
  -pn PASS_NAME, --pass_name PASS_NAME
                        Specify the password attribute by name
  -pc PASS_CLASS, --pass_class PASS_CLASS
                        Specify the password attribute by class, No Spaces
  -ps PASS_CSS_SELECTOR, --pass_css_selector PASS_CSS_SELECTOR
                        Specify the password attribute by css selector, handle Spaces
  -bi BUTTON_ID, --button_id BUTTON_ID
                        Specify the login button attribute by id
  -bn BUTTON_NAME, --button_name BUTTON_NAME
                        Specify the login button attribute by name
  -bc BUTTON_CLASS, --button_class BUTTON_CLASS
                        Specify the login button attribute by class, No Spaces
  -bs BUTTON_CSS_SELECTOR, --button_css_selector BUTTON_CSS_SELECTOR
                        Specify the button attribute by css selector, handle Spaces
  -ud USER_DICT, --user_dict USER_DICT
                        Specify the login username dict
  -pd PASS_DICT, --pass_dict PASS_DICT
                        Specify the login password dict
  -k KEYWORD, --keyword KEYWORD
                        Specifies the keyword to match in the return message
  -bh BROWSER_HEADLESS, --browser_headless BROWSER_HEADLESS
                        Specifies the Browser browser_headless, eg: True
  -bp BROWSER_PROXY, --browser_proxy BROWSER_PROXY
                        Specifies the Browser Proxy IP for HTTP or HTTPS , eg: http://127.0.0.1:8080
  -bua BROWSER_USERAGENT, --browser_useragent BROWSER_USERAGENT
                        Specifies the Browser UserAgent , eg: Mozilla/5.0 Version/4.0
  -bud BROWSER_USER_DIR, --browser_user_dir BROWSER_USER_DIR
                        Specifies the Browser User Dir , eg: D: emp\Chrome User Data
  -bcp BROWSER_CHROME_PATH, --browser_chrome_path BROWSER_CHROME_PATH
                        Specifies the Browser Chrome.exe Path , eg: C:\chrome\chrome.exe
  -bdp BROWSER_DRIVER_PATH, --browser_driver_path BROWSER_DRIVER_PATH
                        Specifies the Browser Driver Path, eg: D: emp\chromedriver.exe
  -v, --version         显示程序当前版本号

Examples:
  python3 browser-brute.py -lu http://www.baidu.com
  python3 browser-brute.py -lu http://www.baidu.com -p http://127.0.0.1:8080

  其他控制细节参数请通过setting.py进行配置

  T00L Version: Ver 0.1.3 2022-03-23 13:30
```



# NEED STAR And ISSUE

```
1、右上角点击Star支持更新.
2、ISSUE或NOVASEC提更新需求
```

![NOVASEC](doc/NOVASEC.jpg)
