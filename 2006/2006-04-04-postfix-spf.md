


date: 2006-04-04 20:42:41+00:00


# Postfix + SPF

categories:
- Howto
- Linux
- Postfix


Enable SPF if you believe you need it..
For your information, SPF is not widely used

<!-- more -->

You'll need Mail::SPF::Query :
`1. perl -MCPAN -e shell
2. Under CPAN : install Mail::SPF::Query
3. Quit CPAN after installation of the library`

Install libspf2-1.0.4 and libspf2-devel-1.0.4 from http://www.city-fan.org/ftp/contrib/libraries/

wget http://spf.pobox.com/postfix-policyd.txt -O /etc/postfix/spf-policy.pl

chmod 755 /etc/postfix/spf-policy.pl

Edit /etc/postfix/master.cf :
`spfpolicy unix  -       n       n       -       -       spawn user=nobody argv=/usr/bin/perl /etc/postfix/spf-policy.pl`

Edit /etc/postfix/main.cf : 

    
    <code>check_policy_service unix:private/spfpolicy
    
    smtpd_recipient_restrictions =
            reject_unauth_destination
            reject_unknown_recipient_domain
            reject_unverified_recipient
            check_policy_service unix:private/spfpolicy</code>



service postfix restart

Check /var/log/maillog for SPF output


