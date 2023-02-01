
## Element
1. element 按需引入，官方文档其实并不是全部的，比如skeleton,Loading都没写 

2. ElementUI响应式布局bug、其中el-col-sm-0会导致响应式布局失效。  
解决方法: 获取body宽度，if判断隐藏元素  
参考：https://javaforall.cn/190289.html

3. Element输入框，选择器，有值组件不更新  
解决方法: this.$forceUpdate()

4. el-image 组件使用本地图片不显示的问题
    ```html
    <!-- 解决方案 -->
    <el-image :src="require('../assets/bg_login.jpeg')"></el-image>
    ```

5. element数值输入框小数点最后一位，会出现异常情况

## Git

1. Failed to connect to github.com port 443     
```js
    //编辑host文件
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

## 依赖包
monment工具库
```js
  Date.parse() //得到的值是以毫秒为单位的，且后三位默认为0，即不具体到毫秒如果想将时间戳转化为日期，moment的参数必须是毫秒为单位的,它就是识别为毫秒的，如果不是的话，会使结果出错
  
  moment().unix() // 获得的时间戳单位为秒
  moment().valueOf() // 等同于 new Date().getTime() 获得的时间戳单位为毫秒
```


## 其他问题
1. 后端生成的PDF附件，文本框显示的数字和字母不会自动换行   
  原因：html的p标签，遇到长数字和字母不会换行    
  解决方案：`style="word-wrap:break-word;word-break:break-all;"`

2. 网页卡死，无响应   
  原因：axios 接口请求失败导致页面卡死问题    
  解决方案：获取错误catch，在接口错误的时候处理