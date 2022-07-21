# Buschlab Github Workshop

### The Basics

Whenever you initialize a repository on Github, it will live on the Github server. This server version is called the "remote" or "origin". If you want to have a local copy of your repo e.g. on your office computer or on the stimulation computer in the EEG lab, you can `clone` the repository to create such a copy. If you now commit some changes to this copy, you might want to sync such changes with the server version of your repository. This "syncing" is called a `push`. Reversely, when the server version might have new changes that aren't synced with your local copy yet, you update the local copy by a so-called `pull`.

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/basics1.png)

However, a github repo does not only allow for syncing between different copys of a project, but also a very sophisticated version control. This version control is achieved by logging every change that you perform in a repository. More specifically, it doesn't do that automatically, but you have to `commit` each chunk of changes that needs to be logged. By doing so, you will create a commit history of your project, which allows you to keep track of your changes and allows restoring of older versions. 

Another important feature is branching. By default, your project will only have a `main` or `master` branch. Normally, this branch of your project will store the last stable version. Whenever you want to work on a new feature of your project, it is best practice to leave the master branch untouched and create a separate branch of your project to develop this new feature. Switching between different branches can be done by a `checkout` of the respective branch. After checking out the "feature" branch and developing the new feature, you might arrive to the point in which you consider it ready to be added to the main branch. By performing a `merge` of the feature branch into the master branch, all the commits you have applied to the feature branch will then be incorporated in the master. 

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/basics2.png)

However, sometimes you might only want to merge a few selected changes from a branch into another branch. While a `merge` will always incorporate all changes into the target branch, the `cherry-pick` allows you to select only the desired changes and applies them to the target branch. Especially in our case in which we will most likely change a lot of aspects of the template EEG analysis pipeline, most of these changes will be project-specific, while only a few will be bug-fixes or general improvements that might be relevant to be merged into the template pipeline. Here, the cherry-pick command comes in very handy!

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/cherrypick1.png)

Another important feature of github is the `fork`. It allows you to create a copy of an existing repository hosted by another user. This `forked` repository will then be a stand-alone repo of yours, in which only you have writing access. Forking is benefitial for two reasons: First, it allows you to take another person's repo as a starting point for your own project, and it facilitates contributing to the original repository without having writing access to it (i.e. being a collaborator). For example, when you have forked a repo, committed some changes and you consider those changes to be relevant also to the so-called `upstream` repository (which is the original one), instead of directly pushing those changes, you can send a `pull-request` to the repo's owner. The owner can then decide whether or not to implement the suggested changes. For the EEG pipeline scenario, the `buschlab-muenster` pipeline repository will be the upstream, while every lab member can create an own fork of this repository. 

![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/fork1.png)
![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/fork2.png)
![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/fork3.png)
![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/workflow1.png)
### What is a fork?

- The concept behind forks (in contrast to clones) is well explained [here](https://www.youtube.com/watch?v=EAC6zUmgkgQ)

### GitKraken workflow

- you can download Gitkraken [here](https://www.gitkraken.com/)
- A Gitkraken workflow is well expained [here](https://www.youtube.com/watch?v=j_qpzND5yAg)

### Commandline workflow

For those of you who do not want to use a GUI and instead want to work in the commandline, the following steps will do the job ([The following steps were derived from this tutorial video](https://www.youtube.com/watch?v=deEYHVpE1c8&t=480s))

1. fork a repository
2. clone the new, forked repository to your local computer `git clone [reponame]`
3. check your remotes with `git remote -v` (up to now, only origin should be listed)
4. add a new remote (convention is to call it "upstream") via `git remote add upstream [url of original repo]`
5. check if it was successful with `git remote -v` again
6. to get all updates from the original repo, type `git fetch upstream`
7. to incorporate the updates into your local branch, use `git merge upstream/[branchname] [branchname]` 
8. to checkout branches , you now need to specify whether you want to checkout the origin or upstream , e.g. `git checkout origin/[branchname]`
9. until now, you just updated your local branch with the updates from upstream. to update your remote origin, you need to `git push origin [branchname]`
