





[TOC]



# 软件安装

autojs下载地址：    https://wwc.lanzouq.com/iloaG02jz2va

autojs打包插件：   https://wwc.lanzouq.com/iIWEH02jz37c

电脑端vscode安装Auto.js-VSCodeExt插件



手机安装auto.js后，需要打开无障碍模式（为了脚本能执行）和悬浮框（为了查看控件信息）

![img](https://pic2.zhimg.com/80/v2-d4e13298c8d1475792bb5a5a0d7d8479_720w.jpg)



# 连接手机

确保手机和电脑在同一个局域网中。你可以将手机和电脑都连到同一个Wifi上，或者电脑开启热点给手机连接，或者手机开启热点给电脑连接。如果以上都无法做到，你还可以通过USB线连接手机，参考《adb连接手机(USB)》。



+ 电脑：在VS Code中按快捷键`Ctrl + Shift + P`，命令窗口点击 `Autojs Start Server`。
+ 手机：autojs中侧边栏点击连接电脑，输入电脑的ip地址



编写代码

运行代码：电脑：在VS Code中按快捷键`Ctrl + Shift + P`，命令窗口点击 `Autojs: run`



基础操作

```js
launchApp(appName); //打开应用
sleep(3000);        //等待3秒钟
text("领喵币").findOne(3000);   //查找text中的文字。查找3秒钟，没有找到返回null
text("领喵币").findOnce();   //查找text中的文字。没有找到返回null
toast("文本");   //弹出框
```





https://hyb1996.github.io/AutoJs-Docs/#/app?id=appintentoptions

## App

app模块提供的一系列函数，用于和其他应用交互，列如发送图片，打开邮件等。

同时提供了进阶函数startActivity和sendBroadcast，用户完成app模块没有内置的和其他应用交互

```js
//app命令可以不写，省略，全局函数
launchApp("Auto.js");
```



**[app.versionCode](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appversioncode)**

当前软件版本号。整数

**[app.versionName](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appversionname)**

当前软件的版本名称。字符串

**[app.autojs.versionCode](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appautojsversioncode)**

当前软件版本号。整数

**[app.autojs.versionName](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appautojsversionname)**

当前软件的版本名称。字符串

**[app.launchApp(appName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=applaunchappappname)**

通过应用名称启动应用。找到返回true，返回false。（如果有重名，那么将启动某一个）

**[app.launch(packageName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=applaunchpackagename)**

通过应用包名启动应用，找到返回ture，返回false（微信："com.tencent.mm"）

**[app.launchPackage(packageName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=applaunchpackagepackagename)**

通过应用包名启动应用，（同app.launch一样）

**[app.getPackageName(appName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appgetpackagenameappname)**

输入应用名称，返回应用包名。找不到返回null

**[app.getAppName(packageName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appgetappnamepackagename)**

输入应用包名，返回应用名称。，找不到返回null

**[app.openAppSetting(packageName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appopenappsettingpackagename)**

打开应用的设置页面。找不到返回false，返回true

**[app.viewFile(path)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appviewfilepath)**

用其他应用查看文件。（没有应用可以打开该文件，则抛出`ActivityNotException`。文件不存在的情况由查看文件的应用处理）

**[app.editFile(path)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appeditfilepath)**

用其他应用编辑文件。（没有应用可以编辑该文件，则抛出`ActivityNotException`。文件不存在的情况由查看文件的应用处理）

**[app.uninstall(packageName)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appuninstallpackagename)**

卸载应用。使用应用包名卸载`com.tencent.mobileqq`

**[app.openUrl(url)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appopenurlurl)**

用浏览器打开URL。（如果没有安装浏览器应用，则抛出`ActivityNotException`。）

**[app.sendEmail(options)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appsendemailoptions)**

调用邮箱软件发送邮件。（如果没有安装邮箱应用，则抛出`ActivityNotException`。）

+ `options`{Object} 发送邮件的参数。包括:
  + `email` {string} | {Array} 收件人的邮件地址。如果有多个收件人，则用字符串数组表示
  + `cc` {string} | {Array} 抄送收件人的邮件地址。如果有多个抄送收件人，则用字符串数组表示
  + `bcc` {string} | {Array} 密送收件人的邮件地址。如果有多个密送收件人，则用字符串数组表示
  + `subject` {string} 邮件主题(标题)
  + `text` {string} 邮件正文
  + `attachment` {string} 附件的路径。

**[app.startActivity(name)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appstartactivityname)**

启动Auto.js的特定界面，该函数在Auto.js内运行则会打开Auto.js内的界面



**进阶 intent**

一个消息传递对象，可以使用它从其他应用组件请求操作。



**[app.intent(options)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appintentoptions)**

`options` {Object} 选项，包括：

- `action` {string} 意图的Action，指意图要完成的动作，是一个字符串常量，比如"android.intent.action.SEND"。当action以"android.intent.action"开头时，可以省略前缀，直接用"SEND"代替。参见[Actions](https://developer.android.com/reference/android/content/Intent.html#standard-activity-actions)。
- `type` {string} 意图的MimeType，表示和该意图直接相关的数据的类型，表示比如"text/plain"为纯文本类型。
- `data` {string} 意图的Data，表示和该意图直接相关的数据，是一个Uri, 可以是文件路径或者Url等。例如要打开一个文件, action为"android.intent.action.VIEW", data为"file:///sdcard/1.txt"。
- `category` {Array} 意图的类别。比较少用。参见[Categories](https://developer.android.com/reference/android/content/Intent.html#standard-categories)。
- `packageName` {string} 目标包名
- `className` {string} 目标Activity或Service等组件的名称
- `extras` {Object} 以键值对构成的这个Intent的Extras(额外信息)。提供该意图的其他信息，例如发送邮件时的邮件标题、邮件正文。参见[Extras](https://developer.android.com/reference/android/content/Intent.html#standard-extra-data)。
- `flags` {Array} intent的标识，字符串数组，例如`["activity_new_task", "grant_read_uri_permission"]`。参见[Flags](https://developer.android.com/reference/android/content/Intent.html#setFlags(int))。
- `root` {Boolea} 是否以root权限启动、发送该intent。使用该参数后，不能使用`context.startActivity()`等方法，而应该直接使用诸如`app.startActivity({...})`的方法。

例如：

```js
//打开应用来查看图片文件
var i = app.intent({
    action: "VIEW",
    type: "image/png",
    data: "file:///sdcard/1.png"
});
context.startActivity(i);
```



**[app.startActivity(options)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appstartactivityoptions)**

启动该Activity（页面）

```js
app.startActivity({
    action: "SEND",
    type: "text/plain",
    data: "file:///sdcard/1.txt"
});
```

**[app.sendBroadcast(options)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appsendbroadcastoptions)**

发送广播

**[app.startService(options)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appstartserviceoptions)**

启动该服务

**[app.sendBroadcast(name)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appsendbroadcastname)**

特定的广播名称，包括

- `name`{string} 特定的广播名称，包括：
  - `inspect_layout_hierarchy` 布局层次分析
  - `inspect_layout_bounds` 布局范围

发送以上特定名称的广播可以触发Auto.js的布局分析，方便脚本调试。这些广播在Auto.js发送才有效，在打包的脚本上运行将没有任何效果。

```
app.sendBroadcast("inspect_layout_bounds");
```

**[app.intentToShell(options)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appintenttoshelloptions)**

转换为对应的shell的intent命令的参数。

```js
shell("am start " + app.intentToShell({
    packageName: "org.autojs.autojs",
    className: "org.autojs.autojs.ui.settings.SettingsActivity_"
}), true);
```

**[app.parseUri(uri)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appparseuriuri)**

一个代表Uri的字符串。返回一个代表url的对象

**[app.getUriForFile(path)](https://hyb1996.github.io/AutoJs-Docs/#/app?id=appgeturiforfilepath)**

文件路径。返回指向该文件的url的对象。



## 全局变量与函数

全局变量和函数在所有模块中均可使用，但是以下变量的作用域只在模块内

+ exports
+ modeule
+ require() 以下的对象是特定于Auto.js的，有些内置对象是JavaScript语言本身的一部分。



**[sleep(n)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=sleepn)**

暂停运行n毫秒

**[currentPackage()](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=currentpackage)**

返回最近一次检测到的正在运行的应用包名（依赖于无障碍服务，如果未开启，则抛出异常提示）

**[currentActivity()](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=currentactivity)**

返回最近一次检测到的正在运行的Activity的名称（依赖于无障碍服务，如果未开启，则抛出异常提示）

**[setClip(text)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=setcliptext)**

设置剪贴板内容，直接长按粘贴

**[getClip()](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=getclip)**

返回剪贴板的内容

**[toast(message)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=toastmessage)**

气泡消息（显示时间一般是两秒，具体取决于系统）

注意：信息的显示是”异步“执行的，不会等待上一条消失，会立即执行所有的消息

**[toastLog(message)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=toastlogmessage)**

要显示的信息（相当于toast（））

**waitForActivity(activity[, period = 200\])](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=waitforactivityactivity-period-200)**

+ `activity` Activity名称
+ `period` 轮询等待间隔（毫秒）

等待指定的Activity出现，period为检查Activity的间隔。

**waitForPackage(package[, period = 200\])](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=waitforpackagepackage-period-200)**

- `package` 包名
- `period` 轮询等待间隔（毫秒）

等待指定的应用出现。例如`waitForPackage("com.tencent.mm")`为等待当前界面为微信。

**[exit()](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=exit)**

立即停止脚本运行

**[random(min, max)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=randommin-max)**

返回一个随机值，在固定的大小内

**[random()](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=random)**

返回在0和1的随机浮点数

**[requiresApi(api)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=requiresapiapi)**

表示此脚本需要达到Android版本多少才能运行，19代表版本4.4（可以参考以下Android API和版本的对照表:）

**[requiresAutojsVersion(version)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=requiresautojsversionversion)**

表示此脚本需要Auto.js版本达到指定版本才能运行。

**[runtime.requestPermissions(permissions)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=runtimerequestpermissionspermissions)**

动态申请安卓的权限。（目前Auto.js只有两个权限）

- `access_fine_location` GPS权限
- `record_audio` 录音权限

**[runtime.loadJar(path)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=runtimeloadjarpath)**

加载目标jar文件，加载成功后将可以使用该Jar文件的类。

**[runtime.loadDex(path)](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=runtimeloaddexpath)**

加载目标dex文件，加载成功后将可以使用该dex文件的类。

**[context](https://hyb1996.github.io/AutoJs-Docs/#/globals?id=context)**

全局变量。一个android.content.Context对象。

注意该对象为ApplicationContext，因此不能用于界面、对话框等的创建。



## Console

控制台模块提供了一个和web浏览器中相似的用于调试的控制台，用于输出一些调试信息，中间结果等。

**[console.show()](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleshow)**

显示控制台。这会显示一个控制台的悬浮窗(需要悬浮窗权限)。

**[console.hide()](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolehide)**

隐藏控制台悬浮窗。

**[console.clear()](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleclear)**

清空控制台

**[console.log([data\][, ...args])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolelogdata-args)**

多个参数，第一个为主要信息，其他为代替值

**[console.verbose([data\][, ...args])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleverbosedata-args)**

与console.log类似，但输出结果以灰色字体显示。输出优先级低于log，用于输出观察性质的信息。

**[console.info([data\][, ...args])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleinfodata-args)**

与console.log类似，但输出结果以绿色字体显示。输出优先级高于log, 用于输出重要信息

**[console.warn([data\][, ...args])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolewarndata-args)**

与console.log类似，但输出结果以蓝色字体显示。输出优先级高于info, 用于输出警告信息。

**[console.error([data\][, ...args])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleerrordata-args)**

与console.log类似，但输出结果以红色字体显示。输出优先级高于warn, 用于输出错误信息。

**[console.assert(value, message)](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleassertvalue-message)**

断言。如果value为false则输出错误信息message并停止脚本运行。`console.assert(a == 2, "加法出错啦");`

**console.time([label\])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoletimelabel)**

启动一个定时器，用以计算一个操作的持续时间。

**[console.timeEnd(label)](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoletimeendlabel)**

停止之前通过调用 `console.time()` 启动的定时器，并打印结果到控制台。

**[console.trace([data\][, ...args])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoletracedata-args)**

与console.log类似，同时会打印出调用这个函数所在的调用栈信息（即当前运行的文件、行数等信息）。

**console.input(data[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consoleinputdata-args)**

与console.log一样输出信息，并在控制台显示输入框等待输入。按控制台的确认按钮后会将输入的字符串用eval计算后返回。

**console.rawInput(data[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolerawinputdata-args)**

与console.log一样输出信息，并在控制台显示输入框等待输入。按控制台的确认按钮后会将输入的字符串直接返回。

**[console.setSize(w, h)](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolesetsizew-h)**

设置控制台的大小，单位像素。(无需加单位)

**[console.setPosition(x, y)](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolesetpositionx-y)**

设置控制台的位置，单位像素。(无需加单位)

**[console.setGlobalLogConfig(config)](https://hyb1996.github.io/AutoJs-Docs/#/console?id=consolesetgloballogconfigconfig)**

- config{Object} 日志配置，可选的项有：
  - `file` {string} 日志文件路径，将会把日志写入该文件中
  - `maxFileSize` {number} 最大文件大小，单位字节，默认为512 * 1024 (512KB)
  - `rootLevel` {string} 写入的日志级别，默认为"ALL"（所有日志），可以为"OFF"(关闭), "DEBUG", "INFO", "WARN", "ERROR", "FATAL"等。
  - `maxBackupSize` {number} 日志备份文件最大数量，默认为5
  - `filePattern` {string} 日志写入格式，参见[PatternLayout](http://logging.apache.org/log4j/1.2/apidocs/org/apache/log4j/PatternLayout.html)

设置日志保存的路径和配置。例如把日志保存到"/sdcard/1.txt":

**[print(text)](https://hyb1996.github.io/AutoJs-Docs/#/console?id=printtext)**

- text {string} | {Object} 要打印到控制台的信息。（相当于log(text)）



## 基于坐标的触摸模拟

+ 坐标点击、滑动函数，有些需要安卓7.0以上，有的需要root权限。
+ 要获取点击的位置的坐标，可以在开发模式中开启“指针位置”。
+ 基于坐标的脚本通常会有分辨率的问题，这时可以通过`setScreenMetrics()`函数来进行自动坐标放缩。

**[setScreenMetrics(width, height)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=setscreenmetricswidth-height)**

设置脚本坐标i点击所合适的屏幕宽高，屏幕宽度不一致会自动缩放坐标。



注意以下命令只有Android7.0及以下才有效

****

**[click(x, y)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=clickx-y)**

模拟点击坐标（x，y），并返回点击是否成功

**[longClick(x, y)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=longclickx-y)**

模拟长按坐标（x，y），并返回是否成功

**[press(x, y, duration)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=pressx-y-duration)**

模拟按住坐标(x, y), 并返回是否成功。（时间发过短，会被认为是点击，过长超过500毫秒，则认为是长按）

**[swipe(x1, y1, x2, y2, duration)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=swipex1-y1-x2-y2-duration)**

模拟从坐标(x1, y1)滑动到坐标(x2, y2)，并返回是否成功。只有滑动操作执行完成时脚本才会继续执行。

**[gesture(duration, [x1, y1\], [x2, y2], ...)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=gestureduration-x1-y1-x2-y2-)**

模拟手势操作。例如`gesture(1000, [0, 0], [500, 500], [500, 1000])`为模拟一个从(0, 0)到(500, 500)到(500, 100)的手势操作，时长为2秒。

**[gestures([delay1, duration1, [x1, y1\], [x2, y2], ...\], [delay2, duration2, [x3, y3\], [x4, y4\], ...\], ...\)](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=gesturesdelay1-duration1-x1-y1-x2-y2-delay2-duration2-x3-y3-x4-y4-)**

同时模拟多个手势。每个手势的参数为[delay, duration, 坐标], delay为延迟多久(毫秒)才执行该手势；duration为手势执行时长；坐标为手势经过的点的坐标。其中delay参数可以省略，默认为0。

****

**[RootAutomator](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomator)**

RootAutomator是一个使用root权限来模拟触摸的对象，用它可以完成触摸与多点触摸，并且这些动作的执行没有延迟。



**注意以下命令需要root权限**

****

**RootAutomator.tap(x, y[, id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatortapx-y-id)**

点击位置(x, y)。其中id是一个整数值，用于区分多点触摸，不同的id表示不同的"手指"，

如果不需要多点触摸，则不需要id这个参数。 多点触摸通常用于手势或游戏操作，例如模拟双指捏合、双指上滑等。

**RootAutomator.swipe(x1, x2, y1, y2[, duration, id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatorswipex1-x2-y1-y2-duration-id)**

模拟一次从(x1, y1)到(x2, y2)的时间为duration毫秒的滑动。

**RootAutomator.press(x, y, duration[, id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatorpressx-y-duration-id)**

模拟按下位置(x, y)，时长为duration毫秒。

**RootAutomator.longPress(x, y[\, id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatorlongpressx-y-id)**

以上为简单模拟触摸操作的函数。如果要模拟一些复杂的手势，需要更底层的函数。

**RootAutomator.touchDown(x, y[, id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatortouchdownx-y-id)**

模拟手指按下位置(x, y)。

**RootAutomator.touchMove(x, y[, id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatortouchmovex-y-id)**

模拟移动手指到位置(x, y)。

**RootAutomator.touchUp([id\])](https://hyb1996.github.io/AutoJs-Docs/#/coordinatesBasedAutomation?id=rootautomatortouchupid)**

模拟手指弹起。

****



## Device

device模块提供了与设备有关的信息与操作，列如获取设备宽高，内存使用率等。

此模块部分函数，例如调整音量，需要“修改系统设置”的权限。如果没有该权限，会抛出`SecurityException`并跳转到权限设置界面。



**[device.width](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicewidth)**

设置屏幕分辨率宽度，列如1080

**[device.height](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deviceheight)**

设备屏幕分辨率高度。例如1920。

**[device.buildId](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicebuildid)**

修订版本号，或者诸如"M4-rc20"的标识。

**[device.broad](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicebroad)**

设备的主板(?)型号。

**[device.brand](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicebrand)**

与产品或硬件相关的厂商品牌，如"Xiaomi", "Huawei"等。

**[device.device](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicedevice)**

设备在工业设计中的名称。

**[deivce.model](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deivcemodel)**

设备型号。

**[device.product](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deviceproduct)**

整个产品的名称。

**[device.bootloader](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicebootloader)**

设备Bootloader的版本。

**[device.hardware](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicehardware)**

设备的硬件名称(来自内核命令行或者/proc)。

**[device.fingerprint](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicefingerprint)**

构建(build)的唯一标识码。

**[device.serial](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deviceserial)**

硬件序列号。

**[device.sdkInt](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesdkint)**

安卓系统API版本。例如安卓4.4的sdkInt为19。

**[device.incremental](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deviceincremental)**

The internal value used by the underlying source control to represent this build. E.g., a perforce changelist number or a git hash.

**[device.release](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicerelease)**

Android系统版本号。例如"5.0", "7.1.1"。

**[device.baseOS](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicebaseos)**

The base OS build the product is based on.

**[device.securityPatch](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesecuritypatch)**

安全补丁程序级别。

**[device.codename](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicecodename)**

开发代号，例如发行版是"REL"。

**[device.getIMEI()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetimei)**

返回设备的IMEI.

**[device.getAndroidId()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetandroidid)**

返回设备的Android ID。

Android ID为一个用16进制字符串表示的64位整数，在设备第一次使用时随机生成，之后不会更改，除非恢复出厂设置。

**[device.getMacAddress()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetmacaddress)**

返回设备的Mac地址。该函数需要在有WLAN连接的情况下才能获取，否则会返回null。

**可能的后续修改**：未来可能增加有root权限的情况下通过root权限获取，从而在没有WLAN连接的情况下也能返回正确的Mac地址，因此请勿使用此函数判断WLAN连接。

**[device.getBrightness()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetbrightness)**

返回当前的(手动)亮度。范围为0~255。

**[device.getBrightnessMode()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetbrightnessmode)**

返回当前亮度模式，0为手动亮度，1为自动亮度。

**[device.setBrightness(b)](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesetbrightnessb)**

- `b` {number} 亮度，范围0~255

设置当前手动亮度。如果当前是自动亮度模式，该函数不会影响屏幕的亮度。

此函数需要"修改系统设置"的权限。如果没有该权限，会抛出SecurityException并跳转到权限设置界面。

**[device.setBrightnessMode(mode)](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesetbrightnessmodemode)**

- `mode` {number} 亮度模式，0为手动亮度，1为自动亮度

设置当前亮度模式。

此函数需要"修改系统设置"的权限。如果没有该权限，会抛出SecurityException并跳转到权限设置界面。

**[device.getMusicVolume()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetmusicvolume)**

返回当前媒体音量。

**[device.getNotificationVolume()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetnotificationvolume)**

返回当前通知音量。

**[device.getAlarmVolume()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetalarmvolume)**

返回当前闹钟音量。

**[device.getMusicMaxVolume()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetmusicmaxvolume)**

返回媒体音量的最大值。

**[device.getNotificationMaxVolume()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetnotificationmaxvolume)**

返回通知音量的最大值。

**[device.getAlarmMaxVolume()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetalarmmaxvolume)**

返回闹钟音量的最大值。

**[device.setMusicVolume(volume)](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesetmusicvolumevolume)**

设置当前媒体音量。

此函数需要"修改系统设置"的权限。如果没有该权限，会抛出SecurityException并跳转到权限设置界面。

**[device.setNotificationVolume(volume)](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesetnotificationvolumevolume)**

设置当前通知音量。

此函数需要"修改系统设置"的权限。如果没有该权限，会抛出SecurityException并跳转到权限设置界面。

**[device.setAlarmVolume(volume)](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicesetalarmvolumevolume)**

设置当前闹钟音量。

此函数需要"修改系统设置"的权限。如果没有该权限，会抛出SecurityException并跳转到权限设置界面。

**[device.getBattery()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetbattery)**

返回当前电量百分比。

**[device.isCharging()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deviceischarging)**

返回设备是否正在充电。

**[device.getTotalMem()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegettotalmem)**

返回设备内存总量，单位字节(B)。1MB = 1024 * 1024B。

**[device.getAvailMem()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicegetavailmem)**

返回设备当前可用的内存，单位字节(B)。

**[device.isScreenOn()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=deviceisscreenon)**

返回设备屏幕是否是亮着的。如果屏幕亮着，返回`true`; 否则返回`false`。

需要注意的是，类似于vivo xplay系列的息屏时钟不属于"屏幕亮着"的情况，虽然屏幕确实亮着但只能显示时钟而且不可交互，此时`isScreenOn()`也会返回`false`。

**[device.wakeUp()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicewakeup)**

唤醒设备。包括唤醒设备CPU、屏幕等。可以用来点亮屏幕。

**[device.wakeUpIfNeeded()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicewakeupifneeded)**

果屏幕没有点亮，则唤醒设备。

**device.keepScreenOn([timeout\])](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicekeepscreenontimeout)**

- `timeout` {number} 屏幕保持常亮的时间, 单位毫秒。如果不加此参数，则一直保持屏幕常亮。

保持屏幕常亮。

此函数无法阻止用户使用锁屏键等正常关闭屏幕，只能使得设备在无人操作的情况下保持屏幕常亮；同时，如果此函数调用时屏幕没有点亮，则会唤醒屏幕。

在某些设备上，如果不加参数timeout，只能在Auto.js的界面保持屏幕常亮，在其他界面会自动失效，这是因为设备的省电策略造成的。因此，建议使用比较长的时长来代替"一直保持屏幕常亮"的功能，例如`device.keepScreenOn(3600 * 1000)`。

可以使用`device.cancelKeepingAwake()`来取消屏幕常亮。

一直保持常量 `device.keepScreenOn()`

**device.keepScreenDim([timeout\])](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicekeepscreendimtimeout)**

- `timeout` {number} 屏幕保持常亮的时间, 单位毫秒。如果不加此参数，则一直保持屏幕常亮。

保持屏幕常亮，但允许屏幕变暗来节省电量。此函数可以用于定时脚本唤醒屏幕操作，不需要用户观看屏幕，可以让屏幕变暗来节省电量。

此函数无法阻止用户使用锁屏键等正常关闭屏幕，只能使得设备在无人操作的情况下保持屏幕常亮；同时，如果此函数调用时屏幕没有点亮，则会唤醒屏幕。

可以使用`device.cancelKeepingAwake()`来取消屏幕常亮。

**[device.cancelKeepingAwake()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicecancelkeepingawake)**

取消设备保持唤醒状态。用于取消`device.keepScreenOn()`, `device.keepScreenDim()`等函数设置的屏幕常亮。

**[device.vibrate(millis)](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicevibratemillis)**

使设备震动一段时间。

**[device.cancelVibration()](https://hyb1996.github.io/AutoJs-Docs/#/device?id=devicecancelvibration)**

如果设备处于震动状态，则取消震动。



## Dialogs

dialogs 模块提供了简单的对话框支持，可以通过对话框和用户进行交互。最简单的例子如下：

`alert("您好");`

这段代码会弹出一个消息提示框显示"您好"，并在用户点击"确定"后继续运行。稍微复杂一点的例子如下：

````js
var clear = confirm("要清除所有缓存吗?");
if(clear){
    alert("清除成功!");
}
````

`confirm()`会弹出一个对话框并让用户选择"是"或"否"，如果选择"是"则返回true。

需要特别注意的是，对话框在ui模式下不能像通常那样使用，应该使用回调函数或者[Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)的形式。理解这一点可能稍有困难。举个例子:

````js
"ui";
//回调形式
 confirm("要清除所有缓存吗?", function(clear){
     if(clear){
          alert("清除成功!");
     }
 });
//Promise形式
confirm("要清除所有缓存吗?")
    .then(clear => {
        if(clear){
          alert("清除成功!");
        }
    });
````

**dialogs.alert(title[, content, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsalerttitle-content-callback)**

- `title` {string} 对话框的标题。
- `content` {string} 可选，对话框的内容。默认为空。
- `callback` {Function} 回调函数，可选。当用户点击确定时被调用,一般用于ui模式。

显示一个只包含“确定”按钮的提示对话框。直至用户点击确定脚本才继续运行。

该函数也可以作为全局函数使用。

```js
alert("出现错误~", "出现未知错误，请联系脚本作者”);
```

在ui模式下该函数返回一个`Promise`。例如:

```js
"ui";
alert("嘿嘿嘿").then(()=>{
    //当点击确定后会执行这里
});
```

**dialogs.confirm(title[, content, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsconfirmtitle-content-callback)**

- `title` {string} 对话框的标题。
- `content` {string} 可选，对话框的内容。默认为空。
- `callback` {Function} 回调函数，可选。当用户点击确定时被调用,一般用于ui模式。

显示一个包含“确定”和“取消”按钮的提示对话框。如果用户点击“确定”则返回 `true` ，否则返回 `false` 。

该函数也可以作为全局函数使用。

在ui模式下该函数返回一个`Promise`。例如:

```js
"ui";
confirm("确定吗").then(value=>{
    //当点击确定后会执行这里, value为true或false, 表示点击"确定"或"取消"
});
```

**dialogs.rawInput(title[, prefill, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsrawinputtitle-prefill-callback)**

- `title` {string} 对话框的标题。
- `prefill` {string} 输入框的初始内容，可选，默认为空。
- `callback` {Function} 回调函数，可选。当用户点击确定时被调用,一般用于ui模式。

显示一个包含输入框的对话框，等待用户输入内容，并在用户点击确定时将输入的字符串返回。如果用户取消了输入，返回null。

该函数也可以作为全局函数使用。

```
var name = rawInput("请输入您的名字", "小明");
alert("您的名字是" + name);
```

在ui模式下该函数返回一个`Promise`。例如:

```
"ui";
rawInput("请输入您的名字", "小明").then(name => {
    alert("您的名字是" + name);
});
```

当然也可以使用回调函数，例如:

```
rawInput("请输入您的名字", "小明", name => {
     alert("您的名字是" + name);
});
```

**dialogs.input(title[, prefill, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsinputtitle-prefill-callback)**

等效于 `eval(dialogs.rawInput(title, prefill, callback))`, 该函数和rawInput的区别在于，会把输入的字符串用eval计算一遍再返回，返回的可能不是字符串。

可以用该函数输入数字、数组等。例如：

```js
var age = dialogs.input("请输入您的年龄", "18");
// new Date().getYear() + 1900 可获取当前年份
var year = new Date().getYear() + 1900 - age;
alert("您的出生年份是" + year);
```

在ui模式下该函数返回一个`Promise`。例如:

```js
"ui";
dialogs.input("请输入您的年龄", "18").then(age => {
    var year = new Date().getYear() + 1900 - age;
    alert("您的出生年份是" + year);
});
```

**dialogs.prompt(title[, prefill, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsprompttitle-prefill-callback)**

相当于 `dialogs.rawInput()`;

**[dialogs.select(title, items, callback)](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsselecttitle-items-callback)**

- `title` {string} 对话框的标题。
- `items` {Array} 对话框的选项列表，是一个字符串数组。
- `callback` {Function} 回调函数，可选。当用户点击确定时被调用,一般用于ui模式。

显示一个带有选项列表的对话框，等待用户选择，返回用户选择的选项索引(0 ~ item.length - 1)。如果用户取消了选择，返回-1。

```
var options = ["选项A", "选项B", "选项C", "选项D"]
var i = dialogs.select("请选择一个选项", options);
if(i >= 0){
    toast("您选择的是" + options[i]);
}else{
    toast("您取消了选择");
}
```

在ui模式下该函数返回一个`Promise`。例如:

```
"ui";
dialogs.select("请选择一个选项", ["选项A", "选项B", "选项C", "选项D"])
    .then(i => {
        toast(i);
    });
```

**dialogs.singleChoice(title, items[, index, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogssinglechoicetitle-items-index-callback)**

- `title` {string} 对话框的标题。
- `items` {Array} 对话框的选项列表，是一个字符串数组。
- `index` {number} 对话框的初始选项的位置，默认为0。
- `callback` {Function} 回调函数，可选。当用户点击确定时被调用,一般用于ui模式。

显示一个单选列表对话框，等待用户选择，返回用户选择的选项索引(0 ~ item.length - 1)。如果用户取消了选择，返回-1。

在ui模式下该函数返回一个`Promise`。

**dialogs.multiChoice(title, items[, indices, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsmultichoicetitle-items-indices-callback)**

- `title` {string} 对话框的标题。
- `items` {Array} 对话框的选项列表，是一个字符串数组。
- `indices` {Array} 选项列表中初始选中的项目索引的数组，默认为空数组。
- `callback` {Function} 回调函数，可选。当用户点击确定时被调用,一般用于ui模式。

显示一个多选列表对话框，等待用户选择，返回用户选择的选项索引的数组。如果用户取消了选择，返回`[]`。

在ui模式下该函数返回一个`Promise`。

**[dialogs.build(properties)](https://hyb1996.github.io/AutoJs-Docs/#/dialogs?id=dialogsbuildproperties)**

- `properties` {Object} 对话框属性，用于配置对话框。
- 返回 {Dialog}

创建一个可自定义的对话框，例如：

```
dialogs.build({
    //对话框标题
    title: "发现新版本",
    //对话框内容
    content: "更新日志: 新增了若干了BUG",
    //确定键内容
    positive: "下载",
    //取消键内容
    negative: "取消",
    //中性键内容
    neutral: "到浏览器下载",
    //勾选框内容
    checkBoxPrompt: "不再提示"
}).on("positive", ()=>{
    //监听确定键
    toast("开始下载....");
}).on("neutral", ()=>{
    //监听中性键
    app.openUrl("https://www.autojs.org");
}).on("check", (checked)=>{
    //监听勾选框
    log(checked);
}).show();
```

选项properties可供配置的项目为:

- `title` {string} 对话框标题

- `titleColor` {string} | {number} 对话框标题的颜色

- `buttonRippleColor` {string} | {number} 对话框按钮的波纹效果颜色

- `icon` {string} | {Image} 对话框的图标，是一个URL或者图片对象

- `content` {string} 对话框文字内容

- `contentColor`{string} | {number} 对话框文字内容的颜色

- `contentLineSpacing`{number} 对话框文字内容的行高倍数，1.0为一倍行高

- `items` {Array} 对话框列表的选项

- `itemsColor` {string} | {number} 对话框列表的选项的文字颜色

- ```
  itemsSelectMode
  ```

   

  {string} 对话框列表的选项选择模式，可以为:

  - `select` 普通选择模式
  - `single` 单选模式
  - `multi` 多选模式

- `itemsSelectedIndex` {number} | {Array} 对话框列表中预先选中的项目索引，如果是单选模式为一个索引；多选模式则为数组

- `positive` {string} 对话框确定按钮的文字内容(最右边按钮)

- `positiveColor` {string} | {number} 对话框确定按钮的文字颜色(最右边按钮)

- `neutral` {string} 对话框中立按钮的文字内容(最左边按钮)

- `neutralColor` {string} | {number} 对话框中立按钮的文字颜色(最左边按钮)

- `negative` {string} 对话框取消按钮的文字内容(确定按钮左边的按钮)

- `negativeColor` {string} | {number} 对话框取消按钮的文字颜色(确定按钮左边的按钮)

- `checkBoxPrompt` {string} 勾选框文字内容

- `checkBoxChecked` {boolean} 勾选框是否勾选

- `progress`{Object} 配置对话框进度条的对象：

  - `max` {number} 进度条的最大值，如果为-1则为无限循环的进度条
  - `horizontal` {boolean} 如果为true, 则对话框无限循环的进度条为水平进度条
  - `showMinMax` {boolean} 是否显示进度条的最大值和最小值

- `cancelable` {boolean} 对话框是否可取消，如果为false，则对话框只能用代码手动取消

- `canceledOnTouchOutside` {boolean} 对话框是否在点击对话框以外区域时自动取消，默认为true

- `inputHint` {string} 对话框的输入框的输入提示

- `inputPrefill` {string} 对话框输入框的默认输入内容

通过这些选项可以自定义一个对话框，并通过监听返回的Dialog对象的按键、输入事件来实现交互。



## Engines

engines模块包含了一些与脚本环境、脚本运行、脚本引擎有关的函数，包含运行其他脚本，关闭i脚本等。

**engines.execScript(name, script[, config\])](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesexecscriptname-script-config)**

- `name` {string} 要运行的脚本名称。这个名称和文件名称无关，只是在任务管理中显示的名称。
- `script` {string} 要运行的脚本内容。
- `config`{Object} 运行配置项
  - `delay` {number} 延迟执行的毫秒数，默认为0
  - `loopTimes` {number} 循环运行次数，默认为1。0为无限循环。
  - `interval` {number} 循环运行时两次运行之间的时间间隔，默认为0
  - `path` {Array} | {string} 指定脚本运行的目录。这些路径会用于require时寻找模块文件。

在新的脚本环境中运行脚本script。返回一个[ScriptExectuion](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=engines_scriptexecution)对象。

所谓新的脚本环境，指定是，脚本中的变量和原脚本的变量是不共享的，并且，脚本会在新的线程中运行。

**engines.execScriptFile(path[, config\])](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesexecscriptfilepath-config)**

- `path` {string} 要运行的脚本路径。
- `config`{Object} 运行配置项
  - `delay` {number} 延迟执行的毫秒数，默认为0
  - `loopTimes` {number} 循环运行次数，默认为1。0为无限循环。
  - `interval` {number} 循环运行时两次运行之间的时间间隔，默认为0
  - `path` {Array} | {string} 指定脚本运行的目录。这些路径会用于require时寻找模块文件。

在新的脚本环境中运行脚本文件path。返回一个[ScriptExecution](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptexecution)对象。

**engines.execAutoFile(path[, config\])](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesexecautofilepath-config)**

- `path` {string} 要运行的录制文件路径。
- `config`{Object} 运行配置项
  - `delay` {number} 延迟执行的毫秒数，默认为0
  - `loopTimes` {number} 循环运行次数，默认为1。0为无限循环。
  - `interval` {number} 循环运行时两次运行之间的时间间隔，默认为0
  - `path` {Array} | {string} 指定脚本运行的目录。这些路径会用于require时寻找模块文件。

在新的脚本环境中运行录制文件path。返回一个[ScriptExecution](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptexecution)对象。

**[engines.stopAll()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesstopall)**

停止所有正在运行的脚本。包括当前脚本自身。

**[engines.stopAllAndToast()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesstopallandtoast)**

停止所有正在运行的脚本并显示停止的脚本数量。包括当前脚本自身。

**[engines.myEngine()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesmyengine)**

返回当前脚本的脚本引擎对象([ScriptEngine](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=engines_scriptengine))

**[engines.all()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=enginesall)**

返回当前所有正在运行的脚本的脚本引擎[ScriptEngine](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=engines_scriptengine)的数组。

**[ScriptExecution](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptexecution)**

执行脚本时返回的对象，可以通过他获取执行的引擎、配置等，也可以停止这个执行。

要停止这个脚本的执行，使用`exectuion.getEngine().forceStop()`.

**[ScriptExecution.getEngine()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptexecutiongetengine)**

返回执行该脚本的脚本引擎对象([ScriptEngine](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=engines_scriptengine))

**[ScriptExecution.getConfig()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptexecutiongetconfig)**

返回该脚本的运行配置([ScriptConfig](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=engines_scriptconfig))

**[ScriptEngine](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptengine)**

脚本引擎对象。

**[ScriptEngine.forceStop()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptengineforcestop)**

停止脚本引擎的执行。

**[ScriptEngine.cwd()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptenginecwd)**

返回脚本的路径，如果是脚本文件就返回所在的文件夹，如果是字符串，就返回null或者设置的值

**[ScriptEngine.getSource()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptenginegetsource)**

返回当前脚本引擎正在执行的脚本对象。

**ScriptEngine.emit(eventName[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptengineemiteventname-args)**

- `eventName` {string} 事件名称
- `...args` {any} 事件参数

向该脚本引擎发送一个事件，该事件可以在该脚本引擎对应的脚本的events模块监听到并在脚本主线程执行事件处理。

**[ScriptConfig](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=scriptconfig)**

脚本执行时的配置。

**[delay](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=delay)**

延迟执行的毫秒数

**[interval](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=interval)**

循环运行时两次运行之间的时间间隔

**[loopTimes](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=looptimes)**

循环运行次数

**[getPath()](https://hyb1996.github.io/AutoJs-Docs/#/engines?id=getpath)**

返回一个字符串数组表示脚本运行时模块寻找的路径。



## 悬浮窗

floaty模块提供了悬浮窗的相关函数，可以在屏幕上显示自定义悬浮窗，控制悬浮窗大小、位置等。

悬浮窗在脚本停止运行时会自动关闭，因此，要保持悬浮窗不被关闭，可以用一个空的setInterval来实现，例如：

`setInterval(()=>{}, 1000);`

**[floaty.window(layout)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=floatywindowlayout)**

- `layout` {xml} | {View} 悬浮窗界面的XML或者View

指定悬浮窗的布局，创建并显示一个悬浮窗。

该悬浮窗自带关闭，调整大小，调整位置按键，可根据需要调用`setAdjustEnabled()`函数来显示或隐藏。

**[floaty.rawWindow(layout)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=floatyrawwindowlayout)**

指定悬浮窗的布局，创建并**显示**一个原始悬浮窗。

与`floaty.window()`函数不同的是，该悬浮窗不会增加任何额外设施（例如调整大小、位置按钮），您可以根据自己需要编写任何布局。

而且，该悬浮窗支持完全全屏，可以覆盖状态栏，因此可以做护眼模式之类的应用。

**[floaty.closeAll()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=floatycloseall)**

关闭所有本脚本的悬浮窗。

**[FloatyWindow](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=floatywindow)**

悬浮窗对象，可通过`FloatyWindow.{id}`获取悬浮窗界面上的元素。例如, 悬浮窗window上一个控件的id为aaa, 那么`window.aaa`即可获取到该控件，类似于ui。

**[window.setAdjustEnabled(enabled)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowsetadjustenabledenabled)**

如果enabled为true，则在悬浮窗左上角、右上角显示可供位置、大小调整的标示，就像控制台一样； 如果enabled为false，则隐藏上述标示。

**[window.setPosition(x, y)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowsetpositionx-y)**

设置悬浮窗位置。

**[window.getX()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgetx)**

返回悬浮窗位置的X坐标。

**[window.getY()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgety)**

返回悬浮窗位置的Y坐标。

**[window.setSize(width, height)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowsetsizewidth-height)**

设置悬浮窗宽高。

**[window.getWidht()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgetwidht)**

返回悬浮窗宽度。

**[window.getHeight()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgetheight)**

返回悬浮窗高度。

**[window.close()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowclose)**

关闭悬浮窗。如果悬浮窗已经是关闭状态，则此函数将不执行任何操作。

被关闭后的悬浮窗不能再显示。

**[window.exitOnClose()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowexitonclose)**

使悬浮窗被关闭时自动结束脚本运行。

**[FloatyRawWindow](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=floatyrawwindow)**

原始悬浮窗对象，可通过`window.{id}`获取悬浮窗界面上的元素。例如, 悬浮窗window上一个控件的id为aaa, 那么`window.aaa`即可获取到该控件，类似于u

**[window.setTouchable(touchable)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowsettouchabletouchable)**

设置是否可触摸，ture：则接受触摸，false：点击事件直接传递给下层，穿透悬浮窗

**[window.setPosition(x, y)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowsetpositionx-y-1)**

设置悬浮窗位置。

**[window.getX()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgetx-1)**

返回悬浮窗位置的X坐标。

**[window.getY()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgety-1)**

返回悬浮窗位置的Y坐标。

**[window.setSize(width, height)](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowsetsizewidth-height-1)**

设置悬浮窗宽高。

特别地，如果设置为-1，则为占满全屏；设置为-2则为根据悬浮窗内容大小而定

**[window.getWidht()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgetwidht-1)**

返回悬浮窗宽度。

**[window.getHeight()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowgetheight-1)**

返回悬浮窗高度。

**[window.close()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowclose-1)**

关闭悬浮窗。如果悬浮窗已经是关闭状态，则此函数将不执行任何操作。

被关闭后的悬浮窗不能再显示。

**[window.exitOnClose()](https://hyb1996.github.io/AutoJs-Docs/#/floaty?id=windowexitonclose-1)**

使悬浮窗被关闭时自动结束脚本运行。



## 文件系统

files模块提供了一些常见的文件处理，包括文件读写，移动，复制，删除等。

一次性的文件读写可以直接使用`files.read()`, `files.write()`, `files.append()`等方便的函数，但如果需要频繁读写或随机读写，则使用`open()`函数打开一个文件对象来操作文件，并在操作完毕后调用`close()`函数关闭文件。

**[files.isFile(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesisfilepath)**

返回路径path是否为文件

**[files.isDir(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesisdirpath)**

返回路径path是否是文件夹

**[files.isEmptyDir(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesisemptydirpath)**

返回文件夹path是否为空文件夹。如果该路径并非文件夹，则直接返回`false`。

**[files.join(parent, child)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesjoinparent-child)**

- `parent` {string} 父目录路径
- `child` {string} 子路径
- 返回 {string}

连接两个路径并返回，例如`files.join("/sdcard/", "1.txt")`返回"/sdcard/1.txt"。

**[files.create(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filescreatepath)**

创建一个文件或文件夹并返回是否创建成功。如果文件已经存在，则直接返回`false`。

**[files.createWithDirs(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filescreatewithdirspath)**

创建一个文件或文件夹并返回是否创建成功。如果文件所在文件夹不存在，则先创建他所在的一系列文件夹。如果文件已经存在，则直接返回`false`。

**[files.exists(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesexistspath)**

返回在路径path处的文件是否存在。

**[files.ensureDir(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesensuredirpath)**

确保路径path所在的文件夹存在。如果该路径所在文件夹不存在，则创建该文件夹。

例如对于路径"/sdcard/Download/ABC/1.txt"，如果/Download/文件夹不存在，则会先创建Download，再创建ABC文件夹。

**files.read(path[, encoding = "utf-8"\])](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesreadpath-encoding-quotutf-8quot)**

- `path` {string} 路径
- `encoding` {string} 字符编码，可选，默认为utf-8
- 返回 {string}

读取文本文件path的所有内容并返回。如果文件不存在，则抛出`FileNotFoundException`。

**[files.readBytes(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesreadbytespath)**

读取文件path的所有内容并返回一个字节数组。如果文件不存在，则抛出`FileNotFoundException`。

注意，该数组是Java的数组，不具有JavaScript数组的forEach, slice等函数。

**files.write(path, text[, encoding = "utf-8"\])](https://hyb1996.github.io/AutoJs-Docs/#/files?id=fileswritepath-text-encoding-quotutf-8quot)**

- `path` {string} 路径
- `text` {string} 要写入的文本内容
- `encoding` {string} 字符编码

把text写入到文件path中。如果文件存在则覆盖，不存在则创建。

**[files.writeBytes(path, bytes)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=fileswritebytespath-bytes)**

把bytes写入到文件path中。如果文件存在则覆盖，不存在则创建。

**files.append(path, text[, encoding = 'utf-8'\])](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesappendpath-text-encoding-39utf-839)**

- `path` {string} 路径
- `text` {string} 要写入的文本内容
- `encoding` {string} 字符编码

把text追加到文件path的末尾。如果文件不存在则创建。

**files.appendBytes(path, text[, encoding = 'utf-8'\])](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesappendbytespath-text-encoding-39utf-839)**

把bytes追加到文件path的末尾。如果文件不存在则创建。

**[files.copy(fromPath, toPath)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filescopyfrompath-topath)**

- `fromPath` {string} 要复制的原文件路径
- `toPath` {string} 复制到的文件路径
- 返回 {boolean}

复制文件，返回是否复制成功。例如`files.copy("/sdcard/1.txt", "/sdcard/Download/1.txt")`。

**[files.move(fromPath, toPath)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesmovefrompath-topath)**

- `fromPath` {string} 要移动的原文件路径
- `toPath` {string} 移动到的文件路径
- 返回 {boolean}

移动文件，返回是否移动成功。例如`files.move("/sdcard/1.txt", "/sdcard/Download/1.txt")`会把1.txt文件从sd卡根目录移动到Download文件夹。

**[files.rename(path, newName)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesrenamepath-newname)**

命名文件，并返回是否重命名成功。例如`files.rename("/sdcard/1.txt", "2.txt")`。

**[files.renameWithoutExtension(path, newName)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesrenamewithoutextensionpath-newname)**

重命名文件，不包含拓展名，并返回是否重命名成功。例如`files.rename("/sdcard/1.txt", "2")`会把"1.txt"重命名为"2.txt"。

**[files.getName(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesgetnamepath)**

返回文件的文件名。例如`files.getName("/sdcard/1.txt")`返回"1.txt"。

**[files.getNameWithoutExtension(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesgetnamewithoutextensionpath)**

返回不含拓展名的文件的文件名。例如`files.getName("/sdcard/1.txt")`返回"1"。

**[files.getExtension(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesgetextensionpath)**

返回文件的拓展名。例如`files.getExtension("/sdcard/1.txt")`返回"txt"。

**[files.remove(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesremovepath)**

删除文件或**空文件夹**，返回是否删除成功。

**[files.removeDir(path)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesremovedirpath)**

删除文件夹，如果文件夹不为空，则删除该文件夹的所有内容再删除该文件夹，返回是否全部删除成功。

**[files.getSdcardPath()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filesgetsdcardpath)**

返回SD卡路径。所谓SD卡，即外部存储器。

**[files.cwd()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filescwd)**

返回脚本的"当前工作文件夹路径"。该路径指的是，如果脚本本身为脚本文件，则返回这个脚本文件所在目录；否则返回`null`获取其他设定路径。

例如，对于脚本文件"/sdcard/脚本/1.js"运行`files.cwd()`返回"/sdcard/脚本/"。

**[files.path(relativePath)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=filespathrelativepath)**

返回相对路径对应的绝对路径。例如`files.path("./1.png")`，如果运行这个语句的脚本位于文件夹"/sdcard/脚本/"中，则返回`"/sdcard/脚本/1.png"`。

**files.listDir(path[, filter\])](https://hyb1996.github.io/AutoJs-Docs/#/files?id=fileslistdirpath-filter)**

- `path` {string} 路径
- `filter` {Function} 过滤函数，可选。接收一个`string`参数（文件名），返回一个`boolean`值。

列出文件夹path下的满足条件的文件和文件夹的名称的数组。如果不加filter参数，则返回所有文件和文件夹。

**open(path[, mode = "r", encoding = "utf-8", bufferSize = 8192\])](https://hyb1996.github.io/AutoJs-Docs/#/files?id=openpath-mode-quotrquot-encoding-quotutf-8quot-buffersize-8192)**

- `path` {string} 文件路径，例如"/sdcard/1.txt"。
- `mode`{string} 文件打开模式，包括:
  - "r": 只读文本模式。该模式下只能对文件执行**文本**读取操作。
  - "w": 只写文本模式。该模式下只能对文件执行**文本**覆盖写入操作。
  - "a": 附加文本模式。该模式下将会把写入的文本附加到文件末尾。
  - "rw": 随机读写文本模式。该模式下将会把写入的文本附加到文件末尾。
    目前暂不支持二进制模式，随机读写模式。
- `encoding` {string} 字符编码。
- `bufferSize` {number} 文件读写的缓冲区大小。

打开一个文件。根据打开模式返回不同的文件对象。包括：

- "r": 返回一个ReadableTextFile对象。
- "w", "a": 返回一个WritableTextFile对象。

对于"w"模式，如果文件并不存在，则会创建一个，已存在则会清空该文件内容；其他模式文件不存在会抛出FileNotFoundException。

**[ReadableTextFile](https://hyb1996.github.io/AutoJs-Docs/#/files?id=readabletextfile)**

可读文件对象

**[ReadableTextFile.read()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=readabletextfileread)**

返回该文件剩余的所有内容的字符串。

**[ReadableTextFile.read(maxCount)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=readabletextfilereadmaxcount)**

读取该文件接下来最长为maxCount的字符串并返回。即使文件剩余内容不足maxCount也不会出错。

**[ReadableTextFile.readline()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=readabletextfilereadline)**

读取一行并返回（不包含换行符）。

**[ReadableTextFile.readlines()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=readabletextfilereadlines)**

读取剩余的所有行，并返回它们按顺序组成的字符串数组。

**[close()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=close)**

关闭该文件。

**打开一个文件不再使用时务必关闭**

**[PWritableTextFile](https://hyb1996.github.io/AutoJs-Docs/#/files?id=pwritabletextfile)**

可写文件对象。

**[PWritableTextFile.write(text)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=pwritabletextfilewritetext)**

把文本内容text写入到文件中。

**[PWritableTextFile.writeline(line)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=pwritabletextfilewritelineline)**

把文本line写入到文件中并写入一个换行符。

**[PWritableTextFile.writelines(lines)](https://hyb1996.github.io/AutoJs-Docs/#/files?id=pwritabletextfilewritelineslines)**

把很多行写入到文件中....

**[PWritableTextFile.flush()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=pwritabletextfileflush)**

把缓冲区内容输出到文件中。

**[PWritableTextFile.close()](https://hyb1996.github.io/AutoJs-Docs/#/files?id=pwritabletextfileclose)**

关闭文件。同时会被缓冲区内容输出到文件。

**打开一个文件写入后，不再使用时务必关闭，否则文件可能会丢失**



## HTTP

http提供了一些进行http请求的函数

**http.get(url[, options, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/http?id=httpgeturl-options-callback)**

- `url` {string} 请求的URL地址，需要以"[http://"或"https://"开头。如果url没有以"http://"开头，则默认为"http://"。](http://xn--""https-mz8v//"开头。如果url没有以"http://"开头，则默认为"http://"。)
- `options` {Object} 请求选项。参见[http.request()][]。
- `callback` {Function} 回调

**http.post(url, data[, options, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/http?id=httpposturl-data-options-callback)**

- `url` {string} 请求的URL地址，需要以"[http://"或"https://"开头。如果url没有以"http://"开头，则默认为"http://"。](http://xn--""https-mz8v//"开头。如果url没有以"http://"开头，则默认为"http://"。)
- `data` {string} | {Object} POST数据。
- `options` {Object} 请求选项。
- `callback` {Function} 回调，其参数是一个[Response][]对象。如果不加回调参数，则该请求将阻塞、同步地执行。

**http.postJson(url[, data, options, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/http?id=httppostjsonurl-data-options-callback)**

- `url` {string} 请求的URL地址，需要以"[http://"或"https://"开头。如果url没有以"http://"开头，则默认为"http://"。](http://xn--""https-mz8v//"开头。如果url没有以"http://"开头，则默认为"http://"。)
- `data` {Object} POST数据。
- `options` {Object} 请求选项。
- `callback` {Function} 回调，其参数是一个[Response][]对象。如果不加回调参数，则该请求将阻塞、同步地执行。

**http.postMultipart(url, files[, options, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/http?id=httppostmultiparturl-files-options-callback)**

- `url` {string} 请求的URL地址，需要以"[http://"或"https://"开头。如果url没有以"http://"开头，则默认为"http://"。](http://xn--""https-mz8v//"开头。如果url没有以"http://"开头，则默认为"http://"。)
- `files` {Object} POST数据。
- `options` {Object} 请求选项。
- `callback` {Function} 回调，其参数是一个`Response`对象。如果不加回调参数，则该请求将阻塞、同步地执行。

**http.request(url[, options, callback\])](https://hyb1996.github.io/AutoJs-Docs/#/http?id=httprequesturl-options-callback)**

- `url` {string} 请求的URL地址，需要以"[http://"或"https://"开头。如果url没有以"http://"开头，则默认为"http://"。](http://xn--""https-mz8v//"开头。如果url没有以"http://"开头，则默认为"http://"。)
- `options` {Object} 请求选项。参见[http.buildRequest()][]。
- `callback` {Function} 回调，其参数是一个[Response][]对象。如果不加回调参数，则该请求将阻塞、同步地执行。

**[Response](https://hyb1996.github.io/AutoJs-Docs/#/http?id=response)**

HTTP请求的响应。

**[Response.statusCode](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responsestatuscode)**

当前响应的HTTP状态码。例如200(OK), 404(Not Found)等。

**[Response.statusMessage](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responsestatusmessage)**

当前响应的HTTP状态信息。例如"OK", "Bad Request", "Forbidden"。

**[Response.headers](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responseheaders)**

当前响应的HTTP头部信息。该对象的键是响应头名称，值是各自的响应头值。 所有响应头名称都是小写的(吗)。

**[Response.body](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responsebody)**

当前响应的内容。他有以下属性和函数：

- bytes() {Array} 以字节数组形式返回响应内容
- string() {string} 以字符串形式返回响应内容
- json() {Object} 把响应内容作为JSON格式的数据并调用JSON.parse，返回解析后的对象
- contentType {string} 当前响应的内容类型

**[Response.request](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responserequest)**

- {Request} 当前响应所对应的请求。参见[Request][]。

**[Response.url](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responseurl)**

- {number} 当前响应所对应的请求URL。

**[Response.method](https://hyb1996.github.io/AutoJs-Docs/#/http?id=responsemethod)**

- {string} 当前响应所对应的HTTP请求的方法。例如"GET", "POST", "PUT"等。



## 图片与颜色

**colors**

在Auto.js中有两种方式表示一个颜色

一种是使用字符串"#AARRGGBB"或"#RRGGBB"，其中AA表示透明度。

另一种是使用一个16进制的"32位整数" 0xAARRGGBB 来表示一个颜色，例如 `0xFF112233`表示颜色"#112233", `0x11223344`表示颜色"#11223344"。

可以通过`colors.toString()`把颜色整数转换为字符串，通过`colors.parseColor()`把颜色字符串解析为颜色整数。

*注意：js中是最后两位数表示透明度，Auto中是前两位表示透明度*

**[colors.toString(color)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorstostringcolor)**

返回颜色值的字符串，格式为 "#AARRGGBB"。

**[colors.red(color)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsredcolor)**

返回颜色color的R通道的值，范围0~255.

**[colors.green(color)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsgreencolor)**

返回颜色color的G通道的值，范围0~255.

**[colors.blue(color)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsbluecolor)**

返回颜色color的B通道的值，范围0~255.

**[colors.alpha(color)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsalphacolor)**

返回颜色color的Alpha通道的值，范围0~255.

**[colors.rgb(red, green, blue)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsrgbred-green-blue)**

返回这些颜色通道构成的整数颜色值。Alpha通道将是255（不透明）。

**[colors.argb(alpha, red, green, blue)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsargbalpha-red-green-blue)**

返回这些颜色通道构成的整数颜色值。

**[colors.parseColor(colorStr)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsparsecolorcolorstr)**

返回颜色的整数值。

**colors.isSimilar(color2, color2[[, threshold, algorithm\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsissimilarcolor2-color2-threshold-algorithm)**

- `color1` {number} | {string} 颜色值1
- `color1` {number} | {string} 颜色值2
- `threshold` {number} 颜色相似度临界值，默认为4。取值范围为0~255。这个值越大表示允许的相似程度越小，如果这个值为0，则两个颜色相等时该函数才会返回true。
- `algorithm`{string} 颜色匹配算法，默认为"diff", 包括:
  - "diff": 差值匹配。与给定颜色的R、G、B差的绝对值之和小于threshold时匹配。
  - "rgb": rgb欧拉距离相似度。与给定颜色color的rgb欧拉距离小于等于threshold时匹配。
  - "rgb+": 加权rgb欧拉距离匹配([LAB Delta E](https://en.wikipedia.org/wiki/Color_difference))。
  - "hs": hs欧拉距离匹配。hs为HSV空间的色调值。
- 返回 {Boolean}

返回两个颜色是否相似。

**[colors.equals(color1, color2)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsequalscolor1-color2)**

返回两个颜色是否相等。**注意该函数会忽略Alpha通道的值进行比较*。

**[colors.BLACK](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsblack)**

黑色，颜色值 #FF000000

**[colors.DKGRAY](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsdkgray)**

深灰色，颜色值 #FF444444

**[colors.GRAY](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsgray)**

灰色，颜色值 #FF888888

**[colors.LTGRAY](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsltgray)**

亮灰色，颜色值 #FFCCCCCC

**[colors.WHITE](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorswhite)**

白色，颜色值 #FFFFFFFF

**[colors.RED](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsred)**

红色，颜色值 #FFFF0000

**[colors.GREEN](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsgreen)**

绿色，颜色值 #FF00FF00

**[colors.BLUE](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsblue)**

蓝色，颜色值 #FF0000FF

**[colors.YELLOW](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsyellow)**

黄色，颜色值 #FFFFFF00

**[colors.CYAN](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorscyan)**

青色，颜色值 #FF00FFFF

**[colors.MAGENTA](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorsmagenta)**

品红色，颜色值 #FFFF00FF

**[colors.TRANSPARENT](https://hyb1996.github.io/AutoJs-Docs/#/images?id=colorstransparent)**

透明，颜色值 #00000000



###  [图片处理](https://hyb1996.github.io/AutoJs-Docs/#/images?id=图片处理)

**[images.read(path)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesreadpath)**

读取在路径path的图片文件并返回一个image对象，如果文件不存在或者文件无法解码则返回null

**[images.load(url)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesloadurl)**

加载在地址URL的网络图片并返回一个Image对象。如果地址不存在或者图片无法解码则返回null。

**[images.copy(img)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagescopyimg)**

复制一张图片并返回新的副本。该函数会完全复制img对象的数据。

**images.save(image, path[, format = "png", quality = 100\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagessaveimage-path-format-quotpngquot-quality-100)**

- `image` {Image} 图片
- `path` {string} 路径
- `format`{string} 图片格式，可选的值为:
  - `png`
  - `jpeg`/`jpg`
  - `webp`
- `quality` {number} 图片质量，为0~100的整数值

把图片image以PNG格式保存到path中。如果文件不存在会被创建；文件存在会被覆盖。

```js
//把图片压缩为原来的一半质量并保存
var img = images.read("/sdcard/1.png");
images.save(img, "/sdcard/1.jpg", "jpg", 50);
app.viewFile("/sdcard/1.jpg");
```

**[images.fromBase64(base64)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfrombase64base64)**

解码Base64数据并返回解码后的图片Image对象。如果base64无法解码则返回`null`。

**images.toBase64(img[, format = "png", quality = 100\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagestobase64img-format-quotpngquot-quality-100)**

把图片编码为base64数据并返回。

**[images.fromBytes(bytes)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfrombytesbytes)**

解码字节数组bytes并返回解码后的图片Image对象。如果bytes无法解码则返回`null`。

**images.toBytes(img[, format = "png", quality = 100\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagestobytesimg-format-quotpngquot-quality-100)**

把图片编码为字节数组并返回。

**[images.clip(img, x, y, w, h)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesclipimg-x-y-w-h)**

- `img` {Image} 图片
- `x` {number} 剪切区域的左上角横坐标
- `y` {number} 剪切区域的左上角纵坐标
- `w` {number} 剪切区域的宽度
- `h` {number} 剪切区域的高度
- 返回 {Image}

从图片img的位置(x, y)处剪切大小为w * h的区域，并返回该剪切区域的新图片。

```js
var src = images.read("/sdcard/1.png");
var clip = images.clip(src, 100, 100, 400, 400);
images.save(clip, "/sdcard/clip.png");
```

**images.resize(img, size[, interpolation\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesresizeimg-size-interpolation)**

调整图片大小，并返回调整后的图片。例如把图片放缩为200*300：`images.resize(img, [200, 300])`。

**images.scale(img, fx, fy[, interpolation\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesscaleimg-fx-fy-interpolation)**

放缩图片，并返回放缩后的图片。例如把图片变成原来的一半：`images.scale(img, 0.5, 0.5)`。

**images.rotate(img, degress[, x, y\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesrotateimg-degress-x-y)**

- `img` {Image} 图片
- `degress` {number} 旋转角度。
- `x` {number} 旋转中心x坐标，默认为图片中点
- `y` {number} 旋转中心y坐标，默认为图片中点
- 返回 {Image}

将图片逆时针旋转degress度，返回旋转后的图片对象。

例如逆时针旋转90度为`images.rotate(img, 90)`。

**images.concat(img1, image2[, direction\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesconcatimg1-image2-direction)**

- `img1` {Image} 图片1
- `img2` {Image} 图片2
- direction {string} 连接方向，默认为"RIGHT"，可选的值有：
  - `LEFT` 将图片2接到图片1左边
  - `RIGHT` 将图片2接到图片1右边
  - `TOP` 将图片2接到图片1上边
  - `BOTTOM` 将图片2接到图片1下边
- 返回 {Image}

连接两张图片，并返回连接后的图像。如果两张图片大小不一致，小的那张将适当居中。

**[images.grayscale(img)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesgrayscaleimg)**

灰度化图片，并返回灰度化后的图片。

**image.threshold(img, threshold, maxVal[, type\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagethresholdimg-threshold-maxval-type)**

- `img` {Image} 图片
- `threshold` {number} 阈值
- `maxVal` {number} 最大值
- `type` {string} 阈值化类型，默认为"BINARY"，参见[ThresholdTypes](https://docs.opencv.org/3.4.4/d7/d1b/group__imgproc__misc.html#gaa9e58d2860d4afa658ef70a9b1115576), 可选的值:
  - `BINARY`
  - `BINARY_INV`
  - `TRUNC`
  - `TOZERO`
  - `TOZERO_INV`
  - `OTSU`
  - `TRIANGLE`
- 返回 {Image}

将图片阈值化，并返回处理后的图像。可以用这个函数进行图片二值化。例如：`images.threshold(img, 100, 255, "BINARY")`，这个代码将图片中大于100的值全部变成255，其余变成0，从而达到二值化的效果。如果img是一张灰度化图片，这个代码将会得到一张黑白图片。

**[images.adaptiveThreshold(img, maxValue, adaptiveMethod, thresholdType, blockSize, C)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesadaptivethresholdimg-maxvalue-adaptivemethod-thresholdtype-blocksize-c)**

- `img` {Image} 图片
- `maxValue` {number} 最大值
- `adaptiveMethod`{string} 在一个邻域内计算阈值所采用的算法，可选的值有：
  - `MEAN_C` 计算出领域的平均值再减去参数C的值
  - `GAUSSIAN_C` 计算出领域的高斯均值再减去参数C的值
- `thresholdType`{string} 阈值化类型，可选的值有：
  - `BINARY`
  - `BINARY_INV`
- `blockSize` {number} 邻域块大小
- `C` {number} 偏移值调整量
- 返回 {Image}

对图片进行自适应阈值化处理，并返回处理后的图像。

**images.cvtColor(img, code[, dstCn\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagescvtcolorimg-code-dstcn)**

- `img` {Image} 图片

- `code`{string} 颜色空间转换的类型，可选的值有一共有205个（参见

  ColorConversionCodes

  ），这里只列出几个：

  - `BGR2GRAY` BGR转换为灰度
  - `BGR2HSV` BGR转换为HSV
  - ``

- `dstCn` {number} 目标图像的颜色通道数量，如果不填写则根据其他参数自动决定。

- 返回 {Image}

对图像进行颜色空间转换，并返回转换后的图像。

**[images.inRange(img, lowerBound, upperBound)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesinrangeimg-lowerbound-upperbound)**

- `img` {Image} 图片
- `lowerBound` {string} | {number} 颜色下界
- `upperBound` {string} | {number} 颜色下界
- 返回 {Image}

将图片二值化，在lowerBound~upperBound范围以外的颜色都变成0，在范围以内的颜色都变成255。

例如`images.inRange(img, "#000000", "#222222")`。

**[images.interval(img, color, interval)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesintervalimg-color-interval)**

- `img` {Image} 图片
- `color` {string} | {number} 颜色值
- `interval` {number} 每个通道的范围间隔
- 返回 {Image}

将图片二值化，在color-interval ~ color+interval范围以外的颜色都变成0，在范围以内的颜色都变成255。这里对color的加减是对每个通道而言的。

例如`images.interval(img, "#888888", 16)`，每个通道的颜色值均为0x88，加减16后的范围是[0x78, 0x98]，因此这个代码将把#787878~#989898的颜色变成#FFFFFF，而把这个范围以外的变成#000000。

**images.blur(img, size[, anchor, type\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesblurimg-size-anchor-type)**

对图像进行模糊（平滑处理），返回处理后的图像。

**[images.medianBlur(img, size)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesmedianblurimg-size)**

对图像进行中值滤波，返回处理后的图像。

**images.gaussianBlur(img, size[, sigmaX, sigmaY, type\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesgaussianblurimg-size-sigmax-sigmay-type)**

对图像进行高斯模糊，返回处理后的图像。

**[images.matToImage(mat)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesmattoimagemat)**

把Mat对象转换为Image对象。



### [找图找色](https://hyb1996.github.io/AutoJs-Docs/#/images?id=找图找色)

**images.requestScreenCapture([landscape\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesrequestscreencapturelandscape)**

- `landscape` {boolean} 布尔值， 表示将要执行的截屏是否为横屏。如果landscape为false, 则表示竖屏截图; true为横屏截图。

向系统申请屏幕截图权限，返回是否请求成功。

第一次使用该函数会弹出截图权限请求，建议选择“总是允许”。

这个函数只是申请截图权限，并不会真正执行截图，真正的截图函数是`captureScreen()`。

该函数在截图脚本中只需执行一次，而无需每次调用`captureScreen()`都调用一次。

**如果不指定landscape值，则截图方向由当前设备屏幕方向决定**，因此务必注意执行该函数时的屏幕方向。

建议在本软件界面运行该函数，在其他软件界面运行时容易出现一闪而过的黑屏现象。

该函数也可以作为全局函数使用。

**[images.captureScreen()](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagescapturescreen)**

截取当前屏幕并返回一个Image对象。没有截图权限时执行该函数会抛出SecurityException。

该函数不会返回null，两次调用可能返回相同的Image对象。这是因为设备截图的更新需要一定的时间，短时间内（一般来说是16ms）连续调用则会返回同一张截图。

截图需要转换为Bitmap格式，从而该函数执行需要一定的时间(0~20ms)。

另外在requestScreenCapture()执行成功后需要一定时间后才有截图可用，因此如果立即调用captureScreen()，会等待一定时间后(一般为几百ms)才返回截图。

例子:

```js
//请求横屏截图
requestScreenCapture(true);
//截图
var img = captureScreen();
//获取在点(100, 100)的颜色值
var color = images.pixel(img, 100, 100);
//显示该颜色值
toast(colors.toString(color));
```

该函数也可以作为全局函数使用。

**[images.captureScreen(path)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagescapturescreenpath)**

截取当前屏幕并以PNG格式保存到path中。如果文件不存在会被创建；文件存在会被覆盖。

该函数不会返回任何值。该函数也可以作为全局函数使用。

**[images.pixel(image, x, y)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagespixelimage-x-y)**

返回图片image在点(x, y)处的像素的ARGB值。

**[images.findColor(image, color, options)](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfindcolorimage-color-options)**

在图片中寻找颜色color。找到时返回找到的点Point，找不到时返回null。

**images.findColorInRegion(img, color, x, y[, width, height, threshold\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfindcolorinregionimg-color-x-y-width-height-threshold)**

区域找色。该函数也可以作为全局函数使用。

**images.findColorEquals(img, color[, x, y, width, height\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfindcolorequalsimg-color-x-y-width-height)**

在图片img指定区域中找到颜色和color完全相等的某个点，并返回该点的左边；如果没有找到，则返回`null`。

找色区域通过`x`, `y`, `width`, `height`指定，如果不指定找色区域，则在整张图片中寻找。

该函数也可以作为全局函数使用。

**images.findMultiColors(img, firstColor, colors[, options\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfindmulticolorsimg-firstcolor-colors-options)**

多点找色。整张图片都找不到时返回`null`

如果要指定找色区域，则在options中指定，例如:

```js
var p = images.findMultiColors(img, "#123456", [[10, 20, "#ffffff"], [30, 40, "#000000"]], {
    region: [0, 960, 1080, 960]
});
```

**images.detectsColor(image, color, x, y[, threshold = 16, algorithm = "diff"\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesdetectscolorimage-color-x-y-threshold-16-algorithm-quotdiffquot)**

返回图片image在位置(x, y)处是否匹配到颜色color。用于检测图片中某个位置是否是特定颜色。

一个判断微博客户端的某个微博是否被点赞过的例子：

```js
requestScreenCapture();
//找到点赞控件
var like = id("ly_feed_like_icon").findOne();
//获取该控件中点坐标
var x = like.bounds().centerX();
var y = like.bounds().centerY();
//截图
var img = captureScreen();
//判断在该坐标的颜色是否为橙红色
if(images.detectsColor(img, "#fed9a8", x, y)){
    //是的话则已经是点赞过的了，不做任何动作
}else{
    //否则点击点赞按钮
    like.click();
}
```

**images.findImage(img, template[, options\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfindimageimg-template-options)**

找图。在大图片img中查找小图片template的位置（模块匹配），找到时返回位置坐标(Point)，找不到时返回null。

**images.findImageInRegion(img, template, x, y[, width, height, threshold\])](https://hyb1996.github.io/AutoJs-Docs/#/images?id=imagesfindimageinregionimg-template-x-y-width-height-threshold)**

在大图片中搜索小图片，并返回搜索结果MatchingResult。该函数可以用于找图时找出多个位置，可以通过max参数控制最大的结果数量。也可以对匹配结果进行排序、求最值等操作。



## 画布

canvas提供了使用画布进行2D画图的支持，可用于简单的小游戏开发或者图片编辑。使用canvas可以轻松地在一张图片或一个界面上绘制各种线与图形。

canvas的坐标系为平面直角坐标系，以屏幕左上角为原点，屏幕上边为x轴正方向，屏幕左边为y轴正方向。例如分辨率为1920*1080的屏幕上，画一条从屏幕左上角到屏幕右下角的线段为:

```js
canvas.drawLine(0, 0, 1080, 1920, paint);
```

canvas的绘制依赖于画笔Paint, 通过设置画笔的粗细、颜色、填充等可以改变绘制出来的图形。例如绘制一个红色实心正方形为：

```js
var paint = new Paint();
//设置画笔为填充，则绘制出来的图形都是实心的
paint.setStyle(Paint.STYLE.FILL);
//设置画笔颜色为红色
paint.setColor(colors.RED);
//绘制一个从坐标(0, 0)到坐标(100, 100)的正方形
canvas.drawRect(0, 0, 100, 100, paint);
```

如果要绘制正方形的边框，则通过设置画笔的Style来实现：

```js
var paint = new Paint();
//设置画笔为描边，则绘制出来的图形都是轮廓
paint.setStyle(Paint.STYLE.STROKE);
//设置画笔颜色为红色
paint.setColor(colors.RED);
//绘制一个从坐标(0, 0)到坐标(100, 100)的正方形
canvas.drawRect(0, 0, 100, 100, paint);
```

结合画笔canvas可以绘制基本图形、图片等。



## 按键模拟

按键模拟部分提供了一些模拟物理按键的全局函数，包括Home、音量键、照相键等，有的函数依赖于无障碍服务，有的函数依赖于root权限。

一般来说，以大写字母开头的函数都依赖于root权限。执行此类函数时，如果没有root权限，则函数执行后没有效果，并会在控制台输出一个警告。

**[back()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=back)**

模拟按下返回键。返回是否执行成功。 此函数依赖于无障碍服务。

**[home()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=home)**

模拟按下Home键。返回是否执行成功。 此函数依赖于无障碍服务。

**[powerDialog()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=powerdialog)**

弹出电源键菜单。返回是否执行成功。 此函数依赖于无障碍服务。

**[notifications()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=notifications)**

拉出通知栏。返回是否执行成功。 此函数依赖于无障碍服务。

**[quickSettings()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=quicksettings)**

示快速设置(下拉通知栏到底)。返回是否执行成功。 此函数依赖于无障碍服务。

**[recents()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=recents)**

显示最近任务。返回是否执行成功。 此函数依赖于无障碍服务。

**[splitScreen()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=splitscreen)**

分屏。返回是否执行成功。 此函数依赖于无障碍服务, 并且需要系统自身功能的支持。

**[Home()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=home-1)**

模拟按下Home键。 此函数依赖于root权限。

**[Back()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=back-1)**

模拟按下返回键。 此函数依赖于root权限。

**[Power()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=power)**

模拟按下电源键。 此函数依赖于root权限。

**[Menu()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=menu)**

模拟按下菜单键。 此函数依赖于root权限。

**[VolumeUp()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=volumeup)**

按下音量上键。 此函数依赖于root权限。

**[VolumeDown()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=volumedown)**

按键音量上键。 此函数依赖于root权限。

**[Camera()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=camera)**

模拟按下照相键。

**[Up()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=up)**

模拟按下物理按键上。 此函数依赖于root权限。

**[Down()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=down)**

模拟按下物理按键下。 此函数依赖于root权限。

**[Left()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=left)**

模拟按下物理按键左。 此函数依赖于root权限。

**[Right()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=right)**

模拟按下物理按键右。 此函数依赖于root权限。

**[OK()](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=ok)**

模拟按下物理按键确定。 此函数依赖于root权限。

**[Text(text)](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=texttext)**

- text {string} 要输入的文字，只能为英文或英文符号 输入文字text。例如`Text("aaa");`

**[KeyCode(code)](https://hyb1996.github.io/AutoJs-Docs/#/keys?id=keycodecode)**

- code {number} | 要按下的按键的数字代码或名称。参见下表。 模拟物理按键。例如`KeyCode(29)`和`KeyCode("KEYCODE_A")`是按下A键。



## 多媒体

media模块提供多媒体编程的支持。目前仅支持音乐播放和媒体文件扫描。后续会结合UI加入视频播放等功能。

需要注意是，使用该模块播放音乐时是在后台异步播放的，在脚本结束后会自动结束播放，因此可能需要插入诸如`sleep()`的语句来使脚本保持运行。例如：

```js
//播放音乐
media.playMusic("/sdcard/1.mp3");
//让音乐播放完
sleep(media.getMusicDuration());
```

**[media.scanFile(path)](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediascanfilepath)**

扫描路径path的媒体文件，将它加入媒体库中；或者如果该文件以及被删除，则通知媒体库移除该文件。

媒体库包括相册、音乐库等，因此该函数可以用于把某个图片文件加入相册。

```js
//请求截图
requestScreenCapture(false);
//截图
var im = captureScreen();
var path = "/sdcard/screenshot.png";
//保存图片
im.saveTo(path);
//把图片加入相册
media.scanFile(path);
```

**media.playMusic(path[, volume, looping\])](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediaplaymusicpath-volume-looping)**

- `path` {string} 音乐文件路径
- `volume` {number} 播放音量，为0~1的浮点数，默认为1
- `looping` {boolean} 是否循环播放，如果looping为`true`则循环播放，默认为`false`

播放音乐文件path。该函数不会显示任何音乐播放界面。如果文件不存在或者文件不是受支持的音乐格式，则抛出`UncheckedIOException`异常。

**[media.musicSeekTo(msec)](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediamusicseektomsec)**

- `msec` {number} 毫秒数，表示音乐进度

把当前播放进度调整到时间msec的位置。如果当前没有在播放音乐，则调用函数没有任何效果。

**[media.pauseMusic()](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediapausemusic)**

暂停音乐播放。如果当前没有在播放音乐，则调用函数没有任何效果。

**[media.resumeMusic()](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediaresumemusic)**

继续音乐播放。如果当前没有播放过音乐，则调用该函数没有任何效果。

**[media.stopMusic()](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediastopmusic)**

停止音乐播放。如果当前没有在播放音乐，则调用函数没有任何效果。

**[media.isMusicPlaying()](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediaismusicplaying)**

返回当前是否正在播放音乐。

**[media.getMusicDuration()](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediagetmusicduration)**

返回当前音乐的时长。单位毫秒。

**[media.getMusicCurrentPosition()](https://hyb1996.github.io/AutoJs-Docs/#/media?id=mediagetmusiccurrentposition)**

返回当前音乐的播放进度(已经播放的时间)，单位毫秒。



## 模块

Auto.js 有一个简单的模块加载系统。 在 Auto.js 中，文件和模块是一一对应的（每个文件被视为一个独立的模块）。







## 基于控件的操作

选择屏幕上的控件，获取其信息或对其进行操作。对于一般软件而言，基于控件的操作对不同机型有很好的兼容性；但是对于游戏而言，由于游戏界面并不是由控件构成，无法采用本章节的方法，也无法使用本章节的函数。有关游戏脚本的编写，请参考《基于坐标的操作》。

基于控件的操作依赖于无障碍服务，因此最好在脚本开头使用`auto()`函数来确保无障碍服务已经启用。如果运行到某个需要权限的语句无障碍服务并没启动，则会抛出异常并跳转到无障碍服务界面。这样的用户体验并不好，因为需要重新运行脚本，后续会加入等待无障碍服务启动并让脚本继续运行的函数。

您也可以在脚本开头使用`"auto";`表示这个脚本需要无障碍服务，但是不推荐这种做法，因为这个标记必须在脚本的最开头(前面不能有注释或其他语句、空格等)，我们推荐使用`auto()`函数来确保无障碍服务已启用。

### auto([mode])

- `fast` 快速模式。该模式下会启用控件缓存，从而选择器获取屏幕控件更快。对于需要快速的控件操作的脚本可以使用该模式，一般脚本则没有必要使用该函数。
- `normal` 正常模式，默认。

检查无障碍服务是否已经启用，**如果没有启用则抛出异常并跳转到无障碍服务启用界面**

**[auto.waitFor()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=autowaitfor)**

检查无障碍服务是否已经启用，**如果没有启用则跳转到无障碍服务界面，并等待启动；已启用后脚本会继续运行。**

**[auto.setMode(mode)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=autosetmodemode)**

设置无障碍模式为mode



#### SimpleActionAutomator

SimpleActionAutomator提供了一些模拟简单操作的函数，例如点击文字、模拟按键等。这些函数可以直接作为全局函数使用。

**click(text[, i\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=clicktext-i)**

- `text` {string} 要点击的文本
- `i` {number} 如果相同的文本在屏幕中出现多次，则i表示要点击第几个文本, i从0开始计算

返回是否点击成功。当屏幕中并未包含该文本，或者该文本所在区域不能点击时返回false，否则返回true。

当不指定参数i时则会尝试点击屏幕上出现的所有文字text并返回是否全部点击成功。

**[click(left, top, bottom, right)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=clickleft-top-bottom-right)**

**注意，该函数一般只用于录制的脚本中使用，在自己写的代码中使用该函数一般不要使用该函数。**

有些按钮或者部件是图标而不是文字（例如发送朋友圈的照相机图标以及QQ下方的消息、联系人、动态图标），这时不能通过`click(text, i)`来点击，可以通过描述图标所在的区域来点击。left, bottom, top, right描述的就是点击的区域。

**longClick(text[, i\]))](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=longclicktext-i)**

返回是否点击成功。当屏幕中并未包含该文本，或者该文本所在区域不能点击时返回false，否则返回true。

当不指定参数i时则会尝试点击屏幕上出现的所有文字text并返回是否全部长按成功。

**scrollUp([[i\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=scrollupi)**

- `i` {number} 要滑动的控件序号

找到第i+1个可滑动控件上滑或**左滑**。返回是否操作成功。屏幕上没有可滑动的控件时返回false。

另外不加参数时`scrollUp()`会寻找面积最大的可滑动的控件上滑或左滑，例如微信消息列表等。

参数为一个整数i时会找到第i + 1个可滑动控件滑动。例如`scrollUp(0)`为滑动第一个可滑动控件。

**scrollDown([i\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=scrolldowni)**

下滑或**右滑**

**setText([i, \]text)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=settexti-text)**

- i {number} 表示要输入的为第i + 1个输入框
- text {string} 要输入的文本

返回是否输入成功。当找不到对应的文本框时返回false。

不加参数i则会把所有输入框的文本都置为text。例如`setText("测试")`。

这里的输入文本的意思是，把输入框的文本置为text，而不是在原来的文本上追加。

**input([i, \]text)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=inputi-text)**

- i {number} 表示要输入的为第i + 1个输入框
- text {string} 要输入的文本

返回是否输入成功。当找不到对应的文本框时返回false。

不加参数i则会把所有输入框的文本追加内容text。例如`input("测试")`。



#### UiSelector

UiSelector即选择器，用于通过各种条件选取屏幕上的控件，再对这些控件进行点击、长按等动作。这里需要先简单介绍一下控件和界面的相关知识。

**[selector()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=selector)**

创建一个新的选择器。但一般情况不需要使用该函数，因为可以直接用相应条件的语句创建选择器。

**[UiSelector.text(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectortextstr)**

为当前选择器附加控件"text等于字符串str"的筛选条件。

**[UiSelector.textContains(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectortextcontainsstr)**

为当前选择器附加控件"text需要包含字符串str"的筛选条件。

**[UiSelector.textStartsWith(prefix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectortextstartswithprefix)**

为当前选择器附加控件"text需要以prefix开头"的筛选条件。

**[UiSelector.textEndsWith(suffix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectortextendswithsuffix)**

为当前选择器附加控件"text需要以suffix结束"的筛选条件。

**[UiSelector.textMatches(reg)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectortextmatchesreg)**

为当前选择器附加控件"text需要满足正则表达式reg"的条件。

**[UiSelector.desc(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectordescstr)**

为当前选择器附加控件"desc等于字符串str"的筛选条件。

**[UiSelector.descContains(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectordesccontainsstr)**

为当前选择器附加控件"desc需要包含字符串str"的筛选条件。

**[UiSelector.descStartsWith(prefix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectordescstartswithprefix)**

为当前选择器附加控件"desc需要以prefix开头"的筛选条件。

**[UiSelector.descEndsWith(suffix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectordescendswithsuffix)**

为当前选择器附加控件"desc需要以suffix结束"的筛选条件。

**[UiSelector.descMatches(reg)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectordescmatchesreg)**

为当前选择器附加控件"desc需要满足正则表达式reg"的条件。

**[UiSelector.id(resId)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoridresid)**

为当前选择器附加"id等于resId"的筛选条件。

**[UiSelector.idContains(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoridcontainsstr)**

为当前选择器附加控件"id包含字符串str"的筛选条件。比较少用。

**[UiSelector.idStartsWith(prefix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoridstartswithprefix)**

为当前选择器附加"id需要以prefix开头"的筛选条件。比较少用。

**[UiSelector.idEndsWith(suffix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoridendswithsuffix)**

为当前选择器附加"id需要以suffix结束"的筛选条件。比较少用。

**[UiSelector.idMatches(reg)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoridmatchesreg)**

附加id需要满足正则表达式。

**[UiSelector.className(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorclassnamestr)**

为当前选择器附加控件"className等于字符串str"的筛选条件。

控件的className(类名)表示一个控件的类别，例如文本控件的类名为android.widget.TextView。

如果一个控件的类名以"android.widget."开头，则可以省略这部分，例如文本控件可以直接用`className("TextView")`的选择器。

- `android.widget.TextView` 文本控件
- `android.widget.ImageView` 图片控件
- `android.widget.Button` 按钮控件
- `android.widget.EditText` 输入框控件
- `android.widget.AbsListView` 列表控件
- `android.widget.LinearLayout` 线性布局
- `android.widget.FrameLayout` 帧布局
- `android.widget.RelativeLayout` 相对布局
- `android.widget.RelativeLayout` 相对布局
- `android.support.v7.widget.RecyclerView` 通常也是列表控件

**[UiSelector.classNameContains(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorclassnamecontainsstr)**

为当前选择器附加控件"className需要包含字符串str"的筛选条件。

**[UiSelector.classNameStartsWith(prefix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorclassnamestartswithprefix)**

为当前选择器附加控件"className需要以prefix开头"的筛选条件。

**[UiSelector.classNameEndsWith(suffix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorclassnameendswithsuffix)**

为当前选择器附加控件"className需要以suffix结束"的筛选条件。

**[UiSelector.classNameMatches(reg)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorclassnamematchesreg)**

为当前选择器附加控件"className需要满足正则表达式reg"的条件。

**[UiSelector.packageName(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorpackagenamestr)**

为当前选择器附加控件"packageName等于字符串str"的筛选条件。

控件的packageName表示控件所属界面的应用包名。例如微信的包名为"com.tencent.mm", 那么微信界面的控件的packageName为"com.tencent.mm"。

要查看一个应用的包名，可以用函数`app.getPackageName()`获取，例如`toast(app.getPackageName("微信"))`。

**[UiSelector.packageNameContains(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorpackagenamecontainsstr)**

为当前选择器附加控件"packageName需要包含字符串str"的筛选条件。

**[UiSelector.packageNameStartsWith(prefix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorpackagenamestartswithprefix)**

为当前选择器附加控件"packageName需要以prefix开头"的筛选条件。

**[UiSelector.packageNameEndsWith(suffix)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorpackagenameendswithsuffix)**

为当前选择器附加控件"packageName需要以suffix结束"的筛选条件。

**[UiSelector.packageNameMatches(reg)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorpackagenamematchesreg)**

为当前选择器附加控件"packageName需要满足正则表达式reg"的条件。

**[UiSelector.bounds(left, top, right, buttom)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorboundsleft-top-right-buttom)**

一个控件的bounds属性为这个控件在屏幕上显示的范围。我们可以用这个范围来定位这个控件。尽管用这个方法定位控件对于静态页面十分准确，却无法兼容不同分辨率的设备；同时对于列表页面等动态页面无法达到效果，因此使用不推荐该选择器。

注意参数的这四个数字不能随意填写，必须精确的填写控件的四个边界才能找到该控件。例如，要点击QQ主界面的右上角加号，我们用布局分析查看该控件的属性，如下图：

可以看到bounds属性为(951, 67, 1080, 196)，此时使用代码`bounds(951, 67, 1080, 196).clickable().click()`即可点击该控件。

**[UiSelector.boundsInside(left, top, right, buttom)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorboundsinsideleft-top-right-buttom)**

这个条件用于限制选择器在某一个区域选择控件。

**[UiSelector.boundsContains(left, top, right, buttom)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorboundscontainsleft-top-right-buttom)**

这个条件用于限制控件的范围必须包含所给定的范围。

**[UiSelector.drawingOrder(order)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectordrawingorderorder)**

为当前选择器附加控件"drawingOrder等于order"的条件。

drawingOrder为一个控件在父控件中的绘制顺序，通常可以用于区分同一层次的控件。

但该属性在Android 7.0以上才能使用。

**UiSelector.clickable([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorclickableb-true)**

- `b` {Boolean} 表示控件是否可点击

为当前选择器附加控件是否可点击的条件。但并非所有clickable为false的控件都真的不能点击，这取决于控件的实现。对于自定义控件(例如显示类名为android.view.View的控件)很多的clickable属性都为false都却能点击。

**UiSelector.longClickable([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorlongclickableb-true)**

为当前选择器附加控件是否可长按的条件。

**UiSelector.checkable([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorcheckableb-true)**

为当前选择器附加控件是否可勾选的条件。勾选通常是对于勾选框而言的，例如图片多选时左上角通常有一个勾选框。

**UiSelector.selected([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorselectedb-true)**

为当前选择器附加控件是否已选中的条件。被选中指的是，例如QQ聊天界面点击下方的"表情按钮"时，会出现自己收藏的表情，这时"表情按钮"便处于选中状态，其selected属性为true。

**UiSelector.enabled([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorenabledb-true)**

为当前选择器附加控件是否已启用的条件。大多数控件都是启用的状态(enabled为true)，处于“禁用”状态通常是灰色并且不可点击。

**UiSelector.scrollable([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorscrollableb-true)**

为当前选择器附加控件是否可滑动的条件。滑动包括上下滑动和左右滑动。

**UiSelector.editable([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoreditableb-true)**

为当前选择器附加控件是否可编辑的条件。一般来说可编辑的控件为输入框(EditText)，但不是所有的输入框(EditText)都可编辑。

**UiSelector.multiLine([b = true\])](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectormultilineb-true)**

为当前选择器附加控件是否文本或输入框控件是否是多行显示的条件。

**[UiSelector.findOne()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorfindone)**

根据条件对控件搜索，**返回找到的第一个控件，当屏幕内容发生变化时会重新寻找。找不到就保持阻塞**

**[UiSelector.findOne(timeout)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorfindonetimeout)**

根据条件对控件搜索，**规定时间内如果找到控件就返回控件，没有就返回null**

**[UiSelector.findOnce()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorfindonce)**

根据条件对控件搜索，**找到控件就返回，没有就返回null**

**[UiSelector.findOnce(i)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorfindoncei)**

根据条件对控件搜索，**返回第 i + 1 个符合条件的控件，没有就返回null**

**[UiSelector.find()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorfind)**

根据条件对控件搜索，**找到所有满足条件的内容，返回集合，没有找到返回空集合**

**[UiSelector.untilFind()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectoruntilfind)**

根据条件对控件搜索，**至少找到一个满足条件的内容，找不到就保持阻塞**

**[UiSelector.exists()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorexists)**

根据条件对控件搜索，**找到返回ture否false**

**[UiSelector.waitFor()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorwaitfor)**

根据条件对控件搜索，**等待屏幕出现符合条件的控件，找不到就保持阻塞**

**[UiSelector.filter(f)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiselectorfilterf)**

为当前选择器附加自定义的过滤条件。



#### [UiObject](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobject)

UiObject表示一个控件，可以通过这个对象获取到控件的属性，也可以对控件进行点击、长按等操作。

**[UiObject.click()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectclick)**

点击该控件，并返回是否点击成功。

**[UiObject.longClick()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectlongclick)**

长按该控件，并返回是否点击成功。

**[UiObject.setText(text)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectsettexttext)**

设置输入框控件的文本内容，并返回是否设置成功。

**[UiObject.copy()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectcopy)**

对输入框文本的选中内容进行复制，并返回是否操作成功。

**[UiObject.cut()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectcut)**

对输入框文本的选中内容进行剪切，并返回是否操作成功。

该函数只能用于输入框控件，并且当前输入框控件有选中的文本。可以通过`setSelection()`函数来设置输入框选中的内容。

**[UiObject.paste()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectpaste)**

对输入框控件进行粘贴操作，把剪贴板内容粘贴到输入框中，并返回是否操作成功。

**[UiObject.setSelection(start, end)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectsetselectionstart-end)**

对输入框控件设置选中的文字内容，并返回是否操作成功。

**[UiObject.scrollForward()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectscrollforward)**

对控件执行向前滑动的操作，并返回是否操作成功。

**[UiObject.scrollBackward()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectscrollbackward)**

对控件执行向后滑动的操作，并返回是否操作成功。

**[UiObject.select()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectselect)**

对控件执行"选中"操作，并返回是否操作成功。"选中"和`isSelected()`的属性相关，但该操作十分少用。

**[UiObject.collapse()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectcollapse)**

对控件执行折叠操作，并返回是否操作成功。

**[UiObject.expand()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectexpand)**

对控件执行操作，并返回是否操作成功。

**[UiObject.show()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectshow)**

对集合中所有控件执行显示操作，并返回是否全部操作成功。

**[UiObject.scrollUp()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectscrollup)**

对集合中所有控件执行向上滑的操作，并返回是否全部操作成功。

**[UiObject.scrollDown()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectscrolldown)**

对集合中所有控件执行向下滑的操作，并返回是否全部操作成功。

**[UiObject.scrollLeft()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectscrollleft)**

对集合中所有控件执行向左滑的操作，并返回是否全部操作成功。

**[UiObject.scrollRight()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uiobjectscrollright)**

对集合中所有控件执行向右滑的操作，并返回是否全部操作成功。

**[children()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=children)**

返回该控件的所有子控件组成的控件集合。可以用于遍历一个控件的子控件

**[childCount()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=childcount)**

返回子控件数目。

**[child(i)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=childi)**

返回第i+1个子控件。如果i>=控件数目或者小于0，则抛出异常。

**[parent()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=parent)**

返回该控件的父控件。如果该控件没有父控件，返回`null`。

**[bounds()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=bounds)**

返回控件在屏幕上的范围，其值是一个[Rect](https://hyb1996.github.io/AutoJs-Docs/widgets-based-automation.html#widgets_based_automation_rect)对象。

**[boundsInParent()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=boundsinparent)**

返回控件在父控件中的范围，其值是一个[Rect](https://hyb1996.github.io/AutoJs-Docs/widgets-based-automation.html#widgets_based_automation_rect)对象。

**[drawingOrder()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=drawingorder)**

返回控件在父控件中的绘制次序。该函数在安卓7.0及以上才有效，7.0以下版本调用会返回0。

**[id()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=id)**

获取控件的id，如果一个控件没有id，则返回`null`。

**[text()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=text)**

获取控件的文本，如果控件没有文本，返回`""`。

**[findByText(str)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=findbytextstr)**

根据文本text在子控件中递归地寻找并返回文本或描述(desc)**包含**这段文本str的控件，返回它们组成的集合。

该函数会在当前控件的子控件，孙控件，曾孙控件...中搜索text或desc包含str的控件，并返回它们组合的集合。

**[findOne(selector)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=findoneselector)**

根据选择器selector在该控件的子控件、孙控件...中搜索符合该选择器条件的控件，并返回找到的第一个控件；如果没有找到符合条件的控件则返回`null`。

**[find(selector)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=findselector)**

根据选择器selector在该控件的子控件、孙控件...中搜索符合该选择器条件的控件，并返回它们组合的集合。



#### [UiCollection](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uicollection)

UiCollection, 控件集合, 通过选择器的`find()`, `untilFind()`方法返回的对象。

**[UiCollection.size()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uicollectionsize)**

返回集合中的控件数。

**[UiCollection.get(i)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uicollectiongeti)**

返回集合中第i+1个控件(UiObject)。

**[UiCollection.each(func)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uicollectioneachfunc)**

遍历集合。

**[empty()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=empty)**

返回控件集合是否为空。

**[nonEmpty()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=nonempty)**

返回控件集合是否非空。

**[UiCollection.find(selector)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uicollectionfindselector)**

根据selector所确定的条件在该控件集合的控件、子控件、孙控件...中找到所有符合条件的控件并返回找到的控件集合。

**[UiCollection.findOne(selector)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=uicollectionfindoneselector)**

根据选择器selector在该控件集合的控件的子控件、孙控件...中搜索符合该选择器条件的控件，并返回找到的第一个控件；如果没有找到符合条件的控件则返回`null`。



#### [Rect](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rect)

`UiObject.bounds()`, `UiObject.boundsInParent()`返回的对象。表示一个长方形(范围)。

**[Rect.left](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectleft)**

长方形左边界的x坐标、

**[Rect.right](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectright)**

长方形右边界的x坐标、

**[Rect.top](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=recttop)**

长方形上边界的y坐标、

**[Rect.bottom](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectbottom)**

长方形下边界的y坐标、

**[Rect.centerX()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectcenterx)**

长方形中点x坐标。

**[Rect.centerY()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectcentery)**

长方形中点y坐标。

**[Rect.width()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectwidth)**

长方形宽度。通常可以作为控件宽度。

**[Rect.height()](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectheight)**

长方形高度。通常可以作为控件高度。

**[Rect.contains(r)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectcontainsr)**

返回是否包含另一个长方形r。包含指的是，长方形r在该长方形的里面(包含边界重叠的情况)。

**[Rect.intersect(r)](https://hyb1996.github.io/AutoJs-Docs/#/widgetsBasedAutomation?id=rectintersectr)**

返回是否和另一个长方形相交。



### 传感器

sensors模块提供了获取手机上的传感器的信息的支持，这些传感器包括距离传感器、光线光感器、重力传感器、方向传感器等。需要指出的是，脚本只能获取传感器的数据，**不能模拟或伪造传感器的数据和事件**，因此诸如模拟摇一摇的功能是无法实现的。

要监听一个传感器时，需要使用`sensors.register()`注册监听器，之后才能开始监听；不需要监听时则调用`sensors.unregister()`注销监听器。在脚本结束时会自动注销所有的监听器。同时，这种监听会使脚本保持运行状态，如果不注销监听器，脚本会一直保持运行状态。



### Shell函数

shell即Unix Shell，在类Unix系统提供与操作系统交互的一系列命令。

很多程序可以用来执行shell命令，例如终端模拟器。



### 本地存储

storages模块提供了保存简单数据、用户配置等的支持。保存的数据除非应用被卸载或者被主动删除，否则会一直保留。

storages支持`number`, `boolean`, `string`等数据类型以及把`Object`, `Array`用`JSON.stringify`序列化存取。

storages保存的数据在脚本之间是共享的，任何脚本只要知道storage名称便可以获取到相应的数据，因此它不能用于敏感数据的储存。 storages无法像Web开发中LocalStorage一样提供根据域名独立的存储，因为脚本的路径随时可能改变。

**[storages.create(name)](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storagescreatename)**

创建一个本地存储并返回一个`Storage`对象。不同名称的本地存储的数据是隔开的，而相同名称的本地存储的数据是共享的。

**[storages.remove(name)](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storagesremovename)**

删除一个本地存储以及他的全部数据。如果该存储不存在，返回false；否则返回true。



#### [Storages](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storages-1)

**Storage.get(key[, defaultValue\])](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storagegetkey-defaultvalue)**

从本地存储中取出键值为key的数据并返回。

如果该存储中不包含该数据，这时若指定了默认值参数则返回默认值，否则返回undefined。

返回的数据可能是任意数据类型，这取决于使用`Storage.put`保存该键值的数据时的数据类型。

**[Storage.put(key, value)](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storageputkey-value)**

把值value保存到本地存储中。value可以是undefined以外的任意数据类型。如果value为undefined则抛出TypeError。

存储的过程实际上是使用JSON.stringify把value转换为字符串再保存，因此value必须是可JSON化的才能被接受。

**[Storage.remove(key)](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storageremovekey)**

移除键值为key的数据。不返回任何值

**[Storage.contains(key)](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storagecontainskey)**

返回该本地存储是否包含键值为key的数据。是则返回true，否则返回false。

**[Storage.clear()](https://hyb1996.github.io/AutoJs-Docs/#/storages?id=storageclear)**

移除该本地存储的所有数据。不返回任何值。



### 多线程

threads模块提供了多线程支持，可以启动新线程来运行脚本。

脚本主线程会等待所有子线程执行完成后才停止执行，因此如果子线程中有死循环，请在必要的时候调用`exit()`来直接停止脚本或`threads.shutDownAll()`来停止所有子线程。

通过`threads.start()`启动的所有线程会在脚本被强制停止时自动停止。

**[threads.start(action)](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsstartaction)**

启动一个新线程并执行action。

**[threads.shutDownAll()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsshutdownall)**

停止所有通过`threads.start()`启动的子线程。

**[threads.currentThread()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadscurrentthread)**

返回当前线程。

**[threads.disposable()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsdisposable)**

新建一个Disposable对象，用于等待另一个线程的某个一次性结果。

**threads.atomic([initialValue\])](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsatomicinitialvalue)**

新建一个整数原子变量。

**[threads.lock()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadslock)**



#### [Thread](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=thread)

线程对象，`threads.start()`返回的对象，用于获取和控制线程的状态，与其他线程交互等。

Thread对象提供了和timers模块一样的API，例如`setTimeout()`, `setInterval()`等，用于在该线程执行相应的定时回调，从而使线程之间可以直接交互。

**[Thread.interrupt()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadinterrupt)**

中断线程运行。

**Thread.join([timeout\])](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadjointimeout)**

等待线程执行完成。如果timeout为0，则会一直等待直至该线程执行完成；否则最多等待timeout毫秒的时间。

**[isAlive()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=isalive)**

返回线程是否存活。如果线程仍未开始或已经结束，返回`false`; 如果线程已经开始或者正在运行中，返回`true`。

**[waitFor()](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=waitfor)**

等待线程开始执行。调用`threads.start()`以后线程仍然需要一定时间才能开始执行，因此调用此函数会等待线程开始执行；如果线程已经处于执行状态则立即返回。

**Thread.setTimeout(callback, delay[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsettimeoutcallback-delay-args)**

区别在于, 该定时器会在该线程执行。如果当前线程仍未开始执行或已经执行结束，则抛出`IllegalStateException`。

**Thread.setInterval(callback, delay[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsetintervalcallback-delay-args)**

区别在于, 该定时器会在该线程执行。如果当前线程仍未开始执行或已经执行结束，则抛出`IllegalStateException`。

**Thread.setImmediate(callback[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadsetimmediatecallback-args)**

区别在于, 该定时器会在该线程执行。如果当前线程仍未开始执行或已经执行结束，则抛出`IllegalStateException`。

**[Thread.clearInterval(id)](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadclearintervalid)**

区别在于, 该定时器会在该线程执行。如果当前线程仍未开始执行或已经执行结束，则抛出`IllegalStateException`。

**[Thread.clearTimeout(id)](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadcleartimeoutid)**

区别在于, 该定时器会在该线程执行。如果当前线程仍未开始执行或已经执行结束，则抛出`IllegalStateException`。

**[Thread.clearImmediate(id)](https://hyb1996.github.io/AutoJs-Docs/#/threads?id=threadclearimmediateid)**

区别在于, 该定时器会在该线程执行。如果当前线程仍未开始执行或已经执行结束，则抛出`IllegalStateException`。



### 定时器

timers 模块暴露了一个全局的 API，用于在某个未来时间段调用调度函数。 因为定时器函数是全局的，所以使用该 API 无需调用 timers。

Auto.js 中的计时器函数实现了与 Web 浏览器提供的定时器类似的 API，除了它使用了一个不同的内部实现，它是基于 Android Looper-Handler消息循环机制构建的。其实现机制与Node.js比较相似。

**setInterval(callback, delay[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/timers?id=setintervalcallback-delay-args)**

- `callback` {Function} 当定时器到点时要调用的函数。
- `delay` {number} 调用 callback 之前要等待的毫秒数。
- `...args` {any} 当调用 callback 时要传入的可选参数。

预定每隔 delay 毫秒重复执行的 callback。 返回一个用于 clearInterval() 的 id。

当 delay 小于 0 时，delay 会被设为 0。

**setTimeout(callback, delay[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/timers?id=settimeoutcallback-delay-args)**

预定在 delay 毫秒之后执行的单次 callback。 返回一个用于 clearTimeout() 的 id。

callback 可能不会精确地在 delay 毫秒被调用。 Auto.js 不能保证回调被触发的确切时间，也不能保证它们的顺序。 回调会在尽可能接近所指定的时间上调用。

当 delay 小于 0 时，delay 会被设为 0。

**setImmediate(callback[, ...args\])](https://hyb1996.github.io/AutoJs-Docs/#/timers?id=setimmediatecallback-args)**

预定立即执行的 callback，它是在 I/O 事件的回调之后被触发。 返回一个用于 clearImmediate() 的 id。

当多次调用 setImmediate() 时，callback 函数会按照它们被创建的顺序依次执行。 每次事件循环迭代都会处理整个回调队列。 如果一个立即定时器是被一个正在执行的回调排入队列的，则该定时器直到下一次事件循环迭代才会被触发。

setImmediate()、setInterval() 和 setTimeout() 方法每次都会返回表示预定的计时器的id。 它们可用于取消定时器并防止触发。

**[clearInterval(id)](https://hyb1996.github.io/AutoJs-Docs/#/timers?id=clearintervalid)**

取消一个由 setInterval() 创建的循环定时任务。

**[clearTimeout(id)](https://hyb1996.github.io/AutoJs-Docs/#/timers?id=cleartimeoutid)**

取消一个由 setTimeout() 创建的定时任务。

**[clearImmediate(id)](https://hyb1996.github.io/AutoJs-Docs/#/timers?id=clearimmediateid)**

取消一个由 setImmediate() 创建的 Immediate 对象。



### 用户界面

ui模块提供了编写用户界面的支持。

带有ui的脚本的的最前面必须使用`"ui";`指定ui模式，否则脚本将不会以ui模式运行。

字符串"ui"的前面可以有注释、空行和空格**[v4.1.0新增]**，但是不能有其他代码。

不加单位默认dp，可以使用px，mm，in。

**vertical**

垂直布局

**horizontal**

水平布局

**w**

宽度

**h**

高度

**id**

id选择器

**[gravit](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=gravity)**

显示位置，类似定位

这些属性是可以组合的，例如`gravity="right|bottom"`的View他的内容会在右下角。

**[layout_gravit](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=layout_gravity)**

View在布局中的"重力"，用于决定View本身在他的**父布局**的位置，可以设置的值和gravity属性相同。注意把这个属性和gravity属性区分开来。

**[margin](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=margin)**

margin为View和其他View的间距，即外边距。

**[marginLeft](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=marginleft)**

**[marginRight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=marginright)**

**[marginTop](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=margintop)**

**[marginBottom](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=marginbottom)**

**[padding](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=padding)**

View和他的自身内容的间距，也就是内边距。

**[paddingLeft](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=paddingleft)**

**[paddingRight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=paddingright)**

**[paddingTop](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=paddingtop)**

**[paddingBottom](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=paddingbottom)**

**[bg](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=bg)**

View的背景。其值可以是一个链接或路径指向的图片，或者RGB格式的颜色，或者其他背景。

**[alpha](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=alpha)**

View的透明度，其值是一个0~1之间的小数，0表示完全透明，1表示完全不透明。例如`alpha="0.5"`表示半透明。

**[foreground](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=foreground)**

View的前景。前景即在一个View的内容上显示的内容，可能会覆盖掉View本身的内容。其值和属性bg的值类似。

**[minHeight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=minheight)**

View的最小高度。该值不总是生效的，取决于其父布局是否有足够的空间容纳。

**[minWidth](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=minwidth)**

View的最小宽度。该值不总是生效的，取决于其父布局是否有足够的空间容纳。

**[visbility](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=visbility)**

View的可见性，该属性可以决定View是否显示出来。其值可以为：

- `gone` 不可见。
- `visible` 可见。默认情况下View都是可见的。
- `invisible` 不可见，但仍然占用位置。

**[rotation](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=rotation)**

View的旋转角度。通过该属性可以让这个View顺时针旋转一定的角度。例如`rotation="90"`可以让他顺时针旋转90度。

如果要设置旋转中心，可以通过`transformPivotX`, `transformPivotY`属性设置。默认的旋转中心为View的中心。

**[transformPivotX](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=transformpivotx)**

View的变换中心坐标x。用于View的旋转、放缩等变换的中心坐标。例如`transformPivotX="10"`。

该坐标的坐标系以View的左上角为原点。也就是x值为变换中心到View的左边的距离。

**[ransformPivotY](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=transformpivoty)**

View的变换中心坐标y。用于View的旋转、放缩等变换的中心坐标。例如`transformPivotY="10"`。

该坐标的坐标系以View的左上角为原点。也就是y值为变换中心到View的上边的距离。



### [style](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=style)

设置View的样式。不同控件有不同的可选的内置样式。具体参见各个控件的说明。

需要注意的是，style属性只支持安卓5.1及其以上。



### [文本控件: text](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=文本控件-text)

**[text](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=text)**

设置文本的内容。例如`text="一段文本"`。

**[textColor](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=textcolor)**

设置字体的颜色，可以是RGB格式的颜色(例如#ff00ff)

**[textSize](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=textsize)**

设置字体的大小，单位一般是sp。

**[textStyle](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=textstyle)**

设置字体的样式，比如斜体、粗体等。可选的值为：

- bold 加粗字体
- italic 斜体
- normal 正常字体

可以用或("|")把他们组合起来，比如粗斜体为"bold|italic"。

**[lines](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=lines)**

设置文本控件的行数。即使文本内容没有达到设置的行数，控件也会留出相应的宽度来显示空白行；如果文本内容超出了设置的行数，则超出的部分不会显示。

**[maxLines](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=maxlines)**

设置文本控件的最大行数。

**[typeface](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=typeface)**

设置字体。可选的值为：

- `normal` 正常字体
- `sans` 衬线字体
- `serif` 非衬线字体
- `monospace` 等宽字体

**[ellipsize](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=ellipsize)**

设置文本的省略号位置。文本的省略号会在文本内容超出文本控件时显示。可选的值为：

- `end` 在文本末尾显示省略号
- `marquee` 跑马灯效果，文本将滚动显示
- `middle` 在文本中间显示省略号
- `none` 不显示省略号
- `start` 在文本开头显示省略号

**[ems](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=ems)**

当设置该属性后,TextView显示的字符长度（单位是em）,超出的部分将不显示，或者根据ellipsize属性的设置显示省略号。

**[autoLink](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=autolink)**

控制是否自动找到url和电子邮件地址等链接，并转换为可点击的链接。默认值为“none”。

设置该值可以让文本中的链接、电话等变成可点击状态。

可选的值为以下的值以其通过或("|")的组合：

- `all` 匹配所有连接、邮件、地址、电话
- `email` 匹配电子邮件地址
- `map` 匹配地图地址
- `none` 不匹配 (默认)
- `phone` 匹配电话号码
- `web` 匹配URL地址

示例：`<text autoLink="web|phone" text="百度: http://www.baidu.com 电信电话: 10000"/>`



### [按钮控件: button](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=按钮控件-button)

按钮控件是一个特殊的文本控件，因此所有文本控件的函数的属性都适用于按钮控件。

除此之外，按钮控件有一些内置的样式，通过`style`属性设置，包括：

- Widget.AppCompat.Button.Colored 带颜色的按钮
- Widget.AppCompat.Button.Borderless 无边框按钮
- Widget.AppCompat.Button.Borderless.Colored 带颜色的无边框按钮

这些样式的具体效果参见"示例/界面控件/按钮控件.js"。

例如：`<button style="Widget.AppCompat.Button.Colored" text="漂亮的按钮"/>`



### [输入框控件: input](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=输入框控件-input)

输入框控件也是一个特殊的文本控件，因此所有文本控件的函数的属性和函数都适用于按钮控件。输入框控件有自己的属性和函数，要查看所有这些内容，阅读[EditText](http://www.zhdoc.net/android/reference/android/widget/EditText.html)。

对于一个输入框控件，我们可以通过text属性设置他的内容，通过lines属性指定输入框的行数；在代码中通过`getText()`函数获取输入的内容。

**[hint](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=hint)**

输入提示。这个提示会在输入框为空的时候显示出来。

**[textColorHint](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=textcolorhint)**

指定输入提示的字体颜色。

**[textSizeHint](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=textsizehint)**

指定输入提示的字体大小。

**[inputType](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=inputtype)**

指定输入框可以输入的文本类型。可选的值为以下值及其用"|"的组合:

- `date` 用于输入日期。
- `datetime` 用于输入日期和时间。
- `none` 没有内容类型。此输入框不可编辑。
- `number` 仅可输入数字。
- `numberDecimal` 可以与number和它的其他选项组合，以允许输入十进制数(包括小数)。
- `numberPassword` 仅可输入数字密码。
- `numberSigned` 可以与number和它的其他选项组合，以允许输入有符号的数。
- `phone` 用于输入一个电话号码。
- `text` 只是普通文本。
- `textAutoComplete` 可以与text和它的其他选项结合, 以指定此字段将做自己的自动完成, 并适当地与输入法交互。
- `textAutoCorrect` 可以与text和它的其他选项结合, 以请求自动文本输入纠错。
- `textCapCharacters` 可以与text和它的其他选项结合, 以请求大写所有字符。
- `textCapSentences` 可以与text和它的其他选项结合, 以请求大写每个句子里面的第一个字符。
- `textCapWords` 可以与text和它的其他选项结合, 以请求大写每个单词里面的第一个字符。
- `textEmailAddress` 用于输入一个电子邮件地址。
- `textEmailSubject` 用于输入电子邮件的主题。
- `textImeMultiLine` 可以与text和它的其他选项结合，以指示虽然常规文本视图不应为多行, 但如果可以, 则IME应提供多行支持。
- `textLongMessage` 用于输入长消息的内容。
- `textMultiLine` 可以与text和它的其他选项结合, 以便在该字段中允许多行文本。如果未设置此标志, 则文本字段将被限制为单行。
- `textNoSuggestions` 可以与text及它的其他选项结合, 以指示输入法不应显示任何基于字典的单词建议。
- `textPassword` 用于输入密码。
- `textPersonName` 用于输入人名。
- `textPhonetic` 用于输入拼音发音的文本, 如联系人条目中的拼音名称字段。
- `textPostalAddress` 用于输入邮寄地址。
- `textShortMessage` 用于输入短的消息内容。
- `textUri` 用于输入一个URI。
- `textVisiblePassword` 用于输入可见的密码。
- `textWebEditText` 用于输入在web表单中的文本。
- `textWebEmailAddress` 用于在web表单里输入一个电子邮件地址。
- `textWebPassword` 用于在web表单里输入一个密码。
- `time` 用于输入时间。

**[password](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=password)**

指定输入框输入框是否为密码输入框。默认为`false`。

**[numeric](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=numeric)**

指定输入框输入框是否为数字输入框。默认为`false`。

**[phoneNumber](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=phonenumber)**

输入框输入框是否为电话号码输入框。默认为`false`。

**[digits](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=digits)**

指定输入框可以输入的字符。

**[singleLine](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=singleline)**

指定输入框是否为单行输入框。默认为`false`。您也可以通过`lines="1"`来指定单行输入框。



### [图片控件: img](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=图片控件-img)

图片控件用于显示来自网络、本地或者内嵌数据的图片，并可以指定图片以圆角矩形、圆形等显示。但是不能用于显示gif动态图。

**[src](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=src)**

使用一个Uri指定图片的来源。可以是图片的地址(http://....)，本地路径(file://....)或者base64数据("data:image/png;base64,...")。

如果使用图片地址或本地路径，Auto.js会自动使用适当的缓存来储存这些图片，减少下次加载的时间。

**[tint](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=tint)**

图片着色，其值是一个颜色名称或RGB颜色值。使用该属性会将图片中的非透明区域都涂上同一颜色。可以用于改变图片的颜色。

**[scaleType](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=scaletype)**

控制图片根据图片控件的宽高放缩时的模式。可选的值为：

- `center` 在控件中居中显示图像, 但不执行缩放。
- `centerCrop` 保持图像的长宽比缩放图片, 使图像的尺寸 (宽度和高度) 等于或大于控件的相应尺寸 (不包括内边距padding)并且使图像在控件中居中显示。
- `centerInside` 保持图像的长宽比缩放图片, 使图像的尺寸 (宽度和高度) 小于视图的相应尺寸 (不包括内边距padding)并且图像在控件中居中显示。
- `fitCenter` 保持图像的长宽比缩放图片, 使图片的宽**或**高和控件的宽高相同并使图片在控件中居中显示
- `fitEnd` 保持图像的长宽比缩放图片, 使图片的宽**或**高和控件的宽高相同并使图片在控件中靠右下角显示
- `fitStart` 保持图像的长宽比缩放图片, 使图片的宽**或**高和控件的宽高相同并使图片在控件靠左上角显示
- `fitXY` 使图片和宽高和控件的宽高完全匹配，但图片的长宽比可能不能保持一致
- `matrix` 绘制时使用图像矩阵进行缩放。需要在代码中使用`setImageMatrix(Matrix)`函数才能生效。

默认的scaleType为`fitCenter`；除此之外最常用的是`fitXY`， 他能使图片放缩到控件一样的大小，但图片可能会变形。

**[radius](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=radius)**

图片控件的半径。如果设置为控件宽高的一半并且控件的宽高相同则图片将剪切为圆形显示；否则图片为圆角矩形显示，半径即为四个圆角的半径，也可以通过`radiusTopLeft`, `radiusTopRight`, `radiusBottomLeft`, `radiusBottomRight`等属性分别设置四个圆角的半径。

**[radiusTopLeft](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=radiustopleft)**

图片控件的左上角圆角的半径。

**[radiusTopRight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=radiustopright)**

**[radiusBottomLeft](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=radiusbottomleft)**

**[radiusBottomRight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=radiusbottomright)**

**[borderWidth](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=borderwidth)**

图片控件的边框宽度。用于在图片外面显示一个边框，边框会随着图片控件的外形(圆角等)改变而相应变化。

**[borderColor](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=bordercolor)**

图片控件的边框颜色。

**[circle](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=circle)**

指定该图片控件的图片是否剪切为圆形显示。如果为`true`，则图片控件会使其宽高保持一致(如果宽高不一致，则保持高度等于宽度)并使圆形的半径为宽度的一半。



### [垂直布局: vertical](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=垂直布局-vertical)

垂直布局是一种比较简单的布局，会把在它里面的控件按照垂直方向依次摆放，如下图所示：

垂直布局:

—————

| 控件1 |

| 控件2 |

| 控件3 |

| ............ |

——————



**[layout_weight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=layout_weight)**

垂直布局中的控件可以通过`layout_weight`属性来控制控件高度占垂直布局高度的比例。



### [水平布局: horizontal](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=水平布局-horizontal)

水平布局是一种比较简单的布局，会把在它里面的控件按照水平方向依次摆放，如下图所示： 水平布局: ————————————————————————————

| 控件1 | 控件2 | 控件3 | ... |

————————————————————————————

**[layout_weight](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=layout_weight-1)**

水平布局中也可以使用layout_weight属性来控制子控件的**宽度**占父布局的比例。

**[线性布局: linear](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=线性布局-linear)**

实际上，垂直布局和水平布局都属于线性布局。线性布局有一个orientation的属性，用于指定布局的方向，可选的值为`vertical`和`horizontal`。



**[帧布局: frame](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=帧布局-frame)**

**[相对布局: relative](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=相对布局-relative)**

**[勾选框控件: checkbox](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=勾选框控件-checkbox)**

**[选择框控件: radio](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=选择框控件-radio)**

**[选择框布局: radiogroup](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=选择框布局-radiogroup)**

**[开关控件: switch](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=开关控件-switch)**

**[进度条控件: progressbar](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=进度条控件-progressbar)**

**[拖动条控件: seekbar](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=拖动条控件-seekbar)**

**[下来菜单控件: spinner](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=下来菜单控件-spinner)**

**[时间选择控件: timepicker](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=时间选择控件-timepicker)**

**[日期选择控件: datepicker](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=日期选择控件-datepicker)**

**[浮动按钮控件: fab](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=浮动按钮控件-fab)**

**[标题栏控件: toolbar](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=标题栏控件-toolbar)**

**[卡片: card](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=卡片-card)**

**[抽屉布局: drawer](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=抽屉布局-drawer)**

**[列表: list](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=列表-list)**

**[Tab: tab](https://hyb1996.github.io/AutoJs-Docs/#/ui?id=tab-tab)**
