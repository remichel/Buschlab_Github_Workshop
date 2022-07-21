# Buschlab Github Workshop

### The Basics

##### Syncing between local copys and the Github server 
Whenever you initialize a repository on Github, it will live on the Github server. This server version is called the "remote" or "origin". If you want to have a local copy of your repo e.g. on your office computer or on the stimulation computer in the EEG lab, you can `clone` the repository to create such a copy. If you now commit some changes to this copy, you might want to sync such changes with the server version of your repository. This "syncing" is called a `push`. Reversely, when the server version might have new changes that aren't synced with your local copy yet, you update the local copy by a so-called `pull`.

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/basics1.png)

##### Version control

However, a github repo does not only allow for syncing between different copys of a project, but also a very sophisticated version control. This version control is achieved by logging every change that you perform in a repository. More specifically, it doesn't do that automatically, but you have to `commit` each chunk of changes that needs to be logged. By doing so, you will create a commit history of your project, which allows you to keep track of your changes and allows restoring of older versions. 

##### Branches

Another important feature is branching. By default, your project will only have a `main` or `master` branch. Normally, this branch of your project will store the last stable version. Whenever you want to work on a new feature of your project, it is best practice to leave the master branch untouched and create a separate branch of your project to develop this new feature. Switching between different branches can be done by a `checkout` of the respective branch. After checking out the "feature" branch and developing the new feature, you might arrive to the point in which you consider it ready to be added to the main branch. By performing a `merge` of the feature branch into the master branch, all the commits you have applied to the feature branch will then be incorporated in the master. 

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/basics2.png)

##### Cherry-picking

However, sometimes you might only want to merge a few selected changes from a branch into another branch. While a `merge` will always incorporate all changes into the target branch, the `cherry-pick` allows you to select only the desired changes and applies them to the target branch. Especially in our case in which we will most likely change a lot of aspects of the template EEG analysis pipeline, most of these changes will be project-specific, while only a few will be bug-fixes or general improvements that might be relevant to be merged into the template pipeline. Here, the cherry-pick command comes in very handy!


<p align="center">
  <img src="https://github.com/remichel/fork_it_like_its_hot/blob/master/cherrypick1.png"/>
</p>



##### Forking 

Another important feature of github is the `fork` (The concept behind forks, e.g. in contrast to clones, is well explained [here](https://www.youtube.com/watch?v=EAC6zUmgkgQ)). It allows you to create a copy of an existing repository hosted by another user. This `forked` repository will then be a stand-alone repo of yours, in which only you have writing access. Forking is benefitial for two reasons: First, it allows you to take another person's repo as a starting point for your own project, and it facilitates contributing to the original repository without having writing access to it (i.e. being a collaborator). For example, when you have forked a repo, committed some changes and you consider those changes to be relevant also to the so-called `upstream` repository (which is the original one), instead of directly pushing those changes, you can send a `pull-request` to the repo's owner. The owner can then decide whether or not to implement the suggested changes. On the other hand, if the there have been changes to the upstream repository (e.g. bug fixes), you can fetch those changes in the upstream repository and merge them into your forked repository.

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/fork1.png)

### The Buschlab Pipeline workflow

For the EEG pipeline scenario, the `buschlab-muenster` pipeline repository will be the upstream, while every lab member can create an own fork of this repository. Furthermore, directly after forking the repo, create a separate branch (e.g. called `pr` for pull-request). Then, you can checkout your master branch again and start working on your project while leaving the pr branch untouched. However, if you spot a relevant commit that might be a candidate for a pull-request for the upstream repo, cherry-pick this command and add it to the pr branch. Then send a pull-request to merge the pr branch into the upstream master, i.e. suggest adding your selected commit to the default EEG analysis pipeline.

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/fork3.png)

As long as you will have only a single project involving EEG preprocessing, this workflow will suffice to conveniently (1) use the default pipeline as a starting point, (2) easily fetch updates from the upstream, and (3) send pull-requests for e.g. bug-fixes or additional features. 

However, if you have more than a single project ongoing involving EEG, you will realize that Github does not allow for forking the same repository multiple times. Therefore, a slightly adjusted setup is required (see the Figure below): Instead of having a master branch (storing your project-specific preprocessing pipeline) and a pr branch (containing the upstream version of the pipeline AND your suggested changes to it), you will use the master branch as the exact copy of the upstream repository (i.e. it now has the role of the pr branch), and create a branch for every project you start (e.g. name the branches after your projects). This means that you will need to checkout and work in the project branches most of the times, while leaving the master branch untouched. Now, if you want to suggest any changes from one of your projects' code to the upstream repo, cherry-pick this commit and add it to your fork's master branch. Now, you can send a pull-request to merge your master into the upstream master. Vice versa, if there are any changes in the upstream, merge those into your master branch first, and then incorporate those changes also into your project branches if necessary. 

Once one of your projects is ready for submission/publication, you might want to share the code in a convenient way. One option to do so is a GitHub release of the respective project branch (you can find a description of a Github release [here](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)). Alternatively, you can of course also paste the final version of the project's code into a new stand-alone repository and refer to this new repo in your publication.


![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/workflow1.png)

# Recommended tools

### GitKraken

As working with different branches, forks and cherry-picks can be very complicated, it's highly recommended to make use of a sophisticated GUI that visualizes the commit history and all dependencies between branches and forks. A powerful tool for that is [GitKraken](https://www.gitkraken.com/). A Gitkraken workflow is well expained [here](https://www.youtube.com/watch?v=j_qpzND5yAg).

### Commandline workflow

For those of you who do not want to use a GUI and instead want to work in the commandline, the following steps will do the job of initializing your fork (the following steps were derived from [this tutorial video](https://www.youtube.com/watch?v=deEYHVpE1c8&t=480s))

1. fork a repository
2. clone the new, forked repository to your local computer `git clone [reponame]`
3. check your remotes with `git remote -v` (up to now, only origin should be listed)
4. add a new remote (convention is to call it "upstream") via `git remote add upstream [url of original repo]`
5. check if it was successful with `git remote -v` again
6. to get all updates from the original repo, type `git fetch upstream`
7. to incorporate the updates into your local branch, use `git merge upstream/[branchname] [branchname]` 
8. to checkout branches , you now need to specify whether you want to checkout the origin or upstream , e.g. `git checkout origin/[branchname]`
9. until now, you just updated your local branch with the updates from upstream. to update your remote origin, you need to `git push origin [branchname]`
