操作顺序如下：

```
npm install 安装包
npm run serve: 起一个server
npm run dev: 时时编译
上线时 npm run build: 打包
```

另外，weex playground是个不错的工具，建议使用，扫一扫非常便捷。<https://weex-project.io/cn/playground.html>


楼主博客 <https://ganchengyuan1990.github.io/blog/>，欢迎交流


***

一直想做一个APP，去年也自学过一段时间的`React Native`, 但是RN相对来说学习曲线比较陡峭，并且很多资源包在下载时都不是那么容易，经常error（这个大家都懂）, 所以这事儿就不了了之了。

前两天看了weex的会议，觉得阿里又在放大招了，这个工具虽然目前学习社区不多，资源组件不丰富，但是本身调式来发非常便捷，weex playground非常不错，并且因为weex是基于vue的，所以入门简单，`npm run build`打包以后部署到自己的服务器上，用二维码扫描以后就可以拥有一个自己的APP了，并且是兼容三端的，这一点非常诱人。

于是，我就从github上找到了一个别人的项目，<https://github.com/dodola/WeexOne>，然后改造一个属于自己的APP。

开始动手！

首先，引入了picker组件，这个组件用来进行时间选择，前端效果不错。
<img src="https://ganchengyuan1990.github.io/blog/img/weex2.jpg" alt="" />


春节在家无聊的时候，继续跟进了一下Weex的学习，主要把“关于我”这个Page进行了一些优化，这里主要是一些体力活，并没有太多可说的，简单总结以下几点：
1. Weex中所有的文字都要放在<text></text>这个标签里，在普通的网页开发甚至Vue开发中，我偶尔会直接把文字放在div标签里，但是Weex中并不识别这样的语法。
2. Weex的页面布局虽然也使用css语法，但是与Vue以及普通页面并不完全相同，我试验了一下，text-align：center必须用在text标签上，才能使文字居中，但是因为HTML并没有这个标签，所以要加载文字所在的父标签上，这个要注意，另外就是建议在Weex中多应用flex布局。

<img src="https://ganchengyuan1990.github.io/blog/img/psb.jpg" alt="">


## 外部链接问题
在“关于我”这个page中，有一个需求，就是链接到外部网站，因为之前缺少APP开发经验，所以我想当然地认为这个问题非常简单，只需要价格a标签，或者像Vue一样采用Router的方法就可以了，但是后来发现这样并不能正常work。


其实在Weex中，必须要用到webview去访问H5页面（做原生开发的亲肯定懂，H5的各位朋友可以去了解一下，大致就是在APP中打开一个浏览器，从而可以访问H5页面）。

Weex官方提供了一个`web`组件：
```
<web class="content" id="webview" src='https://ganchengyuan1990.github.io/blog/' onpagestart="startload" onpagefinish="finishload" onerror="failload"></web>

```

要注意的一点是，在本地server中无法正常在webview中打开页面，但是部署到服务器就好了。
然后打包部署提交到服务器以后看，就OK啦：

<img src="https://ganchengyuan1990.github.io/blog/img/weex20170216.png" alt=""> 



