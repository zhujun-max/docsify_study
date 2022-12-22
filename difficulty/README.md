# 项目难点

element 按需引入，官方文档其实并不是全部的，比如skeleton,Loading都没写

ElementUI响应式布局bug、其中中el-col-sm-0会导致响应式布局失效的解决方法
https://javaforall.cn/190289.html

element输入框，选择器，有值组件不更新
this.$forceUpdate()



Failed to connect to github.com port 443 
<!-- 编辑host文件 -->
```js
  # GitHub Start 
  # 192.30.253.112 github.com 
  # 192.30.253.119 gist.github.com
  # 151.101.184.133 assets-cdn.github.com
  # 151.101.184.133 raw.githubusercontent.com
  # 151.101.184.133 gist.githubusercontent.com
  # 151.101.184.133 cloud.githubusercontent.com
  # 151.101.184.133 camo.githubusercontent.com
  151.101.184.133 avatars0.githubusercontent.com
  151.101.184.133 avatars1.githubusercontent.com
  151.101.184.133 avatars2.githubusercontent.com
  151.101.184.133 avatars3.githubusercontent.com
  151.101.184.133 avatars4.githubusercontent.com
  151.101.184.133 avatars5.githubusercontent.com
  151.101.184.133 avatars6.githubusercontent.com
  151.101.184.133 avatars7.githubusercontent.com
  151.101.184.133 avatars8.githubusercontent.com
```

monment工具库
 - moment().unix() 获得的时间戳单位为秒
 - moment().valueOf() 等同于 new Date().getTime() 获得的时间戳单位为毫秒
 - Date.parse() 得到的值是以毫秒为单位的，且后三位默认为0，即不具体到毫秒如果想将时间戳转化为日期，moment的参数必须是毫秒为单位的,它就是识别为毫秒的，如果不是的话，会使结果出错


	
 el-image 组件导致本地图片不显示的问题
 ```vue 
 <!-- 解决方案 -->
  <el-image :src="require('../assets/bg_login.jpeg')"></el-image>
 ```


问题：PDF附件文本框，输入数字和字母不会自动换行
 原因：html的p标签，遇到长数字和字母不会换行
 解决方案：style="word-wrap:break-word;word-break:break-all;"