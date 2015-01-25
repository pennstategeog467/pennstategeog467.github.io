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

A GeoJSON file is just a text file. You can open it, copy and paste all the text it into another place, and it will still be GeoJSON. I have placed all the GeoJSON for the tracing assignments in <a href="/geojson-tracing-assignments/">another post--open it in a new tab.</a>

This is the GeoJSON, and it probably looks like a long and confusing list of brackets, 
