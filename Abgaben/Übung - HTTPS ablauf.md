# Übung HTTPS ablauf
1. User setzt anfrage zum Webserver
2. TCP Verbindung Port 443
3. TLS-Handshake + Cerifikat
4. Verschlüsselung aufbauen
5. Browser sendet HTTPS request
6. Webserver lädt CMS Datei
7. CMS verbindet sich mit der DB
8. DB liefert Daten
9. Webserver sendet daten an User

![help](../Screenshot/https.png)

## Aufgabe 3.
HTTPS: User <--> Webserver
mysqli: Webserver <--> DB-server
ext4: /var/www/html/super-cms

## Angepasste config datei
```
<?php

// This is the database connection configuration.
return array(
	//'connectionString' => 'sqlite:'.dirname(__FILE__).'/../data/testdrive.db',
	// uncomment the following lines to use a MySQL database

	'connectionString' => 'mysql:host=192.168.22.10;port=3306;dbname=superCMS',
	'emulatePrepare' => true,
	'username' => 'sCMS',
	'password' => 'xYzzAB23!',
	'charset' => 'utf8',



);
```