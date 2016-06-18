


date: 2007-05-16 21:26:45+00:00


# 'LibClamAV Error: Database Directory: /var/clamav not locked'

categories:
- Linux


If you get that message when using freshclam, check out the clamd sock file...

Usually stored under /var/run/clamav/clamd.sock

Verify the ownership on the file, directory, and verify if the owner is similar to the user running clamd.
