---
layout: page
title: Brickspace
permalink: /brickspace/
---

> This page was written in 2014 and has only been lightly edited since.

Brickspace is my University of Houston Summer Undergraduate Research Fellowship 2014 project, developed under the supervision of Ioannis Kakadiaris and the [UH Computational Biomedicine Laboratory](http://cbl.uh.edu).

1. Put your Lego bricks on a table.
1. Take a picture of the bricks with Brickspace.
1. Receive custom model instructions featuring your bricks.

Brickspace can detect red, orange, yellow, green, blue, and black 2x4 bricks, as seen in the video below.

During the research project, the app included support for the [Structure Sensor](http://structure.io) from Occipital. The Structure is like a mini-[Kinect](http://en.wikipedia.org/wiki/Kinect) for mobile devices. When the Structure is attached, it provides depth data to the app. Brickspace uses this data to esimate the size of each brick and assign it one of the four supported sizes: 2x1, 2x2, 2x3, or 2x4. The public version does not contain Structure support. If you're interested, I've written [an extensive explanation](http://ansonj.org/blog/2014/10/2/brickspace-and-the-structure-sensor) of how this version of Brickspace uses the Structure Sensor.
<!-- TODO: Update blog post link above and also below -->

## YouTube

Watch a [90-second demo video here](https://youtu.be/Ku-ucqea0Ho).
<!-- 
I tried everything I could find for a reasonable amount of time, but it doesn't seem like embedding an iframe in a Markdown source file works with the GFM Markdown parser. Using an `_includes` file (such as is mentioned here: http://www.beingy.net/blog/embed-youtube-video-in-jekyll/) will work if the page source is HTML, but not Markdown. I wish I could directly embed the video here, but it's really not worth any further struggle.
-->

## Code

The source code for the entire application is available on [GitHub](http://github.com/ansonj/Brickspace). The [`structureEnabled`](http://github.com/ansonj/Brickspace/tree/structureEnabled) branch contains the code for the frozen research version with Structure Sensor support, and [`master`](http://github.com/ansonj/Brickspace/tree/master) contains the latest public version.

## Press

[Turning Cancer to Fat, Drunk Fruit Flies Among Student Projects](http://www.uh.edu/news-events/stories/2014/August/080414SURF2014.php) from Lisa Merkl at UH

## Requirements

1. iPad of your choice.
1. Building bricks of various colors. Designed for red, orange, yellow, green, blue, and black Lego 2x4 bricks.
1. A white or lightly-colored surface.

## The process

1. Dump out your bricks onto your white surface.
1. Spread the bricks out a bit so that they're not touching each other.
1. Use the app to take a picture of the bricks. The app will detect the bricks in the image.
1. Review the results of the image capture and processing. You may need to change the size or color of the bricks, since the app assumes all bricks are 2x4. Also, the app sometimes counts extra shapes (like shadows) as bricks, which you can delete during this step.
1. The app will then give you custom model instructions using the bricks that it has detected. Build away!

## Limitations

* Adding bricks: The app does not yet support tapping the image to add bricks that the image processing missed, but this will be supported in a future release.
* Available models: The app currently knows how to build three different models. More models will be available in future updates. 
  1. Basic Tower: All of your 2x4s stacked on top of each other.
  1. Flat Pyramid: All of your 2x4s arranged into a pyramid.
  1. Spiral Tower: All of your 2x4s arranged into a square tower with jagged, spiraling edges and a colorful pattern.
* Scanning / image detection: The image processing stumbles over shadows and any patterns on the scanning surface. Small bricks that are close together are seen as one brick. Tweaking parameters to detect smaller objects often results in the detector registering the studs on top of a brick as bricks.
* Brick size detection: In the research version with support for the Structure Sensor, the app only correctly assigned sizes to bricks about 50% of the time.

---

![Research poster]({{ 'projects/brickspace/URDposter.png' | prepend: site.asset_url_prefix }})

Research poster, presented at the University of Houston Undergraduate Research Day event, October 9, 2014.

---

![Class diagram]({{ 'projects/brickspace/classdiagram.png' | prepend: site.asset_url_prefix }})

---

## Under the hood

Brickspace uses [OpenCV](http://opencv.org) for image processing and object detection&mdash;specifically, [`SimpleBlobDetector`](http://docs.opencv.org/modules/features2d/doc/common_interfaces_of_feature_detectors.html) from `features2d.h`. This allows the app to detect where bricks are and estimate their color.

In the research version, the [Structure SDK](http://structure.io/developers) handles communication with the Structure Sensor. When Brickspace captures an image, the SDK provides a depth measurement at each pixel. This is used to estimate the volume of each brick. If you're interested, I've written [an explanation of how this works](http://ansonj.org/blog/2014/10/2/brickspace-and-the-structure-sensor).
<!-- TODO: Update blog post link above -->

## Stats, just for kicks

- 27 header files
- Lines of code (counting only the header files and their implementations plus `main.m`):
    - Research version (with Structure support): 4,301
    - Public version: 3,762

## Disclaimer

Brickspace is not affiliated with, sponsored by, or related to [The Lego Group](https://en.wikipedia.org/wiki/The_Lego_Group), [Lego Fusion](http://mashable.com/2014/07/31/lego-fusion-town-master-review/), or [Occipital](http://occipital.com).
