# Organizing projects

You should organize your code into functions, targets, and conceptual "phases" of work. 

Often we create temporary code or are sent scripts that look like the following:

**replace with real example from templace repo?**
```r
library(dplyr)
library(scipiper)
library(sf)
library(sp)

all_lakes <- readRDS('C:\Users\me_mine\projects\lakes\canonical_lakes_sf.rds') %>% 
  st_transform(crs = "+init=epsg:2811")

# simplify lakes to speed up the plot
all_lakes_simple <- sf::st_simplify(all_lakes, dTolerance = 40) %>% mutate(area = st_area(Shape) %>% as.numeric) #%>%
  #filter(area < 11196632079)

setwd('..\low-flows')
conus_states <- readRDS('conus_states.rds')

png(filename = 'C:\Users\me_mine\Downloads\navico_update_2020-05-04.png', width = 6, height = 6, units = 'in', res = 550)
par(omi = c(0,0,0,0), mai = c(0,0,0,0), xaxs = 'i', yaxs = 'i')

plot(conus_states[names(conus_states) %in% c('minnesota','wisconsin','michigan','indiana')], col = NA, border = 'grey50', lwd = 1.5,
     reset = FALSE, expandBB = c(0.01,0.2,0.01,0.05))

plot(st_geometry(all_lakes_simple), col = 'grey70', border = 'grey70', lwd = 0.1, add = TRUE)
plot(conus_states, col = NA, border = 'grey50', lwd = 1.5, add = TRUE)

dev.off()
```

This code has some major issues, including that it uses a directory that is specific to a user, it plots to a non-project file location, and the 
structure of the code makes it hard to figure out what is happening. This simple example is a starting point for understanding the investments we make
to move towards code that is more reproducible, more shareable, and understandable. Additionally, we want to structure our code and our projects 
in a way where we can build on top of them as the projects progress. 


Assign this issue to yourself and we'll get started on code and project structures

<hr>
<h3 align="center">I'll sit patiently until you've assigned yourself to this one.</h3>
