We're going to combine several things into this assignment. You'll be asked to make some modifications to your training repository and also to create a [pull request](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) that captures these changes. 

#### background

We use team conventions for how our pipelines are organized, which make it easier to hop in and out of collaborative projects and to rapidly understand what is going on where. 

We refer to major elements of a pipeline as "phases", and name phases according to their purpose, such as `1_fetch` or `2_process`. These phases are used to separate files and data based on the _intent_ of the code we are writing, and make it tractable to figure out where you'd need to edit code if you were coming in fresh to the project

For medium to large pipelines projects, you'll see these workflow phases explicitly named by a number often followed by a verb (separated by an underscore). We use these phases to create different folders :file_folder: for data and code, and also to specify how we orchestrate the running of code (more on that later...)

So, if we have a `1_fetch` phase, code in the fetch folder :file_folder: would be used to do things like get data from web services, google drive, an FTP, or to scrape a website. `2_process` (or `2_munge`) might contain code that transforms the "fetched" data into more usable formats. 

We recommend having `src` and `out` folders within each phase that contain code _for_ this phase (`src`) and data (or other files) produced _by_ this phase (`out`). When seeing some of our existing pipelines in action, you will also see other folders :file_folder: for `in`, `log`, and `tmp` to represent manually added files, logged/diagnostic output, or intermediate output locations. 


### :keyboard: Activity: restructure your code repository to follow our team's best practices for folders and files

Create a two phase directory structure for "fetch" and "process" concepts, and include `src` and `out` folders. Move your example script into one of the `src` folders (at this time, it doesn't matter which one you choose) and delete any existing folders that aren't part of the intended structure.

When you are done, open a [pull request]({{ repoUrl }}/pulls) with the changes.
