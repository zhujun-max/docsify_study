### 页面跳转方式
wx.navigateTo(Object)：保留当前页面，跳转到应用内的某个页面，使用 wx.navigateBack 可以返回到原页（新页面入栈）  
wx.redirectTo(Object)：关闭当前页面，跳转到应用内的某个页面（当前页面出栈，新页面入栈）  
wx.switchTab(Object)：跳转到 tabBar 页面，同时关闭其他非 tabBar 页面（非Tab页面全部出栈，只留下新的 Tab 页面）  
wx.navigateBack(Object)：返回上一页面（页面不断出栈）  
wx.reLaunch(Object)：关闭所有页面，打开到应用内的某个页面（页面全部出栈，只留下新的页面）  

### 页面栈
小程序页面栈最多十层，页面栈的层数最多不会超过5层。 


### 小程序中是否存在跨域的问题

+ 小程序中不存在跨域的问题，因为不是浏览器
+ 小程序中需要在管理平台设置对应可访问的授权地址，可以设置多个，最多20个域名设置
+ 只能支持https协议
+ 最大并发数为10个，socket的并发限制为5个

### 优点和缺点是什么
优点：
1. 容易推广。在微信中，小程序拥有众多入口，且微信用户基数大，这些都有助于推广小程序；
2. 使用便捷。微信下拉即可打开小程序列表，点击即可使用小程序，不需要额外的安装操作等；
3. 体验良好。小程序不会像H5页面一样经常出现卡顿、延时、加载慢、权限不足等问题；
4. 成本更低，从开发成本到运营推广成本，小程序的花费仅为APP的十分之一。

缺点：
1. 单个包大小限制为2M，这导致无法开发大型的应用，采用分包最大是20M；
2. 需要像app一样审核上架，这点相对于H5的发布要麻烦一些；
3. 处处受微信限制。例如不能直接分享到朋友圈，涉及到积分，或者虚拟交易的时候，小程序也是不允许的。


### 生命周期
分为应用生命周期和页面生命周期

应用生命周期
onLaunch：小程序初始化完成时触发，全局只触发一次
onShow：小程序启动，或从后台进入前台显示时触发
onHide：小程序从前台进入后台时触发
onError：小程序发生脚本错误，或者 api 调用失败时触发
onPageNotFound：小程序要打开的页面不存在时触发
onUnhandledRejection：小程序有未处理的 Promise 拒绝事件时触发
onThemeChange： 监听系统主题变化

页面生命周期
onLoad：监听页面加载
onShow：监听页面显示
onReady：监听页面初次渲染完成
onHide：监听页面隐藏
onUnload：监听页面卸载
onPullDownRefresh：监听用户下拉动作
onReachBottom：页面上拉触底事件的处理函数
onShareAppMessage：用户点击右上角转发
onPageScroll：监听页面滚动
onResize：监听窗口尺寸变化
onTabItemTap：当前是 tab 页时，点击 tab 时触发


### bindtap和catchtap的区别是什么

bindtap是不会阻止冒泡事件的，catchtap是阻值冒泡的

### webview中的页面怎么跳转回小程序
+ webview中可以利用wx.miniProgram.navigateTo等方式跳转回小程序，跳转方法与小程序一致

+ 跳转回小程序如果通过switchTab等方式进行操作，默认情况是不会重新加载数据，可以尝试如下方式：
    + 利用onShow生命周期钩子函数，跳转之前设置全局变量，在onShow中进行条件判断是否进行业务逻辑操作（减少操作次数，优化性能）
    + 页面重新加载
    ```javascript
        wx.miniProgram.switchTab({
            url: '/pages/index/index'
            success: function(e) {
                var page = getCurrentPages().pop();
                if (page == undefined || page == null) return;
                page.onLoad();
            }
        })
        ```

### 如何获取用户手机号码
+ 目前该接口针对非个人开发者，且完成了认证的小程序开放（不包含海外主体）
+ 在微信小程序管理平台设置->基本信息的微信认证中进行确认，是否已经进行认证，认证过程需要提供公司相关信息，并且涉及到一定费用问题（微信公众平台申请微信认证，需支付300元/次认证费）
+  利用wx.login获取登录凭证code，通过code与开发者服务器交互获取加密后的openId，并将openId与session_key进行服务器数据库信息存储（后台利用nodejs、php、java等操作，具体参见：https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/login/auth.code2Session.html）
+ 利用jsonwebtoken（或者其它加密方式，前后端人员需要确认）对openId进行加密传递回小程序端
+ 利用button进行open-type的类型设置，值为getPhoneNumber，并且需要进行bindgetphonenumber事件绑定
```js
<view class="container">
    <button open-type="getPhoneNumber" bindgetphonenumber="getPhoneNumber">getPhoneNumber</button>
</view>
```
+ 绑定回调getPhoneNumber中可以找到手机加密数据
+ 将加密的openId、encryptedData、iv等数据发送至服务器端
+ 服务器端通过解密openId，查询sesskon_key，获取encryptedData、iv以后（4个内容），需要对加密手机等信息数据进行解密处理
+ 解密介绍以及对应后台程序语言解密算法示例，https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/signature.html#%E5%8A%A0%E5%AF%86%E6%95%B0%E6%8D%AE%E8%A7%A3%E5%AF%86%E7%AE%97%E6%B3%95

### 分包的操作以及如何来计划分包
+ 分包主要包括：使用分包、独立分包、分包预下载
+ 分包：主包添加跳转路径，分包放内容，在app.json配置subpakeages声明项目分包结构。代码包总包大小为20M，单个主包/分包大小不能超过2M。
+ 按照功能划分的打包原则：可以按照功能的划分，拆分成几个分包，当需要用到某个功能时，才加载这个功能对应的分包；公共逻辑、组件放在主包内。
+ 首次启动时，先下载小程序主包，显示主包内的页面；如果进入了某个分包的页面，再下载这个对应分包，下载完毕后，显示分包的页面，
+ 总结：首先配置好打包路径，tabbar页面必须在主包内，各分包之间不能互相调用，能调用的都在主包内

### 一个邮箱可以注册几个小程序？个人、个体工商户和企业分别可以注册几个小程序？
+ 同一个邮箱只能申请注册1个小程序
+ 个人和个体工商户可以注册5个小程序
+ 企业资质可以注册50个小程序

### 小程序排名如何优化？
+ 小程序上线时间越早，排名越靠前
+ 描述中出现完全匹配出现关键词次数越多，排名靠前
+ 标题中关键词出现1次，且整体标题的字数越短，排名靠前
+ 微信小程序用户使用数量越多，排名靠前
+ 小程序的名称作为核心关键词语排名