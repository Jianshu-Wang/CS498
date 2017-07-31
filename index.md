<title>Life Satisfaction Research of all Countries</title>
<p>This is a narrative visualization of the life satisfaction of people all around the world, I use the drill down story method to show the data for my map</p>
<p>What is the relatioship between life satisfaction and gdp?
From this workbook we can explore the relationship between life satisfaction and gdp. the first sheet overview shows a increasing life satisfaction map on a increasing gdp per capita. but we still need to pay attention on the the second sheet which shows life satisfaction is not always raising with gdp per capita. In order to make it clear, we can pick some samples in the 3rd sheet. I draw my conclustion that, gdp per capita can have a very important effect on life satisfaction, but life satisfaction can depend on many other issues, and situation can be vary in each country.
As we can see there are three charts in the workbook, the dashboard shows a overview and details of the life satisfaction investigation data of the world in the past 30 years. 
The first sheet uses the averge gdp per capita as the horizontal axis and values are logarithmically map on the axis,  the mean values of the life satisfaction are shown on the vertical axis from 3 - 8, I use discrete circles to represent each country and by this method I can show the general overview of situation of all the recorded countries.
The second sheet shows the avg GDP per capita actually is raising from 1988 to 2018, and the color palette is used to show the average life satisfaction of all the country over time, from this effective color palette we can see that there is a sharp decrease of life satisfaction in 2005 even though gdp per capita is still raising.
The third chart shows the data details, in this sheet you can check the life satisfaction and gdp per capita over time in each country, discrete  bars are used to represent the values in the corresponding category.
I think in these 3 charts, the dashboard can a very general overview of the data, we can gain gain all the knowledge that we want to know from different sight.
</p>
{
  "$schema": "https://vega.github.io/schema/vega/v3.0.json",
  "width": 900,
  "height": 500,
  "autosize": "none",

  "encode": {
    "update": {
      "fill": {"signal": "background"}
    }
  },

  "signals": [
    {
      "name": "type",
      "value": "mercator",
      "bind": {
        "input": "select",
        "options": [
          "albers",
          "albersUsa",
          "azimuthalEqualArea",
          "azimuthalEquidistant",
          "conicConformal",
          "conicEqualArea",
          "conicEquidistant",
          "equirectangular",
          "gnomonic",
          "mercator",
          "orthographic",
          "stereographic",
          "transverseMercator"
        ]
      }
    },
    { "name": "scale", "value": 150,
      "bind": {"input": "range", "min": 50, "max": 2000, "step": 1} },
    { "name": "rotate0", "value": 0,
      "bind": {"input": "range", "min": -180, "max": 180, "step": 1} },
    { "name": "rotate1", "value": 0,
      "bind": {"input": "range", "min": -90, "max": 90, "step": 1} },
    { "name": "rotate2", "value": 0,
      "bind": {"input": "range", "min": -180, "max": 180, "step": 1} },
    { "name": "center0", "value": 0,
      "bind": {"input": "range", "min": -180, "max": 180, "step": 1} },
    { "name": "center1", "value": 0,
      "bind": {"input": "range", "min": -90, "max": 90, "step": 1} },
    { "name": "translate0", "update": "width / 2" },
    { "name": "translate1", "update": "height / 2" },

    { "name": "graticuleDash", "value": 0,
      "bind": {"input": "radio", "options": [0, 3, 5, 10]} },
    { "name": "borderWidth", "value": 1,
      "bind": {"input": "text"} },
    { "name": "background", "value": "#ffffff",
      "bind": {"input": "color"} },
    { "name": "invert", "value": false,
      "bind": {"input": "checkbox"} }
  ],

  "projections": [
    {
      "name": "projection",
      "type": {"signal": "type"},
      "scale": {"signal": "scale"},
      "rotate": [
        {"signal": "rotate0"},
        {"signal": "rotate1"},
        {"signal": "rotate2"}
      ],
      "center": [
        {"signal": "center0"},
        {"signal": "center1"}
      ],
      "translate": [
        {"signal": "translate0"},
        {"signal": "translate1"}
      ]
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
        { "type": "graticule" }
      ]
    }
  ],

  "marks": [
    {
      "type": "shape",
      "from": {"data": "graticule"},
      "encode": {
        "update": {
          "strokeWidth": {"value": 1},
          "strokeDash": {"signal": "[+graticuleDash, +graticuleDash]"},
          "stroke": {"signal": "invert ? '#444' : '#ddd'"},
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
        "update": {
          "strokeWidth": {"signal": "+borderWidth"},
          "stroke": {"signal": "invert ? '#777' : '#bbb'"},
          "fill": {"signal": "invert ? '#fff' : '#000'"},
          "zindex": {"value": 0}
        },
        "hover": {
          "strokeWidth": {"signal": "+borderWidth + 1"},
          "stroke": {"value": "firebrick"},
          "zindex": {"value": 1}
        }
      },
      "transform": [
        { "type": "geoshape", "projection": "projection" }
      ]
    }
  ]
}
