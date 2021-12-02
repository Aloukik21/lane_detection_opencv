
# Canny edge detection
Canny edge detection is a technique to extract useful structural information from different vision objects and dramatically reduce the amount of data to be processed. It has been widely applied in various computer vision systems. Canny has found that the requirements for the application of edge detection on diverse vision systems are relatively similar. Thus, an edge detection solution to address these requirements can be implemented in a wide range of situations. The general criteria for edge detection include:

1. Detection of edge with low error rate, which means that the detection should accurately catch as many edges shown in the image as possible
2. The edge point detected from the operator should accurately localize on the center of the edge.
3. A given edge in the image should only be marked once, and where possible, image noise should not create false edges.


# Hough Line Transform
The Hough Line Transform is a transform used to detect straight lines.
To apply the Transform, first an edge detection pre-processing is desirable.
How does it work?
As you know, a line in the image space can be expressed with two variables. For example:

In the Cartesian coordinate system: Parameters: (m,b).
In the Polar coordinate system: Parameters: (r,θ)
![image](https://user-images.githubusercontent.com/30460954/144478986-0e82e0d5-d8c0-4395-ab96-86c137ea911b.png)

For Hough Transforms, we will express lines in the Polar system. Hence, a line equation can be written as:

y=(−cosθsinθ)x+(rsinθ)
Arranging the terms: r=xcosθ+ysinθ
In general for each point (x0,y0), we can define the family of lines that goes through that point as:

rθ=x0⋅cosθ+y0⋅sinθ
Meaning that each pair (rθ,θ) represents each line that passes by (x0,y0).

If for a given (x0,y0) we plot the family of lines that goes through it, we get a sinusoid. For instance, for x0=8 and y0=6 we get the following plot (in a plane θ - r):

![image](https://user-images.githubusercontent.com/30460954/144479023-cee3866c-d749-44ae-a583-bd2fd171e426.png)

We consider only points such that r>0 and 0<θ<2π.

We can do the same operation above for all the points in an image. If the curves of two different points intersect in the plane θ - r, that means that both points belong to a same line. For instance, following with the example above and drawing the plot for two more points: x1=4, y1=9 and x2=12, y2=3, we get:

![image](https://user-images.githubusercontent.com/30460954/144479064-246ecfd1-174e-42b6-9040-e1106900df9a.png)

The three plots intersect in one single point (0.925,9.6), these coordinates are the parameters ( θ,r) or the line in which (x0,y0), (x1,y1) and (x2,y2) lay.

What does all the stuff above mean? It means that in general, a line can be detected by finding the number of intersections between curves.The more curves intersecting means that the line represented by that intersection have more points. In general, we can define a threshold of the minimum number of intersections needed to detect a line.
This is what the Hough Line Transform does. It keeps track of the intersection between curves of every point in the image. If the number of intersections is above some threshold, then it declares it as a line with the parameters (θ,rθ) of the intersection point.



#Demonstration:

![ezgif com-gif-maker](https://user-images.githubusercontent.com/30460954/144479087-e6ee2c9d-23c0-453e-b4ec-f6c28774fa19.gif)

