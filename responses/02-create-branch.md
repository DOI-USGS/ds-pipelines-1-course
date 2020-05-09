
first things first you are going to need to clone this training repository to your local machine, so that you can make file changes and commits there. 

Starting in the directory you work in for projects in R (for me, this is `Documents/R`), clone the repository and set your working directory to the new project folder that was created:
```
git clone git@github.com:{{ user.username }}/{{ repo }}.git
cd ds-pipelines-1
```

Now we'll need you create a local branch and push that branch up to the "remote" location (which is the github host of your repository). We're having you create a "structure" (representing concepts in this section of the lab) branch, but in the future you'll probably choose branch names according to the type of work they contain. 

```
git checkout -b structure
git push -u origin structure
```

By using `checkout`, you have switched your local branch from `master` to `structure`, and any changes you make from here on out to _tracked_ files will not show up on the master branch. To take a look back at master, you can always use `git checkout master` and return to structure with `git checkout structure`. We needed the `-b` flag initially because we wanted to combine two operations - creating a new branch and switching to that new branch. 

While you are at it, this is a good time to invite a few collaborators to your repository, which will make it easier to assign them as reviewers in the future. In the :gear: Settings widget at the top of [your repo]({{ repoUrl }}), select "Manage access". Go ahead and invite your cohort coworkers, aappling-usgs, and jread-usgs. It should look something like this: 
![add some friends](https://user-images.githubusercontent.com/2349007/81471981-c0094900-91ba-11ea-93b0-0ffd31ec4ea9.png)

<hr>
<h3 align="center">Close this issue when you've successfully pushed your branch to remote and added some collaborators.</h3>

