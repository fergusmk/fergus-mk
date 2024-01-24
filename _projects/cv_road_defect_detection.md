---
layout: post
title: Road Defect Detection (Computer Vision)
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

### Data Processing ###
To take advantage of well studied 2D object detection techniques, and noting the planar nature of most road defects, a 2D quadratic plane was fitted to the road surface, to which the point clouds were projected onto.

![Raw, registered point cloud data](/assets/images/recap.png "Raw, registered point cloud data")

![Projection of points in 3D space to the fitted road surface](/assets/images/quadratic_fit.png "Projection of points in 3D space to the fitted road surface")




### Model Choices ###

Results
============


### An h3 header ###

Now a nested list:

 1. First, get these ingredients:

      * carrots
      * celery
      * lentils

 2. Boil some water.

 3. Dump everything in the pot and follow
    this algorithm:

        find wooden spoon
        uncover pot
        stir
        cover pot
        balance wooden spoon precariously on pot handle
        wait 10 minutes
        goto first step (or shut off burner when done)

    Do not bump wooden spoon or it will fall.

Notice again how text always lines up on 4-space indents (including
that last line which continues item 3 above).

Here's a link to [a website](http://foo.bar), to a [local
doc](local-doc.html), and to a [section heading in the current
doc](#an-h2-header). Here's a footnote [^1].

[^1]: Some footnote text.

Tables can look like this:

| Header 1 | Header 2                   | Header 3 |
|:--------:|:--------------------------:|:--------:|
| data1a   | Data is longer than header | 1        |
| d1b      | add a cell                 |          |
| lorem    | ipsum                      | 3        |
|          | empty outside cells        |          |
| skip     |                            | 5        |
| six      | Morbi purus                | 6        |


A horizontal rule follows.

***

Here's a definition list:

apples
  : Good for making applesauce.

oranges
  : Citrus!

tomatoes
  : There's no "e" in tomatoe.

Again, text is indented 4 spaces. (Put a blank line between each
term and  its definition to spread things out more.)

Here's a "line block" (note how whitespace is honored):

| Line one
|   Line too
| Line tree

and images can be specified like so:

![example image](https://images.unsplash.com/photo-1488190211105-8b0e65b80b4e?w=500&h=500&fit=crop "An exemplary image")

Inline math equation: $\omega = d\phi / dt$. Display
math should get its own line like so:

$$I = \int \rho R^{2} dV$$

And note that you can backslash-escape any punctuation characters
which you wish to be displayed literally, ex.: \`foo\`, \*bar\*, etc.
