# 项目难点

element 按需引入，官方文档其实并不是全部的，比如skeleton,Loading都没写

ElementUI响应式布局bug、其中中el-col-sm-0会导致响应式布局失效的解决方法
https://javaforall.cn/190289.html

element输入框，选择器，有值组件不更新
this.$forceUpdate()



Failed to connect to github.com port 443 

monment工具库
 - moment().unix() 获得的时间戳单位为秒
 - moment().valueOf() 等同于 new Date().getTime() 获得的时间戳单位为毫秒
 - Date.parse() 得到的值是以毫秒为单位的，且后三位默认为0，即不具体到毫秒如果想将时间戳转化为日期，moment的参数必须是毫秒为单位的,它就是识别为毫秒的，如果不是的话，会使结果出错

