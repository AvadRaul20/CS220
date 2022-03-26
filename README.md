# CS220

# Project 1 - Image Processing
The goal of this assignment is to introduce you to the basic features of JavaScript, such as functions,
variables, conditionals, and loops. You should already be familiar with these concepts from other
programming languages (e.g., Java). You will use these features to write several image processing functions
(e.g., blur, sharpen, and adjust brightness). Project also showcases testing methodology for images after 
processing. 

# Project 2 - Higher Order Functions and Image Processing


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
let data =
 lib220.loadJSONFromURL('https://people.cs.umass.edu/~joydeepb/yelp.json');
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
