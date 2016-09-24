# webapp(fekit工程化，加入缓存机制) #

----------
## webapp##
直接点击进入查看demo：[https://htmlk.github.io/webapp/index.html](https://htmlk.github.io/webapp/index.html "https://htmlk.github.io/webapp/index.html")

1、采用flex布局、基本实现webapp页面布局

2、采用fekit工程化

3、采用缓存机制

## fekit工程化 ##

> 点击进入我的另一个fekitdemo工程：[https://github.com/htmlk/fekitdemo](https://github.com/htmlk/fekitdemo "https://github.com/htmlk/fekitdemo")
> 
> 这里面有我对fekit的详细介绍
> 

## 加入缓存机制 ##
### 一、离线存储的作用 ###
1、用户可离线访问你的应用，这对于无法随时保持联网状态的移动终端用户来说尤其重要

2、用户访问本地的缓存文件，通常意味着更快的访问速度

3、仅仅加载被修改过的资源，避免同一资源对服务器多次的请求，大大降低了对服务器的访问压力
### 二、如何实现离线存储 ###
1、在html标签里通过manifest属性引用一个offline.manifest文件，该文件里声明了浏览器需缓存的所有资源文件，如下所示： 

    <!DOCTYPE html>
    <html lang="en" manifest="offline.appcache">
    <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
     <meta http-equiv="X-UA-Compatible" content="ie=edge">
     <link rel="stylesheet" href="/webapp/prd/styles/app@3d41ad27e7a10bf19c35da7b98d55bba.css">
      <title>Document</title>
    </head>
     <body>
       <script src="/webapp/prd/scripts/app@bec66952e4afdde7747728e2c6618472.js"></script>
     </body>
    </html>
2、关于offline.manifest的定义

    CACHE MANIFEST  //标题定义
	#1.1  //版本号
	
	CACHE:   //需要缓存的文件
	/webapp/prd/styles/app@3d41ad27e7a10bf19c35da7b98d55bba.css
	/webapp/prd/scripts/app@bec66952e4afdde7747728e2c6618472.js
	/webapp/fonts/iconfont.ttf
	/webapp/fonts/iconfont.woff
	/webapp/fonts/iconfont1.ttf
	/webapp/fonts/iconfont1.woff
	/webapp/fonts/iconfont2.ttf
	/webapp/fonts/iconfont2.woff
	/webapp/offline.appcache

	NETWORK:  //联网的文件 *号代表其余的全部					
	*

	FALLBACK:  //需要替换的文件
	offline.appcache /webapp/offline.appcache

### 4、归纳起来，步骤如下： ###


1、配置服务器支持 cache.manifest 的Content-type: manifest

2、编写 cache.manifest 文件

3、html页面引用cache.manifest文件

## 三、applicationCache对象，及属性、事件、接口##

	//当前文档对应的applicationCache对象
	window.applicationCache
	
	//当前缓存所处的状态，为0～5的整数值，分别对应一个状态，并分别对应一个常量
	window.applicationCache.status
	
	window.applicationCache.UNCACHED === 0//未缓存，比如一个页面没有制定缓存清单，其状态就是UNCACHED
	window.applicationCache.IDLE === 1 //空闲，缓存清单指定的文件已经全部被页面缓存，此时状态就是IDLE
	window.applicationCache.CHECKING === 2 //页面正在检查当前离线缓存是否需要更新
	window.applicationCache.DOWNLOADING === 3 //页面正在下载需要更新的缓存文件
	window.applicationCache.UPDATEREADY === 4  //页面缓存更新完毕
	window.applicationCache.OBSOLETE === 5  //缓存过期，比如页面检查缓存是否过期时，发现服务器上的.manifest文件被删掉了
	
	//常用API，在后面会稍详细介绍
	window.applicationCache.update()  //update方法调用时，页面会主动与服务器通信，检查页面当前的缓存是否为最新的，如不是，则下载更新后的资源
	window.applicationCache.swapCache()  //updateready后，更新到最新的应用缓存
	复制代码

## # TODO # ##
	
1、页面需进一步优化，请持续关注；

2、页面后台数据未开发；

3、没有实现在app里面
## github 上传 ##

echo "# web" >> README.md

git init

git add README.md

git commit -m "first commit"

git remote add origin https://github.com/htmlk/web.git

git push -u origin master

