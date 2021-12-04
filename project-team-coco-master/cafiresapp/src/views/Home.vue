<template>
  <div>
    <h1 style="color: white; padding-top: 100px">
      Hundread Years of California burning: Forest Fires
    </h1>
    <div style="width: 60%; margin: auto; height: 140px">
      <p style="color: #bcccdc">
        Wildfires was always an issue for the forests of California. However,
        enormous wildfires have been constantly raging in California in recent
        summers. What is it about California that makes wildfires so
        catastrophic and how has it changed over the years?
      </p>
    </div>

    <!-- Mapbox Container -->
    <div id="mapContainer" class="basemap">
      <div id="map"></div>
      <!-- Mapbox Map Legend -->
      <div id="state-legend" class="legend">
        <h4 style="color: white">Type of Fire</h4>
        <div style="color: white">
          <span style="background-color: #b30000"></span>Critical
        </div>
        <div style="color: white">
          <span style="background-color: #e34a33"></span>Large
        </div>
        <div style="color: white">
          <span style="background-color: #fc8d59"></span>Medium
        </div>
        <div style="color: white">
          <span style="background-color: #fdcc8a"></span>Small
        </div>
        <div style="color: white">
          <span style="background-color: #fef0d9"></span>Minor
        </div>
      </div>
      <!-- Mapbox Map Console -->
      <div id="control-console" class="console">
        <!-- <h1 style="display: inline-block">California Forest Fires</h1> -->
        <a id="reset" class="button1" style="float: right">Reset</a>

        <h6
          style="
            color: white;
            padding-top: 10px;
            padding-left: 70px;
            font-size: 20px;
          "
        >
          <b>Select Year</b>
        </h6>
        <div class="slider" style="position: relative; top: 50px">
          <input type="range" min="1920" max="2020" value="2017" id="myRange" />
          <p id="sliderValue">0</p>
        </div>

        <!-- Mapbox Map Legend -->
        <div style="position: relative; top: 50px">
          <label for="cause" style="color: white; font-size: 18px"
            >Filter by Cause:</label
          >
          <br />
          <select name="causes" id="causes">
            <optgroup>
              <option value="All">All</option>
              <option value="Lightning">Lightning</option>
              <option value="Equipment Use">Equipment Use</option>
              <option value="Smoking">Smoking</option>
              <option value="Campfire">Campfire</option>
              <option value="Debris">Debris</option>
              <option value="Railroad">Railroad</option>
              <option value="Arson">Arson</option>
              <option value="Playing with Fire">Playing with Fire</option>
              <option value="Miscellaneous">Miscellaneous</option>
              <option value="Vehicle">Vehicle</option>
              <option value="Power Line">Power Line</option>
              <option value="Firefighter Training">Firefighter Training</option>
              <option value="Non-Firefighter Training">
                Non-Firefighter Training
              </option>
              <option value="Unknown/Unidentified">Unknown/Unidentified</option>
              <option value="Structure">Structure</option>
              <option value="Aircraft">Aircraft</option>
              <option value="Escaped Prescribed Burn">
                Escaped Prescribed Burn
              </option>
              <option value="Illegal Alien Campfire">
                Illegal Alien Campfire
              </option>
            </optgroup>
          </select>
        </div>

        <br />
        <br />
        <!-- Mapbox Map Text -->
        <p id="infotext" style="position: relative; top: 50px; color: white">
          There were
          <span
            id="firecount"
            style="color: red; font-size: 24px; font-weight: 600"
            >607</span
          >
          fires in California in <span id="year">2017</span>.
          <!-- burning a total of <span id="acrecount">0</span> acres of land. -->
        </p>
        <p
          id="causepara"
          style="display: none; position: relative; top: 40px; color: white"
        >
          <span
            id="cause count"
            style="color: red; font-size: 24px; font-weight: 600"
            >0</span
          >
          were caused by
          <span id="causefire">cause</span>
        </p>
      </div>
    </div>

    <hr />

    <!--Animated Lollipop Chart -->
    <div id="anilolli">
      <h2 style="color: white; font-size: 40px">Trends over the century</h2>
      <br />
      <br />
      <br />
      <br />
      <br />
      <br />

      <h5
        id="subtitle-trend"
        style="
          color: white;
          font-size: 30px;
          margin-left: 140px;
          text-decoration: underline;
        "
        align="left"
      >
        Total Number of Fires
      </h5>

      <div style="width: 30%; margin-left: 140px; height: 90px">
        <p style="color: #bcccdc" align="left" id="lollipop-subtext">
          There has been a gradual increase in number of fires each year, which
          is visible from the general upward trend in the graph, with 2017 being
          the most devastating.
        </p>
        <a
          class="button1"
          id="countbut"
          style="position: relative; bottom: 50px; left: 900px"
          >Total Fires</a
        >
        <a
          class="button1"
          id="acrebut"
          style="position: relative; bottom: 50px; left: 900px"
          >Total Acres</a
        >
      </div>
      <svg id="chart2"></svg>
    </div>

    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />

    <!-- Circle Pakcing 4 -->
    <h4
      style="
        color: white;
        font-size: 30px;
        margin-right: 140px;
        text-decoration: underline;
      "
      align="right"
    >
      Evolution of Causes
    </h4>
    <div style="width: 40%; margin-left: 770px; height: 120px">
      <p style="color: #bcccdc" align="right">
        On a closer look, we see that Lightning has increasingly become a cause
        of a lot of wildfires in recent times. Though it looks like a natural
        cause, but research shows climate change is mainly responsible behind
        irregular and aggressive weathers.
        <br />
        Other than that, arson and equipment use being purely caused by humans
        has also continued to gradually increase over time mostly due to
        advancement in technology.
      </p>
    </div>
    <div style="width: 1400px">
      <div class="legendbox">
        <svg id="cirlegend" style="width: 100%">
          <rect
            x="130"
            y="30"
            rx="10"
            ry="10"
            width="1250"
            height="100"
            opacity="0.1"
            fill="white"
          />
          <circle cx="210" cy="50" r="5" fill="#e6194b" />
          <circle cx="320" cy="50" r="5" fill="#3cb44b" />
          <circle cx="460" cy="50" r="5" fill="#ffe119" />
          <circle cx="580" cy="50" r="5" fill="#fffac8" />
          <circle cx="700" cy="50" r="5" fill="#f58231" />
          <circle cx="820" cy="50" r="5" fill="#911eb4" />
          <circle cx="940" cy="50" r="5" fill="#46f0f0" />
          <circle cx="1060" cy="50" r="5" fill="#f032e6" />
          <circle cx="1230" cy="50" r="5" fill="#bcf60c" />

          <circle cx="160" cy="100" r="5" fill="#fabebe" />
          <circle cx="260" cy="100" r="5" fill="#008080" />
          <circle cx="380" cy="100" r="5" fill="#e6beff" />
          <circle cx="560" cy="100" r="5" fill="#9a6324" />
          <circle cx="650" cy="100" r="5" fill="#4363d8" />
          <circle cx="850" cy="100" r="5" fill="#800000" />
          <circle cx="960" cy="100" r="5" fill="#aaffc3" />
          <circle cx="1050" cy="100" r="5" fill="#808000" />
          <circle cx="1180" cy="100" r="5" fill="#000075" />

          <text x="220" y="55" fill="white">Lightning</text>
          <text x="330" y="55" fill="white">Equipment Use</text>
          <text x="470" y="55" fill="white">Smoking</text>
          <text x="590" y="55" fill="white">Campfire</text>
          <text x="710" y="55" fill="white">Debris</text>
          <text x="830" y="55" fill="white">Railroad</text>
          <text x="950" y="55" fill="white">Arson</text>
          <text x="1070" y="55" fill="white">Playing with Fire</text>
          <text x="1240" y="55" fill="white">Miscellaneous</text>

          <text x="170" y="105" fill="white">Vehicle</text>
          <text x="270" y="105" fill="white">Power Line</text>
          <text x="390" y="105" fill="white">Training (Firefighter)</text>
          <text x="570" y="105" fill="white">Training</text>
          <text x="660" y="105" fill="white">Unknown/Unidentified</text>
          <text x="860" y="105" fill="white">Structure</text>
          <text x="970" y="105" fill="white">Aircraft</text>
          <text x="1060" y="105" fill="white">Escaped Burn</text>
          <text x="1190" y="105" fill="white">Illegal Alien Campfire</text>
        </svg>
      </div>
      <svg id="cp4" class="circlepack"></svg>
      <svg id="cp3" class="circlepack"></svg>
      <svg id="cp2" class="circlepack"></svg>
      <svg id="cp1" class="circlepack"></svg>
    </div>

    <br />
    <br />
    <br />
    <br />

    <div style="height: 500px"></div>

    <!-- Responsive Bar Chart -->
    <div>
      <h5
        id="subtitle-trend"
        style="
          color: white;
          font-size: 30px;
          margin-left: 140px;
          text-decoration: underline;
        "
        align="left"
      >
        Top 10 Costliest Fires
      </h5>
      <svg id="resplegend" style="width: 100%">
        <rect
          x="10%"
          y="30"
          rx="10"
          ry="10"
          width="280"
          height="100"
          opacity="0.1"
          fill="white"
        />
        <circle cx="12%" cy="55" r="5" fill="#8DB600" />
        <text x="13%" y="60" fill="white">Dollars($)</text>
        <circle cx="12%" cy="95" r="5" fill="#008000" />
        <text x="13%" y="100" fill="white">Dollars($) (Adjusted 2020)</text>
      </svg>
      <svg id="chart" class="respbar"></svg>
    </div>

    <div style="height: 200px" />

    <!-- Fire Facilities D3 Map -->
    <div id="d3maps" align="left" style='margin-left: 150px;'>
      <h5
        id="subtitle-trend"
        style="
          color: white;
          font-size: 30px;
          margin-left: 8px;
          text-decoration: underline;
        "
        align="left"
      >
        Fire Support Facilities
      </h5>
      <svg id="chloro" width="40%" height="700" />
    </div>
  </div>
</template>

<script>
//Imports
import mapboxgl from "mapbox-gl";
import * as d3 from "d3";

export default {
  name: "BaseMap",
  data() {
    return {
      accessToken:
        "pk.eyJ1IjoiZ29ybGEiLCJhIjoiY2t2M21qOWZ2OGhvOTJ3cTZubjhjemluZyJ9.ZDHpSVPTUjgzB-20jE9BgQ",
    };
  },
  mounted() {
    //=======================================================================================================
    //Mapbox Map Code
    var year = document.getElementById("myRange").value;
    document.getElementById("sliderValue").innerHTML = String(year);
    mapboxgl.accessToken = this.accessToken;

    //Create Map
    const map = new mapboxgl.Map({
      container: "map",
      style: "mapbox://styles/mapbox/dark-v10", // style URL
      center: [-123.38011, 37.07714], // starting position [lng, lat]
      zoom: 5, // starting zoom
      promoteId: "OBJECTID",
    });

    //Event for when map loads
    map.on("load", function () {
      //Add Fire Data Source
      map.addSource("firedata_source", {
        type: "geojson",
        data: "firedata.geojson",
      });

      //Add County Boundaries Source
      map.addSource("county", {
        type: "geojson",
        data: "counties.geojson",
      });

      //Add layer for fire polygons
      map.addLayer({
        id: "firepoly",
        type: "fill",
        source: "firedata_source",
        layout: {},
        paint: {
          "fill-color": [
            "interpolate",
            ["linear"],
            ["number", ["get", "GIS_ACRES"]],
            0,
            "#fef0d9",
            1000,
            "#fdcc8a",
            10000,
            "#fc8d59",
            30000,
            "#e34a33",
            200000,
            "#b30000",
          ],
          "fill-opacity": 0.8,
        },
        filter: ["all", ["==", ["get", "YEAR_"], "2017"]],
      });

      //Add layer for fire polygons border
      map.addLayer({
        id: "firepoly_line",
        type: "line",
        source: "firedata_source",
        layout: {},
        paint: {
          "line-color": "gold",
          "line-width": 2,
          "line-opacity": 0.2,
        },
        filter: ["all", ["==", ["get", "YEAR_"], "2017"]],
      });

      //Add layer for county boundaries
      map.addLayer({
        id: "county_boundaries",
        type: "line",
        source: "county",
        layout: {},
        paint: {
          "line-color": "white",
          "line-width": 1,
          "line-opacity": 0.1,
        },
      });

      //Tooltip Code
      const popup = new mapboxgl.Popup({
        closeButton: false,
        closeOnClick: false,
      });

      map.on("mouseenter", "firepoly", (e) => {
        map.getCanvas().style.cursor = "pointer";
        const coordinates = [e.lngLat.lng, e.lngLat.lat];
        while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
          coordinates[0] += e.lngLat.lng > coordinates[0] ? 360 : -360;
        }

        popup
          .setLngLat(coordinates)
          .setHTML(
            "<p><strong>Fire Name: </strong>" +
              e.features[0].properties.FIRE_NAME +
              "</p>" +
              "<p><strong>Cause of Fire: </strong>" +
              e.features[0].properties.CAUSE +
              "</p>" +
              "<p><strong>Counties Affected: </strong>" +
              e.features[0].properties.COUNTY +
              "</p>" +
              "<p><strong>Acres Burned: </strong>" +
              Math.round(e.features[0].properties.GIS_ACRES * 100) / 100 +
              " acres</p>"
          )
          .addTo(map);
      });

      map.on("mouseleave", "firepoly", () => {
        map.getCanvas().style.cursor = "";
        popup.remove();
      });

      //Disable scroll zoom and add zoom buttons
      map.scrollZoom.disable();
      map.touchZoomRotate.enable();
      map.addControl(new mapboxgl.NavigationControl(), "bottom-right");

      //Fly to the fire if clicked
      map.on("click", "firepoly", (e) => {
        var coors = e.features[0].geometry.coordinates[0][0];

        if (coors.length > 2) {
          coors = coors[0];
        }

        map.flyTo({
          center: coors,
          zoom: 8,
        });
      });
    });

    //Filtering
    d3.csv("firedata.csv", (d) => {
      return {
        id: d.OBJECTID,
        year: d.YEAR_,
        name: d.FIRE_NAME,
        cause: d.CAUSE,
        acres: +d.GIS_ACRES,
      };
    }).then((data) => {
      //Event for slider
      document.getElementById("myRange").addEventListener("input", (event) => {
        const year = parseInt(event.target.value);
        const cause = document.getElementById("causes").value;

        if (cause != "All") {
          map.setFilter("firepoly", [
            "all",
            ["==", "YEAR_", String(year)],
            ["==", "CAUSE", cause],
          ]);
          map.setFilter("firepoly_line", [
            "all",
            ["==", "YEAR_", String(year)],
            ["==", "CAUSE", cause],
          ]);
        } else {
          map.setFilter("firepoly", ["==", "YEAR_", String(year)]);
          map.setFilter("firepoly_line", ["==", "YEAR_", String(year)]);
        }

        document.getElementById("sliderValue").innerHTML = String(year);
        document.getElementById("firecount").innerHTML = String(
          data.filter(function (d) {
            return d.year == String(year);
          }).length
        );
        document.getElementById("year").innerHTML = String(year);
        document.getElementById("causefire").innerHTML = String(cause);
        document.getElementById("cause count").innerHTML = String(
          data.filter(function (d) {
            return d.year == String(year) && d.cause == String(cause);
          }).length
        );
      });

      //Event for causes dropdown
      document.getElementById("causes").addEventListener("input", (e) => {
        const cause = e.target.value;
        const year = document.getElementById("myRange").value;

        document.getElementById("causefire").innerHTML = String(cause);
        document.getElementById("cause count").innerHTML = String(
          data.filter(function (d) {
            return d.year == String(year) && d.cause == String(cause);
          }).length
        );

        if (cause != "All") {
          document.getElementById("causepara").style.display = "inline";
          map.setFilter("firepoly", [
            "all",
            ["==", "YEAR_", String(year)],
            ["==", "CAUSE", cause],
          ]);
          map.setFilter("firepoly_line", [
            "all",
            ["==", "YEAR_", String(year)],
            ["==", "CAUSE", cause],
          ]);
        } else {
          document.getElementById("causepara").style.display = "none";
          map.setFilter("firepoly", ["==", "YEAR_", String(year)]);
          map.setFilter("firepoly_line", ["==", "YEAR_", String(year)]);
        }
        document.getElementById("sliderValue").innerHTML = String(year);
      });

      //Event for reset
      document.getElementById("reset").addEventListener("click", () => {
        map.flyTo({
          center: [-123.38011, 37.07714], // starting position [lng, lat]
          zoom: 5, // starting zoom
          bearing: 0,
          pitch: 0,
        });

        document.getElementById("myRange").value = 2017;
        document.getElementById("causes").value = "All";
        document.getElementById("sliderValue").innerHTML = String(2017);
        document.getElementById("year").innerHTML = String(2017);
        document.getElementById("firecount").innerHTML = String(607);
        document.getElementById("causepara").style.display = "none";

        map.setFilter("firepoly", ["==", "YEAR_", "2017"]);
        map.setFilter("firepoly_line", ["==", "YEAR_", "2017"]);
      });
    });

    //=====================================================================================================
    //Animated Lollipop Chart
    var pScale = d3.scalePoint();
    var yScale = d3.scaleLinear();

    var xAxis = d3.axisBottom().scale(pScale);
    var yAxis = d3.axisLeft().scale(yScale);

    var margin = { top: 10, left: 70, bottom: 40, right: 20 };
    var width = parseInt(1400) - margin.left - margin.right;
    var height = parseInt(500) - margin.top - margin.bottom;

    var svg = d3
      .select("#chart2")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .append("g")
      .attr("transform", "translate(" + margin.left + ", " + margin.top + ")");

    var xax = svg
      .append("g")
      .attr("class", "x axis")
      .attr("transform", "translate(0," + height + ")");

    var yax = svg.append("g").attr("class", "y axis");

    var yaxistext = svg
      .append("text")
      .text("Number of fires")
      .attr("transform", "translate(-40,300)rotate(-90)")
      .attr("fill", "white");

    function update(selvar) {
      d3.csv("resdata.csv", function (d) {
        return {
          year: String(d.year),
          count: +d.count,
          acres: +d.acres,
        };
      }).then(function (data) {
        pScale
          .domain(
            data.map(function (d) {
              return d.year;
            })
          )
          .range([0, width]);

        xax
          .transition()
          .duration(1000)
          .call(xAxis)
          .selectAll("text")
          .attr("transform", "translate(-15,10)rotate(-90)")
          .style("text-anchor", "end");

        yScale
          .domain([
            0,
            d3.max(data, function (d) {
              return +d[selvar] + 50;
            }),
          ])
          .range([height, 0]);

        if (selvar == "count") {
          yax.transition().duration(1000).call(yAxis);

          yaxistext.text("Number of fires");
        } else {
          yax
            .transition()
            .duration(1000)
            .call(
              yAxis.tickFormat(function (d) {
                if (d > 1000) {
                  d = d / 1000000 + "M";
                }

                return d;
              })
            );

          yaxistext.text("Area (acres)");
        }

        var lines = svg.selectAll(".line").data(data, function (d) {
          return d.year;
        });

        lines
          .enter()
          .append("line")
          .merge(lines)
          .transition()
          .duration(1000)
          .attr("class", "line")
          .attr("x1", function (d) {
            return pScale(d.year);
          })
          .attr("y1", function (d) {
            return yScale(d[selvar]);
          })
          .attr("x2", function (d) {
            return pScale(d.year);
          })
          .attr("y2", yScale(0))
          .attr("stroke", "#bdbdbd45")
          .attr("stroke-width", "1px");

        var circles = svg.selectAll(".circle").data(data, function (d) {
          return d.year;
        });

        circles
          .enter()
          .append("circle")
          .merge(circles)
          .transition()
          .duration(1000)
          .attr("class", "circle")
          .attr("cx", function (d) {
            return pScale(d.year);
          })
          .attr("cy", function (d) {
            return yScale(d[selvar]);
          })
          .attr("r", 4)
          .attr("fill", "#FFC68A");
      });
    }

    update("count");

    document.getElementById("acrebut").addEventListener("click", () => {
      update("acres");
      document.getElementById("subtitle-trend").innerHTML =
        "Total Acres Burned";
      document.getElementById("lollipop-subtext").innerHTML =
        "Area consumed by the fires was normal until just a few years ago. Research shows that climate change is one of the major factors in aggravating the fires over California in recnt years.";
    });

    document.getElementById("countbut").addEventListener("click", () => {
      update("count");
      document.getElementById("subtitle-trend").innerHTML =
        "Total Number of Fires";
      document.getElementById("lollipop-subtext").innerHTML =
        "There has been a gradual increase in number of fires each year, which is visible from the general upward trend in the graph, with 2017 being the most devastating.";
    });

    //=======================================================================================================
    //Circle Packing Graph

    function cat18(n) {
      var colores_g = [
        "#e6194b",
        "#3cb44b",
        "#ffe119",
        "#fffac8",
        "#f58231",
        "#911eb4",
        "#46f0f0",
        "#f032e6",
        "#bcf60c",
        "#fabebe",
        "#008080",
        "#e6beff",
        "#9a6324",
        "#4363d8",
        "#800000",
        "#aaffc3",
        "#808000",
        "#ffd8b1",
        "#000075",
        "#808080",
      ];
      return colores_g[n % colores_g.length];
    }

    var causelist = {
      Lightning: 0,
      "Equipment Use": 1,
      Smoking: 2,
      Campfire: 3,
      Debris: 4,
      Railroad: 5,
      Arson: 6,
      "Playing with Fire": 7,
      Miscellaneous: 8,
      Vehicle: 9,
      "Power Line": 10,
      "Firefighter Training": 11,
      "Non-Firefighter Training": 12,
      "Unknown/Unidentified": 13,
      Structure: 14,
      Aircraft: 15,
      Volcanic: 16,
      "Escaped Prescribed Burn": 17,
      "Illegal Alien Campfire": 18,
    };

    //1
    d3.json("circlepack1.json").then((data) => {
      var width = 350;
      var height = width + 100;

      var pack = (data) =>
        d3.pack().size([width, height]).padding(3)(
          d3
            .hierarchy(data)
            .sum((d) => d.value)
            .sort((a, b) => b.value - a.value)
        );

      var root = pack(data);

      var svg = d3
        .select("#cp1")
        .attr("viewBox", `-${width / 2} -${height / 2} ${width} ${height}`)
        .style("display", "block")
        .style("margin", "0 -14px")
        .style("background", "#1f1f1f")
        .style("cursor", "pointer")
        .attr("width", width)
        .attr("height", height);

      svg
        .append("text")
        .text("blablblabla")
        .attr("class", "tooltip-text-circle")
        .attr("transform", "translate(-90,-220)")
        .attr("fill", "white")
        .attr("display", "none");

      var node = svg
        .append("g")
        .selectAll("circle")
        .data(root.descendants().slice(1))
        .join("circle")
        .attr("fill", (d) => cat18(causelist[d.data.name]))
        .attr("opacity", "0.7")
        .on("mouseover", function (d) {
          d3.select(this).attr("stroke", "#FFECD5");

          d3.select(".tooltip-text-circle")
            .text(
              d.path[0].__data__.data.name +
                " : " +
                (d.path[0].__data__.data.value / 1000).toFixed(1) +
                "k"
            )
            .attr("display", "initial");
        })
        .on("mouseout", function () {
          d3.select(this).attr("stroke", null);
          d3.select(".tooltip-text-circle").attr("display", "none");
        });

      svg
        .append("rect")
        .attr("x", 10)
        .attr("y", 120)
        .attr("rx", 10)
        .attr("ry", 10)
        .attr("width", 100)
        .attr("height", 25)
        .attr("stroke", "#FFECD5")
        .attr("transform", "translate(-55,56)")
        .attr("fill", "#69a3b245")
        .attr("class", "cirpackbox");

      svg
        .append("text")
        .text("1920  -  1945")
        .attr("class", "circlepackyears")
        .attr("transform", "translate(-40,195)")
        .attr("fill", "#FFECD5");

      zoomTo([root.x, root.y, root.r * 2]);

      function zoomTo(v) {
        var k = width / v[2];
        node.attr(
          "transform",
          (d) => `translate(${(d.x - v[0]) * k},${(d.y - v[1]) * k - 30})`
        );
        node.attr("r", (d) => d.r * k);
      }
    });

    //2
    d3.json("circlepack2.json").then((data) => {
      var width = 350;
      var height = width + 100;

      var pack = (data) =>
        d3.pack().size([width, height]).padding(3)(
          d3
            .hierarchy(data)
            .sum((d) => d.value)
            .sort((a, b) => b.value - a.value)
        );

      var root = pack(data);

      var svg = d3
        .select("#cp2")
        .attr("viewBox", `-${width / 2} -${height / 2} ${width} ${height}`)
        .style("display", "block")
        .style("margin", "0 -14px")
        .style("background", "#1f1f1f")
        .style("cursor", "pointer")
        .attr("width", width)
        .attr("height", height);
      // .on("click", (event) => zoom(event, root));

      svg
        .append("rect")
        .attr("x", 10)
        .attr("y", 120)
        .attr("rx", 10)
        .attr("ry", 10)
        .attr("width", 100)
        .attr("height", 25)
        .attr("stroke", "#FFECD5")
        .attr("transform", "translate(-55,56)")
        .attr("fill", "#69a3b245")
        .attr("class", "cirpackbox");

      svg
        .append("text")
        .text("1946  -  1970")
        .attr("class", "circlepackyears")
        .attr("transform", "translate(-40,195)")
        .attr("fill", "#FFECD5");

      svg
        .append("text")
        .text("blablblabla")
        .attr("class", "tooltip-text-circle2")
        .attr("transform", "translate(-90,-220)")
        .attr("fill", "white")
        .attr("display", "none");

      var node = svg
        .append("g")
        .selectAll("circle")
        .data(root.descendants().slice(1))
        .join("circle")
        .attr("fill", (d) => cat18(causelist[d.data.name]))
        .attr("opacity", "0.7")
        .on("mouseover", function (d) {
          d3.select(this).attr("stroke", "#FFECD5");
          d3.select(".tooltip-text-circle2")
            .text(
              d.path[0].__data__.data.name +
                " : " +
                (d.path[0].__data__.data.value / 1000).toFixed(1) +
                "k"
            )
            .attr("display", "initial");
        })
        .on("mouseout", function () {
          d3.select(this).attr("stroke", null);
          d3.select(".tooltip-text-circle2").attr("display", "none");
        });

      zoomTo([root.x, root.y, root.r * 2]);

      function zoomTo(v) {
        var k = width / v[2];
        node.attr(
          "transform",
          (d) => `translate(${(d.x - v[0]) * k},${(d.y - v[1]) * k - 30})`
        );
        node.attr("r", (d) => d.r * k);
      }
    });

    //3
    d3.json("circlepack3.json").then((data) => {
      var width = 350;
      var height = width + 100;

      var pack = (data) =>
        d3.pack().size([width, height]).padding(3)(
          d3
            .hierarchy(data)
            .sum((d) => d.value)
            .sort((a, b) => b.value - a.value)
        );

      var root = pack(data);

      var svg = d3
        .select("#cp3")
        .attr("viewBox", `-${width / 2} -${height / 2} ${width} ${height}`)
        .style("display", "block")
        .style("margin", "0 -14px")
        .style("background", "#1f1f1f")
        .style("cursor", "pointer")
        .attr("width", width)
        .attr("height", height);
      // .on("click", (event) => zoom(event, root));

      svg
        .append("rect")
        .attr("x", 10)
        .attr("y", 120)
        .attr("rx", 10)
        .attr("ry", 10)
        .attr("width", 100)
        .attr("height", 25)
        .attr("stroke", "#FFECD5")
        .attr("transform", "translate(-55,56)")
        .attr("fill", "#69a3b245")
        .attr("class", "cirpackbox");

      svg
        .append("text")
        .text("1971  -  1995")
        .attr("class", "circlepackyears")
        .attr("transform", "translate(-40,195)")
        .attr("fill", "#FFECD5");

      svg
        .append("text")
        .text("blablblabla")
        .attr("class", "tooltip-text-circle3")
        .attr("transform", "translate(-90,-220)")
        .attr("fill", "white")
        .attr("display", "none");

      var node = svg
        .append("g")
        .selectAll("circle")
        .data(root.descendants().slice(1))
        .join("circle")
        .attr("fill", (d) => cat18(causelist[d.data.name]))
        .attr("opacity", "0.7")
        .on("mouseover", function (d) {
          d3.select(this).attr("stroke", "#FFECD5");
          d3.select(".tooltip-text-circle3")
            .text(
              d.path[0].__data__.data.name +
                " : " +
                (d.path[0].__data__.data.value / 1000).toFixed(1) +
                "k"
            )
            .attr("display", "initial");
        })
        .on("mouseout", function () {
          d3.select(this).attr("stroke", null);
          d3.select(".tooltip-text-circle3").attr("display", "none");
        });

      zoomTo([root.x, root.y, root.r * 2]);

      function zoomTo(v) {
        var k = width / v[2];
        node.attr(
          "transform",
          (d) => `translate(${(d.x - v[0]) * k},${(d.y - v[1]) * k - 30})`
        );
        node.attr("r", (d) => d.r * k);
      }
    });

    //4
    d3.json("circlepack4.json").then((data) => {
      var width = 350;
      var height = width + 100;

      var pack = (data) =>
        d3.pack().size([width, height]).padding(3)(
          d3
            .hierarchy(data)
            .sum((d) => d.value)
            .sort((a, b) => b.value - a.value)
        );

      var root = pack(data);

      var svg = d3
        .select("#cp4")
        .attr("viewBox", `-${width / 2} -${height / 2} ${width} ${height}`)
        .style("display", "block")
        .style("margin", "0 -14px")
        .style("background", "#1f1f1f")
        .style("cursor", "pointer")
        .attr("width", width)
        .attr("height", height);
      // .on("click", (event) => zoom(event, root));

      svg
        .append("rect")
        .attr("x", 10)
        .attr("y", 120)
        .attr("rx", 10)
        .attr("ry", 10)
        .attr("width", 100)
        .attr("height", 25)
        .attr("stroke", "#FFECD5")
        .attr("transform", "translate(-55,56)")

        .attr("fill", "#69a3b245")
        .attr("class", "cirpackbox");

      svg
        .append("text")
        .text("1996  -  2020")
        .attr("class", "circlepackyears")
        .attr("transform", "translate(-40,195)")
        .attr("fill", "#FFECD5");

      svg
        .append("text")
        .text("blablblabla")
        .attr("class", "tooltip-text-circle4")
        .attr("transform", "translate(-90,-220)")
        .attr("fill", "white")
        .attr("display", "none");

      var node = svg
        .append("g")
        .selectAll("circle")
        .data(root.descendants().slice(1))
        .join("circle")
        .attr("fill", (d) => cat18(causelist[d.data.name]))
        .attr("opacity", "0.7")
        .on("mouseover", function (d) {
          d3.select(this).attr("stroke", "#FFECD5");
          d3.select(".tooltip-text-circle4")
            .text(
              d.path[0].__data__.data.name +
                " : " +
                (d.path[0].__data__.data.value / 1000).toFixed(1) +
                "k"
            )
            .attr("display", "initial");
        })
        .on("mouseout", function () {
          d3.select(this).attr("stroke", null);
          d3.select(".tooltip-text-circle4").attr("display", "none");
        });

      zoomTo([root.x, root.y, root.r * 2]);

      function zoomTo(v) {
        var k = width / v[2];
        node.attr(
          "transform",
          (d) => `translate(${(d.x - v[0]) * k},${(d.y - v[1]) * k - 30})`
        );
        node.attr("r", (d) => d.r * k);
      }
    });

    //==========================================================================================================
    //Responsive Bar Chart
    var xScale = d3.scaleBand().round(true).paddingInner(0.3).paddingOuter(0.3);
    var pScale2 = d3.scalePoint();
    var yScale2 = d3.scaleLinear();
    var xAxis2 = d3.axisBottom().scale(xScale);

    var yAxis2 = d3.axisLeft().scale(yScale2);

    d3.csv("top10costliestCA.csv", function (d) {
      return {
        rank: d.Rank,
        year: d.Year,
        name: d.Name,
        dollars: +d.Dollars,
        dollarsinf: +d.DollarsInf,
      };
    }).then(function (data) {
      var margin = { top: 10, left: 70, bottom: 120, right: 20 };
      var width =
        parseInt(d3.select("#chart").style("width")) -
        margin.left -
        margin.right;
      var height =
        parseInt(d3.select("#chart").style("height")) -
        margin.top -
        margin.bottom;

      var svg = d3
        .select("#chart")
        .attr("width", width + margin.left + margin.right)
        .attr("height", height + margin.top + margin.bottom)
        .append("g")
        .attr(
          "transform",
          "translate(" + margin.left + ", " + margin.top + ")"
        );

      xScale
        .domain(
          data.map(function (d) {
            return d.name;
          })
        )
        .range([0, width]);

      pScale2
        .domain(
          data.map(function (d) {
            return d.name;
          })
        )
        .range([0, width]);

      yScale2
        .domain([
          0,
          d3.max(data, function (d) {
            return d.dollarsinf;
          }) + 2000,
        ])
        .range([height, 0]);

      svg
        .append("g")
        .attr("class", "x axis")
        .attr("transform", "translate(0," + height + ")")
        .call(xAxis2);

      svg
        .append("g")
        .attr("class", "y axis")
        .call(yAxis2)
        .append("text")
        .attr("transform", "rotate(-90)")
        .attr("y", 6)
        .attr("dy", ".7em")
        .text("Dollars ($)")
        .append("tspan")
        .style("baseline-shift", "super")
        .style("font-size", "0.7em");

      svg
        .selectAll(".bar2")
        .data(data, function (d) {
          return d.name;
        })
        .enter()
        .append("rect")
        .attr("class", "bar2")
        .attr("x", function (d) {
          return xScale(d.name);
        })
        .attr("y", function (d) {
          return yScale2(d.dollarsinf);
        })
        .attr("width", xScale.bandwidth())
        .attr("height", function (d) {
          return height - yScale2(d.dollars);
        })
        .attr("fill", "#008000");

      svg
        .selectAll(".bar1")
        .data(data, function (d) {
          return d.name;
        })
        .enter()
        .append("rect")
        .attr("class", "bar1")
        .attr("x", function (d) {
          return xScale(d.name);
        })
        .attr("y", function (d) {
          return yScale2(d.dollars);
        })
        .attr("width", xScale.bandwidth())
        .attr("height", function (d) {
          return height - yScale2(d.dollars);
        })
        .attr("fill", "#8DB600");

      d3.select(window).on("resize", resize);

      resize(); //call resize in case we start small!

      function resize() {
        width =
          parseInt(d3.select("#chart").style("width")) -
          margin.left -
          margin.right;
        height =
          parseInt(d3.select("#chart").style("height")) -
          margin.top -
          margin.bottom;

        svg.attr("width", width).attr("height", height);

        xScale.range([0, width]);
        pScale2.range([0, width]);
        yScale2.range([height, 0]).nice();

        svg
          .selectAll(".bar1")
          .data(data, function (d) {
            return d.name;
          }) //UPDATE
          .attr("x", function (d) {
            return xScale(d.name);
          })
          .attr("y", function (d) {
            return yScale2(d.dollars);
          })
          .attr("width", xScale.bandwidth())
          .attr("height", function (d) {
            return height - yScale2(d.dollars);
          })
          .attr("rx", "5px");

        svg
          .selectAll(".bar2")
          .data(data, function (d) {
            return d.name;
          }) //UPDATE
          .attr("x", function (d) {
            return xScale(d.name);
          })
          .attr("y", function (d) {
            return yScale2(d.dollarsinf);
          })
          .attr("width", xScale.bandwidth())
          .attr("height", function (d) {
            return height - yScale2(d.dollarsinf);
          })
          .attr("rx", "5px");

        yAxis2.ticks(Math.max(height / 100, 2)); //one every 100 pixels
        xAxis2.ticks(Math.max(width / 100, 2));

        svg
          .select(".x.axis")
          .attr("transform", "translate(0," + height + ")")
          .call(xAxis2)
          .selectAll("text")
          .attr("transform", "translate(-15,10)rotate(-45)")
          .style("text-anchor", "end");

        svg.select(".y.axis").call(yAxis2);

        svg.select(".x.axis").style("display", "initial");
        svg.select(".y.axis").style("display", "initial");
        svg.selectAll(".bar1").style("display", "initial");
        svg.selectAll(".bar2").style("display", "initial");
      }
    });

    // ============================================================================================
    // D3 Chloropeth Map

    var margin2 = { top: 20, left: 50, bottom: 0, right: 50 };
    var width2 =
      parseInt(d3.select("#chloro").style("width")) -
      margin2.left -
      margin2.right;
    var height2 =
      parseInt(d3.select("#chloro").style("height")) -
      margin2.top -
      margin2.bottom;

    var svgmod = d3
      .select("#chloro")
      .attr("width", width2 + margin2.left + margin2.right)
      .attr("height", height2 + margin2.top + margin2.bottom)
      .append("g");
    

    d3.json("faccount.geojson").then(function (json) {
      var projection = d3.geoMercator().fitSize([width2, height2], json);
      var path = d3.geoPath().projection(projection);
      //data join with features

      var piyg = d3.scaleSequential(d3.interpolateOrRd);
      var max = d3.max(json.features, (d) => d.properties.faccount);

      svgmod
        .append("g")
        .selectAll("path")
        .data(json.features)
        .enter()
        .append("path")
        .attr("fill", (d) => {
          return piyg(d.properties.faccount / max);
        })
        .attr("stroke", "grey")
        .attr("stroke-width", "1px")
        .attr("opacity", "0.8")
        .attr("d", path)
        .attr("transform", "translate(30,0)")
        .on("mouseover", function (d) {
          d3.select(this)
            .attr("stroke", "black")
            .attr("stroke-width", "1.5px")
            .attr("opacity", "0.9");
          
          d3.select("#countyname")
            .text("County: " + d.path[0].__data__.properties.NAME10)
                        .attr("display","initial")
          
          d3.select("#faccount")
            .text("Count: " + d.path[0].__data__.properties.faccount)
                        .attr("display","initial")
          
          d3.select("#tooltip-chloro")
            .attr("display","initial")
        })
        .on("mouseleave", function () {
          d3.select(this)
            .attr("stroke", "grey")
            .attr("stroke-width", "1px")
            .attr("opacity", "0.8");

          d3.select("#countyname")
                        .attr("display","none")
          
          d3.select("#faccount")
                        .attr("display","none")
          
          d3.select("#tooltip-chloro")
            .attr("display","none")
        });


      svgmod
        .append("rect")
        .attr('x', "300")
        .attr('y', "40")
        .attr('rx', "20px")
        .attr('ry', "20px")
        .attr('width', "200")
        .attr('height', "110")
        .attr("fill","#1f1f1f")
        .attr('stroke', "#ffecd5")
        .attr('opacity','0.8')
        .attr("id","tooltip-chloro")
        .attr('display','none')
      
      svgmod
        .append("text")
        .attr("x", "320")
        .attr("y","80")
        .text("County: countyname")
        .attr("fill",'white')
        .attr("id",'countyname')
                .attr('display','none')

      svgmod
        .append("text")
        .attr("x", "320")
        .attr("y","110")
        .text("Count: faccount")
        .attr("fill",'white')
        .attr("id",'faccount')
                .attr('display','none')
      
        
    });
  },
};
</script>

<style scoped>
body {
  margin: 0;
  padding: 0;
  /* font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; */
  font-family: "Roboto", sans-serif;
}
div {
  margin: 100;
}
#map {
  display: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  height: 90%;
}
.legend {
  background-color: #1f1f1f;
  border: 2px solid #ffecd5;
  border-radius: 15px;
  top: 320px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  font: 12px/20px "Helvetica Neue", Arial, Helvetica, sans-serif;
  padding: 10px;
  position: absolute;
  right: 10px;
  z-index: 1;
  opacity: 0.9;
}

.legend h4 {
  margin: 0 0 10px;
}

.legend div span {
  border-radius: 50%;
  display: inline-block;
  height: 10px;
  margin-right: 5px;
  width: 10px;
}

.mapboxgl-popup {
  /* position: absolute; */
  max-width: 400px;
  font: 13px/20px "Helvetica Neue", Arial, Helvetica, sans-serif;
  opacity: 0.8;
}

.basemap {
  /* position: relative; */
  height: 700px !important;
  /* width: 800px !important; */
  /* height: 100% !important; */
  width: 100% !important;
  display: block;
}

.console {
  background-color: #1f1f1f;
  border: 2px solid #ffecd5;
  border-radius: 20px;
  top: 320px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  font: 12px/20px "Helvetica Neue", Arial, Helvetica, sans-serif;
  padding: 10px;
  position: absolute;
  left: 10px;
  z-index: 1;
  opacity: 1;
  width: 500px;
  height: 300px;
}

.console h4 {
  margin: 0 0 10px;
}

.console div span {
  border-radius: 50%;
  display: inline-block;
  height: 10px;
  margin-right: 5px;
  width: 10px;
}

.range-slider {
  margin: 60px 0 0 0%;
}

#chart2 {
  background-color: #1f1f1f;
  border-radius: 20px;
}

.circlepack {
  float: right;
  padding: 2%;
}

>>> .axis path,
>>> .axis line {
  shape-rendering: crispEdges;
  color: #627d98;
}

>>> .axis text {
  fill: white;
  opacity: 0.7;
}

#chart {
  width: 90%;
  height: 700px;
  background-color: #1f1f1f;
  border-radius: 20px;
}

.slider {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 450px;
  height: 60px;
  padding: 30px;
  padding-left: 40px;
  background: #121212;
  border-radius: 20px;
  display: flex;
  align-items: center;
  box-shadow: 0px 15px 40px #ffecd511;
}
.slider p {
  font-size: 26px;
  font-weight: 600;
  font-family: Open Sans;
  padding-left: 30px;
  padding-top: 10px;
  color: #ffecd5;
}
.slider >>> input[type="range"] {
  -webkit-appearance: none !important;
  width: 420px;
  height: 2px;
  background: #ffecd5;
  border: none;
  outline: none;
}
.slider >>> input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none !important;
  width: 30px;
  height: 30px;
  background: #fcfcfc;
  border: 2px solid #121212;
  border-radius: 50%;
  cursor: pointer;
}
.slider input[type="range"]::-webkit-slider-thumb:hover {
  background: #ffecd5;
}

#infotext {
  font-size: 20px;
}
#causepara {
  font-size: 20px;
}

hr {
  border: 0;
  height: 3px;
  background: #333;
  background-image: linear-gradient(to right, #ccc, #333, #ccc);
}

a.button1 {
  display: inline-block;
  padding: 0.3em 1em;
  border: 0.1em solid #ffecd5;
  margin: 0 0.3em 0.3em 0;
  border-radius: 0.12em;
  box-sizing: border-box;
  text-decoration: none;
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  font-size: 13px;
  color: #ffffff;
  text-align: center;
  transition: all 0.2s;
}

a.button1:hover {
  color: #000000;
  background-color: #ffecd5;
}
@media all and (max-width: 30em) {
  a.button1 {
    display: block;
    margin: 0.4em auto;
  }
}

optgroup {
  font-size: 12px;
}

.circlepack {
  border-radius: 20px;
  border: 2px solid #ffecd5;
}

#chloro {
  border: 2px solid #ffecd5;
  border-radius: 20px;
}
</style>


