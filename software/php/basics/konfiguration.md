---
title: Konfiguration
layout: default
---
[Home](/) > [Software](/software/index.html) > [PHP](/software/php/index.html) > Konfiguration

# PHP Konfiguration

## Die Konfigurationsdatei

Die Konfigurationsdatei _php.ini_ wird beim Servermodul nur ein einziges mal
gelesen wenn der Server startet. Bei der CLI & CGI Version wie diese vor jedem
Aufruf gelesen. Danach werden noch weitere Dateien gesucht:

- Spezielle Verzeichnisse für SAPI-Module (`PHPIniDir` Direktive im Apache2,
  `-c` Parameter in CGI in CLI, `php_ini` Parameter in NSAPI, `PHP_INI_PATH`
  Umgebungsvariable im `THTTPD`)
- Die `PHPRC` Umgebungsvariable.
- Seit PHP 5.2.0 kann die Position der _php.ini_ für verschiedene Versionen
  von PHP gesetzt werden. Die folgenden Registrierungsschlüssel werden in der
  angegebenen Reihenfolge durchsucht (x, y, z sind die Major-, Minor- und
  Release-Versionen von PHP):
  `HKEY_LOCAL_MACHINE\SOFTWARE\PHP\x.y.z`,
  `HKEY_LOCAL_MACHINE\SOFTWARE\PHP\x.y` und 
  `HKEY_LOCAL_MACHINE\SOFTWARE\PHP\x`. 
  Falls ein Wert für `IniFilePath` in einem dieser Schlüssel existiert, so
  wird der zuerst gefundene als Position der php.ini verwendet (nur unter
  Windows).
- Aktuelles Arbeitsverzeichnis außer im CLI Betrieb.
- Das Webserververzeichnis für SAPI-Module oder das PHP-Verzeichnis.

## `.user_ini` Dateien

Für Konfigurationsvariablen mit den Modi `PHP_INI_PERDIR` und `PHP_INI_USER`
können für CGI/FastCGI-SAPI noch .user_ini Dateien gelesen werden, deren
Format sich an _.htaccess_ orientiert. Hierzu wird das Verzeichnis der gerade
angeforderten PHP-Datei gescannt, bis hinab zum `$_SERVER['DOCUMENT_ROOT']`.
Durch `user_ini.filename` kann der Name der Userini-Dateien geändert werden
und `user_ini.cache_ttl` bestimmt wann die Datei wieder gelesen werden muss.

## Wo Einstellungen gesetzt werden können

Wo eine bestimmte PHP-Direktive geändert werden bestimmen die folgenden Modi.

| Modus          | Wert | Bedeutung                                                                 |
|----------------|------|---------------------------------------------------------------------------|
| PHP_INI_USER   | 1    | in Benutzerskripten (z. B. mittels `ini_set()`) oder der Windows-Registry |
| PHP_INI_PERDIR | 6    | in der _php.ini_, _.htaccess_ oder _httpd.conf_ gesetzt werden            |
| PHP_INI_SYSTEM | 4    | in der _php.ini_ oder _httpd.conf_ gesetzt werden                         |
| PHP_INI_ALL    | 7    | überall gesetzt werden                                                    |
