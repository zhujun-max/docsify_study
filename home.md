
<!-- "欢迎每一位贡献者积极分享您的新知灼见、过往工作中的宝贵经验、精心设计的代码框架，以及创新的组件开发成果。在这里，每一次分享都是对知识的传承与拓展，让我们携手共进，在学习与分享的道路上不断成长，共创更加丰富的知识宝库。"  -->


  <div class="book">
        <div class="cover">
            <span>速成秘籍</span>
        </div>
        <div class="content">
            <p>欲练此功</p>
            <p>必先自宫</p>
        </div>
    </div>
<style>
    @font-face {
        font-family: "STXinwei"; /* 定义字体名 */
        src: url("./STXinwei.ttf"); /* 引入本体字体文件 */
      }
.book{
    margin: 10vh auto;
    width: 300px;
    height: 400px;
    background-color: #fff;
    /* 开启3D效果 */
    transform-style: preserve-3d;
    /* 设置视距 */
    perspective: 2000px;
    /* 设置阴影 */
    box-shadow: inset 300px 0 30px rgba(0,0,0,0.2),
    0 10px 100px rgba(0,0,0,0.3);
    /* 动画过渡 */
    transition: 1s;
}
/* 鼠标移入，阴影变化+旋转 */
.book:hover{
    transform: rotate(-10deg);
    box-shadow: inset 20px 0 30px rgba(0,0,0,0.2),
    0 10px 100px rgba(0,0,0,0.3);
}
.book::before{
    content: "";
    /* 绝对定位 */
    position: absolute;
    left: 0;
    top: -5px;
    width: 100%;
    height: 5px;
    background-color: #0d2a50;
    /* 设置旋转元素的基点位置 */
    transform-origin: bottom;
    /* 沿X轴倾斜-45度 */
    transform: skewX(-45deg);
}
.book::after{
    content: "";
    position: absolute;
    top: 0;
    right: -5px;
    width: 5px;
    height: 100%;
    background-color: #3d5a83;
    transform-origin: left;
    transform: skewY(-45deg);
}
/* 封面 */
.book .cover{
    width: 100%;
    height: 100%;
    background-color: #2a3f5c;
    display: flex;
    justify-content: center;
    align-items: center;
    /* 相对定位 */
    position: relative;
    transform-origin: left;
    transition: 1s;
}
.book .cover span{
    position: absolute;
    right: 30px;
    top: 30px;
    background-color: #fff;
    font-size: 40px;
    font-family: "STXinwei";
    /* 竖向文本 */
    writing-mode: vertical-lr;
    padding: 10px 5px 5px 5px;
    /* 字间距 */
    letter-spacing: 5px;
}
.book:hover .cover{
    transform: rotateY(-135deg);
}
.book .content{
    margin-top: -40px !important;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    font-size: 40px;
    font-family: "STXinwei";
    line-height: 50px;
    letter-spacing: 5px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.book .content span{
    position: absolute;
    bottom:20px;
    right:40px;
    font-size:10px;
}
</style>