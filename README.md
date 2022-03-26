# CS220

# Project 1 - Image Processing
The goal of this assignment is to introduce you to the basic features of JavaScript, such as functions,
variables, conditionals, and loops. You should already be familiar with these concepts from other
programming languages (e.g., Java). You will use these features to write several image processing functions
(e.g., blur, sharpen, and adjust brightness). Project also showcases testing methodology for images after 
processing. 

# Project 2 - Higher Order Functions and Image Processing
The goal of this assignment is to attempt to process images using higher order functions instead of elementary
structures like for and while loops. We should manage to use different HOFs such as reduce, filter, and map
in order to achieve the following functions: 

<imageMapXY(img: Image, func: (img: Image, x: number, y: number) => Pixel): Image>

The result must be a new image with the same dimensions as img.
The value of each pixel in the new image should be the result of
applying func to the corresponding pixel of img.


<imageMask(img: Image, cond: (img: Image, x: number, y: number) => boolean, maskValue: Pixel): Image>

The result must be a new image, in which the value of the pixel
at (x, y) is either (a) identical to the value of the pixel at (x, y) in
the original image when cond(img, x, y) returns false or
(b) the value maskValue when cond(img, x, y) returns true.

<imageMapCond(img: Image, cond: (img: Image, x: number, y: number) => boolean, func: (p: Pixel) => Pixel): Image>

The result must be a new image, where the value of pixel at (x, y) is either (a) identical to the value of the
pixel at (x, y) in the original image when cond(img, x, y) returns false or (b) the value func(p),
where p is the original pixel, when cond(img, x, y) returns true.

<isGrayish(p: Pixel): boolean>

The result should be true if and only if the difference between the maximum and minimum color channel
value is at most 1/3

<grayHalfImage(img: Image): Image>

The result must be a new image that is the half-grayed version of the argument, where the top part of the
image is grayed out and the bottom part of the image is in color. If the y-position is less than half of the
image height, then transform this part like with the makeGrayish function above.

<blackenLow(img: Image): Image>

The result must be a new image where, for each pixel, any channel value lower than 1/3 is set to 0 for the
corresponding pixel in the new image. Other channels for the pixel are not modified.

# Project 3 - More Higher Order Functions and Image Processing

<blurPixel(img: Image, x: number, y: number): Pixel>
The result is the blurred value of the pixel at coordinates (x, y). To do this, consider the red, green,
and blue channel of each pixel independently. The red channel of the resulting pixel should be
the mean of the red channels of the pixels neighboring (x, y) and the (x, y) pixel itself. Compute
the blue and green channels in the same way. Two distinct pixels are neighbors if both their
x-coordinates and y-coordinates differ by at most 1 in absolute value. 


<blurImage(img: Image): Image>
The result must be a new image that is the blurred version of the argument, with pixels obtained
by applying blurPixel to each pixel of the input image. 

<diffLeft(img: Image, x: number, y: number): Pixel>
It returns a grayscale pixel representing the intensity difference between pixel (x, y) and pixel
(x-1, y) if the latter exists (otherwise, consider there is no intensity difference). Calculate the mean
value of the three color channels for pixel (x, y) (call it m1) and the mean value of pixel (x-1, y)
(call it m2). Set all three channels of the result to |m2-m1|.

A function called highlightEdges that takes an image as argument and returns a new
grayscale version of the input image with highlighted edges. To do so, apply diffLeft to each
pixel. Do not use loops. Use one of the higher-order functions defined in the past homeworks.

<reduceFunctions(fa: ((p: Pixel) => Pixel)[] ): ((x: Pixel) => Pixel)>
ReduceFunctions takes an array of functions, each taking a pixel and returning a pixel.
It returns a single function (also from pixel to pixel) that composes all functions in the array, with
the function at index 0 applied to the pixel first. Use reduce() to implement it.

<combineThree(img: Image): Image>
The result is a new image where each pixel is transformed successively as done by the functions
makeGrayish, blackenLow and shiftRGB, in this order. Use imageMap and reduceFunctions.



# Project 4a & 4b - Oracles and Stable Matching
Writing code that you think is right is not enough for anyone to be confident that your software
is correct. However, almost no software complex enough to be useful can be proved correct by
hand or automatically in a reasonable amount of time. A computer scientist’s solution to this
problem is automated testing. Your job in this assignment is to build an automated testing
oracle for a hypothetical solution to the stable matching problem.

Your oracle’s job is to generate and feed test inputs to a given solution and test the correctness of
the output. In the past, you did this by comparing the output to a precomputed right answer.
This assumes two things: that there is only one right answer, and that it is easy for you to find it.
In the real world, either of these can be false. (How do you know what the right answer to an
arbitrary instance of the problem is if the original problem was to write a program to find it?)
We will generate both correct and incorrect solutions of the stable matching problem to help you
write and test your oracle. You submit your oracle, and we will evaluate its performance in
classifying various implementations as correct or incorrect.

You should write code that is well structured, readable, and employs the right abstractions (use
higher-order functions). This will make it easier to test and debug. Avoid code duplication,
which makes it tedious to inspect and maintain your code when changes are needed.

# Project 5 - Data Wrangling with JSON

The goal of the programming task is to define a class FluentRestaurants that supports the
fluent design pattern to filter the dataset. We can use this class to perform queries such as
“What vegan restaurants are in Wyoming?” Or “Which Mexican restaurants in NY are rated
below 2 stars?” The fluent design thus allows the queries to be chained in arbitrary orders, with
specified constraints, much like a user might wish to, on the Yelp website, to find specific
restaurants of interest. For example, here is how you would use the class FluentRestaurants
to run two queries:

let data = lib220.loadJSONFromURL('https://people.cs.umass.edu/~joydeepb/yelp.json');

let f = new FluentRestaurants(data);

f.ratingLeq(5)
 .ratingGeq(3)
 .category('Restaurants')
 .hasAmbience('casual')
 .fromState('NV')
 .bestPlace().name;
 
f.ratingLeq(4)
 .ratingGeq(2)
 .category('Restaurants')
 .hasAmbience('romantic')
 .fromState('AZ')
 .bestPlace().name;
 
The key idea is that you can compose these functions together to pose complex data queries. In
the above snippet, the first query determines the best “casual” restaurant in Nevada with at
least 3 stars and at most 5 stars. The second query determines the best “romantic” restaurant in
Arizona that has a rating of at least 2 stars and at most 4 stars. Although this is a dataset of
restaurants and businesses, you can assume all objects in the dataset are restaurants. As in a
real-life dataset, not all objects are complete; any of the properties (key-value pairs) in the type
description may be missing.
