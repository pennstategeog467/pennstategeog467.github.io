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

The map above renders the assigned sections by referencing a GeoJSON file. Think of a GeoJSON file as similar to a Shapefile in that it contains vector geographic data, but is contained entirely in one text file that is human readable, instead of several files with information about geometry in one file, related attributes in a second, and projection information in yet another. We use GeoJSON on the web because the text within the file is directly readable as data in Javascript. You'll want to have a solid understanding of this data format for the next part of the exercise. Read more about GeoJSON <a href="http://giscollective.org/github-bringing-geojson-to-life-since-2013/">here</a>.

As you know, OpenStreetMap is a collaborative database that lots of people can contribute to at the same time. This also means sometimes people are unknowingly editing the same part of the map at the same time, which causes obvious issues and ends up wasting everyone's time. That's why we have gone through all this trouble of dividing our mapping project--buildings in State College--into different sections. You'll be able to display the boundary of your assigned section in the OSM iD Editor as you're editing so that you don't step on the toes of anyone else working on the map (like the other people in this class) and they will stay clear of your section. To do that, we'll have to take a closer look at that GeoJSON file, pull out the data relevant to you, and convert it to a data format supported by the iD Editor called a GPX file.
