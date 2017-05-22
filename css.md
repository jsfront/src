### 以下是常用的代码收集，没有任何技术含量，只是填坑的积累。转载请注明出处，谢谢。

#### 1. css 2.x
- 文字换行
```css
/*强制不换行*/
white-space:nowrap;
/*自动换行*/
word-wrap: break-word;
word-break: normal;
/*强制英文单词断行*/
word-break:break-all;
```

- 两端对齐
```css
text-align:justify;text-justify:inter-ideogra
```

- [去掉Webkit(chrome)浏览器中input(文本框)或textarea的黄色焦点框](http://www.cnblogs.com/niao/archive/2012/09/07/2674511.html)
```css
input,button,select,textarea{ outline:none;}
textarea{ resize:none;}
```

- [去掉chrome记住密码后自动填充表单的黄色背景](http://www.tuicool.com/articles/EZ777n )

- ie6: position:fixed
```css
.fixed-top /* position fixed Top */{position:fixed;bottom:auto;top:0; }
* html .fixed-top /* IE6 position fixed Top */{position:absolute;bottom:auto;top:expression(eval(document.documentElement.scrollTop));}
*html{background-image:url(about:blank);background-attachment:fixed;}
```

- clearfix
```css

.clearfix:before,.clearfix:after{display:table;content:"";}
.clearfix:after{clear:both;}

.clearfix:after{visibility:hidden;display:block;font-size:0;content:" ";clear:both;height:0;}
.clearfix{display:inline-block;}
html[xmlns] .clearfix{display:block;}
* html .clearfix{height:1%;}

.clearfix{*zoom: 1;}
.clearfix:after{clear:both;display:table;content:"";}

.clearfix{overflow:hidden;_zoom:1;}
```
[http://www.daqianduan.com/3606.html](http://www.daqianduan.com/3606.html)

- seperate-table
```css
.tab{border-collapse:separate;border:1px solid #e0e0e0;}
.tab th,.tab td{padding:3px;font-size:12px;background:#f5f9fb;border:1px solid;border-color:#fff #deedf6 #deedf6 #fff;}
.tab th{background:#edf4f0;}
.tab tr.even td{background:#fff;}
```
```html
<table class="tab" width="100%" cellpadding="0" cellspacing="0" border="0">
    <tr>
        <th>111</th>
        <td>222</td>
    </tr>
    <tr>
        <th>111</th>
        <td>222</td>
    </tr>
</table>
```

- min-height: 最小高度兼容代码
```css
.minheight500{min-height:500px;height:auto !important;height:500px;overflow:visible;}
```
- 鼠标不允许点击
```css
cursor:not-allowed;
```
- mac font: osx平台字体优化
```css
font-family:"Hiragino Sans GB","Hiragino Sans GB W3",'微软雅黑';
```

- 文字过多后显示省略号
```css
.ellipsis,.ell{white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
```

#### 2. css 3

- title 换行
```html
&#13;
```

- 关闭 x 符号
```html
&#215;
```

- 投影
```css
.b{box-shadow:inset 1px -1px 0 #f1f1f1;text-shadow:1px 1px 0px #630;}
filter:progid:DXImageTransform.Microsoft.gradient(enabled='true',startColorstr='#99000000',endColorstr='#99000000');background:rgba(0,0,0,.6);

background:rgba(0,0,0,0.5);filter:progid:DXImageTransform.Microsoft.gradient(GradientType=0,startColorstr='#50000000',endColorstr='#50000000')\9;
```
- [search占位](http://www.qianduan.net/search-box-style-custom-webkit.html)
```css
::-webkit-input-placeholder {}
::-moz-input-placeholder {}
input:focus::-webkit-input-placeholder { color: transparent; }
-webkit-appearance:none;  google边框去除
input[type="search"]{-webkit-appearance:textfield;} // 去除chrome默认样式
http://i.wanz.im/2011/02/04/remove_border_from_input_type_search/
http://blog.csdn.net/do_it__/article/details/6789699
line-height: normal; /* for non-ie */
line-height: 22px\9; /* for ie */
```

- [全部浏览器的兼容代码生成](http://www.colorzilla.com/gradient-editor/ )
[CSS 实现 textArea 的 placeholder 换行](http://segmentfault.com/a/1190000000362621)

- 阻止默认事件
```css
pointer-events:none;
```

- [去掉输入框聚焦时候的白色背景](http://ntesmailfetc.blog.163.com/blog/static/20628706120139184457401/)
```css
-webkit-user-modify: read-write-plaintext-only;
```

- [input:focus时input不随软键盘升起而抬高的情况](http://www.cnblogs.com/hongru/archive/2013/02/06/2902938.html)
```css
 :focus{-webkit-tap-highlight-color:rgba(255, 255, 255, 0);
 -webkit-user-modify:read-write-plaintext-only;}
```

- 变灰 gray
```css
html{
    filter: grayscale(100%);
    -webkit-filter: grayscale(100%);
    -moz-filter: grayscale(100%);
    -ms-filter: grayscale(100%);
    -o-filter: grayscale(100%);
    filter: url("data:image/svg+xml;utf8,<svg xmlns=\'http://www.w3.org/2000/svg\'><filter id=\'grayscale\'><feColorMatrix type=\'matrix\' values=\'0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0.3333 0.3333 0.3333 0 0 0 0 0 1 0\'/></filter></svg>#grayscale");
    filter:progid:DXImageTransform.Microsoft.BasicImage(grayscale=1);
    -webkit-filter: grayscale(1);
}
```
- firefox 阻止选中
```css
-moz-user-focus:ignore;-moz-user-input:disabled;-moz-user-select:none;
```
- 箭头
```css
display:block;border:solid transparent;line-height: 0;width:0; height:0;border-top:solid #0288ce;border-width:8px 6px 0 6px;

border-style:solid; border-width:7px; border-color:transparent transparent transparent #ff7020;
position:absolute;top: 0;left: 0;border-width:20px;border-style:solid;border-color:#d1ddde transparent transparent #d1ddde;
```
ie6 bug测试，把border-style设为dashed.

- 取消textarea右下角可拖动手柄
```css
resize:none
```
- 取消chrome form表单的聚焦边框
```css
input,button,select,textarea{outline:none}
textarea{resize:none}
```
- 取消a链接的黄色边框
```css
a{-webkit-tap-highlight-color:rgba(0,0,0,0);}
```
- 取消input,button焦点或点击时蓝色边框
```css
input{outline:none;}
```
- webkit 水平居中
```css
display:-webkit-box;-webkit-box-pack:center; -webkit-box-align: center;
position:absolute; top:50%;left:50%;transform:translate(-50%,-50%);
```
- 取消chrome 搜索x提示
```css
input[type=search]::-webkit-search-decoration,
input[type=search]::-webkit-search-cancel-button,
input[type=search]::-webkit-search-results-button,
input[type=search]::-webkit-search-results-decoration {
    display: none;
}
```
- [chrome取消默认黄色背景](http://stackoverflow.com/questions/2338102/override-browser-form-filling-and-input-highlighting-with-html-css)
```css
input:-webkit-autofill {-webkit-box-shadow: 0 0 0px 1000px white inset;}
input:-webkit-autofill,
textarea:-webkit-autofill,
select:-webkit-autofill {
    -webkit-box-shadow: 0 0 0 1000px white inset;
}
autocomplete="off"
```
- 手机版本网页a标记虚线框问题
```css
a:focus {outline:none;-moz-outline:none;}
```
- 焦点去除背景
```css
-webkit-tap-highlight-color:rgba(255, 255, 255, 0);
-webkit-tap-highlight-color:transparent;  // i.e. Nexus5/Chrome and Kindle Fire HD 7''
```
- placeholder占位符颜色自定义
```css
input:-moz-placeholder {color: #369;}
::-webkit-input-placeholder {color:#369;}
```

- [IOS 禁用高亮](http://hi.barretlee.com/2014/03/31/tap-highlight-in-webview/)
```css
-webkit-tap-highlight-color:rgba(255,0,0,0.5);-webkit-tap-highlight-color:transparent; /* For some Androids */
```

- IOS iframe 滚动 [滚动回弹特效](http://www.cnblogs.com/flash3d/archive/2013/09/28/3343877.html)
```css
-webkit-overflow-scrolling:touch;overflow-y:scroll;
```

- [禁止选中文本](http://www.qianduan.net/introduce-user-select/)
```css
-moz-user-select:none;
-webkit-user-select:none;
-ms-user-select:none;
user-select:none;
```
- [模糊(毛玻璃)效果1](http://www.zhangxinxu.com/wordpress/2013/11/%E5%B0%8Ftip-%E4%BD%BF%E7%94%A8css%E5%B0%86%E5%9B%BE%E7%89%87%E8%BD%AC%E6%8D%A2%E6%88%90%E6%A8%A1%E7%B3%8A%E6%AF%9B%E7%8E%BB%E7%92%83%E6%95%88%E6%9E%9C/)
- [模糊(毛玻璃)效果2](http://mao.li/css3-blur-filter-pratice/)
- [模糊(毛玻璃)逼真效果](http://codepen.io/ariona/pen/geFIK)
```css
.blur {    
    -webkit-filter: blur(10px); /* Chrome, Opera */
       -moz-filter: blur(10px);
        -ms-filter: blur(10px);    
            filter: blur(10px);    
}
```
```html
<img src="mm1.jpg" />
<img src="mm1.jpg" class="blur" />
```

- 显示旋转加载图片，[下拉加载数据](https://github.com/chalecao/chale/blob/master/iscroll.js)
```css
#pullDown .pullDownIcon{display:inline-block;vertical-align:middle;width:40px;height:40px;background:url(https://github.com/chalecao/chale/blob/master/pull-icon%402x.png) 0 0 no-repeat;-webkit-background-size:40px 80px;background-size:40px 80px;-webkit-transition-property:-webkit-transform;-webkit-transition-duration:250ms}
#pullDown .pullDownIcon{-webkit-transform:rotate(0deg) translateZ(0)}
#pullDown .pullDownLabel{display:inline-block;vertical-align:middle;margin-left:5px;}
#pullDown.flip .pullDownIcon{-webkit-transform:rotate(-180deg) translateZ(0)}
#pullDown.loading .pullDownIcon{background-position:0 100%;-webkit-transform:rotate(0deg) translateZ(0);-webkit-transition-duration:0ms;-webkit-animation-name:loading;-webkit-animation-duration:2s;-webkit-animation-iteration-count:infinite;-webkit-animation-timing-function:linear}
@-webkit-keyframes loading{
    from{-webkit-transform:rotate(0deg) translateZ(0)}
    to{-webkit-transform:rotate(360deg) translateZ(0)}
}

```

```html
<div id="pullDown" class="none loading">
    <span class="pullDownIcon"></span><span class="pullDownLabel">正在载入中...</span>
</div>
```

- 手机多终端适配 media query[web app iphone4 iphone5 iphone6 响应式布局 适配代码](http://club.zoomla.cn/PItem?id=12594)
```css
@media (device-height:480px) and (-webkit-min-device-pixel-ratio:2){/* 兼容iphone4/4s */
    .class{}
}
@media (device-height:568px) and (-webkit-min-device-pixel-ratio:2){/* 兼容iphone5 */
    .class{}
}
@media (device-height:667px) and (-webkit-min-device-pixel-ratio:2){/* 兼容iphone6 */
    .class{}
}
@media (device-height:736px) and (-webkit-min-device-pixel-ratio:2){/* 兼容iphone6 Plus */
    .class{}
}
```

- 屏蔽苹果浏览器对数字的识别[Meta标签中的format-detection属性及含义](http://blog.sina.com.cn/s/blog_51048da70101cgea.html)
```html
<meta content="telephone=no" name="format-detection">
```

- 移除HTML5 input在type="number"时的上下小箭头
  - 在chrome下：
  ```css
    input::-webkit-outer-spin-button,input::-webkit-inner-spin-button{
        -webkit-appearance: none !important;
        margin: 0; 
    }
  ```
  - Firefox下：
  ```css
    input[type="number"]{-moz-appearance:textfield;}
  ```
    
  - 第二种方案：
    - 将type="number"改为type="tel"，同样是数字键盘，但是没有箭头。
    
- [HTML5手机浏览直接给一个号码打电话，发短信](http://java-er.com/blog/html5-mobile-call-sms/)
  
```html
<a href="tel:15222222222">移动WEB页面JS一键拨打号码咨询功能</a>
<a href="sms:15222222222">移动WEB页面JS一键发送短信咨询功能</a>
<!--移动web页面自动探测电话号码-->
<meta name="format-detection" content="telephone=no">
<meta http-equiv="x-rim-auto-match" content="none">
```

- [CSS判断横屏竖屏](http://www.w3cways.com/1772.html)
```css
@media screen and (orientation: portrait) {
  /*竖屏 css*/
} 
@media screen and (orientation: landscape) {
  /*横屏 css*/
}
```

```javascript
//判断手机横竖屏状态：
window.addEventListener("onorientationchange" in window ? "orientationchange" : "resize", function() {
        if (window.orientation === 180 || window.orientation === 0) { 
            alert('竖屏状态！');
        } 
        if (window.orientation === 90 || window.orientation === -90 ){ 
            alert('横屏状态！');
        }  
    }, false); 
//移动端的浏览器一般都支持window.orientation这个参数，通过这个参数可以判断出手机是处在横屏还是竖屏状态。
```

- rem 适配，内容太多，只贴网址

    - [rem自适应方案](https://github.com/imweb/mobile/issues/3)
    - [html5移动端页面分辨率设置及相应字体大小设置的靠谱使用方式](http://www.cnblogs.com/willian/p/3573353.html)
    - [移动端高清、多屏适配方案](http://www.html-js.com/article/Mobile-terminal-H5-mobile-terminal-HD-multi-screen-adaptation-scheme%203041)
    - [通过rem布局+media-query:aspect-ratio实现移动端全机型适配覆盖](http://xiaoyuze88.github.io/blog/2015/05/12/%E9%80%9A%E8%BF%87rem%E5%B8%83%E5%B1%80+media-query%E7%9A%84aspect-ratio%E5%AE%9E%E7%8E%B0%E7%A7%BB%E5%8A%A8%E7%AB%AF%E5%85%A8%E6%9C%BA%E5%9E%8B%E9%80%82%E9%85%8D%E8%A6%86%E7%9B%96/)
    - [web app变革之rem](http://isux.tencent.com/web-app-rem.html)
    - [手机淘宝的flexible设计与实现](http://www.html-js.com/article/2402)
    - [移动端自适应方案](https://github.com/amfe/lib-flexible)
    - [【原创】移动端高清、多屏适配方案](http://www.html-js.com/article/3041)
    - [6个html5页面适配iphone6的技巧](http://qietuwang.baijia.baidu.com/article/73861)
    - [关于移动端 rem 布局的一些总结](http://segmentfault.com/a/1190000003690140)
    - [从网易与淘宝的font-size思考前端设计稿与工作流](http://www.cnblogs.com/lyzg/p/4877277.html)
    - [移动端自适应方案](http://f2e.souche.com/blog/yi-dong-duan-zi-gua-ying-fang-an/)
    - [MobileWeb 适配总结](http://www.w3ctech.com/topic/979)
    - [移动端web app自适应布局探索与总结](http://www.html-js.com/article/JavaScript-learning-notes%203234)
    - 公式
        
        ```javascript
        var PAGE_MAX_WIDTH = 1280,
            BASE_FONT_SIZE = 50;
        (function() {
            function n() {
                e.fontSize = Math.min(window.innerWidth / PAGE_MAX_WIDTH * BASE_FONT_SIZE, BASE_FONT_SIZE) + "px"
            }
            var e = document.documentElement.style;
            window.addEventListener("load", n),
            window.addEventListener("resize", n),
            n();
        }());
        ```
    
- 页面的切换使用了page-enter
```html
<meta http-equiv="PAGE-ENTER" content="RevealTrans(Duration=0,Transition=1)" />
```
- css相关总结网址

    - [css常用效果总结](http://www.haorooms.com/post/css_common)
    - [css的不常用效果总结](http://www.haorooms.com/post/css_notuse_common)
	- [css开发技巧](http://www.haorooms.com/post/css_skill)
	- [重温css的选择器](http://www.haorooms.com/post/css_selectelement)
	- [css的变量和继承](http://www.haorooms.com/post/css_inherit_bl)
	- [css3的混合模式](http://www.haorooms.com/post/css3_mixblendmode)
	- [css中伪元素before或after中content的特殊用法attr](http://www.haorooms.com/post/content_attr)
