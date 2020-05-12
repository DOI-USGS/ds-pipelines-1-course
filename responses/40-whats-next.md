You are doing a great job, @{{ user.username }}! :star2: :collision: :tropical_fish:

But you may be asking why we asked you to go through all of the hard work of connecting functions, files, and targets together using a yaml file. We don't blame you for wondering...

---

The real power of depedency management is when something changes - that's the EUREKA! moment, but we haven't put you in a situation where it would show up. That will come further down the road on later training activities and also in the project work you will be exposed to. 

In the meantime, here are a few nice tricks given you have a functional pipeline. 

- [ ] run `scmake()` again. What happens? Hopefully not much. I see this: 
![make all is fresh](https://user-images.githubusercontent.com/2349007/81510652-0ead0500-92d9-11ea-8e16-280f2051e709.png)
Which means everthing is up to date so all targets are :OK:

- [ ] access the `processed` target by using `processed_data <- scmake('processed')`. Here we are using the first argument of `make()`, which is `target_names`. Any vector of targets used will be build (default is to build the `all` target in the case where no target names were specified). We can access the output of the target by assigning the result to a variable. Here we have called that variable `processed_data`, and it looks like a data.frame. If you assign the result of a file target, like `file_name <- scmake(target_names = 'model_RMSEs.csv')`, the result is the path to that file. 

- [ ] now try making a change to one of your functions in your code. What happens after running `scmake()` then? 

--- 

Lastly, imagine the following comment appeared on your pull request. 
> Oh shoot @{{ user.username }}, I am using your results for **FANCY BIG PROJECT** and I have coded everything to assume your outputs use a character for the experiment number (the `exper_n` column), of the form "01", "02", etc. It looks like you are using numbers. Can you update your code accordingly? 

Would your code be easy to adjust to satisfy this request? Would you need to re-run any steps that aren't associated with this naming choice? Did the use of a dependency management solution allow you to both make the change efficiently (i.e., by avoiding rebuilding any unnecessary parts of the pipeline) and increase your confidence in delivering the results?

---

### You have completed introductions to pipelines I. Great work!
