# CodeProject.AI-Egge-IPcam-Models

This project has two (overfit) models for use with CodeProject.AI and BlueIris. 

## egge
  * cat,coyote,deer,dog,fox,person,rabbit,raccoon
  * This is built from: https://app.roboflow.com/egge-public/ipcams2/overview

## package
  * package,vehicle
  * This is built from: https://app.roboflow.com/egge-public/packages-vehicles2/overview

## garage
  * garbage bin,honda civic,honda crv,person,tool bucket
  * https://app.roboflow.com/egge-public/garage/overview

For several years now I've run these models on my Jetson Nano. I have each of my ipcams use their ftp functionality to upload jpegs directly to my nano. This has worked quite well, but is rather bespoke. My original motivation was to keep deer from eating my fruit trees. Later, it proved to be quite useful keeping my [[https://blog.roboflow.com/using-computer-vision-to-detect-package-deliveries/][dog from eating my meal deliveries]]. When the Jetson sees a deer, it calls a script on HomeAssistant, which in turns has Alexa announce "Deer, Deer, Deer!". My dog quickly learned what this means and will race outside to chase the deer away. 

On my nano I divide the *egge* dataset into two models, one for day and one for infrared (IR). Note, IR and dark are not the same. When my nano processes a jpeg it first determines if there are 1 or 3 channels, it then routes it to the correct model. I spent rather too much time creating a 608x608x1 model, but it is of course 1/3 the size of the color model. I don't need to have any clever script to say if it should be using a day or night model. There may still be value in having a three channel model for when its dark but the camera is not in IR. These seem to be the hardest to detect. 

It now seems funny to have packages and vehicles together. However, the Jetson has limit memory and I didn't want to have two separate models. I didn't include these in the *egge* dataset because I expect only certain cameras to see these two objects. 

The garage project was actually my first, and probably isn't useful unless your garage looks exactly like mine. It seems creates sensors so I know which cars are in the garage and if the garbage bins are inside or out. 

This repo was inspired by https://github.com/MikeLud/CodeProject.AI-Custom-IPcam-Models, though the content of the models is all images from my 15 cameras. This means my model is likely very overfit to my house. In fact, when the model sees something new, it usually flags it. In general, I'm fine having it overfit, but it will likely not perform as well for other people. But I'm happy to incorporate other peoples images into my Roboflow datasets, which should make the models more robust.
