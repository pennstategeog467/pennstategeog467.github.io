---
layout: post
title: Putting a Map on a Web Page
excerpt: "Copy and paste for a demonstration of how to use the Mapbox.js API"
modified: 2015-3-17
tags: 
author: aaron_dennis
comments: true
image:
  feature: 
  credit: 
  creditlink: 
---

This is all about getting our hands dirty with HTML, CSS, Javascript, and a mapping library API. It's a quick intro, just to give you a sense of how we can integrate tiled maps in web pages.

First, create a new `.html` document by opening a text editor like Notepad or TextEdit and saving a blank file called `web-map.html`. Make sure the file extension is `.html` and not `.txt`. You may have to 'save as all file types'.

Before you start, it's important to know that HTML is written in pairs of opening and closing tags that are contained within each other, like this -- `<first><second></second></first>` -- and never like this -- `<first><second></first></second>`. Paste the following blocks of code into your `.html` document within the specified tags.

The code below is a basic template for an html document and includes a box on the webpage--known as a div--where we'll put our map. Copy and paste this into your `.html` file.

<textarea style="height:400px;font-family:monospace;">

<!--This is an HTML document-->

<!DOCTYPE html>

<!-- Stuff inside these  < !-- -- >  are comments -->

<!-- In programming languages, comments aren't read by the computer, they're just there to make things more understandable by humans. -->

<!-- HTML is written in opening and closing tags. Here is an opening tag <html> for HTML content. The closing tag </html> is at the bottom -->
<html>

  <!-- This next section is the "head" of document. It doesn't show up on the page but it contains some very important stuff. Notice the opening tag <head> and the closing tag </head> later on. -->
  <head>

  
  
  <!-- Here we close out the <head> tag from further up in the HTML document -->
  </head>

  <!-- Stuff inside the <body> tags is content you're going to see visually on the webpage -->
  <body>

    <!-- A <div> tag is like a box on the page. It divides the page into sections. This div has is given the ID of "map" and, you guessed it, it's where we're going to put the map.  -->
    <div id='map'>
    
      <!-- A <p> tag is paragraph text. Feel free to change the words between the tags, save the file, refresh your the web page, and see them change in the browser. Then delete this comment and the <p> tags and the text between them. -->
      <p>Let's put a map in here.</p>
    
    </div>




  </body>

</html>

</textarea>

Save your `.html` file and then open it with a web browser like Chrome. Web browsers are the applications that read and interpret `.html` files. As you make changes to the code in your file, save and then 

Copy and paste this block of code into the space between the `<head></head>` tags.

<textarea style="height:400px;font-family:monospace;">

    <!-- This just says we're using standard characters when we type. Don't worry too much about it -->
    <meta charset=utf-8 />

    <!-- The title of a website shows up on the page tab in your web browser. -->
    <title>I WANT A MAP!</title>
    
    <!-- The meta tag tells the browser some stuff about what the webpage should or should not do. -->
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />

    <!-- This is where the API comes in. Here, we're referencing the Mapbox.js API, which is a plugin/add-on for Leaflet. The script tag references prewritten javascript code (the API) and defines functions and methods for us to use which helps us do things that would otherwise be thousands of times more complicated like make a tiled map.  -->
    <!-- script tags always mean there's javascript between them or in a source (src) file -->
    <script src='https://api.tiles.mapbox.com/mapbox.js/v2.1.5/mapbox.js'></script>

    <!-- the Mapbox.js API also comes with a CSS stylesheet to format things like zoom controls -->
    <link href='https://api.tiles.mapbox.com/mapbox.js/v2.1.5/mapbox.css' rel='stylesheet' />

</textarea>

<textarea style="height:400px;font-family:monospace;">

<!--This is an HTML document-->

<!DOCTYPE html>

<!-- Stuff inside these  < !-- -- >  are comments -->

<!-- In programming languages, comments aren't read by the computer, they're just there to make things more understandable by humans. -->

<!-- HTML is written in opening and closing tags. Here is an opening tag <html> for HTML content. The closing tag </html> is at the bottom -->
<html>

  <!-- This next section is the "head" of document. It doesn't show up on the page but it contains some very important stuff. Notice the opening tag <head> and the closing tag </head> later on. -->
  <head>

    <!-- This just says we're using standard characters when we type. Don't worry too much about it -->
    <meta charset=utf-8 />

    <!-- The title of a website shows up on the page tab in your web browser. -->
    <title>I WANT A MAP!</title>
    
    <!-- The meta tag tells the browser some stuff about what the webpage should or should not do. -->
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />

    <!-- This is where the API comes in. Here, we're referencing the Mapbox.js API, which is a plugin/add-on for Leaflet. The script tag references prewritten javascript code (the API) and defines functions and methods for us to use which helps us do things that would otherwise be thousands of times more complicated like make a tiled map.  -->
    <!-- script tags always mean there's javascript between them or in a source (src) file -->
    <script src='https://api.tiles.mapbox.com/mapbox.js/v2.1.5/mapbox.js'></script>

    <!-- the Mapbox.js API also comes with a CSS stylesheet to format things like zoom controls -->
    <link href='https://api.tiles.mapbox.com/mapbox.js/v2.1.5/mapbox.css' rel='stylesheet' />

    
    <!-- Stuff between <style> tags is CSS. It adds formatting to document elements, like dividers and text, sometimes based on element IDs. -->
    <style>
  
      /* this is what a comment looks like in CSS */
      
      /* This makes the <body> element fill up the whole page. Everything other element will go inside the <body> element. */
      body { margin:0; padding:0; } 
  
      /* This tells the <div> we ID'd as #map to be in a positon that's not relative to anything else, 0 pixels from the top of its container, 0 pixels from the bottom, and 100% of the containers width. Basically, it's always going to be as large as your browser window */
      #map { position:absolute; top:0; bottom:0; width:100%; }

    </style>

  <!-- Here we close out the <head> tag from further up in the HTML document -->
  </head>

  <!-- Stuff inside the <body> tags is content you're going to see visually on the webpage -->
  <body>

    <!-- A <div> tag is like a box on the page. It divides the page into sections. This div has is given the ID of "map" and, you guessed it, it's where we're going to put the map.  -->
    <div id='map'></div>


    <!-- Remember when we referenced that API earlier? Now we'll use it. The code between <script> tags is javascript -->
    <script>

      // This is what a comment looks like in javascript
      
      // This is an access token that's associated with a Mapbox Account. It lets us use the Mapbox plugin
      L.mapbox.accessToken = 'pk.eyJ1IjoiYWFyb25kZW5uaXMiLCJhIjoiem5LLURoYyJ9.T3tswGTI5ve8_wE-a02cMw';

      // Here, the code is telling the browser to make a map in the element with the ID 'map', use the map tiles from the Mapbox tile API associated with the Map ID 'examples.map-i86nkdio' and store it as the variable ourMap so we can reference it later.
      var ourMap = L.mapbox.map('map', 'examples.map-i86nkdio');
      
      // In this line of code, we're using a `method` on ourMap to change the view to a pair of lat/long coordinates and a specific zoom level
      ourMap.setView([40, -74.50], 9);

    </script>

  </body>

</html>

</textarea>