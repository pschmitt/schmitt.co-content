/*
Title: sed Snippets
Description: Various sed stuff
Date: 2013/10/27 
Updated: 2013/12/21
Author: Philipp Schmitt
Tags: sed,bash,sh,zsh
*/

## Basic sed usage

The stream editor is your go-to-guy to alter text files:
    
    echo "matchme matchme matchme matchme" | sed -e 's/matchme/matched/g'
    > matched matched matched matched

This command replaces (`s/`) all (`/g`) occurences of `matchme` by `matched`.

## Usefull flags

`-i`: Operate on a file directly
    
    echo "matchme matchme nomatch matchme" > test
    sed -ie 's/matchme/matched/g' test; cat test
    > matched matched nomatch matched

`-n`: Do not print output (quiet mode) 

## sed as a grep alternative

Most people would simply pipe grep's output into sed for further processing, like this: 
    
    grep something file | sed -e 's/string/replacement/' > file

But there is a simpler way of achieving this:
    
    sed -ie '/something/s/string/replacement/' file

Mimicking `grep`'s behaviour without "harming" any file can be done using:

    sed -n '/string/p' file

Which will "grep" for `string` in `file`.

## Multiple commands

    sed -e 's/matchme/matched/g;s/match2/matched2/g' <<< "matchme matchme nomatch nomatch match2 match2"
    > matched matched nomatch nomatch matched2 matched2 

## Prepend

Appending to a file is pretty straight-forward in standard shell:

    echo "append this to file" >> file

Prepending could be done with a little trick, like:
    
    mv file file.orig
    echo "prepend this to file" > file.prepend
    cat file.prepend file.orig > file
    rm file.prepend file.orig

There may be a slightly shorter version but that's still a lot a commands! Using `sed` it's much shorter:

    sed -i "1i prepend this to file" file

## Get lines X to Y

This is a nice one. The example prints out lines 12-45 from `file`.

    sed -n '12,45p' file
