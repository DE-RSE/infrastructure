# Vorschlag der AG Infrastruktur zur ersten Sitzung des Sprecherrats

- Jan-Philipp Thiele
- Philipp Schäfer
- Philipp Sommer

## Überblick

Unsere Vorschläge basieren auf den in [needs.md](./needs.md) genannten Anforderungen,
soweit wir sie verstanden haben,
sowie den in [status.md](./status.md) beschriebenen Status Quo.
Wenn wir etwas nicht verstanden haben, gehen wir darauf im Text ebenfalls ein.

Der nötige Aufwand,
der beim Selbsthosten von Diensten aufzuwenden wäre,
teilt unsere Vorschläge in zwei Gruppen auf.

Die Dienste, die wir selbst hosten,
würden wir auf einer VM,
z.B. bei dem in Deutschland sitzenden Hoster [windcloud](https://windcloud.de/produkte/vps),
hosten und über die Software [Cloudron](https://cloudron.io) managen.
Beide Vorschläge basieren auf privater Erfahrung mit Anbieter beziehungsweise Software im AK Infrastruktur.
Cloudron macht das hosten von vielen bekannten Webanwendungen für 15$ pro Monat sehr einfach.

## Konkrete Vorschläge

### DNS

Gebraucht wird:

>  - mehrere, frei wählbare Domains
>  - Möglichkeit zu schneller, schneller (bzw. direkter) Änderung von Einträgen von Subdomains (u.a. A, CNAME)

Durch die Nutzung eines passenden Anbieters kann die Domain eigenständig verwaltet und können Subdomains einfach angelegt werden.
Derzeit nutzen wir [Domain Factory](https://www.df.eu).
Hier fehlt uns als AG Zugang.

Sollten dort Möglichkeiten fehlen, könnten wir zu [INWX](inwx.de) wechseln.

Das Routing für die verschiedenen Dienste übernähme dann Cloudron.
Jede Anwendung auf Cloudron liefe über eine eigene Subdomain.

### E-Mail

Gebraucht wird:

> - Email
>     - mehrere, einfache Verteiler
>     - mehrere Mailinglisten
>         - Archiv
>         - Datenvolumen potentiell >1GB / Monat
>         - private und öffentliche Listen
>         - unter eigener Domain!
>         - schnelle Einrichtung & Konfiguration durch uns

Wir wollen keine Mailinglisteninfrastruktur selbst hosten, da das sehr aufwendig ist.
Auch Cloudron bietet das nicht als vorkonfigurierte Anwendung an (siehe [Diskussion im Forum](https://forum.cloudron.io/topic/6012/configure-haraka-for-mailman3/9?_=1708443801561)).

Daher müssen wir bei einem externen Anbieter,
derzeit ???,
bleiben.

Da man nur einen MX-Record pro Domain haben kann,
haben wir hier drei Möglichkeiten:

- ML belassen mit neuen Subdomains für die VM  (z.B. infra.de-rse.org und mail.de-rse.org).
- ML belassen mit neuer Subdomain für die ML (z.B. \<topic\>@ml.de-rse.org).

Das würde aber auch bedeuten,
dass wir die Domain nicht mehr über Cloudron verwalten könnten und damit für die damit gehosteten Dienste ggf. eine eigene Subdomain,
z.B. infra.de-rse.org,
nutzen müssten.
Das würde auch für E-Mail-Konten,
die wir über Cloudron verwalten gelten,
für die aber eine zusätzlich Subdomain,
z.B. mail.de-rse.org,
möglich wäre.

### Webseite

Gebraucht wird:

> - Webseite
>     - unter eigener Domain
>     - momentan: git + jekyll + automatisches Bauen
>     - inkl. Webspace?

Hier gibt es zwei Vorschläge.

Wir bleiben bei dem aktuellen Workflow git + jekyll und hosten es auf eigener Infrastruktur (z.B. via <https://docs.cloudron.io/apps/githubpages/>),
wobei Quellen und CI auf GitHub verbleiben (siehe unten).

Oder wir nutzen das [Django Academic Community Portal](https://codebase.helmholtz.cloud/hcdc/django/clm-community/django-academic-community/),
dass ein CMS mit Webinterface beinhaltet.
Philipp Sommer ist Entwickler dieser Software und betreibt sie für andere wissenschaftliche Communities bereits.
Sie hat noch weitere Features,
die wir hier nicht im Detail vorstellen.

### Datenrepositorien

Gebraucht wird:

> - Datenrepositorien
>     - git
>     - öffentlich und privat

Bei diesem Punkt hätten wir gerne konkretere Nutzungsarten beschrieben.
Wir gehen davon aus,
dass wir kein frei Verfügbares Hosting für Mitglieder angedacht ist.

Bekannt aus der Vergangenheit ist die Ablage von Dateien,
die im Rahmen der Organisation von Veranstaltungen anfallen.

### VMs

Gebraucht wird:

> - VMs für Projekte/Konferenzen (optional)
>     - wenn wieder pretalx/pretix: root-Rechte
>     - in Dtl.
>     - beim selben Anbieter

Hier fragen wir uns,
was wir über die in den anderen Punkten genannten Diensten noch mit VM(s) machen wollen?
Ist zu erwarten,
dass wir in absehbarer Zeit Pretalx/Pretix/Indico/etc. für eine Veranstaltung selbst hosten,
wenn wir bei der Organistation der deRSE 2024 Konferenz so genau darauf geachtet haben,
dass wir als Verein die Organisation nicht in einer Weise unterstützen,
die steuerrechtliche Konsequenzen hat?


### Sichere Datenablage

Gebraucht wird:

> - sichere Datenablage (Umzug zukünftig optional)
>     - in Dtl.
>     - Ende-zu-Ende Verschlüsselung der Daten: keine Klardaten auf Server
>     - "komfortabler" Clientzugang
>     - beim selben Anbieter

Unser Vorschlag ist es CryptPad auf der eigenen VM via Cloudron zu hosten.
Es bietet alle genannten Anforderungen, außer den komfortablen Clientzugang, da alles via Webinterface bedient wird.

### Calendar

Gebraucht wird:

> - Kalender (Umzug zukünftig optional)
>     - öffentlich
>     - guter Support in diversen Anwendungen

### Chat

Gebraucht wird:

> - Chat (Umzug zukünftig optional)
>     - Gruppengröße > 100
>     - Echtzeit
>     - browserbasiert (OS-unabhängig)
>     - Unterstützung für Bilder/Links

Dieser Punkt sollte nun mit dem Matrix-Space erfüllt sein.

Wir wollen keine Matrix-Instanz selbst hosten und erst recht keine Konten vergeben.

### Social Media

> - Twitter
>     - Announceaccount

Wir haben wohl einen Mastodon-Konto: https://mastodon.social/@de_rse

Wir wollen keine eigene Mastodon-Instanz hosten, soweit nicht nötig.

### Pads

> - Textpads (Umzug zukünftig optional)
>     - in Dtl. (teilweise nichtöffentlich)
>     - wenigstens per Passwort/Cryptlink schützbar
>     - Arbeiten im Team und in Echtzeit


### Vereinsverwaltung

> - Vereinsverwaltung
>     - lauffähig unter Linux und Windows
>     - bewährtes Produkt
>     - Klartextexport möglich (kein harter vendor-lock-in)
>     - Arbeiten durch mehrere Personen wengistens durch export/import bzw. backup/restore möglich
>     - wenn möglich: open source
>     - Mitgliederversammlung und Gremienarbeit: https://openslides.com/de

Wir gehen davon aus, dass bezüglich der Mitglieder-/Finanzverwaltung (JVerein) kein Handlungsbedarf besteht.

Welche Anforderungen an Software, für Mitgliederversammlungen, gibt es? Was ist das Budget pro Sitzung?
Welche Anforderungen an Software, die die Gremienarbeit unterstützt, gibt es?
