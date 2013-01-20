---
title: Konfiguration
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Konfiguration

# Konfiguration

## Allgemeine Optionen (Produktivsystem)

- `register_globals = off`
- `display_errors = off` und stattdessen aber `log_errors = on`
- `allow_url_include = off`
- `error_reporting = E_ALL & ~E_DEPRECATED`

## PHP als CGI-Script

Es gib grundsätzlich zwei bekannte Probleme im Umgang mit CGI.

- Zugriff auf Systemdateien: `http://my.host/cgi-bin/php?/etc/passwd`
  Die Angaben hinter dem `?` werden bei CGI als Parameter für das aufgerufene
  Scripts verwendet, der erste Parameter ist in der Regel der Pfad der
  auszuführenden Datei.
- Zugriff auf beliebige Web-Dokumente auf dem Server:
  `http://my.host/cgi-bin/php/secret/doc.html` Der Teil der
  URL-Pfadinformation nach dem Namen der PHP Binärdatei, `/secret/doc.html`,
  wird im Allgemeinen benutzt, um den Namen der Datei zu übergeben, die durch
  das CGI-Programm geöffnet und interpretiert werden soll.

Ersteres Problem existiert für PHP-CGI nicht, weil das CGI-Binary die
Interpretation von Kommandozeilenargumenten verweigert.

Dem zweiten Problem muss man schon während des Kompilierens von PHP oder per
Konfiguration Herr werden.

- Hier wird vom Webserver keine Zugriffsüberprüfung der Datei
  `/secret/script.php`, sondern lediglich der Datei `/cgi-bin/php`
  vorgenommen. So ist jeder Benutzer, der auf `/cgi-bin/php` zugreifen darf,
  in der Lage, sich zu jedem geschützten Dokument auf dem Webserver Zugriff
  zu verschaffen.
- Wenn der Webserver keine Redirects erlaubt oder keine Möglichkeit hat, dem
  PHP-Binary mitzuteilen, dass es sich um eine sicher umgeleitete Anfrage
  handelt, kann die Option `--enable-force-cgi-redirect` im configure-Skript
  angegeben werden. Nichtsdestotrotz muss sichergestellt werden, dass die
  PHP-Scripte nicht auf die eine oder andere Art des Aufrufs angewiesen
  sind, weder direkt durch `http://my.host/cgi-bin/php/dir/script.php` noch
  durch einen Redirect `http://my.host/dir/script.php`.
- Die Konfigurationsdirektive `cgi.force_redirect` verhindert grundsätzlich
  den Aufruf von PHP mit einer URL wie
  `http://my.host/cgi-bin/php/secretdir/script.php`. Stattdessen parst PHP
  in diesem Modus nur dann, wenn der Aufruf durch einen korrekten Redirect
  des Webservers erfolgte (ist per default ON).
  CGI Redirect-Konfiguration für Apache. Beim Redirect setzt Apache die
  Umgebungsvariable `REDIRECT_STATUS` (!ist keine CGI-Konvention).

      Action php-script /cgi-bin/php
      AddHandler php-script .php

- Die ausführbaren PHP-Scripte sollten niemals im erreichbaren Web-Verzeichnis
  liegen. Denn hier könnten sie falls obige Sicherheitsmaßnahmen nicht
  verfügbar oder möglich sind vom Nutzer via URL aufgerufen und miss braucht
  werden. Und vielleicht noch schlimmer, die könnten aufgerufen werden, ohne
  von PHP interpretiert worden zu sein evtl. können Sensible Informationen
  eingesehen werden. Damit die Scripte außerhalb der Web-Verzeichnises liegen
  können, muss man mit Konfigurationsoption `doc_root`  oder der
  Umgebungsvariablen `PHP_DOCUMENT_ROOT` angeben in welchem Verzeichnis die
  auszuführenden PHP-Scripte zu suchen sind.
- Sollen auch Scripte aus dem User-Verzeichnis ausgeführt werden muss noch die
  Konfigurationsoption `user_dir` gesetzt werden.
  - Kein `user_dir` gesetzt. Bei Aufruf von `http://my.host/~user/doc.php`
    wird im `doc_root` das Script `~user/doc.php` ausgeführt.
  - Ist `user_dir=/home/user/public_php` gesetzt, so wird die Datei
    `/home/user/public_php/doc.php` ausgeführt.
- Sehr sicher ist es wohl auch des PHP-Parser-Binary
- Eine sehr sichere Sache ist es, das PHP-Parser-Binary irgendwo außerhalb des
  Webverzeichnisbaums zu platzieren, beispielsweise in `/usr/local/bin`. Dann
  muss es aber jedes PHP-Script wir ein normales Shell-Script geschrieben sein
  und auch ausführbar sein (wird so auch vom [CERT-Advisory][cert] empfohlen)

      #!/usr/local/bin/php
      <?php
      // ... a lot of code here

  Damit PHP bei dieser Konfiguration die `PATH_INFO`- und
  `PATH_TRANSLATED`-Informationen korrekt auswertet, sollte der PHP-Parser mit
  der Option `--enable-discard-path` kompiliert werden.

  
## PHP als Apache-Modul

Der PHP-Interpreter wird mit den Benutzerrechten von Apache ausgeführt! Daher
ist ein besonderes Augenmerk auf die Rechte zu legen, mit denen Apache
gestartet wird.

Ist erst einmal eine Sicherheitsstruktur bis zu dem Punkt eingerichtet, an dem
der PHP-User, in diesem Falle der Apache-User, nur noch ein geringes Risiko
darstellt, hat man meist die Situation, dass PHP gehindert wird, beliebige
Dateien in das Benutzerverzeichnis zu schreiben. Oder vielleicht ist PHP dann
nicht mehr in der Lage, auf Datenbanken lesend oder verändernd zuzugreifen
(wenn diese keine eigene Zugriffskontrolle bereitstellen). In gleicher
Weise wird auch verhindert, "gute" oder "bösartige" Dateien zu schreiben, oder
"gute" bzw. "bösartige" Datenbanktransaktionen durchzuführen. Daher sollte
eine Zugriffskontrolle via `LDAP`, `.htaccess` oder eigenes Zugansmodell
implementiert werden.

Sinnvoll ist auch eine Einschränkung der Dateien die von PHP geöffnet werden
dürfen mit `open_basedir`. `open_basedir` Begrenzt die Dateien, die von PHP
geöffnet werden dürfen.  Wichtig ist, dass der Wert kein Verzeichnis Pfad,
sondern ein Prefix ist. Die Einstellung `open_basedir=/dir/incl` erlaubt den
Zugriff sowohl auf `/dir/include` als auch `/dir/incls`. Aus diesem Grund ist
es besser den Pfad mit dem '/' zu beenden.

Auf gar keinen Fall versuchen eventuellen Problemen dadurch zu begegnen, indem
der Apache mit Root-Rechten ausgeführt wird!

[cert]: http://www.cert.org/advisories/CA-1996-11.html "CERT-Advisory"
