<!-- <html>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.0/jquery.min.js"></script>
<head></head>

<body>

    <div id="decoy-svg-container">
    <svg id="decoy_viz" width="0" height="0"></svg>
    </div>

    <div id="svg-container">
    <svg id="viz" width="720" height="405"></svg>
    </div>


<title>Life Satisfaction Research of all Countries</title>
<p>This is a narrative visualization of the life satisfaction of people all around the world, I use the drill down story method to show the data for my map</p>
<p>What is the relatioship between life satisfaction and gdp?
From this workbook we can explore the relationship between life satisfaction and gdp. the first sheet overview shows a increasing life satisfaction map on a increasing gdp per capita. but we still need to pay attention on the the second sheet which shows life satisfaction is not always raising with gdp per capita. In order to make it clear, we can pick some samples in the 3rd sheet. I draw my conclustion that, gdp per capita can have a very important effect on life satisfaction, but life satisfaction can depend on many other issues, and situation can be vary in each country.
As we can see there are three charts in the workbook, the dashboard shows a overview and details of the life satisfaction investigation data of the world in the past 30 years. 
The first sheet uses the averge gdp per capita as the horizontal axis and values are logarithmically map on the axis,  the mean values of the life satisfaction are shown on the vertical axis from 3 - 8, I use discrete circles to represent each country and by this method I can show the general overview of situation of all the recorded countries.
The second sheet shows the avg GDP per capita actually is raising from 1988 to 2018, and the color palette is used to show the average life satisfaction of all the country over time, from this effective color palette we can see that there is a sharp decrease of life satisfaction in 2005 even though gdp per capita is still raising.
The third chart shows the data details, in this sheet you can check the life satisfaction and gdp per capita over time in each country, discrete  bars are used to represent the values in the corresponding category.
I think in these 3 charts, the dashboard can a very general overview of the data, we can gain gain all the knowledge that we want to know from different sight.
</p><
<script>
var map_spec = 
{
  "$schema": "https://vega.github.io/schema/vega/v3.0.json",
  "width": 900,
  "height": 500,
  "autosize": "none",

  "signals": [
    { "name": "tx", "update": "width / 2" },
    { "name": "ty", "update": "height / 2" },
    {
      "name": "scale",
      "value": 150,
      "on": [{
        "events": {"type": "wheel", "consume": true},
        "update": "clamp(scale * pow(1.0005, -event.deltaY * pow(16, event.deltaMode)), 150, 3000)"
      }]
    },
    {
      "name": "angles",
      "value": [0, 0],
      "on": [{
        "events": "mousedown",
        "update": "[rotateX, centerY]"
      }]
    },
    {
      "name": "cloned",
      "value": null,
      "on": [{
        "events": "mousedown",
        "update": "copy('projection')"
      }]
    },
    {
      "name": "start",
      "value": null,
      "on": [{
        "events": "mousedown",
        "update": "invert(cloned, xy())"
      }]
    },
    {
      "name": "drag", "value": null,
      "on": [{
        "events": "[mousedown, window:mouseup] > window:mousemove",
        "update": "invert(cloned, xy())"
      }]
    },
    {
      "name": "delta", "value": null,
      "on": [{
        "events": {"signal": "drag"},
        "update": "[drag[0] - start[0], start[1] - drag[1]]"
      }]
    },
    {
      "name": "rotateX", "value": 0,
      "on": [{
        "events": {"signal": "delta"},
        "update": "angles[0] + delta[0]"
      }]
    },
    {
      "name": "centerY", "value": 0,
      "on": [{
        "events": {"signal": "delta"},
        "update": "clamp(angles[1] + delta[1], -60, 60)"
      }]
    }
  ],

  "projections": [
    {
      "name": "projection",
      "type": "mercator",
      "scale": {"signal": "scale"},
      "rotate": [{"signal": "rotateX"}, 0, 0],
      "center": [0, {"signal": "centerY"}],
      "translate": [{"signal": "tx"}, {"signal": "ty"}]
    }
  ],

  "data": [
    {
      "name": "world",
      "url": "data/world-110m.json",
      "format": {
        "type": "topojson",
        "feature": "countries"
      }
    },
    {
      "name": "graticule",
      "transform": [
        { "type": "graticule", "step": [15, 15] }
      ]
    }
  ],

  "marks": [
    {
      "type": "shape",
      "from": {"data": "graticule"},
      "encode": {
        "enter": {
          "strokeWidth": {"value": 1},
          "stroke": {"value": "#ddd"},
          "fill": {"value": null}
        }
      },
      "transform": [
        { "type": "geoshape", "projection": "projection" }
      ]
    },
    {
      "type": "shape",
      "from": {"data": "world"},
      "encode": {
        "enter": {
          "strokeWidth": {"value": 0.5},
          "stroke": {"value": "#bbb"},
          "fill": {"value": "#e5e8d3"}
        }
      },
      "transform": [
        { "type": "geoshape", "projection": "projection" }
      ]
    }
  ]
}
</script>

</body> -->
<!DOCTYPE html>
<meta charset="utf-8">
<style>

@import url(https://fonts.googleapis.com/css?family=Open+Sans+Condensed:300|Josefin+Slab|Arvo|Lato|Vollkorn|Abril+Fatface|Old+Standard+TT|Droid+Sans|Lobster|Inconsolata|Montserrat|Playfair+Display|Karla|Alegreya|Libre+Baskerville|Merriweather|Lora|Archivo+Narrow|Neuton|Signika|Questrial|Fjalla+One|Bitter|Varela+Round);

.background {
  fill: #eee;
  pointer-events: all;
}

.map-layer {
  fill: #fff;
  stroke: #aaa;
}

.effect-layer{
  pointer-events:none;
}

text{
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-weight: 300;
}

text.big-text{
  font-size: 30px;
  font-weight: 400;
}

.effect-layer text, text.dummy-text{
  font-size: 12px;
}

</style>
<body>

<svg></svg>

<script src="https://d3js.org/d3.v3.min.js"></script>
<script>

var width = 960,
    height = 500,
    centered;

// Define color scale
var color = d3.scale.linear()
  .domain([1, 20])
  .clamp(true)
  .range(['#fff', '#409A99']);

var projection = d3.geo.mercator()
  .scale(1500)
  // Center the Map in Colombia
  .center([-74, 4.5])
  .translate([width / 2, height / 2]);

var path = d3.geo.path()
  .projection(projection);

// Set svg width & height
var svg = d3.select('svg')
  .attr('width', width)
  .attr('height', height);

// Add background
svg.append('rect')
  .attr('class', 'background')
  .attr('width', width)
  .attr('height', height)
  .on('click', clicked);

var g = svg.append('g');

var effectLayer = g.append('g')
  .classed('effect-layer', true);

var mapLayer = g.append('g')
  .classed('map-layer', true);

var dummyText = g.append('text')
  .classed('dummy-text', true)
  .attr('x', 10)
  .attr('y', 30)
  .style('opacity', 0);

var bigText = g.append('text')
  .classed('big-text', true)
  .attr('x', 20)
  .attr('y', 45);

// Load map data
d3.json('colombia.geo.json', function(error, mapData) {
  var features = mapData.features;

  // Update color scale domain based on data
  color.domain([0, d3.max(features, nameLength)]);

  // Draw each province as a path
  mapLayer.selectAll('path')
      .data(features)
    .enter().append('path')
      .attr('d', path)
      .attr('vector-effect', 'non-scaling-stroke')
      .style('fill', fillFn)
      .on('mouseover', mouseover)
      .on('mouseout', mouseout)
      .on('click', clicked);
});

// Get province name
function nameFn(d){
  return d && d.properties ? d.properties.NOMBRE_DPT : null;
}

// Get province name length
function nameLength(d){
  var n = nameFn(d);
  return n ? n.length : 0;
}

// Get province color
function fillFn(d){
  return color(nameLength(d));
}

// When clicked, zoom in
function clicked(d) {
  var x, y, k;

  // Compute centroid of the selected path
  if (d && centered !== d) {
    var centroid = path.centroid(d);
    x = centroid[0];
    y = centroid[1];
    k = 4;
    centered = d;
  } else {
    x = width / 2;
    y = height / 2;
    k = 1;
    centered = null;
  }

  // Highlight the clicked province
  mapLayer.selectAll('path')
    .style('fill', function(d){return centered && d===centered ? '#D5708B' : fillFn(d);});

  // Zoom
  g.transition()
    .duration(750)
    .attr('transform', 'translate(' + width / 2 + ',' + height / 2 + ')scale(' + k + ')translate(' + -x + ',' + -y + ')');
}

function mouseover(d){
  // Highlight hovered province
  d3.select(this).style('fill', 'orange');

  // Draw effects
  textArt(nameFn(d));
}

function mouseout(d){
  // Reset province color
  mapLayer.selectAll('path')
    .style('fill', function(d){return centered && d===centered ? '#D5708B' : fillFn(d);});

  // Remove effect text
  effectLayer.selectAll('text').transition()
    .style('opacity', 0)
    .remove();

  // Clear province name
  bigText.text('');
}

// Gimmick
// Just me playing around.
// You won't need this for a regular map.

var BASE_FONT = "'Helvetica Neue', Helvetica, Arial, sans-serif";

var FONTS = [
  "Open Sans",
  "Josefin Slab",
  "Arvo",
  "Lato",
  "Vollkorn",
  "Abril Fatface",
  "Old StandardTT",
  "Droid+Sans",
  "Lobster",
  "Inconsolata",
  "Montserrat",
  "Playfair Display",
  "Karla",
  "Alegreya",
  "Libre Baskerville",
  "Merriweather",
  "Lora",
  "Archivo Narrow",
  "Neuton",
  "Signika",
  "Questrial",
  "Fjalla One",
  "Bitter",
  "Varela Round"
];

function textArt(text){
  // Use random font
  var fontIndex = Math.round(Math.random() * FONTS.length);
  var fontFamily = FONTS[fontIndex] + ', ' + BASE_FONT;

  bigText
    .style('font-family', fontFamily)
    .text(text);

  // Use dummy text to compute actual width of the text
  // getBBox() will return bounding box
  dummyText
    .style('font-family', fontFamily)
    .text(text);
  var bbox = dummyText.node().getBBox();

  var textWidth = bbox.width;
  var textHeight = bbox.height;
  var xGap = 3;
  var yGap = 1;

  // Generate the positions of the text in the background
  var xPtr = 0;
  var yPtr = 0;
  var positions = [];
  var rowCount = 0;
  while(yPtr < height){
    while(xPtr < width){
      var point = {
        text: text,
        index: positions.length,
        x: xPtr,
        y: yPtr
      };
      var dx = point.x - width/2 + textWidth/2;
      var dy = point.y - height/2;
      point.distance = dx*dx + dy*dy;

      positions.push(point);
      xPtr += textWidth + xGap;
    }
    rowCount++;
    xPtr = rowCount%2===0 ? 0 : -textWidth/2;
    xPtr += Math.random() * 10;
    yPtr += textHeight + yGap;
  }

  var selection = effectLayer.selectAll('text')
    .data(positions, function(d){return d.text+'/'+d.index;});

  // Clear old ones
  selection.exit().transition()
    .style('opacity', 0)
    .remove();

  // Create text but set opacity to 0
  selection.enter().append('text')
    .text(function(d){return d.text;})
    .attr('x', function(d){return d.x;})
    .attr('y', function(d){return d.y;})
    .style('font-family', fontFamily)
    .style('fill', '#777')
    .style('opacity', 0);

  selection
    .style('font-family', fontFamily)
    .attr('x', function(d){return d.x;})
    .attr('y', function(d){return d.y;});

  // Create transtion to increase opacity from 0 to 0.1-0.5
  // Add delay based on distance from the center of the <svg> and a bit more randomness.
  selection.transition()
    .delay(function(d){
      return d.distance * 0.01 + Math.random()*1000;
    })
    .style('opacity', function(d){
      return 0.1 + Math.random()*0.4;
    });
}

</script>