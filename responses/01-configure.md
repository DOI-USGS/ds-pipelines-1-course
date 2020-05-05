

### :keyboard: Installing tools

To complete this section, you'll need some R packages. You will need to install `remake`, `scipiper`, and `drake`. 

`drake` is available through CRAN, but `remake` and `scipiper` both require installation from github. 

`scipiper` depends on `remake`, so install `remake` and its dependencies first:

```r
install.packages(c("R6", "yaml", "digest", "crayon", "optparse", "storr", "remotes"))
remotes::install_github('richfitz/remake')
```

Next, install `scipiper`
```r
remotes::install_github('usgs-r/scipiper')
```

when you are complete, comment with the message that appears after you run `library(scipiper)`


<hr><h3 align="center">I'll respond when I detect you've commented to this issue.</h3>



Close this issue when you're done and go back to the [Issues]({{ repoUrl }}/issues) page for the next topic.
  
