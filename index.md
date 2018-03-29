# Sebastien Wains
A markdown based [wiki] about Linux, Open Source, VoIP and other geeky stuff.

Sources of this site are available on [Github].

You can't comment here but you can open an issue or submit a merge request on Github if something is incorrect or requires clarification.

## What I'm up to today

For those who have known me for a couple of years now, you've learned that I was really into **Linux**, **Postfix**, **OpenVPN** and **Asterisk** for some time, back when I was managing 5 Linux servers or so.

Today, I manage more than 300. I spend a lot of time automating, centralizing and orchestrating system administration and management with those tools:

- **[Saltstack]**
- **Salt Cloud**
- **Python**
- **Git, [Gitlab CE] and [tig]**
- **[Mkdocs]**
- **[Rundeck]**
- **Jenkins**
- **Artifactory**
- **Nexus**
- **[Postman]**
- **Redhat Satellite**
- **[iTop]**
- **[Graylog]**

In the same vein of automation at a personal level, I'm a huge fan of **[Automagic]** on Android, **[Alfred]** on Mac, **[Albert]** on Linux, and hackable connected devices.

My work environnement is based on Fedora with **[i3]** tiling window manager, running as a KVM on a libvirt RHEL7 host. I'm a die-hard shortcut keyboard user.

I talked about [SaltStack] at [Jeudis du Libre] conference. Check my [Github] for the decks.

## Why a wiki?

Story time. I started this website in **June 2005** (but bought the domain in March of the same year). The idea was to save notes about my findings so I could look them up later. I figured that I would share them online so it would probably help someone else down the line. 

It all started as a self-hosted **Wordpress** blog as `www.wains.be` (changed to `blog.wains.be` around September 2011). I had a lot of times on my hands and I was able to interact with my readers. On the busiest months I was getting 20000 visits a month. After a while, **spam**, **bots** and **security** issues became problematic, and the maintenance became a burden (files and database backup, PHP and security upgrades, dist-upgrades, etc.). I became kind of bored of maintaining or even publishing anything.

I needed something different. Something more automated and less cumbersome.

I wanted to publish things quickly, from anywhere in the world. I wanted to be able to write offline, and see my content pushed online almost automagically as I was getting a connection.

So here we are, **July 2015**, almost exactly 10 years later, the blog platform became a wiki platform. The (somewhat aging) content is still there and I hope you find useful stuff.

This site has gone through five major design revisions: [2005](https://blog.wains.be/Nostalgy/2005.png), [2008](https://blog.wains.be/Nostalgy/2008.png), [2011](https://blog.wains.be/Nostalgy/2011.png), [2015](https://blog.wains.be/Nostalgy/2015.png) and [2017](https://blog.wains.be/Nostalgy/2017.png)

In 2015, it was running [Wikitten](https://github.com/victorstanciu/Wikitten).

In 2017 revision, I moved to [Mkdocs] as Wikitten didn't have a search engine and was not actively developed.

## Why Markdown?

I write articles on my personal computer.

Markdown has some great advantages : 

- stored as plain text on disk
- content is indexed making it easy to find content with Alfred/Spotlight/grep
- you can grep, sed, awk the hell out of them and bring corrections very quickly
- can be stored in a Git repository

This is my current publication workflow:

- I edit articles locally with [Visual Studio Code] (yes, it is an open source Microsoft product, and it is very good)
- I commit changes to my [GitHub] 
- With an Alfred workflow, I connect to my VPS and do:
    - a "git pull" to retrieve updates
    - rebuild the doc (which is served as static files by the HTTP server)
- Article is online

## About me
I like building simple, powerful, resilient, secure and automated infrastructures. Preferably based on open tools and protocols. Privacy and security are a concern.

When I'm not busy at the computer, I travel, hike, ski, camp out and take photos.

I'm an [INTJ]: INTJs are known as the "Systems Builders" of the types, perhaps in part because they possess the unusual trait of combining imagination and reliability. ~ [Marina Margaret Heiss](http://typelogic.com/intj.html)

I work in Brussels, Belgium.

## Contacts
If you want to contact me, just look me [up].

## Found an error on this site?
Open an [issue on Github](https://github.com/sebw/blog.wains.be/issues/new)

[this]: https://github.com/sebw/blog.wains.be/search?utf8=%E2%9C%93&q=postfix
[up]: https://duckduckgo.com/?q=Sebastien+Wains
[wiki]: http://www.mkdocs.org/
[Mkdocs]: http://www.mkdocs.org/
[markdownx]: https://play.google.com/store/apps/details?id=com.ryeeeeee.markdownx
[macdown]: http://macdown.uranusjr.com/
[GitHub]: https://github.com/sebw/
[Alfred]: https://www.alfredapp.com/
[Albert]: https://albertlauncher.github.io/
[Automagic]: https://automagic4android.com/
[Rundeck]: http://www.rundeck.org
[Gitlab CE]: https://about.gitlab.com/downloads/
[Saltstack]: https://www.saltstack.com
[iTop]: https://www.combodo.com/itop-193
[INTJ]: https://en.wikipedia.org/wiki/INTJ
[Graylog]: https://www.graylog.org/
[i3]: https://i3wm.org/
[Postman]: https://www.getpostman.com/
[tig]: http://jonas.nitro.dk/tig/
[Visual Studio Code]: https://code.visualstudio.com/
[Jeudis du Libre]: http://www.jeudisdulibre.be
