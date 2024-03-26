# Cloudron matches for deRSE IT-Anforderungen

## Overview

- geplant ist, die domain de-rse.org selber über einen DNS-Provider zu managen (z.B. https://inwx.de)
- als Infrastruktur wollen wir einen _Virtual private Server_ (VPS) mit [_Cloudron_][cloudron] als Betriebssystem. Der VPS
  sollte in einem deutschen Rechenzentrum gehostet sein. Mögliche Anbieter für solche VPS sind

  - windcloud.de: https://windcloud.de/produkte/vps/

- Die jekyll-basierte statische Website von de-rse.org wollen wir in ein Community Portal umwandeln, das mit einem Content-Management-System ausgestattet ist,
  ein Event-Management beinhaltet, verschiedene Kategorieren von Arbeitsgruppen abbilden kann und einen _Member space_ implementiert

  - Community-Portal (Kontakt: Philipp Sommer): https://codebase.helmholtz.cloud/hcdc/django/clm-community/django-academic-community/
  - Deployment via Cloudron: https://github.com/Chilipp/djac-app
- Zum gemeinsamen Bearbeiten von Dateien wollen wir über den cloudron-Server eine Nextcloud-Instanz auspielen, mit geteilten Addressbüchern
  und Kalendern. Alternativ könnte man cryptpad installieren, dort sind die Dateien ende-zu-ende verschlüsselt
- Für das Finanzmanagement des de-rse wollen wir [Firefly III](https://www.cloudron.io/store/org.fireflyiii.cloudronapp.html) auf dem
  Server installieren

[cloudron]: https://cloudron.io

## Detailed feature overview

folgende Liste basiert auf [needs.md](./needs.md)

> - DNS
>     - mehrere, frei wählbare Domains
>     - Möglichkeit zu schneller, schneller (bzw. direkter) Änderung von Einträgen von Subdomains (u.a. A, CNAME)

Durch die Nutzung von inwx.de kann die Domain eigenständig verwaltet werden und subdomains können einfach angelegt werden. 
Das Routing übernimmt dann cloudron auf dem VPS (jede App auf cloudron läuft über eine eigene domain/subdomain).

> - Email
>     - mehrere, einfache Verteiler
>     - mehrere Mailinglisten
>         - Archiv
>         - Datenvolumen potentiell >1GB / Monat
>         - private und öffentliche Listen
>         - unter eigener Domain!
>         - schnelle Einrichtung & Konfiguration durch uns

Einfache Verteiler können über cloudron selber unkompliziert angelegt werden. Es handelt sich hierbei um ein einfaches Forwarding.
Mitglieder können aber nur von Admins über das Cloudron Web-Frontend (oder via API) hinzugefügt werden. Eine 
Self-Subscribe-Funktion müsste per separater App organisiert werden.

Mailinglisten können leider über cloudron nicht konfiguriert werden, lediglich einfache Weiterleitungen an mehrere Adressen.
Mailman (oder sympa) zu administrieren ist leider auch alles andere als trivial ([s. Cloudron forum][mailman-discussion]). Einzige 
Möglichkeit eine Mailingliste über einen eigenen Server laufen zu lassen, wäre eine separate Django-App für das Community-Portal.
Hier würde man eine extra-Mailbox in Cloudron einrichten die dann von der Django-App via IMAP ausgelesen wird an die Subscriber der
Liste weiterleitet.

[mailman-discussion]: https://forum.cloudron.io/topic/6012/configure-haraka-for-mailman3/9?_=1708443801561

> - Webseite
>     - unter eigener Domain
>     - momentan: git + jekyll + automatisches Bauen
>     - inkl. Webspace?

Auch wenn git + jekyll ein guter und transparenter Workflow ist, ist das Editieren von Content für nicht jekyll-affine Nutzer
recht kompliziert. Das führt dazu, dass nur wenige Personen bei der Website aktiv beitragen. Deshalb wollen wir ein Community-Portal
mit einem Content-Management-System haben, in dem Berechtigungen entsprechend vergeben werden können, um Content auf der Website zu
editieren.

> - Datenrepositorien
>     - git
>     - öffentlich und privat

cloudron bietet einige Apps zum Code-Hosting an, darunter auch gitlab (https://www.cloudron.io/store/index.html#git). Zu bedenken ist, 
dass GitLab selber ziemlich ressourcen-hungrig ist. Gitea ist da vielleicht einfacher. Alternativ, wenn es nicht unbedingt Gitlab sein muss,
kann einfach eine nextcloud-Instanz gehostet werden werden.

https://www.cloudron.io/store/index.html#sync

> - VMs für Projekte/Konferenzen (optional)
>     - wenn wieder pretalx/pretix: root-Rechte
>     - in Dtl.
>     - beim selben Anbieter

VMs können bei windcloud.de jederzeit dazu bestellt werden. Allerdings bietet das Community Portal auch ein Event-Management an 
über das Abstracts eingereicht werden können und Registrierungen gemanaged werden können. Einzelne Events können grundsätzlich auch
über eigene Domains bekommen. Eine Bezahlinfrastruktur wird dadurch aber noch nicht implementiert.

Cloudron bietet aber verschiedene Apps an (z.B. [InvoiceNinja](https://www.cloudron.io/store/index.html#finance)) um invoices zu erstellen
und accounts zu managen (hier fehlt aber noch die Erfahrung und Evaluierung).

> - sichere Datenablage (Umzug zukünftig optional)
>     - in Dtl.
>     - Ende-zu-Ende Verschlüsselung der Daten: keine Klardaten auf Server
>     - "komfortabler" Clientzugang
>     - beim selben Anbieter

Mehrere Apps auf cloudron unterstützen die E2EE Ablage und Bearbeitung von Dokumenten oder sensiblen Informationen.

- [Cryptpad](https://www.cloudron.io/store/fr.cryptpad.cloudronapp.html) zur Bearbeitung und Speicherung von Dokumenten, Tabellen, etc.
- [PrivateBin](https://www.cloudron.io/store/info.privatebin.cloudronapp.html) für One-Time-Secrets oder Dateien
- [VaultWarden](https://www.cloudron.io/store/com.github.bitwardenrs.html) als E2EE-Passwort-Speicher oder zum Versenden von Dateien

> - Kalender (Umzug zukünftig optional)
>     - öffentlich
>     - guter Support in diversen Anwendungen

Ein Kalender oder mehrere Kalender können über eine nextcloud-Installation gemanaged werden. Öffentliche Kalender können via 
Open Web Calendar dargestellt werden (https://www.cloudron.io/store/index.html#). Für das Community Portal ist im Laufe des Jahres
eine Kalender-Implementierung geplant.

> - Chat (Umzug zukünftig optional)
>     - Gruppengröße > 100
>     - Echtzeit
>     - browserbasiert (OS-unabhängig)
>     - Unterstützung für Bilder/Links

Das Community-Portal liefert eine Chat-Infrastruktur. Vorteil ist, dass dort direkt die Community-Struktur abgebildet werden
kann (z.B. Chapter, oder Arbeitskreise) und kein zusätzliches Tool konfiguert werden muss. E2EE ist auch möglich. Die 
Chat-Funktionalitäten sind noch nicht voll ausgereift und es gibt noch keine Integrationen mit anderen Chat-Programmen 
(mit Ausnahme von Email).

Alternativ lässt sich über Cloudron ein [Matrix-Server][matrix] installieren, zusammen mit einer [Element-Instanz][element].

[matrix]: https://www.cloudron.io/store/org.matrix.synapse.html
[element]: https://www.cloudron.io/store/im.riot.cloudronapp.html

> - Twitter
>     - Announceaccount

Will man Twitter nutzen, läuft das nicht über den derse-Server. Via Cloudron lässt sich aber eine Mastodon-Instanz aufsetzen

https://www.cloudron.io/store/org.joinmastodon.cloudronapp.html

> - Textpads (Umzug zukünftig optional)
>     - in Dtl. (teilweise nichtöffentlich)
>     - wenigstens per Passwort/Cryptlink schützbar
>     - Arbeiten im Team und in Echtzeit

Cloudron unterstützt verschiedene Notizen-Apps, unter anderem HedeDoc (wie es auf https://pad.gwdg.de verwendet wird). In
Verbindung mit den User-Management von Cloudron lassen sich hier auch geschützte Dokumente erstellen und gemeinsam bearbeiten.

> - Vereinsverwaltung
>     - lauffähig unter Linux und Windows
>     - bewährtes Produkt
>     - Klartextexport möglich (kein harter vendor-lock-in)
>     - Arbeiten durch mehrere Personen wengistens durch export/import bzw. backup/restore möglich
>     - wenn möglich: open source
>     - Mitgliederversammlung und Gremienarbeit: https://openslides.com/de   

Die Vereinsverwaltung liese sich über das Community-Portal abbilden. Das Community-Portal ist eine recht neue
Software, die momentan noch sehr viel weiterentwickelt wird. Es implementiert eine Versionskontrolle und es können verschiedene
Gruppen abgebildet werden und mit Berechtigungen ausgestattet werden. Das Community-Portal ist [open-source unter EUPL-1.2][djac].

Openslides ist nicht trivial zu installieren und zu administrieren. Das Community-Portal kann aber die notwendigen features abbilden,
personalisierte Umfragen und Abstimmungen könnten per zusätlicher Django-App implementiert werden.

[djac]: https://codebase.helmholtz.cloud/hcdc/django/clm-community/django-academic-community
