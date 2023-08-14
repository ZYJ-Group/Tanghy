//GEE 北京2023-08-01到2023-08-08的云图像数据
var roiCoordinates = [
  [112.65931859449563, 37.74922317697311],
  [120.63539281324563, 37.74922317697311],
  [120.63539281324563, 42.15954015334511],
  [112.65931859449563, 42.15954015334511],
  [112.65931859449563, 37.74922317697311]
];
var roiPolygon = ee.Geometry.Polygon(roiCoordinates);

var dateList = ['2023-08-01', '2023-08-02', '2023-08-03', '2023-08-04', '2023-08-05', '2023-08-06', '2023-08-07', '2023-08-08'];

// 遍历日期列表，导出每天的平均值图像
dateList.forEach(function(dateStr) {
  var currentDate = ee.Date(dateStr);
  
  var collection = ee.ImageCollection('COPERNICUS/S5P/NRTI/L3_CLOUD')
    .select('cloud_fraction')
    .filterDate(currentDate, currentDate.advance(1, 'day'))
    .filterBounds(roiPolygon);

  var band_viz = {
    min: 0,
    max: 0.95,
    palette: ['black', 'blue', 'purple', 'cyan', 'green', 'yellow', 'red']
  };

  // 计算每天的平均值图像
  var meanImage = collection.mean();

  var visualization = meanImage.visualize(band_viz);

  // 导出每天的平均值图像
  Export.image.toDrive({
    image: visualization,
    description: 'S5P_Cloud_' + dateStr,
    folder: 'GEE_Export',
    fileNamePrefix: 'S5P_Cloud_' + dateStr,
    scale: 1000,
    region: roiPolygon,
    maxPixels: 1e13
  });
});
