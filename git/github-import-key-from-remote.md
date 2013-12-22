/*
Title: GitHub: Import SSH keys from remote server
Description: Import SSH keys from remote server
Date: 2013/11/11
Updated: 2013/12/22
Author: Philipp Schmitt
Tags: git,github,ssh
*/

## xsel/xclip

Using `xsel`:

    ssh $REMOTE_SERVER cat ~/.ssh/id_rsa.pub | xsel -b

Using `xclip`:

    ssh $REMOTE_SERVER cat ~/.ssh/id_rsa.pub | xclip -sel clip

And then paste it to [your GitHub](https://github.com/settings/ssh "GitHub - SSH Key Management").

## Alternative

You can also use a CLI pastie like [sprunge.us](http://sprunge.us "sprunge.us - CLI pastie"):

    cat ~/.ssh/id_rsa.pub | curl -F 'sprunge=<-' http://sprunge.us'>'
