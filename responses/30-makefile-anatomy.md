Most of our work to build pipelines in R include using a `remakefile` file to "orchestrate" the connections between different files, functions, and phases. In this issue, we're going to develop a basic understanding of how these files work, by starting with the "anatomy of a remakefile".

#### background

A `remakefile` uses the [yaml file format](https://en.wikipedia.org/wiki/YAML). A basic understanding of yaml is important for making use of `remakefiles`, including creating your own or editing existing files. Additionally, several of the tools and workflows common to USGS data science take advantage of a yaml file to do other things too, so you may bump into them elsewhere. A yaml ("YAML ain't markup language") is fairly simple, flexible, and readable, but can have a bit of a learning curve to get used to. We're not going to get too far into yamls, but reading up on them or finding a good reference for future use might be a good idea.

#### using remakefiles in data science pipeline

In addition to phases (which we covered in {{ store.structure_activity_url }}), it is important to decompose high-level concepts (or existing scripts) into thoughtful functions and "targets" that form the building blocks of data processing pipelines. A target is a noun we use to describe a tangible output of function, which is often a file or an R object. Targets can be used as an end-product (like a summary map) or as input _into_ another function to create _another_ target. 

---
The simplest version of a `remakefile` (adapted from the [remake repo](https://github.com/richfitz/remake)) might look something like this:

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
    command: myplot(target_name, processed)
```


This file defines the relationships between different "targets" (see how "model_RMSEs.csv" is an input to the command that creates `processed`?), tells us where to find any functions that are used to build targets (see that "sources" points you to `code.R`), and isolates the output(s) that _must_ be created in order to complete the `all` target (in this case, it is only the "figure_1.png" file). 

Even though this is a simple example, there is some new syntax that may be confusing. We'll explain a few of these quickly:
 - `target_name` is a special variable name in a `remakefile` that is equivalent to saying, "hey, see the name of the target I am creating? Use that for this input!". So `download_data(target_name)` is really calling `download_data("model_RMSEs.csv")`
 - `command` is a field that specifies what _function_ should be called in order to build the target
 - `depends` is a field that explicity specifies a _dependency_ of a target. So when that dependency is considered "out of date" (more on that later), the target that lists that dependency in `depends` is also going to be "out of date". In this way, the "all" target isn't complete and up-to-date until `figure_1.png` is
 - `all` is a special target that groups other targets. Again, we'll cover group targets - like `all` - more later on.

---

We're going to start with this simple example, and modify it to match our pipeline structure. This will start by creating a new branch, creating a new file, adding that file to git tracking, and opening a new pull request that includes the file:

### :keyboard: Activity: get your code plugged into a remake file

First things first, we're going to want a new branch. You can delete your previous one, since that pull request was merged. 
```
git checkout master
git pull
git branch -d structure
git checkout -b remakefile
git push -u origin remakefile 
```
---
Next, create the file with the contents we've given you by entering the following from your repo directory in terminal/command line:
```
cat > remake.yml
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
    command: myplot(target_name, processed)
```    
then use `Ctrl+D` to exit the file creation mode and return to the prompt. 
---
Finally, create a [pull request]({{ repoUrl }}/pulls) that includes this new file (should be called `remake.yml`)


--- 
# THIS STUFF IS FOR LATER
So, what does this do for you? Well, if you had this `remake.yml` file in your current working directory, and the `download_data()`, `process_data()`, and `myplot()` functions were in `code.R` (which you don't), it would look like this when you run `make` from the `remake` package

![remake run image](https://user-images.githubusercontent.com/2349007/81447341-15edda80-9142-11ea-8321-c490cb6cb9ef.png)


---
Now, building on your existing folders, functions, and code from the previous sections, write a remake file that builds _your_ `figure_1.png` with `remake::make()` and create a [pull request]({{ repoUrl }}/pulls) with your changes. Comment in the pull request with a screenshot of the build message, like we have in the message above :point_up:


Oh neat, some formatting? You'll see that the real power of dependency management comes later...when we make mistakes or changes. 




