# @de-rse.org email addresses

A limited set of @de-rse.org email addresses can be created.
This is limited because we do not have a per-user-management interface with our current provider (jpberlin).
For this reason, we currently limit those adresses to a few functional addresses, as well as addresses for the board and employees.

## Creation

Someone with the necessary credentials has to login to the web interface at [jpberlin](https://verwaltung.heinlein-hosting.de).
For credentials, see keepass.
Next, select "[zur Accountverwaltung](https://verwaltung.heinlein-hosting.de/#/account=de-rse)" and there, click on the number in the email column on the `de-rse.org` domain.
A new page should open listing all currently set up email addresses, with a `+` button on the top right.
Click this to add a new address: enter only the part before the `@`-sign in this new menu, as well as a password, and select "Speichern".

## Client configuration

There is also [web mail](https://webmail.jpberlin.de/) available or use whatever other email client you are used to.
The necessary details to configure the new INBOX are [provided by jpberlin](https://jpberlin.de/hilfe/wie-kann-ich-meine-e-mails-mit-meinem-mailprogramm-abrufen).
The following only copies some of this information in case the former link goes stale.

- Mailserver eingehend (POP3/IMAP): mail.jpberlin.de
- Mailserver ausgehend (SMTP): mail.jpberlin.de
- Username: m.mustermann@jpberlin.de  (m.mustermann@de-rse.de)
- Mailadresse: m.mustermann@jpberlin.de (m.mustermann@de-rse.de)

Since the username does contain an `@` character, specifying the INBOX as URL get a bit cumbersome, as this then needs to be escaped in that case, like so:

```imaps://vorname.nachname%40de-rse.org@mail.jpberlin.de/INBOX```


