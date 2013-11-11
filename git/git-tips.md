/*
Title: Git Tips&amp;Tricks
Description: Various Git Tips 
Author: Philipp Schmitt
Date: 2013/10/26
Tags: git,github,submodule
*/

In this post, I will go over a few FAQs about Git. I'm an ArchLinux user, so I'm using the very latest stable Git (1.8.4 as I am writing this). Keep this in mind as some of the listed commands may not work with older versions.


# Undoing stuff

## Change your last commit message (_prior_ to pushing!)

This one is easy. Try this:

    $ git commit --amend -m "New commit message"

Source: [stackoverflow | How do I edit an incorrect commit message in Git?](http://stackoverflow.com/a/179147/1872036 "How do I edit an incorrect commit message in Git?")

## You pushed a file containing a password, your credit card info, or the reset code for the internet to a public repo

1. Do never, ever, ever do this again
2. Consider killing yourself
3. Read [this](https://help.github.com/articles/remove-sensitive-data "GitHub | Remove sensitive data")
4. Use a `.gitignore` file next time

# Misc

* Do **NOT** use a GUI-wrapper (like turtoiseGIT, eclipse ...)
