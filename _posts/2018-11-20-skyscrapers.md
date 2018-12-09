---
title: "Skyscrapers"
date: 2018-11-20
tags: [algorithm]
header:
  image: "/images/skyscrapers.jpg"
excerpt: "Water collected on skyscrapers"
---

A couple of months ago I came across the following problem:

The Wall Street in New York is known for its breathtaking skyscrapers. But the raining season is approaching, and the amount of water that will fall over the buildings is going to be huge this year.
Since every building is stuck to the buildings to its left and to its right (except for the first and the last one), the water can leak from a building only if the height of the building is higher than the height of the building to its left or to its right (the height of the edges of Wall Street is 0).
All the buildings have the width of 1 meter. You are given the heights (in meters) of the buildings on Wall Street from left to right, and your task is to print to the standard output (stdout) the total amount of water (in cubic meters) held over the buildings on Wall Street.

Example input: heights: [9 8 7 8 9 5 6]  
Example output: 5

To better understand what we are being tasked with is useful to visualize it...

<img src="{{ site.url }}{{ site.baseurl }}/images/skywater.jpg" alt="">

So, below you can find the code and the respective comments that will compute a standard output for any given segment of buildings.

```r
#creation of a vector with the heights of the buildings
tower <- c(9,8,7,8,9,5,6)

#function created to return the volume of water collected after raining, given the height of each building
stdout <- function(tower) {
 left_peak <- vector(mode = "numeric")
 right_peak <- vector(mode = "numeric")
 water_volume <- vector(mode = "numeric")

 #after the creation of the above empty vectors, the following line of code will return a vector with the height of the highest building on the left hand side of each position (starting with a 0)   
 for (n in 1:length(tower)) {
   if (n == 1) {
     left_peak[n] = 0
   } else {left_peak[n] = max(tower[1:(n-1)])
   }}

 #below, the code will return a vector with the height of the highest building on the right hand side of each position (starting with a 0)   
 for (n in length(tower):1) {
   if (n == length(tower)) {
     right_peak[length(tower)] = 0
   } else {right_peak[n] = max(tower[length(tower):(n+1)])
   }}

 #now, to calculate the volume of water we need to take the minimum peak between the left and right hand sides and subtract the tower height at each position. If the tower height is higher than the minimum peak, then no water will be collected.
 for (n in 1:length(tower)) {
   water_volume[n] = max(min(left_peak[n], right_peak[n]) - tower[n], 0)
 }

 #aftwerwards we just need to sum the volume of water accumulated at the top of each building
 return(sum(water_volume))
}

stdout(tower)
```

For further details, you can take a look at this Google Tech Talk by Guy Steele - [Four Solutions to a Trivial Problem](https://youtu.be/ftcIcn8AmSY?t=536).
