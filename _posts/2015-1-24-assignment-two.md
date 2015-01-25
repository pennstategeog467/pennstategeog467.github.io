---
layout: post
title: Assignment 2 - Contributing to OpenStreetMap + GeoJSON & Mapbox Studio fun!
excerpt: "Assignments for OpenStreetMap editting exercise."
modified: 2015-1-24
tags: 
author: aaron_dennis
comments: true
image:
  feature: 
  credit: 
  creditlink: 
---

This assignment will introduce you to OpenStreetMap feature tracing and tagging. You will also learn a little bit about open data formats and the print functionality in Mapbox Studio.

## Tracing Assignments

In the map below you can see State College, Pennsylvania divided into indivual sections by pink polygons. The map also shows the `#building` layer from Mapbox Streets, a global vector tile source built and regularly updated with the OpenStreetMap (OSM) database. As of January 24, 2015, many areas of the OSM database in State College could benefit from someone going through and tracing building outlines. We have assigned each section to a specific contributor. Explore the map until you find your section.

<figure>
  <iframe src="http://aaronpdennis.github.io/geog467-osm-sc-assignments/" style="height:400px;width:100%;"></iframe>
  <figcaption>This map was built with Mapbox GL. You'll need to be in a modern web browser like Chrome or Firefox to view it properly.</figcaption>
</figure>

The map above renders the assigned sections by referencing a GeoJSON file. Think of a GeoJSON file as similar to a Shapefile in that it contains vector geographic data, but it's a single text file that is human readable, instead of several files with information about geometry in one file, related attributes in a second, and projection information in yet another. We use GeoJSON on the web because the text within the file is directly readable as data in Javascript. You'll want to have a solid understanding of this data format for the next part of the exercise. Read more about GeoJSON <a href="http://giscollective.org/github-bringing-geojson-to-life-since-2013/">here</a>.

As you know, OpenStreetMap is a collaborative database that lots of people can contribute to at the same time. This also means sometimes people are unknowingly editing the same part of the map at the same time, which causes obvious issues and ends up wasting everyone's time. That's why we have gone through all this trouble of dividing our mapping project--buildings in State College--into different sections. You'll be able to display the boundary of your assigned section in the OSM iD Editor as you're editing so that you don't step on the toes of anyone else working on the map (like the other people in this class) and they will stay clear of your section. To do that, we'll have to take a closer look at that GeoJSON file, pull out the data relevant to you, and convert it to a data format supported by the iD Editor called a GPX file.

## Referencing Your Assignment in the iD Editor

To display your tracing assignment for reference in the iD Editor, we'll need to extract your specific polygon feature from the GeoJSON file and create a GPX file. Why does it need to be in a GPX file? This particular type of file has a long history with OSM and, consequently, all of the modern OSM editing tools, like the iD Editor, provide great functionality for this data format. A GPX file is what GPS receivers generate when you mark waypoints or create tracks. They were especially useful in the early days of OSM when the primary method of adding roads and other features was not through tracing satellite imagery, but uploading, tracing, and editting data collected in the field by contributors with GPS receivers. This is still a useful method today for collecting geographic data about things like trails, which often can't be seen from space, or in places where high resolution imagery isn't available.

We'll be using the GPX files for a less conventional purpose (designating assigned areas for a coordinated mapping effort), although if you ever contribute to the Humanitarian OpenStreetMap Team's mapping efforts--and you should--you'll see their <a href="http://tasks.hotosm.org/">tasking manager</a> use boundaries in GPX file format to split a larger effort into smaller pieces.

So let's make the GPX file you need and start mapping.

### Select Your Assignment from the GeoJSON

A GeoJSON file is just a text file. You can open it, copy and paste all the text it into another place, and it will still be GeoJSON. I have placed all the GeoJSON for the tracing assignments in <a href="/geojson-tracing-assignments/">another post--open it in a new tab.</a>

This is the GeoJSON, and at first it probably looks like a long and confusing list of brackets, numbers, and punctuation. Let's start with the first three lines and the last two.

<pre><code>
{
  "type": "FeatureCollection",
  "features": [
...
  ]
}
</code></pre>

These are the lines that set up everything else. These lines set up what's known as an object in Javascript. The object is a list of properties between the two curly braces on the first and last lines `{}`. One of those properties is `type`--in this case the value of the type property of the object is a collection of geographic features, or a `FeatureCollection` and the second property is `features`. Inside the features you'll find another list of objects--a feature collection--contained within the two square brackets `[]`.

<pre><code>
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "contributor": "Aaron Dennis"
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
        ...
        ]
      }
    }
  ]
}
</code></pre>

Within the square brackets `[]` of the features property we see another curly brace `{` followed by the familiar `type` property. This time, the value of the `type` property is just `Feature`, not `FeatureCollection`. That's because we're now looking the GeoJSON data for a single polygon representing an individual tracing assignment. The three properties of this `Feature` object are `type`, `properties`, and `geometry`. To make an analogy to Shapefiles, `properties` contains all of the feature's attribute information, like the .dbf file, and `geometry` contains information identifying what type of feature it is and a listing of all the coordinates for the vertices of the feature, like the .shp file.

To select your tracing assignment boundaries `Polygon` `Feature` from within all of the features, you'll need to create a GeoJSON with list of `"features": [...]` that includes only your `Feature`. The tool at http://geojson.io will set you up with an empty GeoJSON `FeatureCollection` you can copy and paste your `Feature` into, or you can copy and paste all the GeoJSON text I have provided into the text pane at http://geojson.io and edit it down to just your assigned feature.

### Convert Your GeoJSON to a GPX File

Now that you have your assigned area in GeoJSON format, it's time to make a quick conversion to GPX. Why didn't we just make a GPX file in the first place? Because GPX files don't play as well with web mapping APIs like Leaflet or Mapbox GL, aren't as readable, and you're much less likely to run into them. Plus, GPX files can't actually draw polygons, just lines around their edges.

I've built an interface at http://aaronpdennis.github.io/geojson-to-gpx/ to help us convert the data. Paste your GeoJSON into the top box, click the button, and then copy and paste the code in the bottom box into a blank text document on your computer (use a basic text editor like NotePad on Windows or TextEdit on Mac OS X). Save that file with the extension *.gpx*.

### Opening Your Tracing Assignment in the iD Editor

You're now almost ready to start contributing to OSM. Go to http://www.openstreetmap.org, log in to your account, and click Edit.
