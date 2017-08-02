<!DOCTYPE html>
<html>
<head>
	<title>Happiness Investigation</title>
	<script src="d3.js">
	</script>
	<script src="https://d3js.org/d3.v3.min.js"></script>
	<link rel="stylesheet" type="text/css" href="jquery.fullPage.css" />
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    <script src="vendors/jquery.easings.min.js"></script>
    <script type="text/javascript" src="jquery.fullPage.min.js"></script>
		<script type="text/javascript">
    $(document).ready(function() {
        $('#fullpage').fullpage();
    });
</script>
	<style>
	#tooltip{
		opacity: 0;
		position: absolute;
		text-align: left;
		width: 260px;
		height: 80px;
		background: orange;
		border: 0px;
	}
	#tooltip2{
		opacity: 0;
		position: absolute;
		text-align: center;
		width: 210px;
		height: 80px;
		background: lightSteelBlue;
		border: 0px;
	}
	.section{
    font-size: 2em;
    text-align: center;
}
	</style>

</head>
<body>
	<!-- <div id="fullpage">
    <div class="section">
			<h2>Life Satisfaction Investigation</h2>
			<p>This fugure shows the happiness investigation result all over the world, I use interactive slide show to show a general data view. Because this is the best way to clarify a good summary of life satisfaction in each country and each area.</p>
			<p>From the first section we can see the rate summary in each continent, once you move the mouseover the bars, you will get a average rate of all the countries in this continent, and the highest and lowest rate and its corresponding country name. </p>
		</div>
    <div class="section">



		</div>
		<div class="section">Section 3</div>
</div> -->
<!-- <script>
$('#fullpage').fullpage({
    sectionsColor: ['#f2f2f2', '#4BBFC3', '#7BAABE', 'whitesmoke'],
		navigation: true,
		afterReader: function(){
			setInterval(function(){
				$.fn.fullpage.moveSectionDown();
			},1500)
		}
});
</script> -->
<svg class="chart"></svg>
<div id="tooltip" opacity=0></div>
<div id="tooltip2" opacity=0></div>
<script>
d3.json("continentRate.json",function(data){
	var tooltip = d3.select("#tooltip");

	var width = 750;
	var height = 600;
	var padding = 100;
	// var heightScale = d3.scale.linear()
	// 									.domain([0,10])
	// 									.range([height - padding, padding]);

	var yScale = d3.scale.linear()
								.domain([0,10])
								.range([height - padding, padding]);

	var xScale = d3.scale.linear()
								.domain([0,10])
								.range([padding, width - padding]);

	var yAxis = d3.svg.axis()
						// .ticks(5)
						.orient("left")
						.scale(yScale);

	var xAxis = d3.svg.axis()
						.ticks(1)
						.orient("bottom")
						.scale(xScale);

	var canvas = d3.select("body")
									.append("svg")
									.attr("width",width)
									.attr("height",height);

	canvas.append("g")
				.attr("transform", "translate("+80+",0)")
				.attr("class", "axis")
				.call(yAxis);

	// canvas.append("g")
	// 				.attr("transform", "translate("+-25+",500)")
	// 	      .attr("class", "axis")
	// 				.call(xAxis);

	canvas.selectAll("rect")
	.data(data)
	.enter()
	.append("rect")
	.attr("height",function(d){return d.rate*40;})
	.attr("width",70)
	.attr("x",function(d,i){return i*80;})
	.attr("y",function(d){return 400-d.rate*40})
	.attr("fill","steelblue")
	.attr("transform", "translate("+100+",100)")
	.on("mouseover",function(d,i){
	tooltip.style("opacity",1)
	.style("left",(d3.event.pageX)+"px")
	.style("top",(d3.event.pageY)+"px")
	.html("Countries Investigated: "+d.number+"<br/>"+"Average Happiness Rate: "+ d.rate + "<br/>"+
				"Highest Rate: "+ d.max+"<br/>"+"Lowest Rate: "+ d.min);})
	.on("mouseout",function(d){tooltip.style("opacity",0);})



	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 50 +","+300+")rotate(-90)")  // text is drawn off the screen top left, move down and out and rotate
					.text("Average Happiness Rate");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 135 +","+530+")")  // centre below axis
					.text("Africa");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 135 +","+380+")")  // centre below axis
					.attr("fill","white").text("36");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 215 +","+530+")")  // centre below axis
					.text("S.America");
	canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 215 +","+290+")")  // centre below axis
						.attr("fill","white").text("10");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 295 +","+530+")")  // centre below axis
					.text("N.America");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 295 +","+310+")")  // centre below axis
					.attr("fill","white").text("13");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 375 +","+530+")")  // centre below axis
					.text("Asia");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 375 +","+330+")")  // centre below axis
					.attr("fill","white").text("39");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 455 +","+530+")")  // centre below axis
					.text("Europe");
  canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 455 +","+300+")")  // centre below axis
					.attr("fill","white").text("39");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 535 +","+530+")")  // centre below axis
					.text("Oceania");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 535 +","+250+")")  // centre below axis
					.attr("fill","white").text("2");
	canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 330 +","+70+")")  // centre below axis
					.text("General happiness rate information in each continent, mouseover to check summary");



})

</script>


<script>

d3.json("happiness.json",function(chart2data){
	var tooltip2 = d3.select("#tooltip2");
	var chart2width = 750;
	var chart2height = 600;
	var chart2padding = 100;


	var y2Scale = d3.scale.linear()
								.domain([0,10])
								.range([chart2height - chart2padding, chart2padding]);

	var x2Scale = d3.scale.log()
								.domain([500,100000])
								.range([chart2padding, chart2width - chart2padding])
								.base(10);
	var y2Axis = d3.svg.axis()
						.scale(y2Scale)
						.ticks(5)
						.orient("left");

	var x2Axis = d3.svg.axis()
						.orient("bottom")
						.scale(x2Scale)
						.tickFormat(function (d) {
        return x2Scale.tickFormat(5,d3.format(",d"))(d)
});

	var chart2canvas = d3.select("body")
									.append("svg")
									.attr("width",chart2width)
									.attr("height",chart2height);

  chart2canvas.append("g")
			.attr("transform", "translate("+80+",0)")
			.attr("class", "axis axis--y")
			.call(y2Axis);

	chart2canvas.append("g")
					.attr("transform", "translate("+-25+",520)")
		      .attr("class", "axis axis--x")
					.call(x2Axis);

  chart2canvas.append("g")
				.attr("transform", "translate("+650+",0)")
				.attr("class", "axis");
	chart2canvas.selectAll("circle")
	.data(chart2data)
	.enter()
	.append("circle")
	.attr("cx",function(d){return Math.log(d.FIELD4)*100-700;})
	.attr("cy",function(d){return 400-d.FIELD5*40;})
	.attr("r",function(d){return 4})
	.attr("fill",function(d){return d.color;})
	.attr("transform", "translate("+150+",100)")
	.on("mouseover",function(d,i){
	tooltip2.style("opacity",1)
	.style("left",(d3.event.pageX)+"px")
	.style("top",(d3.event.pageY)+"px")
	.html(d.FIELD1+"<br/>"+ " Happiness Rate: "+d.FIELD5.toFixed(3)+"<br/>"+"Continent: "+d.Area+"<br/>"+ "Gdp per capita: "+d.FIELD4.toFixed(2));})
	.on("mouseout",function(d){tooltip2.style("opacity",0);})
	;


	chart2canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 50 +","+300+")rotate(-90)")  // text is drawn off the screen top left, move down and out and rotate
					.text("Life Satisfaction Rate");
  chart2canvas.append("text")
					.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
					.attr("transform", "translate("+ 360 +","+560+")")  // centre below axis
					.text("GDP per Capita");

});


</script>







</body>


</html>
