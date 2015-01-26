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

# Tracing Assignments

In the map below you can see State College divided into indivual sections by pink polygons. The dark grey shapes on the map show the `#building` layer from Mapbox Streets, a global vector tile source built and regularly updated from the OpenStreetMap (OSM) database. Any changes to OSM will be reflected on this map within minutes. As of January 24, 2015, many areas of the OSM database in State College could benefit from someone going through and tracing building outlines. We have assigned each section to a specific contributor. You will be using the OSM iD Editor to add building content in your assigned area. Explore the map by clicking on the pink shapes to see who was assigned to each section.

<figure>
  <iframe src="http://aaronpdennis.github.io/geog467-osm-sc-assignments/" style="height:400px;width:100%;" frameBorder="0"></iframe>
  <figcaption>Click on the pink shapes to see assignments for OSM contributions.</figcaption>
</figure>

The map above renders the assigned sections by referencing a GeoJSON file. Think of a GeoJSON file as similar to a Shapefile in that it contains vector geographic data, but it's a single text file that is human readable, instead of several files with information about geometry in the .shp file, related attributes in another file, and projection information in yet another. We use GeoJSON on the web because the text within the file is directly readable by JavaScript as data. You'll want to have a solid understanding of this data format for the next part of the exercise. Read more about GeoJSON <a href="http://giscollective.org/github-bringing-geojson-to-life-since-2013/" target="_blank">here</a>.

As you know, OpenStreetMap is a collaborative database that lots of people can contribute to at any time. This also means sometimes people are unknowingly editing the same part of the map at the same time, which causes issues and ends up wasting everyone's time. That's why we have gone through all this trouble of dividing our mapping project--tracing buildings in State College--into different sections. You'll be able to display the boundary of your assigned section in the OSM iD Editor as you're editing so that you don't step on the toes of anyone else working on the map (like the other people in this class) and they will stay clear of your section. To do that, we'll have to take a closer look at that GeoJSON file, pull out the data relevant to you, and convert it to a data format supported by the iD Editor called a GPX file.

### Referencing Your Assignment in the iD Editor

To display your tracing assignment for reference in the iD Editor, we'll need to extract your specific polygon feature from the GeoJSON file and create a GPX file. Why does it need to be a GPX file? This particular type of file has a long history with OSM and, consequently, all of the modern OSM editing tools, like the iD Editor, provide great functionality for this data format. A GPX file is what GPS receivers generate when you mark waypoints or create tracks while walking around in the field. They were especially useful in the early days of OSM when the primary method of adding roads and other features was not through tracing satellite imagery, but uploading, tracing, and editting data collected by contributors with GPS receivers. This is still a useful method today for collecting geographic data about things like trails, which often can't be seen from space, or in places where high resolution imagery isn't available.

We'll be using the GPX files for the less conventional purpose of designating assigned areas for a coordinated mapping effort, although if you ever contribute to the Humanitarian OpenStreetMap Team's collaborative mapping efforts--and you should--you'll see their <a href="http://tasks.hotosm.org/" target="_blank">tasking manager</a> also uses boundaries in GPX format to split a larger effort into smaller pieces.

So let's make the GPX file you need and start mapping.

### Select Your Assignment from the GeoJSON

A GeoJSON file is just a text file. You can open it, copy and paste all the text it into another place, and it will still be GeoJSON. You can find the GeoJSON for the tracing assignments <a href="https://raw.githubusercontent.com/aaronpdennis/geog467-osm-sc-assignments/gh-pages/assignments.geojson" target="_blank">here.</a>

This is the GeoJSON, and at first it probably looks like a long and confusing list of brackets, numbers, and punctuation. Let's start with the first three lines and the last two.

<pre><code>
{
  "type": "FeatureCollection",
  "features": [
...
  ]
}
</code></pre>

These are the lines that set up everything else. They create what is known as an object in JavaScript. The object is a list of properties and values between the two curly braces on the first and last lines `{}`. One of those properties is `type`--in this case the value of the type property of the object is a collection of geographic features, or a `FeatureCollection` and the second property is `features`. Inside the features you'll find another list of objects--a feature collection--contained within the two square brackets `[]`.

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

To select your tracing assignment boundary's `Polygon` `Feature` from within all of the features, you'll need to create a GeoJSON with list of `"features": [...]` that includes only your `Feature`. The tool at <a href="http://geojson.io" target="_blank">http://geojson.io</a> will set you up with an empty GeoJSON `FeatureCollection` you can copy and paste your `Feature` into, or you can copy and paste all the GeoJSON text I have provided into the text pane at <a href="http://geojson.io" target="_blank">http://geojson.io</a> and edit it down to just your assigned feature.

### Convert Your GeoJSON to a GPX File

Now that you have your assigned area in GeoJSON format, it's time to make a quick conversion to GPX. Why didn't we just make a GPX file in the first place? Because GPX files don't play as well with web mapping APIs like Leaflet, aren't as readable, and you're much less likely to use them in general. Plus, GPX files can't actually draw polygons, just the edges of the polygon.

I've built an interface at <a href="http://aaronpdennis.github.io/geojson-to-gpx/" target="_blank">http://aaronpdennis.github.io/geojson-to-gpx/</a> to help us convert the data. Paste your GeoJSON into the top box, click the button, and then copy and paste the code in the bottom box into a blank text document on your computer (use a basic text editor like Notepad on Windows or TextEdit on Mac OS X). Save that file with the extension *.gpx*.

# Editing OpenStreetMap with the iD Editor

You're now almost ready to start contributing to OSM. Go to <a href="http://www.openstreetmap.org" target="_blank">OpenStreetMap.org</a>, log in to your account, zoom to State College, and click Edit. This will bring you into the iD Editor. You will see an option on the screen to start a walkthrough of the editor's functionality or begin editing immediately. Choose the walkthrough for your first time.

After the walkthrough, click begin editing. The first thing we'll do is drag and drop the GPX file you saved on the computer into the iD Editor. If your GeoJSON to GPX conversion process went without any mistakes, you'll see your assigned area rendered on the map. Now, you can start editing.

Your job is to trace all visible buildings inside your assigned area and tag them appropriately. We will talk about how to properly trace and tag OSM features in class.
