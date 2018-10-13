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
