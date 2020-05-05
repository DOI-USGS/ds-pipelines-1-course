We're going to combine several things into this assignment. You'll be asked to make some modifications to your training repository and also to create a pull request that captures these changes. 

#### background

We use team conventions for how our pipelines are organized, which make it easier to hop in and out of collaborative projects and to rapidly understand what is going on where. 

We refer to major elements of a pipeline as "phases", such as `1_fetch` or `2_process`. These phases are used to separate files and data based on the _intent_ of the code we are writing, and make it tractable to figure out where you'd need to edit code if you were coming in fresh to the project

For medium to large pipelines projects, you'll see these workflow phases explicitly named by a number often followed by a verb (separated by an underscore). We use these phases to create different folders :file_folder: for data and code, and also to specify how we orchestrate the running of code (more on that later...)

So, if we have a `1_fetch` phase, code in this folder :file_folder: would be used to get data from web services, google drive, an FTP, or to scrape a website. `2_process` (or `2_munge`) might contain code that transforms the "fetched" data into more usable formats. 

We recommend having a `src` and `out` folders within each phase that contain code _for_ this phase and data (or other files) produced _by_ this phase, respectively. You'll also see other folders :file_folder: for `in`, `log`, and `tmp` to represent manually added files, logged/diagnostic output, or intermediate output locations. 


### :keyboard: Activity: restructure your code repository to follow our team's best practices for folders and files

Create a two phase directory structure for "fetch" and "process" concepts, and include `src` and `out` folders. Move your example script into the `src` folder and delete any existing folders that aren't part of the intended structure [modify .gitignore to skip data files and/or the whole out directory] 

Git challenge: commit an empty directory (out). Make them google this 

_You can follow the manual steps below, or accept the suggestions in the following comments._

1. Edit your [workflow file]({{ fileUrl }})
1. Configure the `test` job to run only after the `build` job is completed (we'll use ellipses `...` to only show the parts of the workflow we're interested in, but you should not copy the ellipses directly):
    ```yaml
      test:
        needs: build
        runs-on: ubuntu-latest
        ...
    ```
1. Add a step to your `test` job that uses the `download-artifacts` action.
    ```yaml
      test:
        needs: build
        runs-on: ubuntu-latest
        ...
        steps:
        - uses: actions/checkout@v1
        - uses: actions/download-artifact@master
          with: 
            name: webpack artifacts
            path: public
        - name: Use Node.js {% raw %}${{ matrix.node-version }}{% endraw %}
          uses: actions/setup-node@v1
          with:
            node-version: {% raw %}${{ matrix.node-version }}{% endraw %}
        - name: npm install, and test
          run: |
            npm install
            npm test
          env:
            CI: true
    ```
    
I'll respond when you've edited your workflow file. 