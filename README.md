# CSM_GCD_U2_CC
Creative Computing
Yida Zhang
# How to create a split scan processing in p5.js

## 0.Create the canvas with video capture
    function setup() {
      // canvas size
      createCanvas(// width, // height);
      pixelDensity(1);
      video = createCapture(VIDEO);
      // video size
      video.size(// width, // height);
     }
      function draw() {
      background(51);
      // make video appear on the canvas
      image(video,0,0,)
     }

     
## 1.copy pixels from video feedback
Copy Reference Code: https://p5js.org/reference/#/p5/copy
    
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
    
from the reference code, we want to copy from video feedback instead
so that:

     var w=video.width
     var h=video.height
     copy(video, video.w/2,0,1,h)

copy the pixels to the designated column:

     copy(video, w/2,0,1,h,x,0,1,h);
     // making the copied feed back go towards right (x-axis)
     x=x+1
     
# Congrats! You now just have to put the codes togetehr!

// amend your canvas/video dimension as you wish

         let video;

     let x = 0;

     function setup() {
       createCanvas(800, 240);
       pixelDensity(1);
       video = createCapture(VIDEO);
       video.size(320, 240);
       background(51);
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
