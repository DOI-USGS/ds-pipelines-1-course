
first things first you are going to need to clone this training repository to your local machine, so that you can make file changes and commits there. 

```
git clone git@github.com:jread-usgs/ds-pipelines-1.git
cd ds-pipelines-1
```

Now we'll need you create a local branch and push that branch up to the "remote" location (which is the github host of your repository). We're having you create a "dev" (for "development") branch, but in the future you'll probably choose branch names according to the type of work they contain. 

```
git checkout -b dev
git push -u origin dev
```

By using `checkout`, you have switched your local branch from `master` to `dev`, and any changes you make from here on out to _tracked_ files will not show up on the master branch. To take a look back at master, you can always use `git checkout master` and return to dev with `git checkout dev`. We needed the `-b` flag initially because we wanted to combine two operations - creating a new branch and switching to that new branch. 

Close this issue when you've successfully pushed your branch to remote. 
