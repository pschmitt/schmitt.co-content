/*
Title: GitHub: Import SSH keys from remote server
Description: Import SSH keys from remote server
Date: 2013/11/11
Author: Philipp Schmitt
Tags: git,github,ssh
*/

Using `xsel`:

    ssh $REMOTE_SERVER cat ~/.ssh/id_rsa.pub | xsel -b

Using `xclip`:

    ssh $REMOTE_SERVER cat ~/.ssh/id_rsa.pub | xclip -sel clip

And then paste it to [your GitHub](https://github.com/settings/ssh "GitHub - SSH Key Management").
