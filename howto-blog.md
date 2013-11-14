/*
Title: Howto Blog
Description: My workflow and how this site works
Date: 2013/11/15
Tags: blog,github,hosting
*/

Don't get confused by the buzzy title, this post isn't about SEO or anything related. It's more about how this blog works and the workflow I established.

## The backend

[Pico CMS](http://pico.dev7studios.com "PICO") is a simple, flat content-management system. "Y U no use wordpress?" you may ask, well... Wordpress relies on a database engine (mysql/mariadb, sqlite etc.) and since there is no GitHub-equivalent that does DB-Versioning it doesn't fit my needs.
Performance may be a disadvantage but since I do not intend to host thousands of posts here it isn't a real problem for me (but this may change - stay tuned).
Twig templates are easy to dig in too.

## The hoster

@Hetzner

## The flow

My website's files reside in a [GitHub repo](https://github.com/pschmitt/schmitt.co/ "GitHub - schmitt.co"). There I defined a webhook so that each time I push to the main repo a PHP script that resides on my root server gets called. The said script executes a recursive pull of the repository holding my pages. The setup couldn't be easier just go to the settings of the repo, under "Service Hooks" select "WebHook URL" and enter your URL:

![GitHub WebHook Screenshot](./content/img/gihub-webhook.png)

### Security

You should definetly do some IP filtering since without anyone who knows the WebHook URL could request a pull. You can get the IPs on the WebHook settings page:

![GitHub WebHook URLs Screenshot](./content/img/github-webhook-urls.png)

Otherwise adding a `GET` variable check could add an extra layer of security. Yep, that's the part of the URL I blurred. Sorry hackers.

## Mobile

It's 2013, so how do I blog from my smartphone?

* [SGit](https://play.google.com/store/apps/details?id=me.sheimi.sgit "Play Store - SGit") 
* [Vim Touch](https://play.google.com/store/apps/details?id=net.momodalo.app.vimtouch "Play Store - Vim Touch")
