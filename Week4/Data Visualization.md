# World Airports Data Visualization - Assignment 4
## Data visualization in p5js 

### Code
https://editor.p5js.org/soumen02/full/bVxMgSUED

### Objective 

To visualize data (CSV/JSON) from the internet using p5js

### Process 

I have always been a fan of [DataIsBeautful - Reddit](https://www.reddit.com/r/dataisbeautiful/hot/) and its fascinating visualizations - especially the dynamic ones. For this reason I chose to work on a data visualization code (rather than text generation). Since it is one of my first visualizations, I chose to go for something simple - a csv file with coordinates I could plot. The best dataset I could find was flights.csv which consisted of rows of flight data - with their airports, countries, coordinates, ... After cleaning up the data and keeping the ones I felt were necessary, I loaded and plotted them on the canvas. 
The very first visual of the data looked too simple so I thought of adding some colours to it. If a flight entry was domestic, it was marked with a red circle, but if it was international it was marked with a blue circle.

### Challenges
The first challenge I faced was finding the data. Datasets I found on the internet were extremely compled and would require hours of cleaning if I chouse to visualize them, so find the right data - one which had less columns to take care of was important to me. This too had to be visualizable i.e. have coordinates I could plot. 

Another challenge I faced was with the mapping of distance. It took me some time to figure out how to use distance to add a kind of variation to the data plots. 

### Future Improvements

While cleaning the data, I made sure to leave behind data I didn't currently use, but could later develop upon - probably by making the visualization dynamic. I would want to implement a code where the user can place their mouse on a location and the code would draw lines from that airport to ever incoming or outgoing flights. 
