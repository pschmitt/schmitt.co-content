/*
Title: Howto Blog
Description: My workflow and how this site works
Date: 2013/12/23
Updated: 2014/02/07
Author: Philipp Schmitt
Tags: blog,github,hosting
*/

Don't get confused by the buzzy title, this post isn't about SEO or anything related. It's more about how this blog works and the workflow I established.

## The backend

[Phile](http://philecms.github.io/Phile/ "Phile's homepage") is a simple, flat content-management system based on [Pico](http://pico.dev7studios.com "Pico's homepage"). "Y U no use wordpress?" you may ask, well... Wordpress relies on a database engine (mysql/mariadb, sqlite etc.) and since there is no GitHub-equivalent that does DB-Versioning it doesn't fit my needs.
Performance may be a disadvantage but since I do not intend to host thousands of posts here it isn't a real problem for me (but this may change - stay tuned).
[Twig templates](http://twig.sensiolabs.org/ "Twig's homepage") are easy to dig in too.

## The hoster

[Hetzner](http://hetzner.de "Hetzner homepage") offers great deals on root server, especially on their [bidding site](https://robot.your-server.de/order/market "Hetzner robot bidding") where you can get a dedicated server for as low as 23€/month. They don't support ArchLinux installations, but I've got [a fix for that](https://github.com/pschmitt/hetzner-arch "Install ArchLinux on a Hetzner root server").

_PS: Nope this isn't a sponsored post._

## The flow

My website's files reside in a [GitHub repo](https://github.com/pschmitt/schmitt.co/ "GitHub - schmitt.co"). There I defined a webhook so that each time I push to the main repo a PHP script that resides on my root server gets called. The said script executes a recursive pull of the repository holding my pages. The setup couldn't be easier just go to the settings of the repo, under "Service Hooks" select "WebHook URL" and enter your URL:

![GitHub WebHook Screenshot](%base_url%/content/howto-blog/img/gihub-webhook.png)

### Security

You should definitely do some IP filtering since without anyone who knows the WebHook URL could request a pull. You can get the IPs on the WebHook settings page:

![GitHub WebHook URLs Screenshot](%base_url%/content/howto-blog/img/github-webhook-urls.png)

Otherwise adding a `GET` variable check could add an extra layer of security. Yep, that's the part of the URL I blurred. Sorry hackers.

## Alternative

If you don't plan on pseudo-hosting your website on GitHub like I do, you should take a look at [codeforest's post](http://www.codeforest.net/pico-cms-and-draft "Pico CMS and Draft – awesome blogging solution") on integrating Draft with Pico.

## Mobile

It's <del>2013</del> 2014, so how do I blog from my smartphone?

* [SGit](https://play.google.com/store/apps/details?id=me.sheimi.sgit "Play Store - SGit")
* [Vim Touch](https://play.google.com/store/apps/details?id=net.momodalo.app.vimtouch "Play Store - Vim Touch")
