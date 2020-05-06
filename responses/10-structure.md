# Organizing projects

You should organize your code into functions, targets, and conceptual "phases" of work. 

Often we create temporary code or are sent scripts that look like the following:

**replace with real example from templace repo?**
```r

library(dplyr)
library(readr)
library(sbtools)

project_output_dir <- 'C:\Users\me\my_dir'

mendota_file <- file.path(project_output_dir, 'model_RMSEs.csv')
item_file_download('5d925066e4b0c4f70d0d0599', names = 'me_RMSE.csv', destinations = mendota_file, overwrite_file = TRUE)

eval_data <- readr::read_csv(mendota_file, col_types = 'iccd') %>%
  filter(str_detect(exper_id, 'similar_[0-9]+')) %>%
  mutate(col = case_when(
    model_type == 'pb' ~ '#1b9e77',
    model_type == 'dl' ~'#d95f02',
    model_type == 'pgdl' ~ '#7570b3'
  ), pch = case_when(
    model_type == 'pb' ~ 21,
    model_type == 'dl' ~ 22,
    model_type == 'pgdl' ~ 23
  ), n_prof = as.numeric(str_extract(exper_id, '[0-9]+')))



png(file = '~/Downloads/figure_1.png'), width = 8, height = 10, res = 200, units = 'in')
par(omi = c(0,0,0.05,0.05), mai = c(1,1,0,0), las = 1, mgp = c(2,.5,0), cex = 1.5)

plot(NA, NA, xlim = c(2, 1000), ylim = c(4.7, 0.75),
     ylab = "Test RMSE (°C)", xlab = "Training temperature profiles (#)", log = 'x', axes = FALSE)

n_profs <- c(2, 10, 50, 100, 500, 980)

axis(1, at = c(-100, n_profs, 1e10), labels = c("", n_profs, ""), tck = -0.01)
axis(2, at = seq(0,10), las = 1, tck = -0.01)

# slight horizontal offsets so the markers don't overlap:
offsets <- data.frame(pgdl = c(0.15, 0.5, 3, 7, 20, 30)) %>%
  mutate(dl = -pgdl, pb = 0, n_prof = n_profs)


for (mod in c('pb','dl','pgdl')){
  mod_data <- filter(eval_data, model_type == mod)
  mod_profiles <- unique(mod_data$n_prof)
  for (mod_profile in mod_profiles){
    ._d <- filter(mod_data, n_prof == mod_profile) %>% summarize(y0 = min(rmse), y1 = max(rmse), col = unique(col))
    x_pos <- offsets %>% filter(n_prof == mod_profile) %>% pull(!!mod) + mod_profile
    lines(c(x_pos, x_pos), c(._d$y0, ._d$y1), col = ._d$col, lwd = 2.5)
  }
  ._d <- group_by(mod_data, n_prof) %>% summarize(y = mean(rmse), col = unique(col), pch = unique(pch)) %>%
    rename(x = n_prof) %>% arrange(x)
  
  lines(._d$x + tail(offsets[[mod]], nrow(._d)), ._d$y, col = ._d$col[1], lty = 'dashed')
  points(._d$x + tail(offsets[[mod]], nrow(._d)), ._d$y, pch = ._d$pch[1], col = ._d$col[1], bg = 'white', lwd = 2.5, cex = 1.5)
  
}

points(2.2, 0.79, col = '#7570b3', pch = 23, bg = 'white', lwd = 2.5, cex = 1.5)
text(2.3, 0.80, 'Process-Guided Deep Learning', pos = 4, cex = 1.1)

points(2.2, 0.94, col = '#d95f02', pch = 22, bg = 'white', lwd = 2.5, cex = 1.5)
text(2.3, 0.95, 'Deep Learning', pos = 4, cex = 1.1)

points(2.2, 1.09, col = '#1b9e77', pch = 21, bg = 'white', lwd = 2.5, cex = 1.5)
text(2.3, 1.1, 'Process-Based', pos = 4, cex = 1.1)

dev.off()
```

This code has some major issues, including that it uses a directory that is specific to a user, it plots to a non-project file location, and the 
structure of the code makes it hard to figure out what is happening. This simple example is a starting point for understanding the investments we make
to move towards code that is more reproducible, more shareable, and understandable. Additionally, we want to structure our code and our projects 
in a way where we can build on top of them as the projects progress. 


Assign this issue to yourself and then we'll get started on code and project structures

<hr>
<h3 align="center">I'll sit patiently until you've assigned yourself to this one.</h3>
