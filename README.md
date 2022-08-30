# Data Project Society Logo

Hi there! For my first GitHub project I wanted to explore my interest in RStudio visualization. Therefore, this repository will describe my process in brainstorming ideas and generating a RStudio heat map for the Data Project Society's (DPS) logo.

With the help of a Data Science Professor and fellow students, we are creating the Data Project Society this year as a non-intimidating community for anyone interested in exploring Data Science. I thought that this would be a good introduction into visualization and help develop my technical expertise, which is essential for guiding others next year.


## Table of Contents <img src="https://github.com/krisdev-h/data-project-society-logo/blob/eb085a79c0a64415400f3520168e3ad56f4b4642/extraneous%20image%201.png" width="60" height="60">


* Brainstorming
* Implementation
* Refining
* End Product


### Brainstorming
Looking into RStudio visualizations, I decided that a heat map would be suitable as a visually appealing and unique method to construct DPS's logo. Not only is RStudio a staple program that we will utilize throughout the year, but this could be a good introductory exercise in developing models within the program. 

<pre>
<b>Heatmaps</b>: Represented as a heatmap() function in RStudio, heatmaps are graphical representations of data that use 
colors to visualize the values of the given matrix
* brighter colors represent common values/higher activity
* darker colors represent less common values/less activity
</pre>

<pre>
<b>Examples of heatmaps</b>: 
1. set.seed(110) #a pseudorandom number generator, in this case 110 numbers
   data <- matrix(rnorm(100, 0, 5), nrow = 10, ncol = 10) #data object with matrix assigned
   #100 represents n values in rnorm(n, mean, sd) which generates a vector of normally 
   distributed random numbers
   colnames(data) <- paste0("col", 1:10) #naming the 10 rows and 10 columns
   rownames(data) <- paste0("row", 1:10)
   
   heatmap(data) 
   
   <img src="https://github.com/krisdev-h/data-project-society-logo/blob/88041c7e68e82d95fcd10b755b82b4c91c881d02/Ex%201%20heatmap%20%231.png" width="250" height="250">
   
   <i>OR</i>
   
   my_colors <- colorRampPalette(c("cyan", "darkgreen")) #optional manual color change
   heatmap(data, col = my_colors(100)) 

   <img src="https://github.com/krisdev-h/data-project-society-logo/blob/260e5e5c65221a084276e1dd0e1bd1d424487f5d/Ex%201%20heatmap%20%232.png" width="250" height="250">
</pre>

### Implementation
