---
title: leaflet相关配置项
typora-root-url: ..
date: 2019-12-26 10:27:07
tags: leaflet
categories: leaflet
password:
top:
---



### L.Map

API各种类中的核心部分，用来在页面中创建地图并操纵地图。

<!--more-->

##### Constructor（构造器）

通过div元素和带有地图选项的描述的文字对象来实例化一个地图对象，其中文字对象是可选的。

##### Options（选项）

Map State Options（地图状态选项）
 centre（中心）：初始化地图的地理中心。
 zoom（缩放）：初始化地图的缩放。
 layers（图层）：初始化后加载到地图上的图层。
 minZoom（最小视图）：地图的最小视图。可以重写地图图层的最小视图。
 maxZoom（最大视图）：地图的最大视图。可以重写地图图层的最大视图。
 maxBounds（最大边界）：当这个选项被设置后，地图被限制在给定的地理边界内，当用户平移将地图拖动到视图以外的范围时会出现弹回的效果，并且也不允许缩小视图到给定范围以外的区域（这取决于地图的尺寸）。使用setMaxBounds方法可以动态地设置这种约束。
 crs（坐标参考系统）：使用的坐标系，当你不确定坐标系是什么时请不要更改。
 Interaction Options（交互操作）
 dragging（拖动）：决定地图是否可被鼠标或触摸拖动。
 touchZoom（触摸缩放）：决定地图是否可被两只手指触摸拖拽缩放。
 scrollWheelZoom（滚轮缩放）：决定地图是否被被鼠标滚轮滚动缩放。
 doubleClickZoom（双击缩放）：决定地图是否可被双击缩放。
 boxZoom（多边形缩放）：决定地图是否可被缩放到鼠标拖拽出的矩形的视图，鼠标拖拽时需要同时按住shift键。
 trackResize（追踪尺寸改变）：确定地图在窗口尺寸改变时是否可以自动处理浏览器以更新视图。
 worldCopyJump（领域副本跳转）：当这个选项可用时，当你平移地图到其另一个领域时会被地图捕获到，并无缝地跳转到原始的领域以保证所有标注、矢量图层之类的覆盖物仍然可见。
 closePopupOnClick（点击关闭消息弹出框）：当你不想用户点击地图关闭消息弹出框时，请将其设置为false。
 Keyboard Navigation Options（键盘操纵选项）
 keyboard（键盘）：聚焦到地图且允许用户通过键盘的方向键和加减键来漫游地图。
 keyboardPanOffset（键盘平移补偿）：确定按键盘方向键时地图平移的像素。
 keyboardZoomOffset（键盘缩放补偿）：确定键盘加减键对于的缩放级数。
 Panning Inertia Options（平移惯性选项）
 inertia（惯性）：如果该选项可用，在拖动和在某一时间段内持续朝同一方向移动建有动力的地图时，会有惯性的效果。
 inertiaDeceleration（惯性减速）：确定惯性移动减速的速率，单位是像素每秒的二次方。
 inertiaMaxSpeed（惯性最大速度）：惯性移动的最大速度，单位是像素每秒。
 inertiaThreshold（惯性阈值）：放开鼠标或是触摸来停止惯性移动与移动停止之间的毫秒数。
 Control options（控制选项）
 zoomControl（缩放控制）：确定缩放控制是否默认加载在地图上。
 attributionControl（属性控制）：确定属性控制是否默认加载在地图上。
 Animation options（动画选项）
 fadeAnimation（淡出动画）：确定瓦片淡出动画是否可用。通常默认在所有浏览器中都支持CSS3转场，android例外。
 zoomAnimation（缩放动画）：确定瓦片缩放动画是否可用。通常默认在所有浏览器中都支持CSS3转场，android例外。
 markerZoomAnimation（注记缩放动画）：确定注记的缩放是否随地图缩放动画而播放，如果被禁用，注记在动画中拉长时会消失。通常默认在所有浏览器中都支持CSS3转场，android例外。

### Events（事件）

click（点击）：用户点击或触摸地图时触发。
 dbclick（双击）：用户双击或连续两次触摸地图时触发。
 mousedown（鼠标按下）：用户按下鼠标按键时触发。
 mouseup（鼠标抬起）：用户按下鼠标按键时触发。
 mouseover（鼠标经过）：鼠标进入地图时触发。
 mouseout（鼠标移出）：鼠标离开地图时触发。
 mousemove（鼠标移动）：鼠标在地图上移动时触发。
 contextmenu（情景菜单）：当用户在地图上按下鼠标右键时触发，如果有监听器在监听这个时间，则浏览器默认的情景菜单被禁用。
 focus（聚焦）：当用户在地图上进行标引、点击或移动时进行聚焦。
 blur（变暗）:当地图失去焦点时触发。
 preclick（预先点击）：当鼠标在地图上点击之前触发。有时会在点击鼠标时，并在已存在的点击事件开始处理之前想要某件事情发生时用得到。
 load（载入）：当地图初始化时触发。（当地图的中心点和缩放初次设置时）
 viewreset（视图重置）：当地图需要重绘内容时触发。（通常在地图缩放和载入时发生）这对于创建用户自定义的叠置图层非常有用。
 movestart（移动开始）：地图视图开始改变时触发。（比如用户开始拖动地图）
 move（移动）：所有的地图视图移动时触发。
 moveend（移动结束）：当地图视图结束改变时触发。（比如用户停止拖动地图）
 dragstart（拖动开始）：用户开始拖动地图时触发。
 drag（拖动）：用户拖动地图时不断重复地触发。
 dragend（拖动结束）：用户停止拖动时触发。
 zoomstart（缩放开始）：当地图缩放即将发生时触发。（比如缩放动作开始前）
 zoomend（缩放结束）：当地图缩放时触发。
 autopanstart（自动平移开始）：打开弹出窗口时地图开始自动平移时触发。
 layeradd（添加图层）：当一个新的图层添加到地图上时触发。
 layerremove（图层移除）：当一些图层从地图上移除时触发。
 baselayerchange（基础图层改变）：当通过图层控制台改变基础图层时触发。
 locationfound（位置查找）：当地理寻址成功时触发（使用locate方法）。
 locationerror（定位错误）：当地理寻址错误时触发（使用locate方法）。
 popupopen（打开弹出框）：当弹出框打开时触发（使用openPopup方法）。
 popupclose（关闭弹出框）：当弹出框关闭时触发（使用closePopup方法）。

#### Methods for Modifying Map State（地图状态修改）

setView(设定视图)：设定地图（设定其地理中心和缩放），如果forceReset设置的是true，即使移动和缩放动作是合理的，地图也会重载，其默认值是fault。
 setZoom（设定缩放）：设定地图的缩放。
 zoomIn（放大）：通过delta变量放大地图的级别，1是delta的默认值。
 zoomOut（缩小）：通过delta变量缩小地图的级别，1是delta的默认值。
 fitBounds（使适合边界）：将地图视图尽可能大地设定在给定的地理边界内。
 fitWorld（使适合地域范围）：将地图视图尽可能大地设定在包含全部地域的级别上。
 panTo（平移至中心点）：将地图平移到给定的中心。如果新的中心点在屏幕内与现有的中心点不同则产生平移动作。
 panInsideBounds（平移到某边界内）：平移地图到坐落于给定边界最接近的视图内。
 panBy（通过像素点平移）：通过给定的像素值对地图进行平移。
 invalidateSize（无效的大小）：检查地图容器的大小是否改变并更新地图，如果是这样的话，在动态改变地图大小后调用，如果animate是true的话，对地图进行更新。
 setMaxBounds（设置最大边界）：将地图限定在给定的边界内。
 locate（定位）：用地理定位接口获取用户位置信息，在成功定位或定位出错产生locationerror后解除location-found事件与定位数据，且将地图视图设定到检测的确切的用户的位置（如果定位失败则回到地域视图）。在Location Options中有更多详细内容。
 stopLocation（停止定位）：开始map.locate方法时停止预先检测位置信息。

##### Methods for Getting Map State（获取地图状态）

getCenter（获取地图中心）：返回地图视图的地理中心。
 getZoom（获取缩放级别）：获取地图视图现在所处的缩放级别。
 getMixZoom（获取最小缩放级别）：返回地图最小的缩放级别。
 getMaxZoom（获取最大缩放级别）：返回地图最大的缩放级别。
 getBounds（获取边界）：返回地图视图的经纬度边界。
 getBoundsZoom（获取边界缩放级别）：返回适应整个地图视图边界的最大缩放级别。如果inside的设置时true，这个方法返回适应整个地图视图边界的最小缩放级别。
 getSize（获取大小）：返回现有地图容器的大小。
 getPixelBounds（获取像素边界）：返回地图视图在像素投影坐标系下的边界。（很多时候对用户自定义图层和叠加很有用）
 getPixelOrigin（获取像素原点）：返回地图图层像素投影坐标系下的左上角的点。（很多时候对用户自定义图层和叠加很有用）

##### Methods for Layers and Controls（图层控制）

addlayer（添加图层）：将图层添加到地图上。如果insertAtTheBottom的选项为true，图层添加时在所以图层之下。（在切换基底图时比较有用）
 removelayer（移除图层）：将图层在地图上移除。
 haslayer（是否有此图层）：如果添加的图层是当前图层则返回true。
 openPopup（打开弹出框）：当关闭前一个弹出框时弹出指定的对话框。（确定在同一时间只有一个打开并可用）
 closePopup（关闭弹出框）：关闭openPopup打开的弹出框。
 addControl（添加控制）：在地图上添加控制选项。
 removeControl（移除控制）：在地图上移除控制选项。

##### Conversion Methods（转换方法）

latlngToLayerPoint（将经纬度添转变为图层上的点）：返回地图图层上与地理坐标相一致的点。（在地图上进行位置叠加时比较有用）
 layerPointToLatLng（将图层上的点转换为经纬度点）：返回给定地图上点的地理坐标系。
 containerPointToLayerPoint（容器点到图层点）：将于地图容器相关的点转换为地图图层相关的点。
 layerPointToContainerPoint（图层点到容器点）：将地图图层相关的点转换为地图容器相关的点。
 LatLngToContainerPoint（经纬度点到容器点）：返回与给定地理坐标系相符的地图容器的点。
 containerPointToLatLng（容器点转换为经纬度点）：返回给定地理容器点的地理坐标。
 project（投影）：将地理坐标投影到指定缩放级别的像素坐标系中。
 unproject（反投影）：将像素坐标系投影到指定缩放级别的地理坐标系中。（默认为当前的缩放级别）
 mouseEventToContainerPoint（鼠标点击事件到地图容器点）：返回鼠标点击事件对象的像素坐标（与地图左上角相关）。
 mouseEventToLayerPoint（鼠标点击事件到地图容器点）：返回鼠标点击事件对象的像素坐标（与地图图层相关）。
 mouseEventToLatLng（鼠标点击事件到经纬度点）：返回鼠标点击事件对象的地理坐标。

##### Other Methods（其他方法）

getContainer（获取容器）：返回地图容器对象。
 getPanes（获取地图边框）：返回不同地图对象的边框（叠加渲染)
 whenReady（准备就绪）：当地图的位置和缩放初始化好或是时间发生之后，运行给定的回调方法，通常传递一个函数内容。

### Locate options（位置选项）

watch（监听）：如果该值为真，则开始利用W3C的watchPosition方法监听位置变化情况（而不是指监听一次）。你可以通过map.stoplocate()方法来停止监听。
 setView（设置视图）：如果该值为真，则通过自动将地图视图定位到用户一定精度范围内的位置，如果地理定位失败则显示全部地图。
 maxZoom（最大级别）：在使用setView选项时视图缩放的最大级别。
 timeout（超时）：在触发locationerror事件之前等待地理定位的毫秒为单位的时间。
 maximumAge（最大生命周期）：位置监听的最大生命周期。如果比最后定位回复后毫秒用时短，则locate返回一个缓存位置。
 enableHighAccuracy（开启高精度）：开启高精度，参加W3C SPEC的描述。

##### Properties（属性）

地图属性包括互动操作，允许你在运行环境中互动地控制地图行为，比如通过拖拽和点击缩放级别显示和不显示某要素。你也可以通过地图属性来接受默认的地图控制项，比如属性控制。
 dragging（拖拽）：地图拖拽处理程序，可以通过鼠标和触摸的形式。
 touchZoom（触摸缩放按钮）：触摸地图缩放处理程序。
 doubleClickZoom（双击缩放）：双击缩放处理程序。
 scrollWheelZoom（滚动缩放）：滚动缩放处理程序。
 boxZoom（矩形框缩放）：矩形框（利用鼠标拖动）缩放处理程序。
 keyboard（键盘）：键盘导向处理程序。
 zoomControl（缩放控制）：缩放控制。
 attributionControl（属性控制）：属性控制。

##### Map Panes（地图窗口）

望文思义，这是一个包括可以用来放置自定义图层的不同的地图窗口的对象。最大的区别是图层的叠置。
 mapPane（地图窗口）：包含其他地图窗口的窗口。
 tilePane（切片窗口）：切片图层的窗口。
 objectsPane（对象窗口）：包含除切片窗口以外所有窗口的窗口。
 shadowPane（隐含窗口）：用来隐藏图层的窗口（如标注的隐藏）。
 overlayPane（图层窗口）：这线段和多边形一类图层的窗口。
 markerPane（标注窗口）：标注图标的窗口。
 popupPane（弹出窗口）：弹出的窗口。

### L.Marker

用来在地图中放置注记。

##### Constructor（构造函数）

L.Marker（）：通过给定一个地理点和一个具有选项的对象来实例化一个注记。

##### Options（选项）

icon（图标）：图标类用来表达注记。参加Icon documentation以了解自定义注记图标的详细信息。默认设置为new L.Icon.Default()。
 clickable（可点击）：如果是false，注记则不产生鼠标事件并表现为底层地图的一部分。
 draggable（可拖动）：决定注记是否可被鼠标或触摸拖动。
 title（标题）：注记旁边显示浏览器提示的文本信息。
 zIndexOffset（）：默认情况下，注记图片的叠置顺序由纬度自动设置。如果你想将某一注记放置于其他之上可用这个选项，设置一个较大的值即可，比如1000（或是相反地设置一个较大的负值）。
 opacity（不透明度）：决定注记的不透明度。
 riseOnHover（凸显）：如果此值为true，则当把鼠标放置于注记之上时，注记会显示与其他注记之上。
 riseOffset（凸显补偿）：riseOnHover要素凸显时高度的补偿值。

##### Events（事件）

click（点击）：当鼠标点击注记时触发。
 dbclick（双击）：当鼠标双击注记时触发。
 mousedown（鼠标按下）：当鼠标按下鼠标键时触发。
 mouseover（鼠标置于其上）：当鼠标在注记上时触发。
 mouseout（鼠标移出）：当鼠标离开注记时触发。
 contextmenu（文本菜单）：当鼠标右击注记时触发。
 dragstrat（拖动开始）：当用户拖动注记时触发。
 drag（拖动）：当用户拖动注记时不断触发。
 dragend（拖动结束）：当用户停止拖动注记时触发。
 move（移动）：当注记通过定义经纬度而移动时触发。新的坐标包含事件参数。
 remove（删除）：当注记在地图上被删除时触发。

##### Methods（方法）

addTo()：在地图上添加注记。
 getLatLng()：返回当前注记的地理位置。
 setLatLng()：将注记位置更改到给定点。
 setIcon()：更改注记的图标。
 setZIndexOffset()：更改注记的zIndex offset。
 setOpacity()：更改注记的透明度。
 update()：更新注记的位置，在直接更改经纬度对象的坐标时比较有用。
 bindPopup()：当点击一个注记时绑定一个特定的HTML内容的弹出窗口。你也可以用Marker中的openPopup方法打开绑定的弹出窗口。
 unbindPopup()：将先前用bindPopup方法绑定的注记取消。
 openPopup()：打开先前用bindPopup方法绑定的弹出框。
 closePopup()：关闭已打开的注记的弹出框。

##### Interaction handlers（互操作处理程序）

dragging（拖动）：注记拖动处理程序（包括鼠标和触摸）。

### L.Popup

##### Constructor（函数构造器）

L.Popup()：通过给定一些选项构造一个弹出框对象，对象用来描述出现形式和位置还有一个可选对象来根据指向的资源对象标注弹出框。
 maxWidth（最大宽度）：弹出框的最大宽度。
 minWidth（最小宽度）：弹出框的最小宽度。
 maxHeight（最大高度）：设置后，如果内容超过弹出窗口的给定高度则产生一个可以滚动的容器。
 autoPan（自动平移）：如果你不想地图自动平移来适应打开的弹出框，就设置其为false。
 closeButton（关闭按钮）：控制弹出窗口中出现的关闭按钮。
 offset（补偿值）：弹出窗口位置的补偿值。在同一图层中打开弹出窗口时对于控制锚点比较有用。
 autoPanPadding（自动平移填补）：在地图视图自动平移产生后弹出窗口和地图视图之间的边缘。
 zoomAnimation：决定是否在所在级别上弹出窗口。如果你在弹出窗口中有flash内容的最好将其设置为不可用。

##### Methods（方法）

addTo：将弹出窗口添加到地图上。
 openOn：将弹出窗口添加到地图上并将之前的一个关闭。与map.oenPopup(popup)方法相同。
 setLatLng：设置弹出窗口打开的地理上的点位。
 setContent：设置弹出窗口的HTML内容。

### L.TileLayer

用来在地图上载入和显示切片图层，用ILayer接口实现。

##### Constructor（函数构造器）

L.TileLayer()：通过给定URL模板和具有选项的对象来实例化一个切片图层。

##### URL template（URL模板）

见下面的例子
 L.tileLayer('http://{s}[.somedomain.com/](https://link.jianshu.com?t=http://.somedomain.com/){foo}/{z}/{x}/{y}.png', {foo: 'bar'})

##### Options（选项）

minZoom：最小级别数
 maxZoom：最大级别数
 tileSize：切片尺寸（宽度和高度的像素值，假设切片是正方形的）
 subdomains：服务的子域。可以传递一个字符串（其中每一个字母都是一个子域名称）或是一个字符串数组。
 errorTileUrl：图片的URL给出加载错误的位置。
 attribution：用来进行属性控制的字符串，描述了图层数据。
 tms：如果此值为true，反转切片Y轴的编号（对于TMS服务需将此项打开）。
 continuousWorld：如果设置为true，切片的坐标系不会被世界范围的宽度（-180度到180度）所覆盖，也不会被在世界范围的高度（-90度到90度）之内。你可以将此用在不反应真是世界的地图上（比如游戏、室内或照片的地图）。
 noWrap：如果设置此项为true，则切片不会用重复填充来表示世界范围（经度-180到180之间）之外的地方。
 zoomOffset：用此值来补偿URL中地图的缩放级别。
 zoomReverse：如果此项为true，URL中的缩放级别会被反转（用最大到最小缩放级别来替代缩放级别）。
 opacity：切片图层的透明度。
 zIndex：切片图层明确的叠置顺序，默认此项不会被设置。
 unloadInvisibleTiles：如果此项为true，在平移后所有看不到的切片都会被移除（用以更好地显示），在移动设备的webkit中默认是true，其他的默认为false。
 updateWhenIdle：如果此项为false，在平移过程中新的切片将会载入，其他的在其后载入（用以更好地显示），在移动设备webKit中默认是true，其他默认false。
 detectRetina：如果此项为true，并且用户是视网膜显示模式，会请求规定大小一般的四个切片和一个地区内一个更大的缩放级别来利用高分辨率。
 reuseTiles：如果此项为true，在平移后不可见的切片被放入一个队列中，在新的切片开始可见时他们会被取回（而不是动态地创建一个新的）。这理论上可以降低内存使用率并可以去除在需要新的切片时预留内存。

##### Events（事件）

loading：当切片图层开始加载切片时触发。
 load：当切片图层加载完可见切片后触发。
 tileload：在加载切片时触发。
 tileunload：在切片被移除时触发（比如打开了unloadInvisibleTiles）。

##### Methods（方法）

addTo()：将图层加到地图上。
 bringToFront()：将此切片图层放到所有切片图层之上。
 bringToBack()：将此切片图层放到所有切片图层之下。
 setOpacity()：改变切片图层的透明度。
 setZIndex()：设置切片图层的叠放顺序。
 redraw()：清除所有的切片并重新向服务端申请他们。
 setUrl()：更新图层的URL模板并重绘他们。

### L.TileLayer.WMS

用来显示地图上切片图层的WMS服务，继承自TileLayer。

##### Constructor（函数构造器）

L.TileLayer.WMS()： 通过给定一个基本的WMS服务的URL和WMS参数或选项对象来实例化一个WMS切片图层对象。

##### Options（选项）

layers：WMS图层以逗号分隔符隔开的列表。
 styles：WMS样式以逗号分隔符隔开的列表。
 format：WMS图像格式（用“image/png”来显示透明图层）。
 transparent：如果该项为true，WMS服务返回透明图片。
 version：WMS服务的版本。

##### Methods（方法）

setParams()：融合新的参数和在当前屏幕中重申请的切片（除非noRedraw设置为true）。

### L.TileLayer.Canvas

用来创建浏览器端绘制的切片图层的底层画布。

##### Constructor（函数构造器）

L.TileLayer.Canvas()：通过一个具有选项的对象来实例化一个切片图层画布对象。

##### Options（选项）

async：在实例化时可以异步地绘制切片。在全部绘制完后，tileDrawn方法需要在每个切片上使用。

##### Methods（方法）

drawTile()：在创建实例来绘制切片后你需要定义此方法；canvas是你可以绘制的实际上的切片画布，tilePoint反应了切片的数目，zoom是当前的缩放级别。
 tileDrawn()：如果async选项被定义，在全部绘制完后，这个函数需要在每个切片上使用。canvas与画布对象相同，传递参数给drawTile。

### L.ImageOverlay

用来在地图上规定范围内载入和显示单幅图像，继承自ILayer。

##### Constructor（函数构造器）

L.ImageOverlay()：通过给定图像的URL和相关的地理范围来实例化一个图像叠加层对象。

##### Options（选项）

opacity：图像叠加层的透明度。

##### Methods（方法）

addTo()：将图像叠加层添加到地图上。
 setOpacity()：设置叠加层的透明度。
 bringToFront()：将叠加层置于所有层的顶层。
 bringToBack()：将叠加层置于所有层的底层。

### L.Path

是包含选项和与适量叠加层共享常量的抽象类。不可以接使用。

##### Options（选项）

stroke：路径是否描边。设置为false时，多边形和圆的边界将不可见。
 color：描边颜色。
 weight：描边的像素级别的宽度。
 opacity：描边透明度。
 fill：路径是否填充颜色。设置为false时，多边形和圆的填充内容不可见。
 fillColor：填充颜色。
 fillOpacity：填充透明度。
 dashArray：定义描边线型的字符串。这在画布上不起作用。（比如android 2）
 clickable：如果此项为false，则矢量不产生鼠标事件并表现为底图的一部分。

##### Events（事件）

click：用户点击或点触对象时触发。
 dbclick：用户双击或连续两次点触对象时触发。
 mousedown：当用户在对象上按下鼠标时触发。
 mouseover：当鼠标置于对象上方时触发。
 mouseout：当鼠标离开对象时触发。
 contextmenu：当用户在对象上点击鼠标右键时触发，当此事件被监听时，会阻止弹出浏览器本身的右键菜单。
 add：当路径被添加在地图上时触发。
 remove：当路径在地图上移除时触发。

##### Methods（方法）

addTo()：将图层添加到地图上。
 bindPopup()：将具有特定HTML内容的弹出框与点击路径绑定起来。
 unbindPopup()：将之前的弹出框绑定解除。
 openPopup()：打开之前通过bindPopup方法与路径上指定点或未指定情况下某一点绑定的弹出框。
 closePopup()：如果与路径绑定的弹出框是打开状态的，则将其关闭。
 setStyle()：更改给予对象选项对象的路径的表现形式。
 getBounds()：返回路径的经纬度绑定信息。
 bringToFront()：将此层移至所以路径层的最上层。
 bringToBack()：将此层移至所以路径层的最底层。
 redraw()：重绘图层。在更改了路径的坐标时比较有用。

##### Static properties（静态属性）

SVG：如果用SVG来表达矢量，则此值为true（在当前大多数浏览器中是true）。
 VML：如果VML用来表达矢量，则此值为true（在IE 6-8中适用）。
 CANVAS：如果canvas用来表达矢量，则此值为true（在android 2中适用）。你也可以在页面中载入leaflet之前通过设置全局变量L_PREFER_CANVAS为true来强制使用此项——有时在表达上千上万相同的注记时会显著地提高性能，但目前由于漏洞导致移除图层非常慢。
 CLIP_PADDING：决定地图视图周围裁剪区域延展的大小（与大小相关，比如0.5在每个方向上是屏幕的一半）。较小的值意味着在拖动地图时你会看到被裁剪路径的末端，较大值会降低绘制性能。

### L.Polyline

绘制叠加在地图上线段的类。继承自Path。用Map#addLayer来添加到地图上。

##### Constructor（函数构造器）

L.Polyline()：通过给定的地理点组成的数组和任意的选项对象实例化一个线段。

##### Options（选项）

smoothFactor：决定每一个缩放级别上线段简化程度。如果大的话意味着更好的表现和看起来更光滑，小的话意味更准确地表示。
 noClip：：不允许线段裁剪。

##### Methods（方法）

addLatLng()：向线段添加一个点。
 setLatLngs()：用所给的地理点的数组替代线段上的点。
 getLatLngs()：返回路径上的点组成的数组。
 spliceLatLngs()：允许添加、移除和更改线段上的点。同Array#splice的语法一致。返回移除点组成的数组。
 getBounds()：返回线段的经纬度边界。

### L.MultiPolyline

是FeatureGroup的扩展，用来创建多线（在同一图层中由多个共享样式和弹出框的线段组成）。

##### Constructor（函数构造器）

L.MultiPolyline()：通过给定的地理点的二维数组（其中每个一维数组表示一个线段）和选项对象来实例化一个多线对象。

### L.Polygon

在地图上绘制多边形的类。是Polyline的扩展。用Map#addLayer添加到地图上。
 创建多边形时经过的点没有传统意义上的起点和终点——最好将这种点指出来。

##### Constructor（函数构造器）

L.Polygon()：通过给定地理点组成的数组和选项对象来实例化一个多边形（同线段构造方法相同）。你也可以通过传递经纬度的二维数组来创建一个带有洞的多边形，第一个经纬度数组表示外环，剩下的表示里面的洞。

### L.MultiPolygon

是FeatureGroup的扩展，用来创建多多边形（在同一图层上由共享样式和弹出框的多个多边形组成）。

##### Constructor（函数构造器）

L.MultiPolygon()：通过给定的经纬度的二维数组（每个一维数组表示一个多边形）和选项对象实例化多多边形（同多线相同）。

### L.Rectangle

在地图上绘制矩形的类。是多边形的扩展。用Map#addLayer添加到地图上。

##### Constructor（函数构造器）

L.Rectangle()：通过给定的地理边界和选项对象来实例化一个矩形对象。

##### Methods（方法）

setBounds()：根据传递的边界重绘矩形。

### L.Circle

在地图上绘制圆形叠加物的类。是Path的延伸。用Map#addLayer来添加到地图上。

##### Constructor（函数构造器）

L.Circle()：通过给定的地理点和以米为单位的半径和选项对象来实例化一个圆对象。

##### Methods（方法）

getLatLng()：返回圆当前的地理位置。
 getRadius()：返回圆的半径，以米为单位。
 setLatLng()：将圆放置到一个新的位置。
 setRadius()：设置圆的半径，以米为单位。

### L.CircleMarker

是一个特定半径的圆，半径单位是像素。是Circle的延伸。通过Map#addLayer添加到地图上。

##### Constructor（函数构造器）

L.CircleMarker()：通过给定的地理点和选项对象来实例化一个圆注记。默认的半径是10像素，并且可以通过在路径选项中传递一个半径参数来修改半径。

##### Methods（方法）

setLatLng()：将圆注记放置于一个新的位置。
 setRadius()：设置圆注记的半径，以像素为单位。

### L.LayerGroup

用来将几个图层组成一个组并作为一个图层来处理。如果你将其添加到地图上，组中任何图层的添加或移除都将使其同样在地图添加或删除。继承自ILayer接口。

##### Constructor（函数构造器）

L.LayerGroup()：创建一个组，视情况指定一组初始的图层。

##### Methods（方法）

addTo()：将图组添加到地图上。
 addLayer()：将给定的图层添加到组中。
 removeLayer()：将给定的图层从组中移除：
 clearLayer()：将组中的图层清空。
 eachLayer()：遍历组中的图层，需选择一个符合情况的迭代函数。

### L.FeatureGroup

是LayerGroup的扩展，但多了鼠标事件和共享的弹出框方法。继承自ILayer接口。

##### Constructor（函数构造器）

L.FeatureGroup()：创建一个图组，视情况指定一组初始图层。

##### Methods（方法）

具有LayerGroup所以的方法，还有下面多出的方法：
 bindPopup()：在组中任意具有bindPopup方法的图层上绑定一个具有具体HTML内容的弹出框。
 getBounds()：返回要素组的经纬度边界（通过他子图层的边界和坐标获得）。
 setStyle()：设置组中具有setStyle方法的图层的路径选项。
 bringToFront()：将图组置于顶层。
 bringToBack()：将图组置于底层。

##### Events（事件）

click：用户点击或触摸组是触发。
 dbclick：用户双击或连续两次触摸组时触发。
 mouseover：当鼠标置于组上方时触发。
 mouseout：当鼠标离开组时触发。
 mousemove：当鼠标经过组时触发。
 contextmenu：当用户右击图层时触发。
 layeradd：当图层被加入到组时触发。
 layerremove：当图层从组中移除时触发。

### L.GeoJSON

展示一个GeoJSON的图层。允许你在地图上解析并显示GeoJSON数据。是FeatureGroup的延伸。
 由此创建的每个要素层获取要素与之关联的GeoJSON数据属性（因此你随后可以传递它的属性）。

##### Constructor（函数构造器）

L.GeoJSON()：创建一个GeoJSON图层。可以任意地接受GeoJSON格式的对象和选项对象并显示在地图上（随后可以选择用addData方法添加）。

##### Options（选项）

pointToLayer()：在创建GeoJSON点图层时所用到的函数（如果不特意说明，会创建简单的注记）。
 style()：在获取用来创建GeoJSON要素的矢量图层的样式选项时可以用到。
 onEachFeature()：在每个创建的图层上都会调用此函数。对于向要素添加事件和弹出框比较有用。
 filter()：用来决定是否显示某要素的函数。

##### Methods（方法）

addData()：在图层中添加GeoJSON对象。
 setStyle()：通过给定的样式函数改变GeoJSON矢量图层的样式。
 resetStyle()：将矢量图层样式重置为初始GeoJSON样式，对于hover事件之后的重置比较有用。

##### Static methods（静态方法）

geometryToLayer():通过给定的GeoJSON要素创建图层。
 coordsToLatlng():通过在GeoJSON中表示点的两个数字组成（分别表示纬度和经度）的数组来创建经纬度对象。如果reverse设置为true，那么这两个数字被颠倒，表经度和纬度。
 coordsToLatlngs():通过GeoJSON坐标坐标的数组创建多维数组。leversDeep指定具体的嵌套级别（0表示点的数组，1表示点数组的数组等等，0为默认值）。如果reverse设置为true，这些数组变为经度和纬度。

### L.LatLng

表示通过某一经度和纬度确定的地理上的点。
 所以leaflet接受的经纬度对象也接受他们的单一数组的形式（除非在其他方面表明不可以）。

##### Constructor（函数构造器）

L.LatLng()：通过给定的纬度和经度创建表示地理点的对象。

##### Options（选项）

lat：以度数表示的纬度。
 lng：以度数表示的经度。

##### Methods（方法）

distanceTo()：返回到通过半正矢公式计算的经纬度的距离（用米表示）。
 equals()：如果给定的经纬度在相同的位置（具有较小的容差）则返回true。
 toString()：返回点的描述信息（用来调试用）。
 wrap()：返回在经度上left和right边界覆盖范围内（默认为0180到180）的心的经纬度对象。

##### Constants（常量）

DEG_TO_RAD:度数转换为弧度的乘子。
 RAD_TO_DEG:弧度转换为度数的乘子。
 MAX_MARGIN:判断相等的容差。

### L.LatLngBounds

表示地图上一个矩形的区域。
 所有接受LatLngBounds对象的leaflet方法也接受他们简单数组的形式（除非另行说明）。

##### Constructor（函数构造器）

L.LatLngBounds(西南角点,东北角点)：通过定义矩形西南角点和东北角点来创建经纬度的矩形框。
 L.LatLngBounds()：通过定义内在点来创建经纬度的矩形框。当用fitBounds把地图放到适合某些位置的缩放级别时是比较有用的。

##### Methods（方法）

extend()：将边界延伸到包含给定点和边界的范围。
 geSouthWest()：返回边界的西南角点。
 getNorthEast()：返回边界的东北角点。
 getNorthWest()：返回边界的西北角点。
 getSouthEast()：返回边界的东南角点。
 getWest()：返回边界的西点。
 getSouth()：返回边界的南角点。
 getEast()：返回边界的东角点。
 getNorth()：返回边界的北角点。
 getCenter()：返回边界的中心点。
 containg(otherBounds)：如果矩形框包含给定的边界则返回true。
 contains(latlng)：如果矩形框包含给定的点则返回true。
 intersects()：如果矩形框与给定的边界相交则返回true。
 equals()：如果矩形框与给定的范围相等（在一定容差范围内）则返回true。
 toBBoxString()：返回“西南经度，西南纬度，东北经度，东北纬度”形式的外接矩形的坐标。在向网络服务器提交请求返回地理数据时比较有用。
 pad()：返回当前范围扩大一定百分比后的边界。
 isValid()：如果边界可被初始化则返回true。