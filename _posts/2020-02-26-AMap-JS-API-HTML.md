---
layout: post
title: 如何将高德地图JS API嵌入到HTML网页内
categories: HTML
description: 
keywords: HTML
---


**目录**

* TOC
{:toc}

## 序
百度地图API越来越不好用，所以换成高德。

## 1. 高德开放平台注册
先去https://lbs.amap.com/注册一下，直接用淘宝/QQ等OpenID既可实现注册。
没有要求实名制，填写姓名的时候，填写英文名。

## 2. 创建Access Key
进入应用管理-->我的应用  
选择JS API即可创建好Key
这个就是我们调用的Key


## 3. 实现自定义样式
高德地图可以实现自定义地图样式，只需要点击创建并发布即可。
在这里，我们有默认的地图样式可以选择，稍后教大家如何选择地图样式。

## 4. 抄袭官方代码一下
官方说明  
https://lbs.amap.com/api/javascript-api/guide/abc/load

使用异步加载
样板代码
```
<script type="text/javascript">
    window.init = function(){
        var map = new AMap.Map('container', {
           center:[117.000923,36.675807],
           zoom:11
        });
    }
</script>
<script src="https://webapi.amap.com/maps?v=1.4.15&key=您申请的key值&callback=init"></script>
```
在这里复制你的Key   
例如在这里，我假设我的Key是
```
f8cn0ivrdrd3pcldj7xmz0l0v13ifqz9
```
所以最后一段变成
```
<script src="https://webapi.amap.com/maps?v=1.4.15&key=f8cn0ivrdrd3pcldj7xmz0l0v13ifqz9&callback=init"></script>
```

## 5. 修改地图样式
高德目前有10种样式，分别是  
标准normal，幻影黑dark，月光银light，远山黛whitesmoke，草色青fresh，雅士灰grey，涂鸦graffiti，马卡龙macaron，  
靛青蓝blue，极夜蓝darkblue，酱籽wine  
来源：https://lbs.amap.com/api/javascript-api/guide/map/map-style  
  
设置地图样式的方式有两种：  
我只介绍在地图初始化时设置：  
```
var map = new AMap.Map('container',{
    mapStyle: 'amap://styles/whitesmoke', //设置地图的显示样式
});
```

### 修改地图样式为马卡龙
所以，代码应该是：
```
<script type="text/javascript">
    window.init = function(){
        var map = new AMap.Map('container', {
		################################Start################################
		mapStyle: 'amap://styles/macaron', //设置地图的显示样式
		################################End##################################
           center:[117.000923,36.675807],
           zoom:11
        });
    }
</script>
<script src="https://webapi.amap.com/maps?v=1.4.15&key=f8cn0ivrdrd3pcldj7xmz0l0v13ifqz9&callback=init"></script>
```

如果你是使用自定义样式，那么你的mayStayle应该是长这样的。
```
amap://styles/pqd19is40c564urc0kuspe730foc4mlh
```

## 6. 同步加载多个插件
地图不可能是单独是地图，还有工具条，标记等工具。  
这个时候，我们就加载多个插件。
来源：https://lbs.amap.com/api/javascript-api/guide/abc/plugins
```
<script type="text/javascript" src="https://webapi.amap.com/maps?v=1.4.15&key=您申请的key值&plugin=AMap.ToolBar,AMap.Driving"></script> 
```
我们就在plugin=后面添加插件。

但是，我们开始的时候，我们使用的是异步加载，所以以上情况就不合适了。

```
异步加载加载一个插件
<script type="text/javascript" >
    var map = new AMap.Map('container',{
        zoom:12,
        center:[116.39,39.9]
    });
	##########新添加部分##########
    AMap.plugin('AMap.ToolBar',function(){//异步加载插件
        var toolbar = new AMap.ToolBar();
        map.addControl(toolbar);
    });
	##########新添加部分End##########
</script>
#########################################################
#################异步加载加载多个插件#################
<script type="text/javascript" >
    var map = new AMap.Map('container',{
        zoom:12,
        center:[116.39,39.9]
    });
	##########新添加部分##########
      AMap.plugin(['AMap.ToolBar','AMap.Driving'],function(){//异步同时加载多个插件
      var toolbar = new AMap.ToolBar();
      map.addControl(toolbar);
      var driving = new AMap.Driving();//驾车路线规划
      driving.search(/*参数*/)
  });
	##########新添加部分End##########
</script>

```

### 插入到HTML内
嵌入进去的话，只需要在<body>内
加入<div>标签即可  
例如
```
<div id="container-AMap" style="width:100%; height:400px; position: relative"></div>
```
然后，在footer的底部，也就是通常放置script的地方，放置script即可。
因为我们的div id是container-AMap, 所以我们的Script里也需要改一下。  

```
<script type="text/javascript" >
    var map = new AMap.Map('container-AMap',{
```
## 7. 修改经纬度
如果直接通过地址编码-->经纬度，用高德的演示案例查询经纬度会报错。  
请直接百度“查询经纬度”。  
将得到数据反着填写即可。

## 8. 路线规划与导航
通过Web JS API 是无法进行实时导航的。但是可以进行路线规划。  
但是Web版路线规划限制比较多，无法实现类似gaode.com/map.baidu.com这类需求。
我实现的方式是通过官方教程  
位置经纬度 + 驾车规划路线
来源：https://lbs.amap.com/api/javascript-api/example/driving-route/plan-route-according-to-lnglat
因为终点是确定的（也就是我的位置）
但是如何定义起点呢？  
考虑过AMap.Geolocation（浏览器定位），发现测试失败。  
也考虑过AMap.CitySearch(IP定位到城市），感觉也不合适。  
参考来源：https://lbs.amap.com/api/javascript-api/guide/services/geolocation
  
最后，还是决定完全只使用经纬度，然后，用户可以跳转到高德的官网进行修改地址导航。

网站无法实现导航功能，搁置。
但是从演示模板中，得到http参数
也从这里得到的灵感，直接使用
地点关键字 + 驾车路线规划
然后获得他的HTTP跳转导航链接。

## 9. 标记点Marker实现点击打开功能
标记点Marker实现点击打开功能，其实就是打开信息窗体。
https://lbs.amap.com/api/javascript-api/guide/overlays/infowindow  

在这里我们参考自定义信息窗体以及鼠标点击的案例进行合并。

在寻找的过程中发现，其实有点击Marker直接调用高德的方法。
https://lbs.amap.com/api/javascript-api/example/callapp/markonapp/
```
<script type="text/javascript">
  window.init = function(){

  var map = new AMap.Map('container-AMap', {
	  resizeEnable: true, //是否监控地图容器尺寸变化
	  mapStyle: 'amap://styles/whitesmoke',
      center:[116.481181, 39.989792],
      zoom:15
  });
  

var marker = new AMap.Marker({
    position: new AMap.LngLat(116.481181, 39.989792),   // 经纬度对象，也可以是经纬度构成的一维数组[119.920486,30.245285]
    title: '方恒国际酒店'
  });
  //==================异步加载1个插件==================
  AMap.plugin('AMap.ToolBar',function(){//异步加载插件
        var toolbar = new AMap.ToolBar();
        map.addControl(toolbar);
    });
  	
// 将创建的点标记添加到已有的地图实例：
map.add(marker);
#####原有基础添加以下：
marker.on('click',function(e){
            marker.markOnAMAP({
                name:'方恒国际酒店',
                position:marker.getPosition()
            })
        })
  
</script> 
<script>我的Key那一行</script>
```  
但是出于学习如何实现信息窗体打开功能，我就暂时不直接用了。

经过长期探索
结合默认样式信息窗体与鼠标点击，我还是找到了如何实现最基本的功能：
```
<script type="text/javascript">
  window.init = function(){

  var map = new AMap.Map('container-AMap', {
	  resizeEnable: true, //是否监控地图容器尺寸变化
	  mapStyle: 'amap://styles/whitesmoke',
      center:[116.481181, 39.989792],
      zoom:15
  });
  

var marker = new AMap.Marker({
    position: new AMap.LngLat(116.481181, 39.989792),   // 经纬度对象，也可以是经纬度构成的一维数组[119.920486,30.245285]
    title: '方恒国际酒店'
  });
  //==================异步加载1个插件==================
  AMap.plugin('AMap.ToolBar',function(){//异步加载插件
        var toolbar = new AMap.ToolBar();
        map.addControl(toolbar);
    });
  	
// 将创建的点标记添加到已有的地图实例：
map.add(marker);
marker.on('click',openInfo) //鼠标点击标记事件 - 打开信息窗体
 /*=======================上面的原文是marker.on('click', function(e){ 后面一堆=========================*/

/*================================================*/
    //在指定位置打开信息窗体
    function openInfo() {
        //构建信息窗体中显示的内容
        var info = [];
        info.push("<div class='input-card content-window-card'><div><img style=\"float:left;\" src=\" https://webapi.amap.com/images/autonavi.png \"/></div> ");
        info.push("<div style=\"padding:7px 0px 0px 0px;\"><h4>高德软件</h4>");
        info.push("<p class='input-item'>地址 :北京市朝阳区望京阜荣街10号首开广场4层</p></div></div>");
		info.push("<p class='input-item'>点击此处使用高德地图导航</p></div></div>");

        infoWindow = new AMap.InfoWindow({
            content: info.join("")  //使用默认信息窗体框样式，显示信息内容
        });

        infoWindow.open(map, marker.getPosition()); //原文是open(map, map.getCenter());
    }
/*================================================*/	  
}
</script> 
```

## 10. 信息窗体内容添加跳转到高德地图导航
根据markerOnAMAP，我们可以得到HTTPS的参数
```
https://gaode.com/regeo?lng=116.481181&lat=39.989792&name=你想要的标题
```
只需要将这个参数以链接的形式显示到默认的信息窗体内容即可完成。
```
info.push("<p class='input-item'><a href=\"https://gaode.com/regeo?lng=116.481181&lat=39.989792&name=你想要的标题\">点击此处使用高德地图导航</a></p></div></div>");
```
唯一需要注意的是我们需要在"的开始之前添加\ 例如\"  
然后在结束之前添加\, 例如"\  
  
SearchOnAMap这类调起，即使使用手机端，同样只是打开浏览器，无论是直接的HTTPS还是OnAMap都无法实现直接打开App。

## 11. 实现窗口信息的位置偏移
从说明文档中我们知道是在infoWindow = new AMap.InfoWindow的里面添加offset: new AMap.Pixel(0, -20)
也就是
```
/*================================================*/
    function openInfo() {
        var info = [];
        info.push("<div class='input-card content-window-card'><div><img style=\"float:left;\" src=\" https://webapi.amap.com/images/autonavi.png \"/></div> ");
        ... ...
		/*####################修改偏移量准备位置####################*/
        infoWindow = new AMap.InfoWindow({
            content: info.join(""),  //使用默认信息窗体框样式，显示信息内容
			offset: new AMap.Pixel(0, -20), //添加信息窗体的偏移量 
... ...
/*================================================*/	 
```
需要注意的是别忘了逗号。
content: info.join("")与offset... ...要有逗号。
否则这个偏移就出不来了。

## 12. 默认信息窗体的扩展
在认真实践的时候发现，我们的info.push即使加多一行，实际上也不显示。
所以，我们需要Size这个参数来定义。
```
        infoWindow = new AMap.InfoWindow({
            content: info.join(""), //使用默认信息窗体框样式，显示信息内容 
			//可以是content:"aaa"//信息窗体的内容 因为我们定义了info =[], 所以就是info.join("")
			offset: new AMap.Pixel(0, -20), //添加信息窗体的偏移量 
			size: new AMap.Size(300,180) //定义信息窗体的长宽
        });
```
做完这个，你就可以根据实际情况，添加info.push的内容了。

