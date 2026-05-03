# Planung
## Projektplan
Im Rahmen dieses Projekts wird das bestehende Vtiger CRM-System, das aktuell auf einem CentOS 6.6 Server mit MySQL-Datenbank betrieben wird, auf eine moderne und unterstützte Systemumgebung migriert.

**Ist**
* System: Vtiger CRM
* Betriebssystem: CentOS 6.6
```
[root@crmserver ~]# cat /etc/redhat-release
CentOS release 6.6 (Final)
```
* Datenbank: MySQL 14.14 Distrib 5.1.73
```
[root@crmserver ~]# sudo mysql --version
mysql  Ver 14.14 Distrib 5.1.73, for redhat-linux-gnu (x86_64) using readline 5.1
```
* Webserver: Apache/2.2.15 (Unix)
```
[root@crmserver ~]# sudo httpd -v
Server version: Apache/2.2.15 (Unix)
Server built:   Oct 16 2014 14:48:21
```
* Server: crmserver.sample.ch
* System läuft on-prem als VM
* CentOS 6.6 ist veraltet / nicht mehr unterstützt


**Soll**
* System: Vtiger CRM V9
* Betriebssystem: Ubuntu Server 24.04 LTS
Ubuntu 24.04 LTS ist bis 2029 gepflegt und die von Vtiger empfohlene Plattform.
* Datenbank: MySQL 10.6
MariaDB 10.6 ist Long Term Support und kompaktiebel.
* Webserver: Apache 2.4
Version 2.4 bringt HTTP/2-Support, bessere Performance und aktive Sicherheitspflege.
**Diagramm**
![help](../Screenshot/planungdiagramm.png)


**MySQL**:
Bestehende Datenbanken:<br>
* mysql
* test
* vtigercrm
* information_schema
```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| test               |
| vtigercrm          |
+--------------------+
```

Bestehende User:
vtigercrm: 
```
mysql> SELECT user_name, user_password, email1 FROM vtiger_users;

+-----------+------------------------------------+--------------------+
| user_name | user_password                      | email1             |
+-----------+------------------------------------+--------------------+
| admin     | $1$ad000000$r3hzdtsdvtvXX9nD2w4yb0 | hans@sample.com    |
| sepp      | $1$se000000$KRn9kiYxE/S641n24kfbA/ | sepp@sample.com    |
| chantal   | $1$ch000000$9NT/kT3TKqF3tDE0w.YTz1 | chantal@sample.com |
+-----------+------------------------------------+--------------------+
```

### Zeitplan
![help](../Screenshot/Zeitplan.png)

## Vtiger
![help](../Screenshot/vtigerweb.png)

Da das passwort nicht bekannt ist habe ich dies zurückgesetzt.


## Test Cases

# Testcases CRM Migration

## Testing

1. **Lokale DNS-Auflösung**  
   Befehl: `ping crmserver.sample.ch`  
   Erwartet: Antwort von 10.0.2.10  

2. **Zweite Domain**  
   Befehl: `ping crm-soll.sample.ch`  
   Erwartet: Antwort von 10.0.2.10  

3. **DNS extern**  
   Befehl: `nslookup crmserver.sample.ch`  
   Erwartet: NXDOMAIN  

4. **Webserver HTTP**  
   Befehl: `curl -I http://crmserver.sample.ch`  
   Erwartet: HTTP 200 / 301 / 302  

5. **Webserver HTTPS**  
   Befehl: `curl -I https://crmserver.sample.ch`  
   Erwartet: HTTP 200 / 301 / 302  

6. **HTTP → HTTPS Redirect**  
   Befehl: `curl -I http://crmserver.sample.ch`  
   Erwartet: 301 / 302 Redirect  

7. **PHP Version**  
   Befehl: `php -v`  
   Erwartet: Version wird angezeigt  

8. **PHP Module**  
   Befehl: `php -m`  
   Erwartet: mysqli, curl vorhanden  

9. **DB läuft**  
   Befehl: `systemctl status mariadb`  
   Erwartet: active (running)  

10. **DB Login**  
    Befehl: `mysql -u <user> -p`  
    Erwartet: Login erfolgreich  

11. **Tabellenanzahl**  
    SQL: `SELECT COUNT(*) FROM information_schema.tables WHERE table_schema='<db>';`  
    Erwartet: gleiche Anzahl wie vorher  

12. **Benutzerdaten**  
    SQL: `SELECT COUNT(*) FROM vtiger_users;`  
    Erwartet: gleiche Anzahl  

13. **CRM Login**  
    Vorgehen: Login im Browser  
    Erwartet: Dashboard sichtbar  

14. **Daten anzeigen**  
    Vorgehen: Kontakt öffnen  
    Erwartet: Daten korrekt sichtbar  

15. **Datensatz erstellen**  
    Vorgehen: neuen Kontakt erstellen  
    Erwartet: gespeichert  

16. **Datensatz bearbeiten**  
    Vorgehen: Kontakt ändern  
    Erwartet: Änderung gespeichert  

17. **SFTP Zugriff**  
    Befehl: `sftp user@crmserver.sample.ch`  
    Erwartet: Login möglich  

18. **Backup erstellen**  
    Befehl: `mysqldump -u user -p db > backup.sql`  
    Erwartet: Datei erstellt  

19. **Backup Restore**  
    Befehl: `mysql -u user -p testdb < backup.sql`  
    Erwartet: Import erfolgreich  

20. **DB Zugriffsschutz**  
    Befehl: `mysql -u falscherUser -p`  
    Erwartet: Access denied  


## Auftrag #13 – Monitoring

21. **Webserver Monitoring**  
    Erwartet: Status OK im Monitoring  

22. **DB Monitoring**  
    Erwartet: Status OK  

23. **Fehler erkennen**  
    Befehl: `systemctl stop apache2`  
    Erwartet: Fehler erkannt  

24. **Alarm-Mail**  
    Aktion: Webserver stoppen  
    Erwartet: Mail wird gesendet  

25. **Auto-Restart**  
    Befehl: `systemctl stop apache2`  
    Erwartet: Service startet neu  