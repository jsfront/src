### 以下是常用的代码收集，没有任何技术含量，只是填坑的积累。转载请注明出处，谢谢。

#### 1. PC - js
- 返回指定范围的随机数(m-n之间)的公式
```javascript
Math.random()*(n-m)+m
```

- [return false](http://stackoverflow.com/questions/1357118/event-preventdefault-vs-return-false)
- [return false](http://www.75team.com/archives/201)
```javascript
// event.preventDefault()会阻挡预设要发生的事件.
// event.stopPropagation()会阻挡发生冒泡事件.
// 而return false则是前面两者的事情他都会做：
// 他会做event.preventDefault();
// 他会做event.stopPropagation();
// 停止callback function的执行并且立即return回来
```

- 防止被Iframe嵌套
```javascript
if(top != self){
    location.href = ”about:blank”;
}
```

- 两种图片lazy加载的方式
第一个By JS中级交流群 成都-猎巫 第二个By 上海-zenki 
```javascript
// @description 准备为图片预加载使用的插件
// 使用的图片容器css类名为lazy-load-wrap
// 图片真实地址为data-lazy-src
// 当lazy-load-wrap容器进入视口，则开始替换容器内所有需要延迟加载的图片路径，并更改容器的加载状态
//第一种方法
$.fn.compassLazyLoad=function(){
	var _HEIGHT=window.innerHeight,
	_lazyLoadWrap=$('.lazy-load-wrap');

	var methods={
		setOffsetTop:function(){
			$.each(_lazyLoadWrap,function(i,n){
				$(n).attr({
					'top':n.offsetTop-_HEIGHT,
					'status':'wait'
				});
			})
		},
		isShow:function(){
			var _scrollTop=$(window).scrollTop;
			//利用image容器判断是否进入视口，而非image本身
			$.each(_lazyLoadWrap,function(){
				var _that=$(this);
				if (_that.attr('status')==='done') {
					return;
				};
				if (_that.attr('top')<=_scrollTop) {
					_that.find('img[data-lazy-src]').each(function(i,n){
						n.src=$(n).data('lazy-src');
					});
					_that.attr('status','done');
				};
			})
		},
		scroll:function(){
			$(window).on('scroll',function(){
				methods.isShow();
			});
		},
		init:function(){
			methods.setOffsetTop();
			methods.isShow();
			methods.scroll();
		}
	};
	methods.init();

}


//第二种方法

var exist=(function($){
	var timer=null,
	temp=[].slice.call($('.container'));
	ret={};

	for(var i=0,len=temp.length-1;i<=len;i++){
		ret[i]=temp[i];
	}
	var isExist=function(winTop,winEnd){
		for(var i in ret){
			console.log(ret);
			var item=ret[i],
			eleTop=item.offsetTop,
			eleEnd=eleTop+item.offsetHeight;

			if((eleTop>winTop&&eleTop<=winEnd)||(eleEnd>winTop&&eleEnd<=winEnd)){
				$(item).css('background','none');
				new Tab($(item).attr('id'),data).init;
				delete ret[i];
			}
		}
	}
	return {
		timer:timer;
		isExist:isExist;
	};
})($);



//第三种方法
Zepto(function ($) {
    var swiper = new Swiper('.swiper-container', {
        pagination: '.swiper-pagination',
        paginationClickable: true,
        autoplay: 3000,
        loop: true,
        autoplayDisableOnInteraction: false
    });
    (function lazyLoad() {
        var imgs = $(".lazyLoad");
        var src = '';
        $.each(imgs, function (index, item) {
            src = $(item).attr('data-src');
            $(item).attr('src', src);
        });
    })();
});
$(function () {
    var lazyLoadTimerId = null;
    /// 智能加载事件
    $(window).bind("scroll", function () {
        clearTimeout(lazyLoadTimerId);
        lazyLoadTimerId = setTimeout(function () {
            // 延迟加载所有图片
            var isHttp = (location.protocol === "http:");
            $("#ym_images img").each(function () {
                var self = $(this);
                if (self.filter(":above-the-fold").length > 0) {
                    var originUrl = self.attr("data-original");
                    self.attr("src", originUrl);
                }
            });
        }, 500);
    });
});

```

- 某年某月的1号为星期几
```javascript
var weekday = ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六"];
weekday[new Date(2015, 9, 1).getDay()];	//2015年10月1号
```

#### 2. Mobile - js

- [js 判断IOS, 安卓](http://caibaojian.com/browser-ios-or-android.html)
```javascript
var u = navigator.userAgent, app = navigator.appVersion;
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1; //android终端或者uc浏览器
var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
alert('是否是Android：'+isAndroid);
alert('是否是iOS：'+isiOS);
```

#### 3. [微信 weixin](http://loo2k.com/blog/detecting-wechat-client/)

- UserAgent 判断微信客户端
```javascript
// Mozilla/5.0 (iPhone; CPU iPhone OS 8_3 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Mobile/12F70 MicroMessenger/6.1.5 NetType/WIFI
function isWechat() {  
    var ua = navigator.userAgent.toLowerCase();
    return /micromessenger/i.test(ua) || /windows phone/i.test(ua);
}
```
- 获取单个dom元素
```js
function $(selector, el) {
  if (!el) {
    el = document;
  }
  return el.querySelector(selector);
}
```
- 获取多个dom元素
```js
function $$(selector, el) {
  if (!el) {
    el = document;
  }
  return el.querySelectorAll(selector);
  // Note: the returned object is a NodeList.
  // If you'd like to convert it to a Array for convenience, use this instead:
  // return Array.prototype.slice.call(el.querySelectorAll(selector));
}
```
- 将nodeList集合转换为数组
```js
function convertToArray(nodeList) {
  var array = null
  try {
    // IE8-NodeList是COM对象
    array = Array.prototype.slice.call(nodeList, 0)
  } catch (err) {
    array = []
    for (var i = 0, len = nodeList.length; i < len; i++) {
      array.push(nodeList[i])
    }
  }
  return array
}
```
- ajax函数
```js
function ajax(setting) {
  //设置参数的初始值
  var opts = {
    method: (setting.method || "GET").toUpperCase(), //请求方式
    url: setting.url || "", // 请求地址
    async: setting.async || true, // 是否异步
    dataType: setting.dataType || "json", // 解析方式
    data: setting.data || "", // 参数
    success: setting.success || function () { }, // 请求成功回调
    error: setting.error || function () { } // 请求失败回调
  };

  // 参数格式化
  function params_format(obj) {
    var str = "";
    for (var i in obj) {
      str += i + "=" + obj[i] + "&";
    }
    return str
      .split("")
      .slice(0, -1)
      .join("");
  }

  // 创建ajax对象
  var xhr = new XMLHttpRequest();

  // 连接服务器open(方法GET/POST，请求地址， 异步传输)
  if (opts.method == "GET") {
    xhr.open(
      opts.method,
      opts.url + "?" + params_format(opts.data),
      opts.async
    );
    xhr.send();
  } else {
    xhr.open(opts.method, opts.url, opts.async);
    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    xhr.send(opts.data);
  }

  /*
  ** 每当readyState改变时，就会触发onreadystatechange事件
  ** readyState属性存储有XMLHttpRequest的状态信息
  ** 0 ：请求未初始化
  ** 1 ：服务器连接已建立
  ** 2 ：请求已接受
  ** 3 : 请求处理中
  ** 4 ：请求已完成，且相应就绪
  */
  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && (xhr.status === 200 || xhr.status === 304)) {
      switch (opts.dataType) {
        case "json":
          var json = JSON.parse(xhr.responseText);
          opts.success(json);
          break;
        case "xml":
          opts.success(xhr.responseXML);
          break;
        default:
          opts.success(xhr.responseText);
          break;
      }
    }
  };

  xhr.onerror = function (err) {
    opts.error(err);
  };
}
```

- JS接口安全域名不填写，分享onMenuShareAppMessage直接会取默认值。
```javascript
// 分享onMenuShareAppMessage直接会取默认值
```

- 关闭当前页面
```javascript
WeixinJSBridge.call('closeWindow');
```

- [支付接口方法调用必须在addevent里边调用](http://www.cnblogs.com/true_to_me/p/3565039.html)
```javascript
document.addEventListener('WeixinJSBridgeReady', function onBridgeReady(){
    that.initOrder();
}, false);
```

- 支付接口方法调用必须在
```javascript
WeixinJSBridge.invoke('getBrandWCPayRequest', d, function(res){
    if(res.err_msg == "get_brand_wcpay_request:ok"){
        // alert("支付成功");
        // union.release(d.orderId);
        resetUrl();
        paySuccess('home', d.orderId);
    } else {
        cancelOrder(d.orderId);
        // alert(res.err_msg);
    }
    loading.hide();
});
```

- 瀑布流无限加载实例 
```javascript
// be dependent on jquery & jquery.infinitescroll.min.js
// insert this '<div id="more"><a href="api?page="></a></div>' to your page.html
(function($){
  $(function(){
      var $container = $('.list-wrap-gd');
      function layOutCallBack() {
          $container.imagesLoaded(function(){
              $container.masonry({
                  itemSelector: '.item-bar',
                  gutter: 10
              });
          });
          $container.imagesLoaded().progress( function() {
              $container.masonry('layout');
          });
      }

      layOutCallBack();

      $container.infinitescroll({
          navSelector : "#more",
          nextSelector : "#more a",
          itemSelector : ".item-bar",
          pixelsFromNavToBottom: 300,
          loading:{
              img: "/images/masonry_loading.gif",
              msgText: ' ',
              finishedMsg: "<em>已经到最后一页</em>",
              finished: function(){
                  $("#more").remove();
                  $("#infscr-loading").hide();
              }
          },
          errorCallback:function(){
              $(window).unbind('.infscr');
          },
          pathParse: function (path, nextPage) {
              var query = "";
              var keyword=$("#search_keyword").val();
              var cat_id=$("#cat_id").val();
              var brand_id=$("#brand_id").val();
              var country_id = $("#country_id").val();
              query = query + "&namekeyword="+keyword;
              query = query +"&cat_id="+cat_id
              query = query + "&brand_id=" + brand_id; 
              query = query + "&country_id=" + country_id;
              path = [path,query];
              return path;
          }
      },

      function(newElements) {
          var $newElems = $( newElements ).css({ opacity: 0 });
          $newElems.imagesLoaded(function(){
              $newElems.animate({ opacity: 1 });
              $container.masonry( 'appended', $newElems, true );
              layOutCallBack();
          });
      });
  });
})(jQuery);
```
  
- [iOS，Safari浏览器，input等表单focus后fixed元素错位问题](https://www.snip2code.com/Snippet/176582/--iOS-Safari----input---focus-fixed-----)
```javascript
if( /iPhone|iPod|iPad/i.test(navigator.userAgent) ) {
  $(document).on('focus', 'input, textarea', function()
  {
     $('header').css("position", 'absolute');
     $('footer').css("position", 'absolute');
     
  });
  
  $(document).on('blur', 'input, textarea', function()
  {
       $('header').css("position", 'fixed');
       $('footer').css("position", 'fixed');
      
  });
} 

```
  
- 得到地理位置
```javascript
function getLocation(callback){
  if(navigator.geolocation){
      navigator.geolocation.getCurrentPosition(
              function(p){
                  callback(p.coords.latitude, p.coords.longitude);
              },
              function(e){
                  var msg = e.code + "\n" + e.message;
              }
      );
  }
}
```

- [rem计算适配](http://isux.tencent.com/web-app-rem.html)
```javascript
(function(doc, win){
  var docEl = doc.documentElement,
      resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
      recalc = function(){
          var clientWidth = docEl.clientWidth;
          if(!clientWidth) return;
          docEl.style.fontSize = 20 * (clientWidth / 320) + 'px';
      };

  if(!doc.addEventListener) return;
  win.addEventListener(resizeEvt, recalc, false);
  doc.addEventListener('DOMContentLoaded', recalc, false);
})(document, window);
```

- [另外一种rem方案](http://www.html-js.com/article/3041)
```javascript
var dpr, rem, scale;
var docEl = document.documentElement;
var fontEl = document.createElement('style');
var metaEl = document.querySelector('meta[name="viewport"]');

dpr = window.devicePixelRatio || 1;
rem = docEl.clientWidth * 2 / 10;
scale = 1 / dpr;


// 设置viewport，进行缩放，达到高清效果
metaEl.setAttribute('content', 'width=' + dpr * docEl.clientWidth + ',initial-scale=' + scale + ',maximum-scale=' + scale + ', minimum-scale=' + scale + ',user-scalable=no');

// 设置data-dpr属性，留作的css hack之用
docEl.setAttribute('data-dpr', dpr);

// 动态写入样式
docEl.firstElementChild.appendChild(fontEl);
fontEl.innerHTML = 'html{font-size:' + rem + 'px!important;}';

// 给js调用的，某一dpr下rem和px之间的转换函数
window.rem2px = function(v) {
    v = parseFloat(v);
    return v * rem;
};
window.px2rem = function(v) {
    v = parseFloat(v);
    return v / rem;
};

window.dpr = dpr;
window.rem = rem;
```

- 获取js所在路径
```js
function getJsDir (src) {
    var script = null;

    if (src) {
        script = [].filter.call(document.scripts, function (v) {
            return v.src.indexOf(src) !== -1;
        })[0];
    } else {
        script = document.scripts[document.scripts.length - 1];
    }

    return script ? script.src.substr(0, script.src.lastIndexOf('/')) : script;
}
```
- 页面加载自执行函数
```js
function addload(func) {
  var old = window.onload;
  if (typeof window.onload != "function") {
    window.onload = func;
  } else {
    window.onload = function () {
      old();
      func();
    }
  }
}
```

- 从全局捕获错误
```js
window.onerror = function (errMsg, scriptURI, lineNumber, columnNumber, errorObj) {
    setTimeout(function () {
        var rst = {
            "错误信息：": errMsg,
            "出错文件：": scriptURI,
            "出错行号：": lineNumber,
            "出错列号：": columnNumber,
            "错误详情：": errorObj
        };

        alert(JSON.stringify(rst, null, 10));
    });
};
```

- [如何通过 js 修改微信浏览器的title?](https://www.zhihu.com/question/26228251/answer/32405529)
```javascript
var $body = $('body');
document.title = 'title'; // hack在微信等webview中无法修改document.title的情况    
var $iframe = $('<iframe src="/favicon.ico"></iframe>').on('load', function(){ 
    setTimeout(function(){ 
        $iframe.off('load').remove() 
    }, 0) 
}).appendTo($body)
```

#### 1. 常用方法 - js
- 字符串长度截取
```js
function cutstr(str, len) {
    var temp,
        icount = 0,
        patrn = /[^\x00-\xff]/，
        strre = "";
    for (var i = 0; i < str.length; i++) {
        if (icount < len - 1) {
            temp = str.substr(i, 1);
                if (patrn.exec(temp) == null) {
                   icount = icount + 1
            } else {
                icount = icount + 2
            }
            strre += temp
            } else {
            break;
        }
    }
    return strre + "..."
}
```

- 替换全部
```js
String.prototype.replaceAll = function(s1, s2) {
    return this.replace(new RegExp(s1, "gm"), s2)
}
````

- 清除空格
```js
String.prototype.trim = function() {
    var reExtraSpace = /^\s*(.*?)\s+$/;
    return this.replace(reExtraSpace, "$1")
}
```

- 清除左空格/右空格
```js
function ltrim(s){ return s.replace( /^(\s*|　*)/, ""); } 
function rtrim(s){ return s.replace( /(\s*|　*)$/, ""); }
```
- 判断是否以某个字符串开头
```js
String.prototype.startWith = function (s) {
    return this.indexOf(s) == 0
}
```
- 判断是否以某个字符串结束	
```js
String.prototype.endWith = function (s) {
    var d = this.length - s.length;
    return (d >= 0 && this.lastIndexOf(s) == d)
}
```
- 转义html标签
```js
function HtmlEncode(text) {
    return text.replace(/&/g, '&').replace(/\"/g, '"').replace(/</g, '<').replace(/>/g, '>')
}
```
- 时间日期格式转换
```js
Date.prototype.Format = function(formatStr) {
    var str = formatStr;
    var Week = ['日', '一', '二', '三', '四', '五', '六'];
    str = str.replace(/yyyy|YYYY/, this.getFullYear());
    str = str.replace(/yy|YY/, (this.getYear() % 100) > 9 ? (this.getYear() % 100).toString() : '0' + (this.getYear() % 100));
    str = str.replace(/MM/, (this.getMonth() + 1) > 9 ? (this.getMonth() + 1).toString() : '0' + (this.getMonth() + 1));
    str = str.replace(/M/g, (this.getMonth() + 1));
    str = str.replace(/w|W/g, Week[this.getDay()]);
    str = str.replace(/dd|DD/, this.getDate() > 9 ? this.getDate().toString() : '0' + this.getDate());
    str = str.replace(/d|D/g, this.getDate());
    str = str.replace(/hh|HH/, this.getHours() > 9 ? this.getHours().toString() : '0' + this.getHours());
    str = str.replace(/h|H/g, this.getHours());
    str = str.replace(/mm/, this.getMinutes() > 9 ? this.getMinutes().toString() : '0' + this.getMinutes());
    str = str.replace(/m/g, this.getMinutes());
    str = str.replace(/ss|SS/, this.getSeconds() > 9 ? this.getSeconds().toString() : '0' + this.getSeconds());
    str = str.replace(/s|S/g, this.getSeconds());
    return str
}
```
- 判断是否为数字类型	
```js
function isDigit(value) {
    var patrn = /^[0-9]*$/;
    if (patrn.exec(value) == null || value == "") {
        return false
    } else {
        return true
    }
}
```
- 判断具体类型	
```js
function getType(a) {
    var typeArray = Object.prototype.toString.call(a).split(" ");
    return typeArray[1].slice(0, -1);
}
```
- 设置cookie值
```js
function setCookie(name, value, Hours) {
    var d = new Date();
    var offset = 8;
    var utc = d.getTime() + (d.getTimezoneOffset() * 60000);
    var nd = utc + (3600000 * offset);
    var exp = new Date(nd);
    exp.setTime(exp.getTime() + Hours * 60 * 60 * 1000);
    document.cookie = name + "=" + escape(value) + ";path=/;expires=" + exp.toGMTString() + ";domain=360doc.com;"
}
```
- 获取cookie值
```js
function getCookie(name) {
    var arr = document.cookie.match(new RegExp("(^| )" + name + "=([^;]*)(;|$)"));
    if (arr != null) return unescape(arr[2]);
    return null
}
```
- 加载样式文件表	
```js
function LoadStyle(url) {
    try {
        document.createStyleSheet(url)
    } catch(e) {
        var cssLink = document.createElement('link');
        cssLink.rel = 'stylesheet';
        cssLink.type = 'text/css';
        cssLink.href = url;
        var head = document.getElementsByTagName('head')[0];
        head.appendChild(cssLink)
    }
}
```
- 返回脚本内容
```js
function evalscript(s) {
    if(s.indexOf('<script') == -1) return s;
    var p = /<script[^\>]*?>([^\x00]*?)<\/script>/ig;
    var arr = [];
    while(arr = p.exec(s)) {
        var p1 = /<script[^\>]*?src=\"([^\>]*?)\"[^\>]*?(reload=\"1\")?(?:charset=\"([\w\-]+?)\")?><\/script>/i;
        var arr1 = [];
        arr1 = p1.exec(arr[0]);
        if(arr1) {
            appendscript(arr1[1], '', arr1[2], arr1[3]);
        } else {
            p1 = /<script(.*?)>([^\x00]+?)<\/script>/i;
            arr1 = p1.exec(arr[0]);
            appendscript('', arr1[2], arr1[1].indexOf('reload=') != -1);
        }
    }
    return s;
}
```
- 清除脚本内容
```js
function stripscript(s) {
    return s.replace(/<script.*?>.*?<\/script>/ig, '');
}
```
- 动态加载脚本文件
```js
function appendscript(src, text, reload, charset) {
    var id = hash(src + text);
    if(!reload && in_array(id, evalscripts)) return;
    if(reload && $(id)) {
        $(id).parentNode.removeChild($(id));
    }
 
    evalscripts.push(id);
    var scriptNode = document.createElement("script");
    scriptNode.type = "text/javascript";
    scriptNode.id = id;
    scriptNode.charset = charset ? charset : (BROWSER.firefox ? document.characterSet : document.charset);
    try {
        if(src) {
            scriptNode.src = src;
            scriptNode.onloadDone = false;
            scriptNode.onload = function () {
                scriptNode.onloadDone = true;
                JSLOADED[src] = 1;
             };
             scriptNode.onreadystatechange = function () {
                 if((scriptNode.readyState == 'loaded' || scriptNode.readyState == 'complete') && !scriptNode.onloadDone) {
                    scriptNode.onloadDone = true;
                    JSLOADED[src] = 1;
                }
             };
        } else if(text){
            scriptNode.text = text;
        }
        document.getElementsByTagName('head')[0].appendChild(scriptNode);
    } catch(e) {}
}
```
- 动态加载js或css文件
```js
function delay_js(url) {
  var type = url.split(".")
    , file = type[type.length - 1];
  if (file == "css") {
    var obj = document.createElement("link")
      , lnk = "href"
      , tp = "text/css";
    obj.setAttribute("rel", "stylesheet");
  } else
    var obj = document.createElement("script")
      , lnk = "src"
      , tp = "text/javascript";
  obj.setAttribute(lnk, url);
  obj.setAttribute("type", tp);
  file == "css" ? document.getElementsByTagName("head")[0].appendChild(obj) : document.body.appendChild(obj);
  return obj;
}
```
- 返回按ID检索的元素对象
```js
function $(id) {
    return !id ? null : document.getElementById(id);
}
```
- 检验URL链接是否有效	
```js
function getUrlState(URL){ 
    var xmlhttp = new ActiveXObject("microsoft.xmlhttp"); 
    xmlhttp.Open("GET",URL, false);  
    try{  
            xmlhttp.Send(); 
    }catch(e){
    }finally{ 
        var result = xmlhttp.responseText; 
        if(result){
            if(xmlhttp.Status==200){ 
                return(true); 
             }else{ 
                   return(false); 
             } 
         }else{ 
             return(false); 
         } 
    }
}
```
- 获取当前路径
```js
var currentPageUrl = "";
if (typeof this.href === "undefined") {
    currentPageUrl = document.location.toString().toLowerCase();
}else {
    currentPageUrl = this.href.toString().toLowerCase();
}
```
- 获取页面高度
```js
function getPageHeight(){
    var g = document, a = g.body, f = g.documentElement, d = g.compatMode == "BackCompat"
                    ? a
                    : g.documentElement;
    return Math.max(f.scrollHeight, a.scrollHeight, d.clientHeight);
}
```
- 获取页面可视宽度
```js
function getPageViewWidth(){
    var d = document, a = d.compatMode == "BackCompat" ? 
       				   d.body: d.documentElement;
    return a.clientWidth;
}
```
- 获取页面宽度
```js
function getPageWidth(){
    var g = document, a = g.body, f = g.documentElement, d = g.compatMode == "BackCompat"?
    					  a: g.documentElement;
    return Math.max(f.scrollWidth, a.scrollWidth, d.clientWidth);
}
```
- 随机数时间戳
```js
function uniqueId(){
    var a=Math.random,b=parseInt;
    return Number(new Date()).toString()+b(10*a())+b(10*a())+b(10*a());
}
```
- 日期格式化函数
```js
Date.prototype.format = function(format){
    var o = {
        "M+" : this.getMonth()+1, //month
        "d+" : this.getDate(),    //day
        "h+" : this.getHours(),   //hour
        "m+" : this.getMinutes(), //minute
        "s+" : this.getSeconds(), //second
        "q+" : Math.floor((this.getMonth()+3)/3),  //quarter
        "S" : this.getMilliseconds() //millisecond
    };
    if(/(y+)/.test(format)) format=format.replace(RegExp.$1,
(this.getFullYear()+"").substr(4 - RegExp.$1.length));
    for(var k in o){
        if(new RegExp("("+ k +")").test(format))
            format = format.replace(RegExp.$1,RegExp.$1.length==1 ? o[k] :("00"+ o[k]).substr((""+ o[k]).length));
    }
    return format;
}
//调用
//new Date().format("yyyy-MM-dd hh:mm:ss");
```
- 返回顶部的通用方法
```js
function backTop(btnId) {
    var btn = document.getElementById(btnId);
    var d = document.documentElement;
    var b = document.body;
    window.onscroll = set;
    btn.style.display = "none";
    btn.onclick = function() {
        btn.style.display = "none";
        window.onscroll = null;
        this.timer = setInterval(function() {
            d.scrollTop -= Math.ceil((d.scrollTop + b.scrollTop) * 0.1);
            b.scrollTop -= Math.ceil((d.scrollTop + b.scrollTop) * 0.1);
            if ((d.scrollTop + b.scrollTop) == 0) clearInterval(btn.timer, window.onscroll = set);
            }, 10);
    };
    function set() {
        btn.style.display = (d.scrollTop + b.scrollTop > 100) ? 'block': "none"
    }
};
backTop('goTop');
```
- 获得URL中GET参数值
```js
// 用法：如果地址是 test.htm?t1=1&t2=2&t3=3, 那么能取得：GET["t1"], GET["t2"], GET["t3"]
function get_get(){ 
    querystr = window.location.href.split("?")
    if(querystr[1]){
        GETs = querystr[1].split("&");
        GET = [];
        for(i=0;i<GETs.length;i++){
              tmp_arr = GETs.split("=")
              key=tmp_arr[0]
              GET[key] = tmp_arr[1]
        }
    }
    return querystr[1];
}
```
- 数组去重
```js
String.prototype.unique=function(){
    var x=this.split(/[\r\n]+/);
    var y='';
    for(var i=0;i<x.length;i++){
        if(!new RegExp("^"+x.replace(/([^\w])/ig,"\\$1")+"$","igm").test(y)){
            y+=x+"\r\n"
        }
    }
    return y
};
```
- 删除数组中某个元素
```js
Array.prototype.remove = function (val) {
  var index = this.indexOf(val);
  if (index > -1) {
    this.splice(index, 1);
  }
};
```

- 判断数组里是否有某个元素
```js
 Array.prototype.isContains = function (e) {
  for (i = 0; i < this.length && this[i] != e; i++);
  return !(i == this.length);
}
```
- 按字典顺序，对每行进行数组排序
```js
function SetSort(){
    var text=K1.value.split(/[\r\n]/).sort().join("\r\n");//顺序
    var test=K1.value.split(/[\r\n]/).sort().reverse().join("\r\n");//反序
    K1.value=K1.value!=text?text:test;
}
```
- 字符串反序输出
```js
function IsReverse(text){
    return text.split('').reverse().join('');
}
```
- 金额大写转换函数
```js
//格式转换
function transform(tranvalue) {
    try {
        var i = 1;
        var dw2 = new Array("", "万", "亿"); //大单位
        var dw1 = new Array("拾", "佰", "仟"); //小单位
        var dw = new Array("零", "壹", "贰", "叁", "肆", "伍", "陆", "柒", "捌", "玖"); //整数部分用
        //以下是小写转换成大写显示在合计大写的文本框中     
        //分离整数与小数
        var source = tranvalue.split(".");
        var num = source[0];
        var dig = source[1];
        //转换整数部分
        var k1 = 0; //计小单位
        var k2 = 0; //计大单位
        var sum = 0;
        var str = "";
        var len = source[0].length; //整数的长度
        for (i = 1; i <= len; i++) {
              var n = source[0].charAt(len - i); //取得某个位数上的数字
              var bn = 0;
              if (len - i - 1 >= 0) {
                bn = source[0].charAt(len - i - 1); //取得某个位数前一位上的数字
              }
              sum = sum + Number(n);
              if (sum != 0) {
                str = dw[Number(n)].concat(str); //取得该数字对应的大写数字，并插入到str字符串的前面
                if (n == '0') sum = 0;
              }
              if (len - i - 1 >= 0) { //在数字范围内
                if (k1 != 3) { //加小单位
                      if (bn != 0) {
                        str = dw1[k1].concat(str);
                      }
                      k1++;
                } else { //不加小单位，加大单位
                      k1 = 0;
                      var temp = str.charAt(0);
                      if (temp == "万" || temp == "亿") //若大单位前没有数字则舍去大单位
                      str = str.substr(1, str.length - 1);
                      str = dw2[k2].concat(str);
                      sum = 0;
                }
              }
              if (k1 == 3){ //小单位到千则大单位进一
                k2++;
              }
        }
        //转换小数部分
        var strdig = "";
        if (dig != "") {
              var n = dig.charAt(0);
              if (n != 0) {
                strdig += dw[Number(n)] + "角"; //加数字
              }
              var n = dig.charAt(1);
              if (n != 0) {
                strdig += dw[Number(n)] + "分"; //加数字
              }
        }
        str += "元" + strdig;
    } catch(e) {
        return "0元";
    }
    return str;
}
```
- 格式化数字
```js
function fmoney(s, n) {
  //s:传入的float数字 ，n:希望返回小数点几位
  n = n > 0 && n <= 20 ? n : 2;
  s = parseFloat((s + "").replace(/[^\d\.-]/g, "")).toFixed(n) + "";
  var l = s
    .split(".")[0]
    .split("")
    .reverse(),
    r = s.split(".")[1];
  t = "";
  for (i = 0; i < l.length; i++) {
    t += l[i] + ((i + 1) % 3 == 0 && i + 1 != l.length ? "," : "");
  }
  return;
  t
    .split("")
    .reverse()
    .join("") +
    "." +
    r;
}
```
