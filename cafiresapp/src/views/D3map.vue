 <template>
  <div class="d3Chart">
    <h1>D3 Map of California Counties with Fire Services</h1>
    <svg id="map" width="900" height="450"></svg>
    <p></p>

    <div class="answer">
      <h1>Fire Facilities in California Counties</h1>
      <div class="commands">
        <span class="sort" id="alpha">Sort Alphabetically</span>
        <span class="sort" id="asc">Sort Ascending</span>
        <span class="sort" id="desc">Sort Descending</span>
      </div>

      <div class="commands">
        <span class="filter" id="all">All</span>
        <span class="filter" id="top">Top 10</span>
        <!-- <span class="filter" id="bottom">Bottom 5</span> -->
      </div>

      <div id="chart"></div>
      <!-- <input type="range"  min="1920" max="2020" value="1920" class="slider" id="selectButton"/> -->
      <!-- <span id="sliderValue">0</span> -->
      <!-- <svg id="pie" width="960" height="500" style="align-items: left"></svg> -->
      <!-- <select id="selectButton"></select> -->
      <br />
      <!-- <div id="pie2" width="960" height="500"></div> -->

      <svg id="chart3" width="900" height="450"></svg>
      <!-- <svg id="legend"></svg> -->

      <!-- <svg id="chloro_map" width="900" height="450"></svg> -->
    </div>
  </div>
</template>

<script>
import * as d3 from "d3";

export default {
  name: "d3Chart",
  data: function () {
    return {
      chartData: null,
    };
  },
  mounted: function () {
    var margin = { top: 20, left: 50, bottom: 0, right: 50 };
    var width =
      parseInt(d3.select("#map").style("width")) - margin.left - margin.right;
    var height =
      parseInt(d3.select("#map").style("height")) - margin.top - margin.bottom;

    var svg1 = d3
      .select("#map")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", "translate(" + margin.left + ", " + margin.top + ")");

    d3.json("Ca_counties.geojson").then(function (json) {
      var projection = d3.geoMercator().fitSize([width, height], json);
      var path = d3.geoPath().projection(projection);
      //data join with features
      svg1
        .append("g")
        .selectAll("path")
        .data(json.features)
        .enter()
        .append("path")
        .attr("fill", "white")
        .attr("stroke", "black")
        .attr("opacity", 0.5)
        .attr("d", path); //generate geographic path

      d3.json("facilities.geojson").then(function (data) {
        var projection = d3.geoMercator().fitSize([width, height], json);
        var path = d3.geoPath().projection(projection);
        svg1
          .append("g")
          .selectAll("circle")
          .data(data.features)
          .enter()
          .append("circle")

          .attr("cx", function (d) {
            if (d.geometry) {
              var marker = projection(d.geometry.coordinates);
              return marker[0];
            }
            return 0;
          })

          .attr("cy", function (d) {
            if (d.geometry) {
              var marker = projection(d.geometry.coordinates);
              return marker[1];
            }
            return 0;
          })

          .attr("r", function (d) {
            if (d.geometry) {
              return 3;
            }
            return 0;
          })

          .attr("fill", "black")
          .attr("stroke", "#eee")
          .attr("opacity", 0.65)
          .attr("d", path);
      });
    });

    //Bar CHart Starting

    (margin = { top: 80, left: 75, bottom: 100, right: 50 }),
      (width = 1300 - margin.left - margin.right),
      (height = 600 - margin.top - margin.bottom);

    var svg = d3
      .select("#chart")
      .append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", "translate(" + margin.left + ", " + margin.top + ")");

    var x = d3.scaleBand();
    var y = d3.scaleLinear();

    var delay = function (d, i) {
      return i * 25;
    };

    var all, top5, bottom;
    var current, sortMode;

    d3.csv("D3BarData.csv", (d) => {
      return {
        name: d.County,
        value: +d.Count,
      };
    }).then((data) => {
      all = data;
      top5 = data.sort((a, b) => d3.descending(a.value, b.value)).slice(0, 10);
      // bottom = data.sort((a, b) => d3.ascending(a.value, b.value)).slice(0, 10);
      filter("#all");
      sort("#alpha");

      toggleFilter("#all");
      toggleSort("#alpha");

      draw();
    });

    //Event Handling for Reset button.
    d3.select("#reset").on("click", () => {
      console.log(current);
      d3.select("#reset")
        .transition()
        .duration(250)
        .style("background-color", "lightblue");
      d3.select("#reset")
        .transition()
        .duration(250)
        .style("background-color", "#eee")
        .delay(250);
      filter("#all");
      sort("#alpha");
      transition();
      toggleFilter("#all");
      toggleSort("#alpha");
      redraw();
    });

    //Event handling for sorting buttons.
    d3.select("#alpha").on("click", () => {
      sort("#alpha");
      transition();
      toggleSort("#alpha");
    });

    d3.select("#asc").on("click", () => {
      sort("#asc");
      transition();
      toggleSort("#asc");
    });

    d3.select("#desc").on("click", () => {
      sort("#desc");
      transition();
      toggleSort("#desc");
    });

    //Event handling for filtering buttons.
    d3.select("#all").on("click", () => {
      filter("#all");
      sort(sortMode);
      transition();
      toggleSort(sortMode);
      toggleFilter("#all");
      redraw();
    });

    d3.select("#top").on("click", () => {
      filter("#top");
      sort(sortMode);
      transition();
      toggleSort(sortMode);
      toggleFilter("#top");
      redraw();
    });

    //Filter Function
    function filter(mode) {
      if (mode === "#all") {
        current = JSON.parse(JSON.stringify(all));
      } else if (mode === "#top") {
        current = JSON.parse(JSON.stringify(top5));
      } else if (mode === "#bottom") {
        current = JSON.parse(JSON.stringify(bottom));
      }
      // filterMode = mode;
    }

    //Sorting Function
    function sort(mode) {
      if (mode === "#alpha") {
        current.sort((a, b) => d3.ascending(a.name, b.name));
      } else if (mode === "#asc") {
        current.sort((a, b) => d3.ascending(a.value, b.value));
      } else if (mode === "#desc") {
        current.sort((a, b) => d3.descending(a.value, b.value));
      }
      x.domain(current.map((d) => d.name));
      sortMode = mode;
    }

    //Sort Button Toggle
    function toggleSort(id) {
      d3.selectAll(".sort").style("background-color", "#eee");
      d3.select(id).style("background-color", "lightblue");
    }

    //Filter Button Toggle
    function toggleFilter(id) {
      d3.selectAll(".filter").style("background-color", "#eee");
      d3.select(id).style("background-color", "lightblue");
    }

    function redraw() {
      //update scale
      x.domain(current.map((d) => d.name));

      ////////////////////////////////
      // DATA JOIN FOR BARS.
      var bars = svg.selectAll(".bar").data(current, (d) => d.name);

      // UPDATE.
      bars
        .transition()
        .duration(750)
        .delay(delay)
        .attr("x", (d) => x(d.name))
        .attr("width", x.bandwidth());

      // ENTER.
      bars
        .enter()
        .append("rect")
        .attr("x", (d) => x(d.name))
        .attr("y", () => y(0))
        .attr("width", x.bandwidth())
        .transition()
        .duration(750)
        .attr("class", "bar")
        .attr("x", (d) => x(d.name))
        .attr("y", (d) => y(d.value))
        .attr("width", x.bandwidth())
        .attr("height", (d) => height - y(d.value));

      // EXIT.
      bars.exit().transition().duration(750).style("opacity", 0).remove();

      svg
        .selectAll(".xaxis")
        .selectAll("text")
        .attr("transform", "translate(-15,10)rotate(-65)")
        .style("text-anchor", "end");
    }

    function transition() {
      var transition = svg.transition().duration(750);

      var xAxis = d3.axisBottom().scale(x);

      transition
        .selectAll(".bar")
        .delay(delay)
        .attr("x", (d) => x(d.name));

      transition.select("#x-axis").call(xAxis);
    }

    function draw() {
      x.domain(current.map((d) => d.name))
        .range([0, width])
        .paddingInner(0.3)
        .paddingOuter(0.1);

      y.domain([0, d3.max(current, (d) => d.value)]).range([height, 0]);

      svg
        .selectAll(".bar")
        .data(current, (d) => d.name)
        .enter()
        .append("rect")
        .attr("class", "bar")
        .attr("x", (d) => x(d.name))
        .attr("y", (d) => y(d.value))
        .attr("width", x.bandwidth())
        .attr("height", (d) => height - y(d.value));

      var xAxis = d3.axisBottom().scale(x);

      svg
        .append("g")
        .attr("id", "x-axis")
        .attr("class", "xaxis")
        .attr("transform", "translate(0," + height + ")")
        .style("font-size", "0.9em")
        .call(xAxis)
        .selectAll("text")
        .attr("transform", "translate(-15,10)rotate(-65)")
        .style("text-anchor", "end");

      var yAxis = d3.axisLeft().scale(y).ticks(5, "d");

      svg.append("g").attr("class", "axis").call(yAxis);

      svg
        .append("text")
        .attr("x", -height / 2)
        .attr("y", -margin.left * 0.7)
        .attr("transform", "rotate(-90)")
        .attr("class", "ylabel")
        .text("Number of Fires")
        .style("baseline-shift", "super")
        .style("font-size", "0.9em");

      svg
        .append("text")
        .attr("x", margin.left)
        .attr("y", -margin.top + 40)
        .attr("class", "title")
        .text("Fires")
        .style("font-size", "28px");
    }
    // ======================================================================
    // PIE Chart

    // d3.csv("piedata.csv", (d) => {
    //   (d.year = +d.year), (d.count = +d.count);
    //   return d;
    // }).then((maindata) => {
    //   var margin = { top: 10, right: 20, bottom: 30, left: 60 },
    //     width = 900 ,
    //     height = 500 - margin.top - margin.bottom;

    //   // var cause_set = new Set();
    //   var year_set = new Set();

    //   for (let elem of maindata) {
    //     year_set.add(elem.year);
    //   }

    //   d3.select("#selectButton")
    //     .selectAll("myOptions")
    //     .data(year_set)
    //     .enter()
    //     .append("option")
    //     .text(function (d) {
    //       return d;
    //     }) // text showed in the menu
    //     .attr("value", function (d) {
    //       return d;
    //     }); // corresponding value returned by the button

    //   var svg = d3
    //     .select("#pie2")
    //     .append("svg")
    //     .attr("width", width + margin.left + margin.right)
    //     .attr("height", height + margin.top + margin.bottom);

    //   var label, arc, path, g, pie, color, radius;

    //   update(1920);

    //   function update(selectedGroup) {
    //     var data = maindata.filter(function (d) {
    //       return d.year == selectedGroup;
    //     });

    //     g = svg
    //       .append("g")
    //       .attr("transform", "translate(" + 250 + "," + 250 + ")");

    //     pie = d3
    //       .pie()
    //       .value((d) => d.value)
    //       .sort(null)
    //       .sortValues(d3.descending);

    //     // color = d3.scaleOrdinal(['#98abc5', '#8a89a6', '#7b6888', '#6b486b']);
    //     color = d3
    //       .scaleOrdinal()
    //       .domain(data)
    //       .range([
    //         "gold",
    //         "blue",
    //         "green",
    //         "yellow",
    //         "black",
    //         "grey",
    //         "darkgreen",
    //         "pink",
    //         "brown",
    //         "slateblue",
    //         "grey1",
    //         "orange",
    //       ]);

    //     radius = Math.min(width, height) / 2;

    //     label = d3
    //       .arc()
    //       .outerRadius(radius - 40)
    //       .innerRadius(radius - 40);

    //     path = d3.arc().outerRadius(radius).innerRadius(0);

    //     arc = g
    //       .selectAll(".arc")
    //       .data(pie(data))
    //       .enter()
    //       .append("g")
    //       .attr("class", "arc");

    //     arc
    //       .append("path")
    //       .attr("d", path)
    //       .attr("fill", (d) => color(d.data.cause))
    //       .attr("stroke", "black");

    //     arc
    //       .append("text")
    //       .attr("transform", (d) => "translate(" + label.centroid(d) + ")")
    //       .text((d) => d.data.value);
    //   }

    //   d3.select("#selectButton").on("change", function () {
    //     var selectedOption = d3.select(this).property("value");
    //     document.getElementById("sliderValue").innerHTML = String(selectedOption);
    //     update(selectedOption);
    //   });
    // });

    // ====================================================================
    // Chloropleth Map

    // function legend({
    //   color,
    //   title,
    //   tickSize = 6,
    //   width = 320,
    //   height = 44 + tickSize,
    //   marginTop = 18,
    //   marginRight = 0,
    //   marginBottom = 16 + tickSize,
    //   marginLeft = 0,
    //   ticks = width / 64,
    //   tickFormat,
    //   tickValues,
    // } = {}) {
    //   //🎒 explain:

    //   const svg = d3
    //     .create("svg")
    //     .attr("width", width)
    //     .attr("height", height)
    //     .attr("viewBox", [0, 0, width, height])
    //     .style("overflow", "visible")
    //     .style("display", "block");

    //   let x;

    //   // Continuous
    //   if (color.interpolator) {
    //     x = Object.assign(
    //       color
    //         .copy()
    //         .interpolator(d3.interpolateRound(marginLeft, width - marginRight)),
    //       {
    //         range() {
    //           return [marginLeft, width - marginRight];
    //         },
    //       }
    //     );

    //     svg
    //       .append("image")
    //       .attr("x", marginLeft)
    //       .attr("y", marginTop)
    //       .attr("width", width - marginLeft - marginRight)
    //       .attr("height", height - marginTop - marginBottom)
    //       .attr("preserveAspectRatio", "none")
    //       .attr("xlink:href", ramp(color.interpolator()).toDataURL());

    //     //scaleSequentialQuantile doesn’t implement ticks or tickFormat.
    //     if (!x.ticks) {
    //       if (tickValues === undefined) {
    //         const n = Math.round(ticks + 1);
    //         tickValues = d3
    //           .range(n)
    //           .map((i) => d3.quantile(color.domain(), i / (n - 1)));
    //       }
    //       if (typeof tickFormat !== "function") {
    //         tickFormat = d3.format(
    //           tickFormat === undefined ? ",f" : tickFormat
    //         );
    //       }
    //     }
    //   }

    //   //discrete
    //   else if (color.invertExtent) {
    //     const thresholds = color.thresholds
    //       ? color.thresholds() // scaleQuantize
    //       : color.quantiles
    //       ? color.quantiles() // scaleQuantile
    //       : color.domain(); // scaleThreshold

    //     const thresholdFormat =
    //       tickFormat === undefined
    //         ? (d) => d
    //         : typeof tickFormat === "string"
    //         ? d3.format(tickFormat)
    //         : tickFormat;

    //     x = d3
    //       .scaleLinear()
    //       .domain([-1, color.range().length - 1])
    //       .rangeRound([marginLeft, width - marginRight]);

    //     svg
    //       .append("g")
    //       .selectAll("rect")
    //       .data(color.range())
    //       .join("rect")
    //       .attr("x", (d, i) => x(i - 1))
    //       .attr("y", marginTop)
    //       .attr("width", (d, i) => x(i) - x(i - 1))
    //       .attr("height", height - marginTop - marginBottom)
    //       .attr("fill", (d) => d);

    //     tickValues = d3.range(thresholds.length);
    //     tickFormat = (i) => thresholdFormat(thresholds[i], i);
    //   }

    //   svg
    //     .append("g")
    //     .attr("transform", `translate(0, ${height - marginBottom})`)
    //     .call(
    //       d3
    //         .axisBottom(x)
    //         .ticks(
    //           ticks,
    //           typeof tickFormat === "string" ? tickFormat : undefined
    //         )
    //         .tickFormat(
    //           typeof tickFormat === "function" ? tickFormat : undefined
    //         )
    //         .tickSize(tickSize)
    //         .tickValues(tickValues)
    //     )
    //     .call((g) =>
    //       g
    //         .selectAll(".tick line")
    //         .attr("y1", marginTop + marginBottom - height)
    //     )
    //     .call((g) => g.select(".domain").remove())
    //     .call((g) =>
    //       g
    //         .append("text")
    //         .attr("y", marginTop + marginBottom - height - 6)
    //         .attr("fill", "currentColor")
    //         .attr("text-anchor", "start")
    //         .attr("font-weight", "bold")
    //         .text(title)
    //     );

    //   return svg.node();
    // }

    // function ramp(color, n = 256) {
    //   const canvas = d3.select(DOM.canvas(n, 1));
    //   const context = canvas.getContext("2d");
    //   for (let i = 0; i < n; ++i) {
    //     context.fillStyle = color(i / (n - 1));
    //     context.fillRect(i, 0, 1, 1);
    //   }
    //   return canvas;
    // }

    // // 			/////////////////////////////////////////////////////////////
    // // 			//Choropleth code

    // var promises = [];

    // promises.push(d3.json("counties-albers-10m.json"));
    // promises.push(d3.csv("D3BarData.csv"));

    // Promise.all(promises).then(function (values) {
    //   //🎒 explain: takes all promises into a list and returns a single promise.
    //   var us = values[0];
    //   var data = values[1];

    //   // var states = new Map(
    //     // us.objects.states.geometries.map((d) => [d.id, d.properties])
    //   // ); //🎒 explain: get the states based on mapping the ids and properties.
    //   // counties = new Map(
    //   //   us.objects.counties.geometries.map((d) => [d.id, d.properties])
    //   // );

    //   // var format = (d) => `${d} facilities`;

    //   var path = d3.geoPath();

    //   var color = d3.scaleQuantize([1, 10], d3.schemeReds[3]); //🎒 explain: creating a quantized color scale based on d3.schemeBlues with 9 shades of colour.

    //   //original line from Observable
    //   //data = Object.assign(new Map(await d3.csv("unemployment.csv", ({id, rate}) => [id, +rate])), {title: "Unemployment rate (%)"})
    //   data = Object.assign(new Map(data.map((d) => [d.id, +d.Count]))); //🎒 explain: modify the data to create a map based on id and rate and force rate to be a integer.
    //   data.title = "Unemployment rate (%)";

    //   path = d3.geoPath();

    //   // const svg = d3.create("svg")
    //   svg = d3.select("#chloro_map").attr("viewBox", [100, 100, 150, 350]);

    //   svg
    //     .append("g")
    //     // .attr("transform", "translate(610,20)")
    //     .append(() => legend({ color, title: data.title, width: 260 }));

    //   svg
    //     .append("g")
    //     .selectAll("path")
    //     .data(topojson.feature(us, us.objects.counties).features) //🎒 explain: extraxting the features.
    //     .join("path")
    //     .attr("fill", (d) => color(data.get(d.id))) //🎒 explain: fill the color based in the  id and color scales.
    //     .attr("d", path)
    //     .append("title");
    //   // .text(d => `${d.properties.name}, ${counties.get(d.id.slice(0, 2)).name} : ${format(data.get(d.id))}`);  //🎒 explain: setting the tooltip.

    //   svg
    //     .append("path")
    //     .datum(topojson.mesh(us, us.objects.counties, (a, b) => a !== b)) //🎒 explain: add the geopath for the borders of all the states to the svg
    //     .attr("fill", "none")
    //     .attr("stroke", "black")
    //     .attr("stroke-opacity", "0.4")
    //     // .attr("stroke-linejoin", "round")
    //     .attr("d", path);
    // });

    // ====================================================================
    // Severity zones

    margin = { top: 20, left: 50, bottom: 0, right: 50 };
    width =
      parseInt(d3.select("#chart3").style("width")) -
      margin.left -
      margin.right;
    height =
      parseInt(d3.select("#chart3").style("height")) -
      margin.top -
      margin.bottom;

    var svg2 = d3
      .select("#chart3")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g");

    // var legend = d3.select("#legend")
    // .attr('transform', 'translate(-50, -300)');

    // // Handmade legend
    // legend.append("circle").attr("cx", 30).attr("cy", 50).attr("r", 6).style("fill", "yellow")
    // legend.append("circle").attr("cx", 30).attr("cy", 80).attr("r", 6).style("fill", "blue")
    // legend.append("circle").attr("cx", 30).attr("cy", 110).attr("r", 6).style("fill", "red")
    // legend.append("text").attr("x", 50).attr("y", 53).text("Moderate").style("font-size", "15px").attr("alignment-baseline", "middle")
    // legend.append("text").attr("x", 50).attr("y", 83).text("High").style("font-size", "15px").attr("alignment-baseline", "middle")
    // legend.append("text").attr("x", 50).attr("y", 113).text("Very High").style("font-size", "15px").attr("alignment-baseline", "middle")

    d3.json("Ca_counties.geojson").then(function (json) {
      var projection = d3.geoMercator().fitSize([width, height], json);
      var path = d3.geoPath().projection(projection);
      //data join with features
      svg2
        .append("g")
        .selectAll("path")
        .data(json.features)
        .enter()
        .append("path")
        .attr("fill", "white")
        .attr("stroke", "black")
        .attr("opacity", 0.5)
        .attr("d", path);
      // .append(legend);  //generate geographic path
    });

    d3.json("sevzones.geojson").then(function (json) {
      var projection = d3.geoMercator().fitSize([width, height], json);
      var path = d3.geoPath().projection(projection);
      //data join with features
      console.log(json);
      svg2
        .append("g")
        .selectAll("path")
        .data(json.features)
        .enter()
        .append("path")
        .attr("fill", "white")
        .attr("stroke", function (d) {
          if (d.properties.HAZ_CLASS === "Moderate") {
            return "yellow";
          } else if (d.properties.HAZ_CLASS === "High") {
            return "blue";
          } else if (d.properties.HAZ_CLASS === "Very High") {
            return "red";
          }
        })
        .attr("opacity", 0.5)
        .attr("d", path) //generate geographic path
        .attr("transform", "translate(-40 , 0)");
    });
  },
};
</script>

<!-- "scoped" attribute limits CSS to this component only -->
<style scoped>
>>> .axis path,
>>> .axis line {
  fill: none;
  stroke: black;
  shape-rendering: crispEdges;
}

>>> .axis text {
  font-family: Courier;
  font-size: 0.85em;
}

>>> text {
  font-family: Courier;
  font-size: 0.65em;
}

q>> div.commands {
  font-family: Courier;
  font-size: 0.85em;
  font-weight: bold;
  text-align: center;
  cursor: default;
  user-select: none;
}

>>> svg {
  display: block;
  margin: auto;
  background-color: #fafafa;
}

>>> .bar {
  fill: #add8e677;
}

>>> text.xlabel {
  text-anchor: middle;
}

>>> text.ylabel {
  text-anchor: middle;
  /* alignment-baseline: central; */
}

>>> text.name {
  font-weight: bold;
  text-anchor: middle;
  /* alignment-baseline: central; */
}

>>> .sort {
  border-radius: 3px;
  background-color: #eee;
  display: inline-block;
  cursor: default;
}

>>> .sort,
label {
  font-family: Courier;
  color: #444;
  padding: 5px;
  margin: 5px;
}

>>> label {
  vertical-align: text-bottom;
}

>>> .filter {
  border-radius: 3px;
  background-color: #eee;
  padding: 5px;
  margin: 5px;
  color: #444;
  text-align: left;
  display: inline-block;
  cursor: default;
}
</style>

 
 