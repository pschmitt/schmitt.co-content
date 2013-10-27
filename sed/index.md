/*
Title: sed Snippets
Description: Various sed stuff
Date: 2013/10/27
Tags: sed,bash,sh,zsh
*/

## Basic sed usage

The stream editor is your go-to-guy to alter text files:
    
    $ echo "1 1 1 1" | sed -e 's/1/2/g'
    > 2 2 2 2

This command replaces (`s/`) all (`/g`) occurences of `1` by `2`.

## Usefull flags

`-i`: Operate on a file directly
    
    $ echo "1 1 1 1" > test
    $ sed -ie 's/1/2/g' test; cat test
    > 2 2 2 2

## sed as grep alternative

Most people would simply pipe grep's output into sed for further processing, like this: 
    
    $ grep something file | sed -e 's/string/replacement/' > file

But there is a simpler way of achieving this:
    
    $ sed -ie '/something/s/string/replacement/' file

