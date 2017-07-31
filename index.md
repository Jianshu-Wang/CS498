

<!DOCTYPE html>

<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.2.0/jquery.min.js"></script>

<html>
<head><title>Life Satisfaction Research of all Countries</title>
<p>This is a narrative visualization of the life satisfaction of people all around the world, I use the drill down story method to show the data for my map</p>
<p>What is the relatioship between life satisfaction and gdp?
From this workbook we can explore the relationship between life satisfaction and gdp. the first sheet overview shows a increasing life satisfaction map on a increasing gdp per capita. but we still need to pay attention on the the second sheet which shows life satisfaction is not always raising with gdp per capita. In order to make it clear, we can pick some samples in the 3rd sheet. I draw my conclustion that, gdp per capita can have a very important effect on life satisfaction, but life satisfaction can depend on many other issues, and situation can be vary in each country.
As we can see there are three charts in the workbook, the dashboard shows a overview and details of the life satisfaction investigation data of the world in the past 30 years. 
The first sheet uses the averge gdp per capita as the horizontal axis and values are logarithmically map on the axis,  the mean values of the life satisfaction are shown on the vertical axis from 3 - 8, I use discrete circles to represent each country and by this method I can show the general overview of situation of all the recorded countries.
The second sheet shows the avg GDP per capita actually is raising from 1988 to 2018, and the color palette is used to show the average life satisfaction of all the country over time, from this effective color palette we can see that there is a sharp decrease of life satisfaction in 2005 even though gdp per capita is still raising.
The third chart shows the data details, in this sheet you can check the life satisfaction and gdp per capita over time in each country, discrete  bars are used to represent the values in the corresponding category.
I think in these 3 charts, the dashboard can a very general overview of the data, we can gain gain all the knowledge that we want to know from different sight.
</p></head>

<body>

    <div id="decoy-svg-container">
    <svg id="decoy_viz" width="0" height="0"></svg>
    </div>

    <div id="svg-container">
    <svg id="viz" width="720" height="405"></svg>
    </div>



<script>

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

</body>