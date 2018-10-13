## About sSMTP

Keeping this around for historical reference... yes, this is old code

for README - see below...

For current debian based systems, better to use apt and grap the ssmtp package there, as it's still supported

## Dependencies

* openssl
* inetutils

## USAGE

sSMTP - simple mail agent

sSMTP is an extremely simple MTA to get mail off the system to a mail hub. It contains no suid-binaries or other dangerous things – no mail spool to poke around in, and no daemons running in the background. Mail is simply forwarded to the configured mailhost. Extremely easy configuration.

This is ideal for web servers and embedded to avoid running MTA daemons like sendmail, Exim and Postfix which use up resources on the server.

## sSMTP and gmail

ssmtp.conf

```
# gmailuser - gmail account
# gmailpassword - password for the account - this is in the clear
# hostname doesn't need to be a FQDN
root=<gmailuser>@gmail.com
hostname=<hostname>
mailhub=smtp.gmail.com:587
UseSTARTTLS=Yes
AuthUser=<gmailuser>@gmail.com
AuthPass=<gmailpassword>
FromLineOverride=YES
```

sSMTP doesn’t run as service so there’s no restart required. sSMTP creates a link to /usr/sbin/sendmail which most programs use by default to send mail including PHP.

## Testing w/Gmail

```
echo "Test message from Linux server using ssmtp" | sudo ssmtp -vvv recipient@domain.com
```

The trace there should be evident - it works or it doesn't

## Errors

Unfortunately - a few things might go wrong, so check the following

* Check gmailuser and gmailpassword again
* Check google is not blocking your new device
* Check Two Factor Auth on Google Account - with two factor auth, you'll need to set an app password


***

# ssmtp-2.64

Purpose and value:
 This is sSMTP, a program that replaces sendmail on workstations that should
 send their mail via the departmental mailhub from which they pick up their
 mail (via pop, imap, rsmtp, pop_fetch, NFS... or the like).  This program
 accepts mail and sends it to the mailhub, optionally replacing the domain in
 the From: line with a different one.

 WARNING: the above is all it does. It does not receive mail, expand aliases
 or manage a queue.  That belongs on a mailhub with a system administrator.
 The man page (ssmtp.8) and the program logic manual (ssmtp_plm) discuss the
 limitations in more detail.

 It uses a minimum of external configuration information, and so can be
 installed by copying the (right!) binary and an optional four-line config
 file to a given machine. 

Type of systems supported:
 Berkeley-derived, or ones otherwise using /usr/lib/sendmail as a mail transfer
 agent. In use on SunOS 4.1.1, NextStep 2.x/3 and Ultrix 4.2, tested briefly on
 AIX 3.2 and RISCos. Tested by others on DG U/X 5 and SVR4.

 You may need to #define USE_OLD_ARPADATE for the Cygwin port of ssmtp
 (otherwise the day of the month would always be the letter "d").

Dependencies:
 External: Berkeley sockets and supporting libraries.

Known limitations:
 This is not a complete sendmail. It is only a program to post mail to a
 mailhub for people who don't *want* a complete sendmail. Therefore a lot of
 flags are not supported. The old header limit of 4K is fixed and the number
 of recipients is as large as can be held in memory.

Known problems:
 Pine uses a lot of sophisticated options to talk to sendmail, and uses
 batched SMTP input which is not supported. The solution is to use your mailhub
 as smtpserver in pine.conf. If the mailhub is not reachable, sSMTP will fail.

Authors:
 David Collier-Brown, davecb@hobbes.ss.org, davecb@sni.ca or dave@lethe.uucp
 Christoph Lameter, clameter@debian.org, clameter@waterf.org, clameter@i-m-f.org
 Hugo Haas, hugo@debian.org, hugo@larve.net, hugo@via.ecp.fr
 Matt Ryan, mryan@debian.org, matt.ryan@banana.org.uk

TLS support from Tobias Rundstrom <tobi@tobi.nu>
IPv6 support from Jun-ya Kato <kato@goto.info.waseda.ac.jp>
MD5 authentication support from TAKIZAWA Takashi <aki@luna.email.ne.jp>

Current Maintainer:
 Anibal Monsalve Salazar, A.Monsalve.Salazar@IEEE.org

Patchlevel:
 See ssmtp.c

Copying conditions:
 GNU GPL
