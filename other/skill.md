## cmd命令隐藏窗口运行
```js
@echo off
if "%1"=="h" goto begin
start mshta vbscript:createobject("wscript.shell").run("""%~nx0"" h",0)(window.close)&&exit
:begin
自定义运行的可执行程序的代码放在此处
```
+ 如果要关闭窗口，只能在控制台进行关闭，或者电脑关机。

## 实现前端量子纠缠
