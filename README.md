# Data Project Society Logo

Hi there! For my first GitHub project I wanted to explore my interest in RStudio visualization. Therefore, this repository will describe my process in brainstorming ideas and generating a RStudio heat map for the Data Project Society's (DPS) logo.

With the help of a Data Science Professor and fellow students, we are creating the Data Project Society this year as a non-intimidating community for anyone interested in exploring Data Science. I thought that this would be a good introduction into visualization and help develop my technical expertise, which is essential for guiding others next year.


## Table of Contents <img src="https://github.com/krisdev-h/data-project-society-logo/blob/eb085a79c0a64415400f3520168e3ad56f4b4642/extraneous%20image%201.png" width="60" height="60">


- Brainstorming
- Implementation
- Refining
- End Product


### Brainstorming
Looking into RStudio visualizations, I decided that a heat map would be suitable as a visually appealing and unique method to construct DPS's logo. Not only is RStudio a staple program that we will utilize throughout the year, but this could be a good introductory exercise in developing models within the program. 

<pre>
<b>Heatmaps</b>: Represented as a heatmap() function in RStudio, heatmaps are graphical representations of data that use 
colors to visualize the values of the given matrix
- brighter colors represent common values/higher activity
- darker colors represent less common values/less activity
- dendograms: along the side of the heatmap, show how variables and rows are independently clustered
- heatmaps show data values for each row and column (possibly standardized into the same range)
- patterns in heatmaps can indicate an association between rows and columns
- you can modify and create patterns in a heatmap by clustering
- a rectangular area of around the same colors in a heatmap suggests that a group of rows are 
  correlated for the corresponding group of columns
</pre>

<pre>
<b>Examples of heatmaps</b>: 
1. <ins>FROM A RANDOM DATASET</ins>
   
   <a href="https://www.geeksforgeeks.org/create-a-heatmap-in-r-programming-heatmap-function/">source<a>
   
   set.seed(110) #a pseudorandom number generator, in this case 110 numbers
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
   
2. <ins>FROM THE MTCARS DATASET</ins>

   <a href="https://r-graph-gallery.com/215-the-heatmap-function.html">source<a>

   - as.matrix() converts a data frame into a matrix, which is required as input for heatmap()
   - t(data) transposes the matrix by switching the X and Y axis
   - column is variable, observation is row, square is value
   
   data <- as.matrix(mtcars) #converting mtcars dataset into a matrix
   heatmap(data) #generating a default heatmap
   
   <img src="https://github.com/krisdev-h/data-project-society-logo/blob/9957825d6c12f38aa67ed67032f5362eeb5f8995/Ex%202%20heatmap%20%231.png" width="250" height="250"> * variation is absorbed by hp and disp variables which have high values
   
   - therefore we need to normalize the matrix: scaling either the row or column within the heatmap function
   
   heatmap(data, scale="column") #want to absorb variation through column
   
   - heatmap() automatically:
        * reorders variables and observations through a clustering algorithm: ordering the distance between each pair
          of rows and columns by similarities
        * maps corresponding dendogram lines: diagrams that show the hierarchical relationship between objects
   - use Rowv and Colv to visualize the raw matrix without reordering or dendogram
   
   heatmap(data, Rowv = NA, Colv = NA, scale="column")
   
   <img src="https://github.com/krisdev-h/data-project-society-logo/blob/7c869b1add5b35190b78a6781bfe308b07fe37c6/Ex%202%20heatmap%20%233.png" width="230" height="230">
   
  - customizing the color palette
       * R palettes: terrain.color(n colors), rainbow(n colors), heat.colors(n colors), 
                     topo.colors(n colors), cm.colors(n colors)
       -> heatmap(data, scale="column", col = cm.colors(256))
       -> heatmap(data, scale="column", col = terrain.colors(256))
       * RColorBrewer: 1. sequential palettes: progress from low (light colors) to high (dark colors) 
                          <img src="https://github.com/krisdev-h/data-project-society-logo/blob/1e2901e6082cdbad9d4808177ce2ff0b02c8a448/Ex%202%20heatmap%20%234.png" width="250" height="160">
                       2. diverging palettes: put equal emphasis on mid-range and extreme values at both ends 
                       of the data range, middle break in legend is light colors, low and high extremes is dark colors 
                       with contrasting hues 
                          <img src="https://github.com/krisdev-h/data-project-society-logo/blob/7bf06c71c95cad17245fe531f758cd7a840fee45/Ex%202%20heatmap%20%235.png" width="280" height="80">
                       3. qualitative palettes: uses hues for primary differences in nominal or
                       categorical data, don't imply differences between legend classes
                          <img src="https://github.com/krisdev-h/data-project-society-logo/blob/1e2901e6082cdbad9d4808177ce2ff0b02c8a448/Ex%202%20heatmap%20%236.png" width="250" height="80">
       -> install.packages("RColorBrewer")
       -> library(RColorBrewer)
       
       -> display.brewer.all() #displaying color schemes
       -> heatmap(data, col=brewer.pal(9, "Blues")) #unpreserved column order
       -> heatmap(data, Colv=NA, col=brewer.pal(9, "Blues")) #preserved column order
       
       <i>OR</i>
       
       -> coul <- colorRampPalette(brewer.pal(8, "PiYG"))(25)
       -> heatmap(data, scale="column", col = coul)
       
  - other features
  heatmap(data, Colv = NA, Rowv = NA, scale="column", col = coul, xlab="variable", ylab="car", main="heatmap") #custom main and axis titles
  heatmap(data, scale="column", cexRow=1.5, labRow=paste("new_", rownames(data),sep=""), col= colorRampPalette(brewer.pal(8, "Blues"))(25)) #adding new_ to y labels
</pre>


### Implementation
First, I created a 10 column by 9 row excel table as values for our heatmap to visualize. I initially tried logging the highest valued digits in a "D", "P", or "S" shape throughout the table, with the lowest values contrasting in areas outside of the letters. Then I opened and attached the file to the program.

<img src="https://github.com/krisdev-h/data-project-society-logo/blob/1caa192f29b6e984c67b55469df8958c9ec9b9f2/Implementation%20Step%201%20excel.jpg" width="500" height="130">

After coding a color palette of blue, gold, and white I called it as the color of the heatmap and saw what was generated. As you can see there is a slight letter "D" that appears in dark blue (less common values) but the "P" and "S" are indistinguishable within the heatmap. There is a dendogram that is visible and axis titles and a heatmap title can be added.

<img src="https://github.com/krisdev-h/data-project-society-logo/blob/015c34ca84b63946dc6aa115a4cd6765f4e297b7/Implementation%20Step%201%20overview.jpg" width="800" height="400">


### Refining
In order to refine my model I wanted to add axis and a main heatmap title to the visualization, remove the dendogram, extend the "D" letter towards the bottom of the heatmap, and make sure that darker values/less common values are represented where "P" and "S" are supposed to be visible in the heatmap. 

<img src="https://github.com/krisdev-h/data-project-society-logo/blob/030f3076b03f93194e0a3b9ca5e4a14f3bdcc3f8/Refining%20Step%201%20Overview.jpg" width="700" height="400">

Here I noticed a yellow value that stuck out towards the left side of the "D" letter, and made corresponding row 7 and column 3 more similar to make sure that value was made darker. I continued this process to try and make the other letters appear. 
