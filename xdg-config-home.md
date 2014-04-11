/*
Title: Move your config files to $XDG_CONFIG_HOME
Description: A collection of short howtos on how to move most of your config files to $XDG_CONFIG_HOME
Date: 2014/02/12
Updated: 2014/04/11
Author: Philipp Schmitt
Tags: zsh,vim,firefox,vimperator,xdg,config
*/

## The problem

It may sound like a cliché comming from [a german guy](http://schmitt.co/about "Who's this german guy?") but I like to have my hard drive organized. It just hate it when every app I install creates its own config file in my `$HOME` directory. It's the default folder shown when I start my file manager and it is just anoying seeing a bunch of "dotfiles" there. They should all reside in `$XDG_CONFIG_HOME`. Come on, that's what this folder is for! In this post I will go over a few tricks to make some apps I frequently use store their configuration files in the one and only right location: `$XDG_CONFIG_HOME/$APP_NAME`

## The solutions

Thanks god (Linus? :D). *Most* of the programs I'm using aren't that hard to educate, mostly it's just a matter of setting an environment variable. For starters I'd recommend making sure the `XDG_CONFIG_HOME` variable is always set by adding this to your `.bashrc` or `.zshenv` file:

    [[ -z $XDG_CONFIG_HOME ]] && export XDG_CONFIG_HOME="$HOME/.config"

### ZSH

First of, ZShell. There's a `$ZDOTDIR` environment variable that tells zsh where to look for its config. So let's set it right by exporting it in `$HOME/.zshenv`:

    export ZDOTDIR="$XDG_CONFIG_HOME/zsh"

If you have root access you could set this in `/etc/zsh/zshenv` which would solve the config file problem for all users (well, at least for those who didn't set `no_global_rcs` which prevents the sourcing of global config files).

**NOTE:** Your config file still has to be named `.zshrc` (notice the dot). Otherwise ZSH won't source it.

### Vim

Same procedure:

    export VIMINIT='let $MYVIMRC="$XDG_CONFIG_HOME/vim/vimrc" | source $MYVIMRC'
    export VIMDOTDIR="$XDG_CONFIG_HOME/vim"

Congrats! Your new `vimrc` path is now: `$XDG_CONFIG_HOME/vim/vimrc` (no dot this time!)

Source: [Vim respect XDG](http://tlvince.com/vim-respect-xdg "Vim respect XDG by Tom Vincent")


### Vimperator

Vimperator is a great Firefox addon (the very best imho) but so as the previous applications, it's config file is **misplaced** by default. Once again, a few `exports` will solve this:

    export VIMPERATOR_RUNTIME="$XDG_CONFIG_HOME/vimperator"
    export VIMPERATOR_INIT=":source $VIMPERATOR_RUNTIME/vimperatorrc"

### Git

Git's trivial, by default it will write its config to `$HOME/.gitconfig`, but if `$XDG_CONFIG_HOME/git/config` exists it will use the latter instead. So just move your config:

    mkdir -p $XDG_CONFIG_HOME/git
    mv ~/.gitconfig !$/config

### rxvt-unicode-daemon

urxvtd has an environment variable (which defaults to `$HOME/.urxvt`):

    export RXVT_SOCKET=$XDG_DATA_HOME/urxvt/urxvt-$HOST

**Note:** urxvtd won't create this directory by its own, so you'll have to `mkdir $RXVT_SOCKET:h`

### mplayer

Yet _another_ environment variable:

    export MPLAYER_HOME=$XDG_CONFIG_HOME/mplayer

## Some symlinks remain

Legacy, legacy... Screw legacy. Some programs aren't that easy to configure. For example there's mutt, firefox, ncmpcpp, wireshark, mplayer, xmonad, gimp... It's 2014 and we, linux users, haven't any **real** standard config directory. OSX solved the problem by just forbidding any program to write anywhere else, but that's not how we roll... I mean, just check your `$HOME` directory. How clamped is yours?! Sure there are a few projects like [libetc](http://ordiluc.net/fs/libetc/ "libetc") that aim to solve this, but wouldn't it be a better world if every Linux developer would embrace `$XDG_CONFIG_HOME`?


_PS: If you know a way to move an app's config files to `$XDG_CONFIG_HOME` that I didn't mention, please let me know in the comments - I'll update this post._


__Read more - External links:__

* [Put your $HOME in .home!](https://bbs.archlinux.org/viewtopic.php?id=77606&amp "Put your $HOME in .home! @archlinux")
* [XDG Base Directory Specification](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html "XDG Base Directory Specification")
