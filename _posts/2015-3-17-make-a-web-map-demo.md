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

This is all about getting our hands dirty with HTML, CSS, Javascript, and a mapping library API. It's a quick intro, just to give you a sense of how we can integrate tiled maps in web pages. Copy and paste the entirety of the code blocks below into your HTML file as instructed.

First, create a new `.html` document by opening a text editor like Notepad or TextEdit and saving a blank file called `web-map.html`. Make sure the file extension is `.html` and not `.txt`. You may have to 'save as all file types'.

Before you start, it's important to know that HTML is written in pairs of opening and closing tags that are contained within each other, like this -- `<first><second></second></first>` -- and never like this -- `<first><second></first></second>`. Paste the following blocks of code into your `.html` document within the specified tags.

The code below is a basic template for an html document and includes a box on the webpage--known as a div--where we'll put our map. Copy and paste this into your `.html` file.

<textarea style="height:400px;font-family:monospace;background-color:lightyellow;">

<!--This is an HTML document-->

<!DOCTYPE html>

<!-- Words inside these  < !-- -- >  are comments -->

<!-- In programming languages, comments aren't read by the computer, they're just there to make things more understandable by humans. -->

<!-- HTML is written in opening and closing tags. Here is an opening tag <html> for HTML content. The closing tag </html> is at the bottom -->
<html>

  <!-- This next section is the "head" of document. It doesn't show up on the page but it contains some very important stuff. Notice the opening tag <head> and the closing tag </head> later on. -->
  <head>

  
  
  <!-- Here we close out the <head> tag from further up in the HTML document -->
  </head>

  <!-- Stuff inside the <body> tags is content you're going to see visually on the webpage -->
  <body>

    <!-- A <div> tag is like a box on the page. It divides the page into sections. This div is given the ID of "map" and it's where we're going to put the map.  -->
    <div id='map'></div>



  </body>

</html>

</textarea>

Save your `.html` file and then open it with a web browser like Chrome. Web browsers are the applications that read and interpret `.html` files. As you make changes to the code in your file, save and then 

Copy and paste this next block of code into the space between the `<head></head>` tags.

<textarea style="height:400px;font-family:monospace;background-color:lightyellow;">

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

Add this next block of code after the stuff you just added, but keep it between the `<head></head>` tags. This is some CSS for the page.


<textarea style="height:400px;font-family:monospace;background-color:lightyellow;">
   
    <!-- Stuff between <style> tags is CSS. It adds formatting to document elements, like dividers and text, sometimes based on element IDs. -->
    <style>
  
      /* this is what a comment looks like in CSS */
      
      /* This makes the <body> element fill up the whole page. Everything other element will go inside the <body> element. */
      body { margin:0; padding:0; } 
  
      /* This tells the <div> we ID'd as #map to be in a positon that's not relative to anything else, 0 pixels from the top of its container, 0 pixels from the bottom, and 100% of the containers width. Basically, it's always going to be as large as your browser window */
      #map { position:absolute; top:0; bottom:0; width:100%; }

    </style>

</textarea>

Add this next block of code in between the `<body></body>` tags and after closing `</div>` tag.

<textarea style="height:400px;font-family:monospace;background-color:lightyellow;">

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

</textarea>

Now, when you open the HTML file in a web browser, you should see a map. Great job!

For a little added fun, we can use javascript to provide further functionality. Add the next code block after the `ourMap.setView([40, -74.50], 9);` line and before the closing `</script>` tag.

<textarea style="height:400px;font-family:monospace;background-color:lightyellow;">

// Here's a list, or array, of other map IDs we could have used when we made our map. We're saving it as the variable otherMaps
      var otherMaps = [ 'mapbox.streets',
                        'mapbox.light',
                        'mapbox.dark',
                        'mapbox.satellite',
                        'mapbox.streets-satellite',
                        'mapbox.wheatpaste',
                        'mapbox.streets-basic',
                        'mapbox.comic',
                        'mapbox.outdoors',
                        'mapbox.run-bike-hike',
                        'mapbox.pencil',
                        'mapbox.pirates',
                        'mapbox.emerald',
                        'mapbox.high-contrast',
                        'examples.map-i86nkdio' ];
      
      // Each of the items in the otherMaps list has an index. For example, otherMaps[0] is equal to 'mapbox.streets' because it is in the first, or 0 position, in the array.
      
      // Let's make an "event listener" with javascript so that each time someone clicks on the button with the ID 'nextMap', we load in a random set of map tiles.
      document.getElementById('nextMap').onclick = newMap;
      
      //The even listener above says "on the click of the 'newMap' button, call the function newMap. We define that function below
      function newMap(){ // Defining a new function that will run a block of code
        ourMap.eachLayer(function(layer) { ourMap.removeLayer(layer); }); // Remove any existing tile layers
        var mapIndex = Math.floor(Math.random() * 15); // This gives a random number between 0 and 14
        var layer = L.mapbox.tileLayer(otherMaps[mapIndex]); // Pick out our new tile map layer from the otherMaps options
        layer.addTo(ourMap); // Add the new map layer
      };
</textarea>

Finally, add this HTML button element after the closing `</div>` tag and before the opening `<script>` tag.

<textarea style="height:400px;font-family:monospace;background-color:lightyellow;">

<!-- This button element has an associated javascript event handler that makes a new map layer when the button is clicked. -->
<button id="nextMap" type="button" style="position:absolute;z-index=2;top:10px;left:60px;">Click for a random map.</button>

</textarea>

Save your file and refresh the page. Now, the webpage should be listening for you to click on the button in the top left. When you do, javascript will load a random new tiled map.