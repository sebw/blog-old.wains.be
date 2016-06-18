
# Switching back from Chrome/Chromium to Firefox and a global rant about Google 
Date: 2015-06-18  
Tags: Google, rant 

I've used Chrome (and Chromium, depending on the platform, from now on I'll refer to it as Chrome) pretty much since it went out of beta.

I started to get annoyed with the last few versions though.

It all started as I tried to install an application on a Windows 7 machine (I'm not in an admin account at the time). That app contained malware not detected by the antivirus (I was not 100% confident it was clean though). It installed a couple of Chrome extensions that were redirecting traffic to ads and opening popups.

Trying to get rid of it has been challenging. If you removed the extension in the extension manager, upon next start up it would appear again. I tried Shield for Chrome but it wasn't helpful, it would just uninstall the extension but it would reappear upon the next restart. It is actually because Chrome was starting with some flags that were calling for extensions located on the filesystem. Run `chrome://version` and see the command line, you would see the directories called.

On the other hand, Chrome has been very good at removing an extension that Google considered "harmful". The extension is called "Download Youtube Chrome" (DYC), and you can only install it by downloading it from the web and installing it as an unpacked extension. Of course, this extension allows to download Youtube videos, so apparently copyrights are more harmful than actual malwares potentially spreading on thousands of machines.

Even before the DYC episode, I was using another extension allowing to download Youtube videos: "Video Downloader Professional". It was working great until Google decided to remove offending extensions from their store and by offending, they probably meant copyright offending (I commute a lot with poor reception, so I download videos for offline viewing).

And even before that, Google started to implement many new features that makes Chrome today twice as big as Firefox as (comparison based on OS X): profile management (`chrome://flags/#enable-new-profile-management`), OK Google voice search (this thing is listening to you constantly if enabled, and any OK Google record is saved in Google Cloud (you can delete them though)), desktop notifications.

You used to be able to specify where desktop notifications were supposed to appear, but Google decided to remove the feature, so you have to stick with notifications in the upper right corner of your screen, an area that you are very likely to click (Wi-Fi picker for example). I can't count how many times I have wrongly clicked on the stupid notification that just poped up in my face, triggering an action.

This goes along with default settings enabling translation and location (well, you get a popup asking if you want to share your location or if you want to translate the page), and those tend to slow down the browser considerably (I'm talking about a late 2008 Macbook here).

I had a couple of bookmarks synced in their "cloud" by signing in. I protected that with my Google password from that time, but today I have a new password and I still need to remind my old password whenever I install Chrome on a new machine. I haven't found how to manage that password (didn't search so much though, but it should be an obvious option).

Lastly, it has been reported that Chromium silently downloads binaries related to voice upon every start on Linux Debian. See [http://www.theregister.co.uk/2015/06/17/debian_chromium_hubbub/](http://www.theregister.co.uk/2015/06/17/debian_chromium_hubbub/) and [https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=786909](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=786909)

So all in all, Chrome has become a memory hog, and Google is controlling your browser in a unprecedented way. The will push or remove whatever features or design, whenever they wish and don't care about what you think. 

And if you believe that the supposedly open source project gives you a voice in the design and implementation, see this link talking about the decision to hide http:// from the URL bar when it's not secured by SSL: [https://code.google.com/p/chromium/issues/detail?id=41467](https://code.google.com/p/chromium/issues/detail?id=41467)

See this comment particularly: [https://code.google.com/p/chromium/issues/detail?id=41467#c19](https://code.google.com/p/chromium/issues/detail?id=41467#c19)

	Chromium UI design is not a democracy and is not based on users' votes ~ Peter Kasting
	
The problem with Chrome design is so important that some people even petionned against Kasting and the UI team: [https://www.change.org/p/lawrence-page-replace-peter-kasting-and-the-google-chrome-ui-team](https://www.change.org/p/lawrence-page-replace-peter-kasting-and-the-google-chrome-ui-team)

Well at least, they haven't given in on the new trend (started by Apple and Safari) to hide the path from the URL in the address bar. How soon though Peter?

I'm now switching back to Firefox, the last time I used it on a daily basis, it was version 3 or so. What is it now? Version 38. Holy cow, time flew.

If only Chrome was the only problem with Google.

Their are trying to force Google+ down our throats in the nastiest ways (you have to have a G+ account to upload Youtube videos, you can't comment Android applications without G+, etc.).

They shut down major applications like Reader probably in a way to increase traffic to G+, but it failed big time. They should have it at least integrated in G+, instead they lost those users.

iGoogle was neat too. Too good probably (my dad loved it), they had to kill it.

They are forcing Hangouts for people who still use Google Talk. Every once in a while, Gmail will switch to Hangouts without notice. Thanks, I'm now using competing products.

I'm done with the force-feeding attitude of Google that got so powerful that they think their vision of the web should be pushed (silently) to users. They know it, a vast majority of users just grasp things and don't question what they are presented with. They also have the right to pull the plug on popular services to serve their purpose of winning the social network business. Give up already Google, 90% of users never posted anything on your G+ toy: [https://www.stonetemple.com/real-numbers-for-the-activity-on-google-plus/](https://www.stonetemple.com/real-numbers-for-the-activity-on-google-plus/)
