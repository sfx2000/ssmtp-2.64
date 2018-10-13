## About

Keeping this around for historical reference...

For current debian based systems, better to use apt and grap the ssmtp package there, as it's still supported

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

* Check <gmailuser> and <gmailpassword> again
* Check google is not blocking your new device
* Check Two Factor Auth on Google Account


