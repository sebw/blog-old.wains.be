# logwatch and logrotate might create a blind spot in reporting

From : [http://www.derkeiler.com/Mailing-Lists/securityfocus/bugtraq/2005-01/0295.html](http://www.derkeiler.com/Mailing-Lists/securityfocus/bugtraq/2005-01/0295.html)



Date: Tue, 25 Jan 2005 16:21:44 +0200 (EET)
To: BUGTRAQ 


-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1

Hello BUGTRAQ,

I'm sorry, if this is old news to you, but I couldn't find similar cases
in BUGTRAQ archives.

logwatch (www.logwatch.org) is widely recommended tool for creating nice
reports of various, often security related logfiles. logwatch is included
at least in recent Red Hat/Fedora linux distributions, probably others as
well.

logrotate script is used to periodically rotate and delete logfiles.

Default configuration in recent Red Hat/Fedora distributions is following:

  * run logwatch daily (from /etc/cron.daily, starting at 04:02) using
    range 'yesterday' and skipping log archives (i.e. secure.1)

  * run logrotate daily (from /etc/cron.daily, after logwatch) using
    rotation period 'weekly', practically every Sunday morning

Above defaults create blind spot every Sunday morning between 00:00:00 -
04:01:59 (system local time), when entries added to any system logs are
discarded from logwatch reports.

Situation is even worse on a busy server, in case you need to rotate some
or all logfiles daily. In that case, the blind spot happens every day.

This is a problem only for organizations or system administrators relying
solely on logwatch reports, as all logged information is still present in
system logs.

There are some ways to make logwatch reports more reliable:

  * set "Archives = yes" in logwatch.conf. You might also want to tune
    archive settings in /etc/log.d/conf/logfiles/ to prevent unnecessary
    processing of really old archives. To cover the blind spot with range
    'yesterday' and weekly rotation, it is usually enough to specify for
    example "Archive = secure.1" in secure.conf

  * move logwatch and logrotate to happen at midnight

  * change date matching logic in /etc/log.d/scripts to match for example
    previous 24 hours

Sami Pitko

-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.2.3 (GNU/Linux)

iD8DBQFB9lMLRtCggsJm46kRAljFAJ9AKPDPt1d0SObw0ogYKJBwOytrOgCgpx1X
CsonunvinrWSaDoageCQtF8=
=c0On
-----END PGP SIGNATURE-----
