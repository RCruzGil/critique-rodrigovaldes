Assigment 1
================
Rodrigo Valdes Ortiz
4/9/2018

``` r
# install.packages("cowplot")
# install.packages("ggpubr")
library(data.table)
```

    ## Warning: package 'data.table' was built under R version 3.3.2

``` r
library(ggplot2)
```

    ## Warning: package 'ggplot2' was built under R version 3.3.2

``` r
library(ggpubr)
```

    ## Warning: package 'ggpubr' was built under R version 3.3.2

    ## Loading required package: magrittr

Critique
========

Is it truthful?
---------------

The graph gives the idea that, in general, life expectancy has increased in the last 50 years. Also, the fertility rate has decreased in the last 50 years. However, it might imply causality to certain people. For instance, does fertility rate affect life expectancy? Which is the direction of the causality (if it exists)?

Despite that, an educated eye will not think about causality.

Is it functional?
-----------------

Yes. It shows the positive trends in the evolutions of human societies.

Is it beautiful?
----------------

The graph is not very beautiful. However, it is not ugly. I would have preferred not using lines on the edge of the graphs. Also, the green color might not be the best combination for the other colors. For instance, certain tones of yellow might have matched better with the other color in the graph.

Is it insightful?
-----------------

Yes. However, the size of the circles may confuse the reader. If the author would like to be clearer, she could have used labels indicating the meaning of the size of the circles. For example, the size of the circles can be population, per capita GDP, education, or other indicators. Then, avoiding this information in the graph is a crucial mistake.

Is it enlightening?
-------------------

Yes. The graph contributes to realize about trends in the data that might not be evident just looking at the raw data.

Own graph
=========

``` r
# Load the data
ArtCites = fread("ArtCites.txt")
ArtCites$cites = ArtCites$cites / 1000000
ArtCites$art = ArtCites$art / 1000000
ArtCites$MeanArt = mean(ArtCites$change_cites, na.rm=TRUE)
```

``` r
# Generate the plot
cites_graph = ggplot(ArtCites, aes(x=year))  + 
    geom_bar(aes(y=cites), stat="identity", fill="steelblue4", colour="steelblue4") +
    labs(title="Evolution of Academic Citations", y = "Citations (millions)", x = " ", colour = "Variables") +
    scale_x_continuous(breaks=c(1985, 1990, 1995, 2000, 2005, 2010, 2015)) +
    theme(plot.title = element_text(hjust = 0.5))

change_graph = ggplot(ArtCites, aes(x=year))  + 
    geom_line(aes(y=change_cites, color="indianred4")) +
    geom_line(aes(y=MeanArt, color="navyblue")) +
    labs(y = "% Change Citations", x = "Year") +
    scale_y_continuous(breaks=c(-2,0,2,4,6,8,10)) +
    scale_x_continuous(breaks=c(1985, 1990, 1995, 2000, 2005, 2010, 2015)) +
    scale_color_discrete(name = "Change", labels = c("Anual", "Mean 1985 - 2014")) +
    theme(legend.position = c(0.8, 0.25), 
          legend.title = element_text(colour="black", size=8, face="bold"), 
          legend.text = element_text(colour="black", size=7.5))
  
ggarrange(cites_graph, change_graph,
          ncol = 1, nrow = 2)
```

    ## Warning: Removed 1 rows containing missing values (geom_path).

![](Assigment1_files/figure-markdown_github/unnamed-chunk-3-1.png)

Story
-----

The number of citations has increased considerably in the last thirty years. However, the growth has not been constant. For instance, there are years where the number of citations has decreased and years where the number of citations has increased more than ten percent. Finally, on average, the number of citations has increased about 6% in the time span. Another final remark is that the number of citations per year has increased about five times since 1985.

Why this form
-------------

I decided to use two stacked graphs. First, the bar graph depicts the increasing number of citations. Second, the line graph shows the percentual change and the mean percentual change. Then, the combination of both graphs gives the perception of 1) the total numbers of citations and its evolution, 2) the percentual change year by year.

Channels to encode data
-----------------------

I used colors that create harmony in the graph. The blues and reds are appealing to the reader. Also, those create a slight contrast between the graph one and the graph two. I utilized a bar graph to show levels, and a line graph to show changes. According to my perception, using a bar graph and a line graph emphasizes that the first graph depicts levels and the second graph changes.

The graphs are stacked to facilitate the comparison between the two pieces of information, the levels, and the changes.

The scale in the first graphs is millions because it helps readers to read the graphs without reading many zeros or scientific notation.

Transformations
---------------

I added the percentual change in the second graph to avoid to show nuances in the data. For instance, a quick view of the first graph might say that the number of citations growths steadily. Without a transformation to show percentual changes, the reader can not understand details in the data, such as years with negative growth or years with extraordinary growth.

Facilitate communication
------------------------

The colors invite the reader to pay attention to the graphs. Also, I preserve only the necessary information to facilitate the interpretation of the graph. Then, any people with basic training on statistics can make a meaningful interpretation of the content.
