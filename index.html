<!DOCTYPE html>
<html>
<head>
	<title>Happiness Investigation</title>
	<script src="d3.js">
	</script>
	<script src="https://d3js.org/d3.v3.min.js"></script>
	<style>
	#tooltip{
		opacity: 0;
		position: absolute;
		text-align: center;
		width: 210px;
		height: 110px;
		background: lightSteelBlue;
		border: 0px;
	}
	</style>
</head>
<body>
	<p>This fugure shows the happiness incestigation result all over the world. From the first figure I can see that Oceania and Europe have the highest happiness rate, this figure uses interactive slideshow as the !</p>
	<svg class="chart"></svg>
	<div id="tooltip" opacity=0></div>
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
		.html("In "+d.continent+" investigation shows a average happiness rate of "+ d.rate +
	 				", the highest rate and country is "+ d.max+", and the lowest rate and country is "+ d.min);})
		.on("mouseout",function(d){tooltip.style("opacity",0);})



		canvas.append("text")
            .attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
            .attr("transform", "translate("+ 50 +","+300+")rotate(-90)")  // text is drawn off the screen top left, move down and out and rotate
            .text("Average Happiness Rate");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 130 +","+530+")")  // centre below axis
						.text("S.America");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 215 +","+530+")")  // centre below axis
						.text("N.America");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 295 +","+530+")")  // centre below axis
						.text("Asia");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 375 +","+530+")")  // centre below axis
						.text("Africa");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 455 +","+530+")")  // centre below axis
						.text("Europe");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 535 +","+530+")")  // centre below axis
						.text("Oceania");
		canvas.append("text")
						.attr("text-anchor", "middle")  // this makes it easy to centre the text as the transform is applied to the anchor
						.attr("transform", "translate("+ 330 +","+70+")")  // centre below axis
						.text("General happiness rate information in each continent");
	})

	</script>

</body>
</html>
