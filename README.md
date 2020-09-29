# New library for RobotFramework



## Contents

- [简介](https://github.com/ChiLincoln/robotframework-appiumlibrary#introduction)
- [关键字文档](https://github.com/ChiLincoln/robotframework-appiumlibrary#keyword-documentation)
- [安装与导入](https://github.com/ChiLincoln/robotframework-appiumlibrary#installation)
- [终端设置](https://github.com/ChiLincoln/robotframework-appiumlibrary#device-setup)
- [调用实例](https://github.com/ChiLincoln/robotframework-appiumlibrary#usage)
- [贡献](https://github.com/ChiLincoln/robotframework-appiumlibrary#contributing)
- [项目贡献者](https://github.com/sChiLincoln/robotframework-appiumlibrary#project-contributors)



## [简介](https://github.com/ChiLincoln/robotframework-newlibrary#id2)

（简单介绍测试库。）

[AppiumLibrary](https://github.com/serhatbolsu/robotframework-appiumlibrary) is an appium testing library for [Robot Framework](https://robotframework.org/). Library can be downloaded from [PyPI](https://pypi.org/project/robotframework-appiumlibrary/).

It uses [Appium](http://appium.io/) to communicate with Android and iOS application similar to how *Selenium WebDriver* talks to web browser.



## [关键字文档](https://github.com/ChiLincoln/robotframework-newlibrary#id3)

（链接到Libdoc.html页面。）

See [Keyword Documentation](http://serhatbolsu.github.io/robotframework-appiumlibrary/AppiumLibrary.html) for available keywords and more information about the library in general.



## [安装与导入](https://github.com/ChiLincoln/robotframework-newlibrary#id4)

（安装、导入测试库的命令。）

The recommended installation method is using [pip](http://pip-installer.org/):

```
pip install --upgrade robotframework-appiumlibrary
```

See [Robot Framework installation instructions](https://github.com/robotframework/robotframework/blob/master/INSTALL.rst) for detailed information about installing Python and Robot Framework itself.



## [终端设置](https://github.com/ChiLincoln/robotframework-newlibrary#id5)

（运行测试库之前，设备需要做的准备。）

After installing the library, you still need to setup an simulator/emulator or real device to use in tests. iOS and Android have separate paths to follow, and those steps better explained in [Appium Driver Setup Guide](http://appium.io/docs/en/about-appium/getting-started/?lang=en). Please follow the **Driver-Specific Setup** according to platform.



## [调用实例](https://github.com/ChiLincoln/robotframework-newibrary#id6)

（调用测试库实例。）

To write tests with Robot Framework and AppiumLibrary, AppiumLibrary must be imported into your RF test suite. See [Robot Framework User Guide](https://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html) for more information.

As it uses Appium make sure your Appium server is up and running. For how to use Appium please refer to [Appium Documentation](http://appium.io/docs/en/about-appium/getting-started/)

When using Robot Framework, it is generally recommended to write tests easy to read/modify. The keywords provided in AppiumLibrary are pretty low level. It is thus typically a good idea to write tests using Robot Framework's higher level keywords that utilize AppiumLibrary keywords internally. This is illustrated by the following example where AppiumLibrary keywords like `Input Text` are primarily used by higher level keywords like `Input Search Query`.

```
*** Settings ***
Documentation  Simple example using AppiumLibrary
Library  AppiumLibrary

*** Variables ***
${ANDROID_AUTOMATION_NAME}    UIAutomator2
${ANDROID_APP}                ${CURDIR}/demoapp/ApiDemos-debug.apk
${ANDROID_PLATFORM_NAME}      Android
${ANDROID_PLATFORM_VERSION}   %{ANDROID_PLATFORM_VERSION=11}

*** Test Cases ***
Should send keys to search box and then check the value
  Open Test Application
  Input Search Query  Hello World!
  Submit Search
  Search Query Should Be Matching  Hello World!


*** Keywords ***
Open Test Application
  Open Application  http://127.0.0.1:4723/wd/hub  automationName=${ANDROID_AUTOMATION_NAME}
  ...  platformName=${ANDROID_PLATFORM_NAME}  platformVersion=${ANDROID_PLATFORM_VERSION}
  ...  app=${ANDROID_APP}  appPackage=io.appium.android.apis  appActivity=.app.SearchInvoke

Input Search Query
  [Arguments]  ${query}
  Input Text  txt_query_prefill  ${query}

Submit Search
  Click Element  btn_start_search

Search Query Should Be Matching
  [Arguments]  ${text}
  Wait Until Page Contains Element  android:id/search_src_text
  Element Text Should Be  android:id/search_src_text  ${text}
```

Create a file with the content above (name it: `test_file.robot`) and execute:

```
robot test_file.robot
```

The above example is single file test case, more examples can be found in a [sample project](https://github.com/serhatbolsu/robotframework-appium-sample) that illustrates using Robot Framework and AppiumLibrary. Check the sample project that you can find examples of mobile web & ios & android.



## [贡献](https://github.com/serhatbolsu/robotframework-appiumlibrary#id7)

Fork the project, make a change, and send a pull request!



## [项目贡献者](https://github.com/serhatbolsu/robotframework-appiumlibrary#id8)

- [Serhat Bolsu](https://github.com/serhatbolsu)
- [William Zhang](https://github.com/jollychang)
- [Xie Lieping](https://github.com/frankbp)
- [Jari Nurminen](https://github.com/yahman72)

AppiumLibrary is modeled after (and forked from) [appiumandroidlibrary](https://github.com/frankbp/robotframework-appiumandroidlibrary), but re-implemented to use appium 1.X technologies.
