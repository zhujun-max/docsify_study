### Element

1. element 按需引入，官方文档其实并不是全部的，比如 skeleton,Loading 都没写

2. ElementUI 响应式布局 bug、其中 el-col-sm-0 会导致响应式布局失效。  
   解决方法: 获取 body 宽度，if 判断隐藏元素  
   参考：https://javaforall.cn/190289.html

3. Element 输入框，选择器，有值组件不更新  
   解决方法: this.$forceUpdate()

4. el-image 组件使用本地图片不显示的问题

   ```html
   <!-- 解决方案 -->
   <el-image :src="require('../assets/bg_login.jpeg')"></el-image>
   ```

5. element 数值输入框小数点最后一位，会出现异常情况

### Git

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

### 依赖包

monment 工具库

```js
Date.parse(); //得到的值是以毫秒为单位的，且后三位默认为0，即不具体到毫秒如果想将时间戳转化为日期，moment的参数必须是毫秒为单位的,它就是识别为毫秒的，如果不是的话，会使结果出错

moment().unix(); // 获得的时间戳单位为秒
moment().valueOf(); // 等同于 new Date().getTime() 获得的时间戳单位为毫秒
```

### vue

1. vue 中使用可选链 ?.报错
   一般是没有安装依赖。
   但是 vue 如果低于 2.7 版本。那么在 template 中使用可选链依然会报错，除非升级 vue 到 2.7 并且 node 升级到 14.0.0
   `https://blog.csdn.net/kaimo313/article/details/126731479`

### 其他问题

1. 后端生成的 PDF 附件，文本框显示的数字和字母不会自动换行  
   原因：html 的 p 标签，遇到长数字和字母不会换行  
   解决方案：`style="word-wrap:break-word;word-break:break-all;"`

2. 网页卡死，无响应  
   原因：axios 接口请求失败导致页面卡死问题  
   解决方案：获取错误 catch，在接口错误的时候处理

3. uniapp 从首页点击到视频详情页。视频未加载出来前，点击返回。整个 app 卡死无响应

   1. 视频分段加载
   2. 使用 iframe 播放

4. uniapp 使用 vant 加载不出来 icon。
   内网开发，没有网络，加载不出来字体图片，可以使用 uniapp-icons，但是需要将 uni-icons 放入到 uni-modules 中

5. uniapp 在 image 标签中使用动态地址图片一直在加载不出来
   需要把图片放到 static 静态文件夹中才能加载

