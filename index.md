# Sebastien Wains
A markdown based [wiki] about Linux, Open Source, VoIP and other geeky stuff.

## What I'm up to today

For those who have known me for a couple of years now, you've learned that I was really into **Linux**, **Postfix**, **OpenVPN** and **Asterisk** for some time, back when I was managing 5 Linux servers or so.

As of today, I manage about 200, so I'm spending a lot of time automating, centralizing and orchestrating management with **Saltstack**, **Rundeck**, **Jenkins**, **Nexus**, **Satellite**, **iTop** and **Graylog/Elasticsearch**. In the same vein, I'm a huge fan of **Automagic** on Android, and **Alfred** on Mac.

## Why a wiki?

Story time. I started this website in **June 2005** (but bought the domain in March of the same year). The idea was to save whatever I was finding so I could look it up later if I needed again. I figured that I would put those notes online so it would probably be helpful to other people. 

It all started as a self-hosted **Wordpress** blog as www.wains.be (changed to blog.wains.be around September 2011). I had a lot of times on my hands and I was able to interact with my readers. On the busiest months I was getting 20000 visits a month. After a while, **spam** and **security** issues became problematic, and the maintenance became a burden (files and database backup, PHP and security upgrades, etc.). As a result, I became kind of bored of maintaining it or even publishing anything.

Today, my focus has changed. I want to publish things quickly. From anywhere in the world, I want to be able to write, connected or not, and as soon as I connect, the content gets published.

So here we are, almost exactly 10 years later, I moved from a blog to a wiki platform in **July 2015**. The content is still there and I hope you find useful stuff.

This site has gone through four design revisions: [2005](https://blog.wains.be/Nostalgy/2005.png), [2008](https://blog.wains.be/Nostalgy/2008.png), [2011](https://blog.wains.be/Nostalgy/2011.png) and [2015](https://blog.wains.be/Nostalgy/2015.png).

## Why Markdown?

Markdown is great because every articles of this site are stored on my MacBook. It is plain text so Spotlight indexes the content, and I can just look up a word and I will get to the article source immediately. I can grep, sed, awk the hell out of them and bring correction very quickly.

It is also very easy to automate publications.

My workflow is this:

- I edit articles in [MacDown] on Mac and [MarkdownX] on Android device
- articles are pushed to my private [Syncthing] cloud and synchronized between devices
- I commit changes to [Github] as a public backup
- I wrote an [Alfred] workflow involving rsync allowing me to publish in a few seconds with a simple keyword
- the article appears instantly

## Can't find anything here?
There is no content search engine on this platform. Try [this] kind of query instead, it should point you to the right page.

## About me
I like building simple, powerful, resilient, secure and automated infrastructures. Preferably based on open tools and protocols. Privacy is a main concern.

When I'm not busy on a computer, I travel, hike, camp and take photos.

I work in Brussels, Belgium.

## Contacts
If you want to contact me, just look me [up].

## Found an error on this site?
Please contact me!

[this]: https://duckduckgo.com/?q=linux+site:blog.wains.be
[up]: https://duckduckgo.com/?q=Sebastien+Wains
[wiki]: https://github.com/victorstanciu/Wikitten
[markdownx]: https://play.google.com/store/apps/details?id=com.ryeeeeee.markdownx
[macdown]: http://macdown.uranusjr.com/
[Github]: https://github.com/sebw/posts
[Syncthing]: https://syncthing.net/
[Alfred]: https://www.alfredapp.com/