# Buschlab Github Workshop

### The Basics


![alt text](https://github.com/remichel/fork_it_like_its_hot/blob/master/fork1.png)

### What is a fork?

- The concept behind forks (in contrast to clones) is well explained [here](https://www.youtube.com/watch?v=EAC6zUmgkgQ)

### GitKraken workflow

- you can download Gitkraken [here](https://www.gitkraken.com/)
- A Gitkraken workflow is well expained [here](https://www.youtube.com/watch?v=j_qpzND5yAg)

### Commandline workflow

- The following steps were derived from [this tutorial video](https://www.youtube.com/watch?v=deEYHVpE1c8&t=480s)

1. fork a repository
2. clone the new, forked repository to your local computer `git clone [reponame]`
3. check your remotes with `git remote -v` (up to now, only origin should be listed)
4. add a new remote (convention is to call it "upstream") via `git remote add upstream [url of original repo]`
5. check if it was successful with `git remote -v` again
6. to get all updates from the original repo, type `git fetch upstream`
7. to incorporate the updates into your local branch, use `git merge upstream/[branchname] [branchname]` 
8. to checkout branches , you now need to specify whether you want to checkout the origin or upstream , e.g. `git checkout origin/[branchname]`
9. until now, you just updated your local branch with the updates from upstream. to update your remote origin, you need to `git push origin [branchname]`
