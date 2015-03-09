Mark Hoffman’s Web Optimization Project (Project 4) Readme.md

Please use the optimize2 branch for analysis.

For this project, I used the following commands to establish a local http server and use ngrok to display and analyze my website.

python -m http.server 8080

ngrok 8080

I used Page Speed Insights to analyze the download speeds for the following:

index.htm.
project-2048.html
project-webperf.html
project-mobile.html
views/pizza.html 

I was able to get a score > 90 for both the mobile and desktop versions by doing the following:

1. Commented out the Google font library, which is not needed:

    <!--<link href="//fonts.googleapis.com/css?family=Open+Sans:400,700" rel="stylesheet">  -->

2. Inlined the style.css inside the html files instead of having it download the file.
3. Used the “async” keyword for the print.css file so that it wouldn’t halt the DOM download waiting for the file to load (even though it’s relatively small).
4. Moved the Google Analytics script and the logCRP script to the bottom of the files since they’re not needed to load the DOM or CSSOM.
5. Resized and defined the sizes many of the images in the /img and the /views/images folders.
6. Minified the following:
a. bootstrap-grid.css (bootstrap-grid.min.css)
b. main.js (main.min.js)
7. For the pizzas.html, I had to change the number of pizzas in the anonymous function in the document.addEventListener function from its original 200 pizzas to 24 pizzas, which is all that are visible.

I was able to resize the pizzas in less than 5ms by modifying the changePizzaSizes(size) function.  By moving the pizzas variable outside the loop and analyzing only one pizza in the pizzas array and using that size to resize all the pizzas.

Finally, I was able to get the FPS parameter well below 60 by doing the following:

1. Moved the Math.sin method out of the for loop in the updatePositions() function.
2. Changing the number of pizzas to 24 made the for loop iterate fewer times than the original 200 pizzas.
Invoked the hardware acceleration feature in the browser by triggering 3D rendering even though it’s only a 2D animation.  I accomplished this by adding the following lines to the .mover class in CSS:

   -webkit-transform: translateZ(0);
   -moz-transform: translateZ(0);
   -ms-transform: translateZ(0);
   -o-transform: translateZ(0);
    transform: translateZ(0);


