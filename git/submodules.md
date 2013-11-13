/*
Title: Git submodules 
Description: Howto Git submodules 
Author: Philipp Schmitt
Date: 2013/11/11
Tags: git,github,submodule
*/

Git is great but there's a lot you need to learn before you could call yourself a "power user". One of the things you should know how to cope with are submodules.
If you do not know what this is read [this](http://git-scm.com/book/en/Git-Tools-Submodules "Git Submodules").

**TL;DR**: Submodules are _somehow_ Git's equivalent to SVN externals 

## Add a new submodule

    $ git submodule add ${URL} ${DIRECTORY}

Note that `${DIRECTORY}` is optional but comes in handy if you want to add a repo to a folder that has a different name than the said repo.

## Remove a submodule

    $ git submodule deinit ${submodule_path}
    $ git rm ${submodule_path}  

If you are using Git 1.8+ this should be it. If your are stuck with an older version, you may need to manually edit `.gitmodules` and remove the line corresponding to the submodule you want to remove.

## Clone including submodules

By default, `git clone` does not clone submodules. If you wish to do this, a simple...

    $ git clone --recursive ${REPO}

will do the job.

## Update all submodules

Let's update all submodules at once. Note that in this example, we will assume we want to retrieve updates from the `master` branch of each submodule.

    $ git pull                                # Update main repo
    $ git submodule update --init --recursive # Init submodules
    $ git submodule foreach --recursive "git checkout master; git pull" 

## Inititalize and update a specific submodule

When dealing with larger projects, fetching all submodules at one may take some time. And maybe you don't need to update them all at once.

    $ git submodule init ${desired_submodule}   # init
    $ git submodule update ${desired_submodule} # update

If you want to initialize **AND** update the said submodule this single command will do the same as above:

    $ git submodule update --init ${desired_submodule}

## Pushing to a submodule

Well, first off make sure you initialized your submodules (`git submodule init`) and that you are on a branch:
    
    $ cd ${submodule}
    $ git status
    > # HEAD detached at 5ff339b

In this case we are not on a branch. Don't panic we can make this right with:

    $ git checkout master

Obviously you need to adjust `master` to the branch you want to check out.

## Forgot to checkout a branch ?

Sh!t happens, luckily enough you won't lose anything if you do a checkout. Remember to commit your changes though.

    $ git commit -am "Awesome new feature"
    > [detached HEAD c92741d] Awesome new feature
    >  1 file changed, 1 deletion(-)
    $ git checkout master
    $ git cherry-pick c92741d
    $ git push

## SSH vs. HTTPS

Submodules are great, but when it comes to sharing stuff with other people on GitHub, things may get tricky. As you may know, the _HTTPS_ protocol allows anonymous clones, but _SSH_ relies on key authentification. Dilemma: should I use _HTTPS_ for *ALL* my submodules, even if this requires password:username input for every `git push` ? Should I set a *huge* timeout for HTTPS Auth ?

Nope: there is a magic trick that allows you to use _HTTPS_ for your submodules and still use the _SSH_ when you are pushing your changes to the remote. Just add the following to your `~/.gitconfig`:

    [url "git@github.com:${USERNAME}/"]
        pushInsteadOf = "https://github.com/${USERNAME}/"

Don't forget to change ${USERNAME} to your username.

Source: [pbrisbin | Git Submodule Config](http://pbrisbin.com/posts/git_submodule_config/ "Git Submodule Config") 

