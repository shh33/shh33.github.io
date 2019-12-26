---
title: leaflet的使用
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

<!--more-->

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
	//添加点
	function addDotted(){
        var chaosIcon= L.icon({
					iconUrl: "./images/carData.png",
					iconSize: [30, 30],
					iconAnchor: [22, 15],
					popupAnchor: [0, -15]
				});
				var personData="<div class='personNumber'>测试人员<span class='onlineType'>行驶</span></div>";
				var pointFeature = new L.marker([lat,lng], { icon: chaosIcon, riseOnHover: true}).bindLabel(personData,{noHide:true});
				pointFeature.addTo(pointLayers);
    }
	//添加线(lineArr==>[[lat,lng],[lat,lng]])
	var pointFeature = new L.polyline(lineArr,{color:'blue',opacity:'0.8',weight:'3'}).addTo(pointLayers);
	//添加轨迹线（data==>[[lat,lng],[lat,lng]]）
    function addLine(data){
        if(data.length>1){
            pointLayers.clearLayers();
            (function (){
                var pointFeature = new L.polyline(data,{color:'blue',opacity:'0.8',weight:'3'}).addTo(pointLayers);
                console.log(data)
            })()
        }
    }
	//1.添加点侧面提示框和气泡弹窗
    function setWaterLayerData(json) {
    if(json.row){
        var Length=json.row.length;
    }
    waterALLMarkers=[];
    //removeLayers();
    for (var i = 0; i < Length; i++) {
        //当前测点坐标
        (function(index){
            if(json.row[index].longitudeName!=""&&json.row[index].latitudeName!=""&&json.row[index].latitudeName!=null){
                var Lon = json.row[index].longitudeName;
                var Lat = json.row[index].latitudeName;
                //默认水位点图标
                var image = _ctx+'/styles/map/images/map/water/w1.png';
                //创建图标对象
                var waterIcon = L.icon({
                    iconUrl: image,
                    iconSize: [20, 20],
                    iconAnchor: [10, 10],
                    popupAnchor: [0, -10]
                });
                var popText =  json.row[index].stationName;
                //设置数据点
                var pointFeature = new L.marker([Lat, Lon], { icon: waterIcon, riseOnHover: true, title: json.row[index].stationName }).bindTooltip(popText, { permanent: true, offset : [15,0], direction : "right", className: 'swLayer_tooltip'}).openTooltip();
                var bgurl = _ctx + '/styles/mark-popup-bg.png';
                var htmlText="<div style='width:190px;height:125px;padding-top:5px;position:relative;' class='mapWaterLayer level-okLevel'>" +
                    "<span onclick=\"showLayer('"+json.row[index].stationCode+"','"+json.row[index].stationName+"','水质')\" style='cursor:pointer;position:absolute;padding:2px 6px;right:4px;bottom:5px;color:#fff;background:#00689c;font-size:12px;'>详情</span>" +
                    "<p style='font-size: 14px'>"+json.row[index].stationName+"</p><p style='font-size: 14px'>导电率: "+json.row[index].conductivity+" μs/cm</p><p style='font-size: 14px'>浊度: "+json.row[index].turbidity+" ntu</p><p style='font-size: 14px'>温度: "+json.row[index].temparature+" ℃</p><p style='font-size: 14px'>溶解氧: "+json.row[index].do+" mg/l</p><p style='font-size: 14px'>PH: "+json.row[index].pH+" ph</p>" +
                    "</div>";
                var popup = L.popup({ maxWidth: 750, maxHeight: 400 })
                    .setLatLng([Lat, Lon])
                    .setContent(htmlText);
                pointFeature.bindPopup(popup);
                // waterALLMarkers.push(popup)
                //将数据点添加到相应图层
                pointFeature.on("mouseover",function(){
                    pointFeature.openPopup();
                });
                pointFeature.on("dbclick",function(){
                    pointFeature.closePopup();
                });
                _szLayer.addLayer(pointFeature);
            }
        })(i)
    }
    if(waterALLMarkers.length>0){
        _map.openPopup(waterALLMarkers[0]);
        setCenter(json.row[0].latitudeName,json.row[0].longitudeName)
    }
}
              
```

> 添加点侧面提示框
>
> ![1577328912964](/images/1577328912964.png)

> 添加气泡弹窗
>
> ![1577328999195](/images/1577328999195.png)

