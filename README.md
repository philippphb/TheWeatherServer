# TheWeatherServer
HTML and Javascript examples on how to access data from <a href/"http://theweatherserver.com">TheWeatherServer</a>.

 
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
      
