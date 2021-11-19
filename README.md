# CSM_GCD_U2_CC
Yida Zhang

# How to create a split scan processing in p5.js


## 0.Create the canvas with video capture
When you open p5.js editor you will see the default:

     function setup() {
       createCanvas(400, 400);
     }

     function draw() {
       background(220);
     }
     
<br>

amend the canavas with video capture:

    function setup() {
      // canvas size
      createCanvas(width, height);
      // density of pixel
      pixelDensity(1);
      video = createCapture(VIDEO);
      // video capture size
      video.size(width, height);
     }
     // display video on canvas
      function draw() {
      // background colour (0-255)
      background(100);
      image(video,0,0,)
     }
     
now you completed your canvas setup!
     
## 1.copy pixels from video feedback to canvas

[Copy] Reference Code: https://p5js.org/reference/#/p5/copy
    
    let img;
    function preload() {
      img = loadImage('assets/rockies.jpg');
    }

    function setup() {
      background(img);
      copy(img, 7, 22, 10, 10, 35, 25, 50, 50);
      stroke(255);
      noFill();
      // Rectangle shows area being copied
      rect(7, 22, 10, 10);
    }
    
from the reference code, we want to copy from video feedback instead of an image:

     // make a x variable so we can amend it later
     let x = 0;
     // let video to load pixels so p5 editor can read
     video.loadPixels();
     // just to assign value to "w" and "h" to make things easier
     // you can use "width" and "height" instead if you wish
     let w=video.width
     let h=video.height
     // copy pixels from video to canvas
     // first 4 values define what is copied
     // w/2,0: copy from the central of the video from the top
     // 1,h: copy a column of width of 1 pixel, height=video height
     // the next 4 value define how it puts to canvas
     // x,0: feed to the left edge (x is defined as 0 previously)
     // 1,h: feed as a 1-pixel column with height of the video
     copy(video, w/2,0,1,h,x,0,1,h)
     // making the copied go towards right by 1 pixels each time ran
     x=x+1
     // when x exceeds the width, make it go back to the very left (0) to make it a loop
     if (x > width) {
        x = 0;
     }
     
# Congrats! You now just have to put the codes togetehr!

// amend your canvas/video dimension as you wish
// make canvas height same as video height if you want to make the output fill up the whole canvas

         let video;

     let x = 0;

     function setup() {
       createCanvas(width, height);
       pixelDensity(1);
       video = createCapture(VIDEO);
       video.size(width, height);
       background(100);
     }

     function draw() {
       video.loadPixels();
       let w = video.width;
       let h = video.height;
       copy(video, w/2, 0, 1, h, x, 0, 1, h);
       x = x + 1;
       if (x > width) {
         x = 0;
       }
     }
