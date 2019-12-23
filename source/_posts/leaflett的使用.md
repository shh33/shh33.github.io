---
title: leaflett的使用
typora-root-url: ..
date: 2019-12-23 14:22:14
tags: leaflet
categories: leaflet
password:
top:
---



1. 需要引入几个必要的文件

```javascript
<link rel="stylesheet" href="/css/leaflet.css">
<script src="/js/jquery-1.11.3.js"></script>
<script src="/js/leaflet-src.js"></script>
<script src="/js/leaflet.label-src.js"></script>
```

2. 创建一个容器

```html
<div class="map" id="map"></div>
```

3. 编写js文件

```javascript
	//切片图层地址
	var serviceLink="http://112.17.127.75:8008/arcgis/rest/services/";
	//设置地图边界
	var topleftbound = L.latLng(30.094642639160156,122.05793380737305),
        rightbottombound = L.latLng(29.900836944580078,122.30701446533203),
        bounds = L.latLngBounds(topleftbound,rightbottombound);
	//地图初始化，设定地图最低层级
	var _map;
    _map= new L.Map('map',{zoom: 13 ,closePopupOnClick:false,crs:L.CRS.EPSG4326,zoomAnimation:true,minZoom:0,maxZoom:18,zoomControl:false,maxBounds:bounds});
	//影像地图图层
	var _baseImgLayer = new L.tileLayer('http://t{s}.tianditu.gov.cn/DataServer?T=img_c&X={x}&Y={y}&L={z}&tk=434967d31e3d3f9d396b2f4c4250b023',{subdomains:[0,1,	2,3,4,5,6,7]});
	//文字地图图层
	var _baseTxtLayer = new L.tileLayer('http://t{s}.tianditu.gov.cn/DataServer?T=cva_c&X={x}&Y={y}&L={z}&tk=434967d31e3d3f9d396b2f4c4250b023',{subdomains:[0,1,2,3,4,5,6,7]});
	//将图层加入到地图中去
	_baseImgLayer.addTo(_map);
	_baseTxtLayer.addTo(_map);
	//设置地图中心点为北京
	//_map.setView(new L.LatLng(39.905,116.399), 13);
	//设置中心点封装方法
	setCenter(39.905,116.399,13);
    function setCenter(centerLat, centerLon,zoom) {
        if (_map != null) _map.setView(new L.LatLng(centerLat, centerLon),  zoom);
    }
	//加载背景切片图层
    _bjLayer = new L.tileLayer(serviceLink+'pinghuPolderArea/MapServer/tile/{z}/{y}/{x}', {subdomains: [0, 1, 2, 3, 4, 5, 6, 7]});
    _bjLayer.addTo(_map);
	//根据鼠标点击获取经纬度
    _map.on("click",function(e){
       console.log(e);
       console.log(e.latlng.lat+"/"+e.latlng.lng)
    })
	//featureGroup是LayerGroup的扩展，但多了鼠标事件和共享的弹出框方法。继承自ILayer接口。
	pointLayers = new L.featureGroup([]);
    _map.addLayer(pointLayers);
	//添加图标
    function addIco (lat,lng,text,data) {
        var textIcon = L.divIcon({
            html: "<img class='reservoirlicon' id='"+data+"' src='images/icon/水库.png'><p class='lableText'>"+text+"</p>",
            className: 'mcon',
            iconSize:60
        });
        L.marker([lat,lng], {icon: textIcon}).addTo(pointLayers);
    }
```

