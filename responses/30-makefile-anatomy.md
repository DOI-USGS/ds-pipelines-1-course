Most of our work to build pipelines in R include using a `remakefile` file to "orchestrate" the connections between different files, functions, and phases. In this issue, we're going work to develop a basic understanding of how these files work, but starting with the "anatomy of a remakefile".

#### background

A `remakefile` uses the [yaml file format](https://en.wikipedia.org/wiki/YAML). A basic understanding yaml is important for the `remakefiles`, but several of the tools and workflows common to USGS data science take advantage of a yaml file to do other things too, so you may bump into them elsewhere. A yaml ("YAML ain't markup language") is fairly simple, flexible, and readable but can have a bit of a learning curve to get used to. We're not going to get too far into yamls, but reading up on them or finding a good reference for future use might be a good idea.



In addition to phases, it is important to decompose high-level concepts (or existing scripts) into thoughtful functions and "targets" that form the building blocks of data processing pipelines. A target is a noun we use to describe a tangible output of function, often a file or an R object, that we can use as a terminal product (like a summary map) or as input into another function. 

Close this issue when you're ready for the next step.

The simplest type of remake file (adapted from the [`remake` repo](https://github.com/richfitz/remake))


```yaml
sources:
  - code.R

targets:
  all:
    depends: figure_1.png

  model_RMSEs.csv:
    command: download_data(target_name)

  processed:
    command: process_data("model_RMSEs.csv")

  figure_1.png:
    command: myplot(processed)
```


This file defines the relationships between different "targets" (see how `"model_RMSEs.csv"` is an input to the command that creates `processed`?), tells us where to find any functions that are used to build targets (see `code.R`), and isolates the output(s) that _must_ be created in order to complete the `all` target (in this case, it is only the `figure_1.png` file). 

Even though this is a simple 
