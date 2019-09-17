<img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Logo.png">


<h1 align="center"> Happy GIS Day! </h1>

如果你是 GIS 专业的同学，一定对 John Snow 这个名字不陌生，他是英国著名内科医生，为霍乱的研究作出重大贡献。

这节课我们一起试试使用 Mapbix Studio 和 Mapbox GL JS 重建 John Snow 在研究 1854 伦敦霍乱爆发使用的空间分析地图。

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

Click the Style tab and the map will switch back to style mode displaying your new layer. You will see the point data on the map with a default style (black with 100% opacity). 

In the Mapbox Studio style editor, you create graduated points based on the number of cholera deaths by increasing or decreasing the radius size of the points. Change the name of your data layer to 'Cholera Death' and select __radius__ ,  __style across a data range__ and then select the __Deaths #__ field.

<p align = "center">
  <img src= "https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Style_Radius.gif">
</p>


The rate of change should be set to __Linear__.

Now it's time to start adding stops! You will create several stops to break the cholera death data up into groups. We will be breaking the data out into 5 classes.

<p align = "center">
  <img src ="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Cholera_Deaths_1.png">
  </p>
  
Once you've finished creating your graduated points, add the Cholera Pumps data to the map twice. Rename one layer 'Pumps' and the other 'Pumps Outline'.

Change the radius of the 'Pumps' layer to 4 and change the color to #7f0101. 

<p align = "center">
  <img src ="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Pumps_Layer.png">
  </p>
  
Next, increase the radius of the 'Pumps Outline' layer to 6, change the color to #000000 and the stroke color to #7f0101. 

<p align = "center">
  <img src ="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Pumps_Outline.png">
  </p>
  

  
## Publish your style 

Now that you've got your map looking good, it's time to publish! Click the Publish style button at the top of the toolbar on the right side of the screen, then click Publish again on the next prompt.

Hooray! Your style is now published! If you go back to your Styles page, you will see your new style at the top of the list.

You can use your ‘Share URL’ to open your style in a new browser tab and share it with collaborators for review.


## Create a web map 

Now that we have edited our layers and created a style, let's create a web map! 

For this part of the lesson, we will be using a program called JSFiddle. You can sign up for a free acount at: https://jsfiddle.net/

JSFiddle is a simple tool for building and testing code for web development. We recommend using JSFiddle in a Chrome browser

For simplicity, we recommend that you change the editor layout settings in JSFiddle to display by ‘tabs’.

Initialize your map by copying the following code into the HTML tab of your JSFiddle:

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

### Add a title and info box(front-end UI):

Add the following code between the <body> opening and </body> closing tags:

```
<div id='map'></div>
<div class='map-overlay' id='features'> <h2>Broad Street, 1854</h2></div>
```

Next, you will also want to apply some CSS to visualize what the layout looks like. This creates the visual rules for our front-end elements (legend, title box, information box). Under the opening ```<style>``` tag at the top of your code, add the following: 
  
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

Hit run to see your changes. 

In the next step, you will add the map to your page and the project will start taking shape.

### Initialize the map 

For the next step you will need a [Mapbox access token](https://docs.mapbox.com/help/how-mapbox-works/access-tokens/) and your [style ID](https://docs.mapbox.com/help/glossary/style-id/). Without this, the rest of the code will not work. 

For the next step you will need a [Mapbox access token](https://docs.mapbox.com/help/how-mapbox-works/access-tokens/) and your [style ID](https://docs.mapbox.com/help/glossary/style-id/). Without this, the rest of the code will not work. 

<p align = "center">
  <img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Access_Token.png">
</p>

<p align = "center">
<img src="https://github.com/mjdanielson/University-of-Buffalo/blob/master/Labs/Choropleth-Map/Images/Style_ID.gif">
</p>

Add the following code after <div class='map-over' id='legend'></div> and before the closing </body> tag

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

Add your style id to the map variable. Edit the line of code that has the comment 'replace this with your style URL'.

```
style: 'your-style-url', // replace this with your style URL
```

Next, we want to center our map on our data. Locate the line of code that is telling the map where to center the view. Try changing the center location by picking a new coordinate using http://geojson.io/ (or looking at the bottom of the right-hand panel in the Mapbox Studio style editor). Change the coordinates in your code and run your changes.

```
center: [,], // starting position [lng, lat] 
```

Change the zoom level to 15.5.

```
zoom: 3 // starting zoom - change the starting zoom position to 15.5
```

Hit run to see your changes. 

<p align="center">
  <img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Map-V1.png">
  </p>

### Add additional information

With some projects, this is where you'd stop: you put a map on a page! But for this map, you will add two pieces of additional information that will make the map even more useful: an information window that gives the user a brief history of the cholera outbreak of 1854 and a pop up that displays the number of cholera deaths for whatever graduated point the cursor is hovering on.

### Add the information box 

Add the following code to your <div> element containing your map overlay class. This text should go after your 'Broad Street, 1854' header. 
  
  
```
<p>During the mid-1800’s in London, Dr. John Snow mapped all the occurrences of cholera by home address, as well as the location of public water pumps. </p>
<p>By analyzing the spatial pattern, Snow was able to determine the water pump on Broad Street was the source of the outbreak. 
</p>
```

### [The load event](https://docs.mapbox.com/help/tutorials/choropleth-studio-gl-pt-2/#the-load-event)

What is a callback?

Initializing the map on the page does more than create a container in the map div. It also tells the browser to request the Mapbox Studio style you created in part 1. This can take variable amounts of time depending on how quickly the Mapbox server can respond to that request, and everything else you're going to add in the code relies on that style being loaded onto the map. As such, it's important to make sure the style is loaded before any more code is executed.

Fortunately, the map object can tell your browser about certain events that occur when the map's state changes. One of these events is load, which is emitted when the style has been loaded onto the map. Through the map.on method, you can make sure that none of the rest of your code is executed until that event occurs by placing it in a [callback function](https://github.com/maxogden/art-of-node#callbacks) that is called when the load event occurs.

To make sure the rest of the code can execute, it needs to live in a callback function that is executed when the map is finished loading.

Add the load event before the closing script tag </script>

```
map.on('load', function() {
  // the rest of the code will go in here
});
```


### Add a popup! 

When the cursor is hovering over a graduate point a popup will display the number of cholera related deaths recorded in that region. 

To do this, add a listener for the mousemove event, identify which graduated point is at the location of the cursor if any, and create a popup:

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


### Mission Complete!

You have successfully recreated John Snow's famous map! Congratulations and happy GIS day! The final map can be accessed [here](https://mjdanielson.github.io/Cholera-Map/). 


<p align="center">
	<img src="https://github.com/mjdanielson/Cholera-Map/blob/master/Images/Final.png">
	</p>
