<img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Logo.png">

<h1 align="center"> Happy GIS Day! </h1>

如果你是 GIS 专业的同学，一定对 John Snow 这个名字不陌生，他是英国著名内科医生，为霍乱的研究作出重大贡献。

这节课我们一起试试使用 Mapbix Studio 和 Mapbox GL JS 重建 John Snow 在研究 1854 伦敦霍乱爆发使用的空间分析地图。

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/broad-street-pump2.jpg">
  </p>

<p align="center"> <i> 1854 伦敦霍乱爆发 </i> </p>
<h2 align="center"> <strong> John Snow 是谁? </strong></h2>
<p align="center">
<img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Dr_John_Snow.jpg"> 
</p> 

John Snow 博士被认为是现代流行病学的先驱之一，部分原因是他在 1854 年伦敦霍乱爆发期间的开创性工作。在 1800 年代中期，流行的理论是这些爆发是由 Miasma（由于颗粒分解导致的空气中疾病传播）引起的。

然而，John Snow 持怀疑态度。他根据家庭住址以及公共水泵的位置，将霍乱事件绘制在地图上。通过分析空间格局，他最终确定 Broad Street 上的水泵是霍乱爆发的源头。

这张地图就是我们今天要学习绘制的 1854 伦敦霍乱爆发地图。

<h1 align="center"> 1854 伦敦霍乱爆发地图制作教程 </h1>

在本教程中，您将会学习到：

* 上传数据并作矢量切片
* 使用 [Cartogram](https://apps.mapbox.com/cartogram/#13.01/40.7251/-74.0051) 获得相应的[地图样式](https://docs.mapbox.com/help/how-mapbox-works/map-design/#how-map-styles-work) 作为底图
* 在样式地图上[添加数据](https://www.mapbox.com/help/uploads/) to a style
* 在样式地图上[管理并编辑图层](https://www.mapbox.com/studio-manual/reference/styles/#style-editor) in your style
* 制作一张网页端在线地图
* 在地图上添加基本的交互

## 软件准备

* Mapbox 账户，可以在 Mapbox.com 进行免费注册
* JSFiddle，实时显示 JS 代码前端效果的神奇工具

## 数据准备

* [Cholera deaths](https://github.com/mjdanielson/Cholera-Map/blob/master/Data/Cholera_Deaths.geojson): 1854 年因霍乱去世，按位置分布的人数 geojson 文件。

* [Location of pumps](https://github.com/mjdanielson/Cholera-Map/blob/master/Data/Cholera_Pumps.geojson)：水泵的位置 geojson 文件。

## 上传数据并作矢量切片

我们可以把数据上传到 [tileset editor](https://studio.mapbox.com/tilesets/) 中. 在 tileset editor 页面顶部，选择
  <img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Tileset.png" title="Tileset Upload">。 选择 __Upload File__ 和 __Select a file__ 导航到相应文件的位置，选择人口数据 GeoJSON 文件，点击 __Confirm__. 

  <p align= 'center'>
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Screen%20Shot%202019-09-05%20at%204.11.18%20PM.png" title="Tileset1">
  </p>

当你在 Mapbox account 中上传矢量数据时，我们的服务器会将其转换为 [vector tileset](https://docs.mapbox.com/help/glossary/tileset/) 以便在 Mapbox Studio 样式编辑器和 Mapbox GL JS 中快速有效地呈现它。 tileset 信息页面显示了一些有关从您上传的数据创建的 tileset 的有用信息。可以登陆上去随便看看每个新 tileset 的信息页面。

将 Cholera_Pump.geojson 上传并自动转化为 tileset. 


## 使用 Cartogram 创建底图样式
  
数据上传后，我们还需要一个新的地图样式来放置这些数据！到 [Cartogram 主页](https://apps.mapbox.com/cartogram/#13.01/40.7251/-74.0051) 中. 我们可以找一张 John Snow 的 Broad Street Map，并传到 Cartogram 中。你可以用下面这张图来做测试。

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/broadstreet(source13)-large.jpg" width="500" height="474" title="Broad Street Pump"> 
</p>

往 Cartogram 中上传了照片后，可以微调建筑、土地、字体和街道的风格，直到你满意为止。

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/cartogram.gif" width="576" height="261.6">
  </p>
   
调整好以后，选择屏幕顶部的 <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/saved_style.png" width="148" height="20"> 。这样就可以自动在 Mapbox Studio 里面打开你刚调整后的样式，可以进行进一步编辑。

在 Mapbox Studio 中，可以重命名你的 Style 名字。我们在这里把 Style 的名字重新命名为 'John Snow Cholera'. 

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Style_Name.png">
  </p>

### 在地图样式上 [添加数据](https://www.mapbox.com/help/uploads/)

为了在地图上添加 Cholera deaths 数据, 你需要新增一个图层。在编辑器左侧的 layer 面板中，点击 <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Add_Layer.png">。

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Add_Layer.gif">
  </p>

现在就像拍了X光片一样，地图进入了“x-ray 模式。” X-ray 模式可以显示所有将会被加到地图上的数据源，无论有没有样式。

在 New layer 面板中，查看 Cholera Deaths 的数据源列表。单击 tileset，然后选择源图层作为此新样式图层的源。

默认的基本地图视图不以英格兰伦敦为中心。 Mapbox Studio 会识别您上传的数据集中在不同的位置，因此会显示消息“This tileset isn't available from your map view”。单击转到数据，地图视图将重新聚焦美国，并缩放到您的图层（伦敦，英格兰）。

通过单击“图层”列表中图层的名称，可以单独设置 Studio 中的每个图层的样式。有几种图层类型可供选择。每个图层类型都有一组可以指定的唯一图层属性。有几个选项可用于指定属性值。您可以根据数据属性，基于缩放级别或其他属性的值单独选择值。有关图层类型及其样式规则的更多信息，请参阅[参考指南]（https://docs.mapbox.com/studio-manual/reference/styles/）。

## 在样式地图中[管理并编辑图层](https://www.mapbox.com/studio-manual/reference/styles/#style-editor)

单击“Style”选项卡，地图将切换回显示新图层的样式模式。您将在地图上看到具有默认样式的点数据（黑色，100％不透明度）。

在 Mapbox Studio 样式编辑器中，您可以通过增加或减少点的半径大小来创建渐变点，用来表示霍乱死亡的人数。更改数据层的名称为'Cholera Death' 并选择  __radius__ ,  __style across a data range__ 和 __Deaths #__ 域.

<p align = "center">
  <img src= "https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Style_Radius.gif">
</p>

变化率（The rate of change）这里我们可以设置成 __Linear__。

现在我们给数据添加一些分级点，这样可以将 cholera death 数据分组，在这里我们按照数量的多少分成了五组，为每一组设置不同的半径大小。

<p align = "center">
  <img src ="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Cholera_Deaths_1.png">
  </p>
  
完成创建分级点后，我们将 Cholera Pumps 数据两次添加到地图上。重命名一层'Pumps'和另一层'Pumps Outline'。

将“Pumps”图层的半径更改为4，并将颜色更改为＃7f0101。

<p align = "center">
  <img src ="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Pumps_Layer.png">
  </p>
  
接下来，将'Pumps Outline' 层的半径增加到 6, 将颜色改为 #000000，并设置 stroke color 为 #7f0101. 

<p align = "center">
  <img src ="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Pumps_Outline.png">
  </p>
  

  
## 发布你的样式 

现在你的地图看起来很好，是时候发布了！单击屏幕右侧工具栏顶部的“Publish”按钮，然后在下一个提示中再次单击“Publish”。

万岁！你的风格现已发布！如果你返回“Style”页面，您将在列表顶部看到新样式。

你可以使用“Share URL”在新的浏览器标签中打开你的样式，并与协作者共享以供审核。


## 制作网页在线地图 

现在我们已经编辑了图层并创建了一个样式，让我们创建一个网页版的在线地图！

对于本课程的这一部分，我们将使用一个名为 JSFiddle 的工具。您可以在以下网址注册免费账号：https：//jsfiddle.net/

JSFiddle 是一个用于构建和测试 Web 开发代码的简单工具。我们建议在 Chrome 浏览器中使用 JSFiddle。

为简单起见，我们建议您更改 JSFiddle 中的编辑器布局设置以通过“tabs”显示。

通过将以下代码复制到 JSFiddle 的HTML选项卡中来初始化地图：

```
<!DOCTYPE html>
<html>

  <head>
    <meta charset='utf-8' />
    <title>Cholera Map</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/v1.3.1/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/v1.3.1/mapbox-gl.css' rel='stylesheet' />
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }

    </style>
  </head>

  <body>
  </body>

</html>

```

### 添加标题和信息框(前端 UI):

在 <body> 和 </body> 之间添加下面的代码:

```
<div id='map'></div>
<div class='map-overlay' id='features'> <h2>Broad Street, 1854</h2></div>
```

接下来，您还需要应用一些CSS来可视化布局的外观。这为我们的前端元素（图例，标题框，信息框）创建了可视化规则。在代码顶部的开头```<style>```标签下，添加以下内容：
  
```  
h2,
h3 {
  margin: 10px;
  font-size: 1.2em;
}

h3 {
  font-size: 1em;
}

p {
  font-size: 0.85em;
  margin: 10px;
  text-align: left;
}

/**
* Set rules for how the map overlays
* information box will be displayed
* on the page. */

.map-overlay {
  position: absolute;
  bottom: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.7);
  margin-right: 20px;
  font-family: Courier, sans-serif;
  overflow: auto;
  border-radius: 3px;
}

#features {
  top: 0;
  height: 200px;
  margin-top: 20px;
  width: 350px;
}



/* Styling your pop-up */
.mapboxgl-popup-close-button {
  display: none;
}

.mapboxgl-popup-content {
  font: 400 12px/20px 'Courier', Sans-serif;
  padding: 2;
  /*controling transparency and color of pop-up */
  background-color: rgba(255,255,255,.75);
}

.mapboxgl-popup-content-wrapper {
  padding: 2%;
}


```

点击运行看看效果吧！ 

下一步，我们将把地图添加到页面中，项目将开始成型了。

### 初始化地图 

这一步你需要一个 [Mapbox access token](https://docs.mapbox.com/help/how-mapbox-works/access-tokens/) 以及 [style ID](https://docs.mapbox.com/help/glossary/style-id/). 否则下面的代码就没办法正常工作了。

<p align = "center">
  <img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Access_Token.png">
</p>

<p align = "center">
<img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Style_ID.gif">
</p>

在 <div class='map-over' id='legend'></div> 和 </body> 之间加入下面的代码。

```
<script>
mapboxgl.accessToken = 'pk.eyJ1IjoibWpkYW5pZWxzb24iLCJhIjoiY2p2bzFlbnZ5MW5pbTN5cGJ2YWp2MW9vaiJ9.kAaZq3iyJwvrMLK7XDs_qw';
var map = new mapboxgl.Map({
    container: 'map', // container id
    style: 'your-style-url', // replace this with your style URL
    center: [,], // starting position [lng, lat] - adjust the starting position to be centered on Soho, London (-0.137,  51.513) 
    zoom: 3 // starting zoom - change the starting zoom position to 15.5 
});
</script>
```

将你的 style id 加到相应区域，如下所示。

```
style: 'your-style-url', // replace this with your style URL
```

接下来，我们希望将地图集中在我们的数据位置。找到告诉地图将视图居中的位置的代码行。尝试使用http://geojson.io/（或在 Mapbox Studio 样式编辑器中查看右侧面板的底部）选择一个新坐标来更改中心位置。更改代码中的坐标并运行更改。

```
center: [,], // starting position [lng, lat] 
```

将缩放值改为 15.5.

```
zoom: 3 // starting zoom - change the starting zoom position to 15.5
```

点击运行查看结果！

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Map-V1.png">
  </p>

### 增加额外的信息

对于某些项目，我们完成的就差不多了：在页面上放置地图！但是对于这张地图，你将添加两条额外的信息，使地图更有用：一个信息窗口，向用户提供1854年霍乱爆发的简要历史记录，以及在光标悬停在渐变点上的时候，显示霍乱死亡人数的弹出窗口。

### 增加信息窗口

将以下代码添加到包含地图覆盖类的 <div> 元素中。这段文字应该在你的'Broad Street，1854'标题之后。
	
  
```
<p>During the mid-1800’s in London, Dr. John Snow mapped all the occurrences of cholera by home address, as well as the location of public water pumps. </p>
<p>By analyzing the spatial pattern, Snow was able to determine the water pump on Broad Street was the source of the outbreak. 
</p>
```

### [加载事件](https://docs.mapbox.com/help/tutorials/choropleth-studio-gl-pt-2/#the-load-event)

什么是回调？

在页面上初始化地图不仅仅是在地图 div 中创建容器。它还告诉浏览器请求您在第1部分中创建的 Mapbox Studio 样式。这可能需要不同的时间，具体取决于 Mapbox服务器响应该请求的速度，以及您要在代码中添加的所有其他内容依赖将该样式加载到地图上。因此，在执行任何更多代码之前确保加载样式非常重要。

幸运的是，地图对象可以告诉您的浏览器有关地图状态发生变化时发生的某些事件。其中一个事件是 load，它在样式加载到地图时发出。通过 map.on 方法，您可以通过将其置于[回调函数]（https://github.com/maxogden/art-of-node）来确保在该事件发生之前不会执行其余任何代码。 #callbacks）在 load事 件发生时调用。

为了确保代码的其余部分可以执行，它需要存在于地图加载完成时执行的回调函数。

在结束脚本标记</ script>之前添加load事件

```
map.on('load', function() {
  // the rest of the code will go in here
});
```


### 添加弹窗！

当光标悬停在渐变点上时，弹出窗口将显示该区域记录的霍乱相关死亡人数。

为此，为 mousemove 事件添加一个监听器，识别哪个渐变点位于光标位置（如果有），并创建一个弹出窗口：

```
var features = map.queryRenderedFeatures(e.point, {
    layers: ['Cholera Deaths'] // replace this with the name of the layer
  });
  
  if (!features.length) {
    return;
  }
  var feature = features[0];

});


//initialize popup 

var popup = new mapboxgl.Popup({ 
		closeButton: false,
                closeOnClick: true,
});

 // When a click event occurs on a feature in the Cholera Deaths layer, open a popup at the
// location of the click, with description HTML from its properties.

map.on('mouseenter', 'Cholera Deaths', function (e) {
//change the cursor style as a UI indicator
map.getCanvas().style.cursor = 'pointer';

// Create variables for your tabular information 
var aggregate = e.features[0].properties.Deaths;

// Populate the popup and set its coordinates
// based on the feature found.
popup.setLngLat(e.lngLat)
.setHTML(aggregate)
.addTo(map);
});

 
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'Cholera Deaths', function () {
map.getCanvas().style.cursor = '';

```


### 任务完成！

你已经成功重建了一个 John Snow 最著名的地图！恭喜！可以到 [这里](https://mjdanielson.github.io/Cholera-Map/) 体验一下最终的成品。记得分享给的你同学哦。


<p align="center">
	<img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Final.png">
	</p>
