---
layout: post
title: Road Defect Detection 
description: Road defect detection through RGB and depth data
---
A research project about using computer vision techniques to automatically detect and classify road defects.
...

Motivation
============

Road defect detection is mostly performed manually, which is inefficient, inaccurate, and unscalable. It is difficult to improve both the quality and frequency of surveys. Therefore, automated methods have been explored. 

> The perceived benefits of more frequent road inspection is too low to justify its implementation.

A further motivation for developing automated detection methods is the proposal to create a [Road Digital Twin](https://drf.eng.cam.ac.uk/research/digital-twins). This proposal relies on having frequent, high quality data as inputs in order to maximize the potential utility.

There are two main modalities of data that can be used for defect detection: 2D RGB images and 3D point cloud images. However, when each modality should be used is not well understood. This project aims at bridging that gap by investigating the stregnths and weaknesses of each input modality. 


Research activities
============

### Data Collection ###
Data was collected on roads around Cambridge. 2D RGB images were collected using an iPad, while 3D point clouds were collected by a FARO Laser Scanner.

![FARO scanner in action](/assets/images/faro_scanner.png "Laser scanning the geometry of potholes")

![Raw, registered point cloud data](/assets/images/recap.jpeg "Raw, registered point cloud data")

### Data Processing ###
To take advantage of well studied 2D object detection techniques, and noting the planar nature of most road defects, point cloud data were transformed into a 2D depth map. A 2D quadratic plane was fitted to the road surface, to which the point clouds were projected onto. In the picture below, the green plane was the fitted road surface, and the greyscale surface was the actual depth levels of each point on the road surface, darker shades mean points are below the surface, indicating possible potholes.

![Projection of points in 3D space to the fitted road surface](/assets/images/quadratic_fit.png "Projection of points in 3D space to the fitted road surface")

### Model Choices ###
Mask RCNN was chosen for the object detector. It has the benefits of being able to not only capture the precise outline of an object, but also being able to count the number of instances in an image. Both of these propoerties are important for road maintenance applications. The former allows the severity of a defect to be documented, the latter allows the recording of all individual instances. 


Results
============
The image below shows defects being detected using RGB input data (top being input image, bottom being output image with defect masks.)
![RGB detection results](/assets/images/example_1.jpg "RGB detection results")

The image below shows another RGB detection with a wet road surface, noting the change in textures of road defects.
![RGB detection results](/assets/images/example_2.jpg "RGB detection results on a wet surface")

The image below shows an example of a detection of the depth input data.
![Depth detection results](/assets/images/example_3.jpg "Depth detection results")

The image below shows a comparison between detection results of the same segmenet of the road of the RGB model and the depth model.
![Detection results comparison](/assets/images/example_5.jpg "Detection results comparison")

Overall, the conclusion is that different road conditions, such as a wet surface or water spills, can affect the appearance of road defects. For example, wet potholes may look brighter if the water inside is reflective. Cracks can appear thicker if water seeps in and dries off more slowly than the surrounding surface. These can negatively affect methods that rely on visual features to classify defects. 

Geometry based methods, like point clouds and depth data, do not suffer from this problem. The physcial shape of the defects do not change with weather. However, this comes at the expense of having lower resolution inputs that make certain defects, such as cracks, invisible. 
