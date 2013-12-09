/*
Title: irssi cap_sasl dependency
Description: The right package to install to get the ssl script to work in irssi
Date: 2013/11/22
Author: Philipp Schmitt
Tags: irssi,perl,archlinux
*/

## The issue

If you are using the awesome irssi script [cap_sasl](http://freenode.net/sasl/cap_sasl.pl "Download cap_sassl.pl @freenode.net") by Michael Tharp and Jilles Tjoelker that allows you to securily log into IRC, you may be wondering about the unmet perl dependencies after you lauch irssi:

    21:02 Can't locate Crypt/DH.pm in @INC (you may need to install the Crypt::DH module) (@INC contains: /home/pschmitt/.irssi/scripts /usr/share/irssi/scripts /usr/lib/perl5/core_perl 
          /usr/lib/perl5/site_perl /usr/share/perl5/site_perl /usr/lib/perl5/vendor_perl /usr/share/perl5/vendor_perl /usr/share/perl5/core_perl .) at 
          /home/pschmitt/.irssi/scripts/autorun/cap_sasl.pl line 237.
    21:02 BEGIN failed--compilation aborted at /home/pschmitt/.irssi/scripts/autorun/cap_sasl.pl line 237.

## Get the right package (ArchLinux) 

The [AUR](https://aur.archlinux.org/ "AUR Homepage") is cluttered with perl packages, this is the one that did solve the problem for me: [perl-crypt-dh](https://aur.archlinux.org/packages/perl-crypt-dh/ "AUR/perl-crypt-dh")

## TL;DR Installation

    wget https://aur.archlinux.org/packages/pe/perl-crypt-dh/PKGBUILD
    makepkg -si

## Read more

* [Pbrisbin's irssi setup](http://pbrisbin.com/posts/irssi/ "Pbrisbin/irssi")
* [Configuring SASL for irssi](http://freenode.net/sasl/sasl-irssi.shtml "Configuring SASL for irssi")
