# TheWeatherServer
HTML and Javascript examples on how to access data from <a href="http://theweatherserver.com">TheWeatherServer</a>.

This repository contains examples that show how you can use the API of TheWeatherServer.com in your project. The MapTilesExample.html gives an example of how to use the API of TheWeatherServer to provide weather tiles in an OpenLayers-based map display.

A Custom `tileURLFunction` for OpenLayers
----------------------------------------

In the MapTilesExample.html, the tile URL, which is passed to the OpenLayers framework to retrieve the weather tiles, has only parameters `x`, `y` and `z` as variables, which is the standard for OpenLayers. With a little more effort, we can obtain a solution that allows to dynamically set all parameters of the map tiles API, such that you can easily change the data type, the illustration and the forecast time, for example.

For this purpose, we first need to define a function that creates the tile URL from the parameters for data type, plot type, area type and forecast interval:

```
    var createTileUrl = function(tileCoord, pixelRatio, projection) {
        var urlTemplate = 'http://theweatherserver.appspot.com//weatherserver_getTile?x={x}&y={y}&z={z}&dt={datatype}&pt={plottype}&at={areatype}&fi={forecastinterval}';
        return urlTemplate
            .replace('{z}', tileCoord[0].toString())
            .replace('{x}', tileCoord[1].toString())
            .replace('{y}', (-tileCoord[2] - 1).toString())
            .replace('{datatype}', datatype)
            .replace('{plottype}', plottype)
            .replace('{areatype}', areatype)
            .replace('{forecastinterval}', forecastinterval_min);
    }
```      

Note that array `tileCoord` comes from the OpenLayers framework and should not be changed. Variables `datatype`, `plottype`, `areatype` and `forecastinterval`, however, do contain the settings specific to theWeatherServer.com.

Now, we need to make sure that above function `createTileUrl` is used instead of the fixed tile URL, as it was defined in the MapTilesExample.html. We can do this by using a pointer to the function in the definition of the layer that contains the weather tiles:

```
    var weatherlayer = new ol.layer.Tile({
        visible: true,
        source: new ol.source.XYZ({
            tileUrlFunction: createTileUrl
        })
    });
```

The remaining steps are similar to the example from MapTilesExamples.html
